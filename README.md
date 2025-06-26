# ⚡eMotion

- **eMotion** is a scalable, event-driven ride-hailing platform built with Node.js, Express.js, MongoDB, WebSockets, and RabbitMQ.
- It supports real time ride management with WebSocket notifications and microservice communication for a smooth user experience.

---

## 🔗 Architecture Overview

eMotion uses a microservices architecture featuring:

- **Nginx** as a reverse proxy and load balancer.
- **Docker Compose** to containerize and decouple services.
- **RabbitMQ** for reliable message queuing and asynchronous communication.
- **WebSocket server** for real-time ride event notifications.
- **MongoDB** to store user, captain, and ride data.
- **Multiple microservices** for User, Captain, Ride, and Central Websocket based Notification handling.

### 🔗 Communication Flow

1. Users and captains authenticate via JWT-secured REST endpoints.
2. Ride requests are created and managed via REST APIs.
3. Ride status updates (accept, start, end) are propagated via RabbitMQ events.
4. WebSocket server pushes real-time notifications to users and captains.
5. Nginx routes incoming requests to appropriate microservices.

---

## ⚙️ Tech Stack

| Technology     | Purpose                                      |
| -------------- | -------------------------------------------- |
| Node.js        | Backend runtime                              |
| Express.js     | REST API framework                           |
| MongoDB        | Persistent data storage                      |
| RabbitMQ       | Message queue for microservice communication |
| WebSocket      | Real-time notifications                      |
| Nginx          | Reverse proxy & load balancing               |
| Docker Compose | Container orchestration                      |
| Azure VM       | Hosting backend infrastructure               |
| Vercel         | Frontend deployment                          |

---

## 🔗 Features

- ✅ User & Captain registration and JWT authentication
- ✅ REST APIs for ride creation, acceptance, start, and completion
- ✅ Real-time ride event notifications via WebSocket with sub-10ms latency
- ✅ Reliable, decoupled microservices communication using RabbitMQ
- ✅ Scalable multi-instance backend containerized with Docker Compose
- ✅ Nginx reverse proxy managing load balancing between services

---

## 🔗 Performance Metrics from Load Testing

- Successfully handled **306+ concurrent WebSocket sessions** with average connection latency under **10ms**
- Supported over **393 ride event checks** with **74% success rate** at peak load (15 VUs, 8 mins)
- Average HTTP request duration: **~11.5 seconds**, median: **1.78 seconds** under stress
- Maintained **100% successful user and captain logins** during tests
- RabbitMQ ensured reliable asynchronous messaging with minimal overhead and zero message loss
- Dockerized microservices maintained clear separation and easy scaling in Azure VM environment

---

## 🛠️ Deployment & Setup

- Frontend is currently hosted on `https://e-motion-eight.vercel.app`
- Backend is currently hosted on `https://distros.tech`

### 1. Prerequisites

- Docker & Docker Compose installed
- Azure Virtual Machine for backend deployment
- Nginx installed on VM as reverse proxy
- MongoDB instance (can be hosted or containerized)
- RabbitMQ instance running (can be containerized)
- Vercel account for frontend hosting

### 2. Clone the repository

```bash
git clone https://github.com/alucard017/eMotion-Backend.git
cd eMotion-Backend

git clone https://github.com/alucard017/eMotion-frontend.git
cd eMotion-frontend
```

### 3. Configure environment variables

- Create a `.env` file inside each user, ride, captain services following `.env.sample` with values like:
- Creating `.env` is optional if you want to directly provide `environments` via `docker-compose`.
- If not using docker-compose you need to run the` gateway server` or else if using docker-compose you need to run `nginx` and configure `nginx.conf `as given as sample.
- `docker-compose file sample` is also provided to follow the structure strictly.

### 4. Running services

- For frontend it will be running on `localhost:3000` if `3000` port is not available it will run in port `3001` alterntaively.
- Make sure to add `.env `variable in frontend too and make sure to use the `API_BASE_UR`L of backend to make API calls. Currently frontend assumes the request comes from hosted frontend and backend so `API_BASE_URL` is ignored.
- For backend if not using docker-compose simply go to `each service folders` and run.

```bash
npm run build
npm run start
```

- Service will start successfuly.
- Make sure that all services will be connected via `gateway server`.
- If using docker-compose then just run the below command

```bash
docker-compose up --build -d
```

- You can see the logs by

```bash
docker compose logs -f
```

- Make sure when using `docker-compose`, place `nginx.conf` as in the `same file` where docker-compose lies.
