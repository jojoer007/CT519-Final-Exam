﻿# CT519-Assign5
จาก Assign #4 ให้นักศึกษา สร้าง Domain name และสมัครขอใช้งาน Cert จาก Lets-Encrypt เพื่อนำมาทำให้ Web server ในงาน Assign #4 รองรับการใช้งานผ่าน HTTPS ได้

ตัวอย่าง คอนฟิกของไฟล์ nginx.conf ที่ทำให้ ์NginX รองรับการเชื่อมต่อแบบ https
events {
#    worker_connections 1024;
}

http {
    upstream backend {
        server ws1:80;
        server ws2:80;
    }

    server {
       listen 80;

       server_name ck.signalschool.co;
       return 301 https://ck.signalschool.co;
    }

    server {
#        listen 80;
        listen 443 ssl;
        server_name ck.signalschool.co;  
        ssl_certificate /etc/ssl/nui-cert.pem;
        ssl_certificate_key /etc/ssl/nui-private-key.pem;
        ssl_protocols TLSv1.1 TLSv1.2;


        location / {
            proxy_pass http://backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        location /www1 {
            proxy_pass http://ws1;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        location /www2 {
            proxy_pass http://ws2;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
    }

}
ตัวอย่างไฟล์ docker-compose ที่มี service ของ RP ด้วย nginX และ Web จำนวน 2 เครื่อง (ws1,ws2) ทำงานด้วย nginx เช่นกัน

services:
  ws1:
    image: nginx:alpine
    volumes:
      - ./ws1:/usr/share/nginx/html
    networks:
      - backend

  ws2:
    image: nginx:alpine
    volumes:
      - ./ws2:/usr/share/nginx/html
    networks:
      - backend

  reverse_proxy:
    image: nginx:alpine
    ports:
      - "443:443"
      - "80:80"
    depends_on:
      - ws1
      - ws2
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./ssl:/etc/ssl
    networks:
      - frontend
      - backend

networks:
  frontend:
    driver: bridge
  backend:
    driver: bridge