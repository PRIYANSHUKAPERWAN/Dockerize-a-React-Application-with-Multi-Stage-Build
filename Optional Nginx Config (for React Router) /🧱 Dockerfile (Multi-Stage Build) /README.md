🚀 Dockerized React Application (Multi-Stage Build)
This project demonstrates how to Dockerize a React application using a multi-stage Docker build to create a production-ready, optimized image.
The multi-stage approach separates build dependencies from runtime, reduces image size, and prepares your app for deployment anywhere Docker is supported.

🧩 Features
Multi-stage Docker build for smaller and efficient images
Production-ready React app served via Nginx
Optional custom Nginx config for React Router support
Easy deployment to Docker, AWS ECS, Kubernetes, or any container platform
🗂️ Project Structure
react-app/ ├── public/ ├── src/ ├── package.json ├── package-lock.json ├── Dockerfile └── nginx.conf (optional)

⚙️ Dockerfile Overview
Multi-Stage Build

# Stage 1: Build React app
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve app with Nginx
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
🔹 Optional Nginx Config
server {
    listen 80;
    server_name localhost;

    root /usr/share/nginx/html;
    index index.html index.htm;

    location / {
        try_files $uri /index.html;
    }
}


✅ Benefits

Lightweight production image (~45–50MB)

Separation of build and runtime dependencies

Optimized and fast serving using Nginx

Ready for scalable deployments

🧰 Tech Stack

Frontend: React.js

Runtime: Nginx (Alpine)

Build: Node.js (Alpine)

Containerization: Docker

🏁 Author

Ayush Rana
Developer | Full-Stack & Cloud Enthusiast
