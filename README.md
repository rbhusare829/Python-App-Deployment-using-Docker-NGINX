# Python-App-Deployment-using-Docker-NGINX
Successfully deployed a Python web application using Docker containers on an AWS EC2 instance. Configured NGINX as a reverse proxy to expose the application over HTTP, following real-world DevOps deployment practices.  🔧 Technologies: Docker, Python, NGINX, AWS EC2, Linux, GitHub
User (Browser)
|
| HTTP :80
v
NGINX Container (Reverse Proxy)
|
| Proxy Pass :5000
v
Python Application Container

---

## 🛠️ Technologies Used

- AWS EC2 (Amazon Linux)
- Docker
- Python 3.8
- NGINX
- Git & GitHub
- Linux (CLI)

---

## 📁 Project Structure

pythonapp/
│
├── Dockerfile
├── app.py
├── requirements.txt
└── README.md

---

## 🐳 Dockerfile (Python Application)

```dockerfile
FROM python:3.8-alpine

WORKDIR /pythonapp

COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000

CMD ["python", "app.py"]
```

⚙️ NGINX Reverse Proxy Configuration

default.conf
server {
    listen 80;

    location / {
        proxy_pass http://pythonapp:5000;
    }
}

🚀 Deployment Steps
1️⃣ Launch EC2 Instance

Instance type: t2.micro

Open inbound ports:

22 (SSH)

80 (HTTP)

2️⃣ Install Docker
```
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
```
3️⃣ Clone Repository
```
git clone https://github.com/iamtruptimane/pythonapp.git
cd pythonapp
```
4️⃣ Build Python Docker Image
```
docker build -t pythonimg .
```
5️⃣ Run Python Application Container
```
docker run -d --name pythonapp pythonimg
```
6️⃣ Run NGINX Reverse Proxy Container
```
docker run -d -p 80:80 --name proxy --link pythonapp:pythonapp nginx
```
7️⃣ Configure NGINX Inside Container
```
docker exec -it proxy /bin/bash
cd /etc/nginx/conf.d/
nano default.conf
nginx -s reload
```
🌐 Access Application

Open your browser and visit:

http://<EC2-PUBLIC-IP>


✅ The Python application will be served through NGINX Reverse Proxy

📸 Output

Python application accessible on port 80

Backend Python service running internally on port 5000

Clean reverse proxy flow using Docker networking

🎯 Key Learnings

Docker image creation & container management

Container linking and networking

NGINX as a reverse proxy

Real-world AWS EC2 deployment

Hands-on DevOps workflow

👨‍💻 Author

Rohit Bhusare
📍 Pune, Maharashtra, India

🔗 GitHub: https://github.com/rbhusare829

🔗 LinkedIn: https://www.linkedin.com/in/rohitbhusare-84b94b368

⭐ Support

If you like this project, give it a ⭐ on GitHub and feel free to fork or contribute!


