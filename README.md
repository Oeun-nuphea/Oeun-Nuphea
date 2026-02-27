# 🚀 Event-Driven Microservices Architecture
### Developed by [Nuphea](https://github.com/nuphea) 👋
**Fullstack Developer | Node.js | Vue.js | TypeScript | MongoDB | MySQL | Docker**

---

<h3 align="center">🛠 Tech Stack ⚛</h3>

<p align="center">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nodejs/nodejs-original.svg" alt="Node.js" width="50" height="50" title="Node.js" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/typescript/typescript-original.svg" alt="TypeScript" width="50" height="50" title="TypeScript" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/express/express-original.svg" alt="Express" width="50" height="50" title="Express.js" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/docker/docker-original.svg" alt="Docker" width="50" height="50" title="Docker" />
  <img src="https://cdn.simpleicons.org/rabbitmq/FF6600" alt="RabbitMQ" width="50" height="50" title="RabbitMQ" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mongodb/mongodb-original.svg" alt="MongoDB" width="50" height="50" title="MongoDB" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mysql/mysql-original.svg" alt="MySQL" width="50" height="50" title="MySQL" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/redis/redis-original.svg" alt="Redis" width="50" height="50" title="Redis" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/jest/jest-plain.svg" alt="Jest" width="50" height="50" title="Jest" />
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/githubactions/githubactions-original.svg" alt="GitHub Actions" width="50" height="50" title="GitHub Actions" />
</p>

---

## 📖 Project Overview
This project is a production-ready **Event-Driven Microservices** ecosystem. It focuses on decoupling business logic through asynchronous messaging using **RabbitMQ**, ensuring that individual services (Auth, Notes, Bank, etc.) can scale and fail independently without crashing the entire system.

### Key Features:
- **Asynchronous Communication:** Services interact via Publish/Subscribe patterns.
- **Database per Service:** Isolated MongoDB/MySQL instances to ensure data sovereignty.
- **Transactional Consistency:** Implementation of Mongoose sessions for reliable data updates.
- **Type Safety:** Shared internal libraries for Zod schemas and TypeScript interfaces.

---

## 🏗 System Architecture

```mermaid
graph TD
    Client[Vue.js Frontend] --> Gateway[API Gateway / Nginx]
    Gateway --> AuthSvc[Auth Service]
    Gateway --> NoteSvc[Note Service]
    Gateway --> BankSvc[Bank Service]

    AuthSvc -- "User Created Event" --> RMQ[(RabbitMQ)]
    RMQ -- "Sync User Data" --> NoteSvc
    RMQ -- "Initialize Wallet" --> BankSvc

    subgraph "Databases"
        AuthDB[(MongoDB)] --- AuthSvc
        NoteDB[(PostgreSQL/MySQL)] --- NoteSvc
        BankDB[(MongoDB)] --- BankSvc
    end
