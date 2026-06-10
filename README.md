# 💬 Real-Time Chat Application — Spring Boot + WebSocket

> A real-time chat application built with Spring Boot 3 and WebSocket (STOMP over SockJS). Supports live multi-user messaging with persistent storage via MySQL and in-memory testing with H2. Demonstrates full-duplex communication patterns and event-driven backend architecture.

![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.1.3-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![WebSocket](https://img.shields.io/badge/WebSocket-STOMP-010101?style=flat-square)
![MySQL](https://img.shields.io/badge/MySQL-Runtime-4479A1?style=flat-square&logo=mysql&logoColor=white)
![H2](https://img.shields.io/badge/H2-In--Memory-1565C0?style=flat-square)
![Thymeleaf](https://img.shields.io/badge/Thymeleaf-3-005F0F?style=flat-square&logo=thymeleaf&logoColor=white)

---

## Features

- **Real-time messaging** — WebSocket with STOMP protocol + SockJS fallback
- **Multi-user chat** — Broadcast messages to all connected clients
- **Persistent messages** — JPA + MySQL for message history
- **In-memory dev mode** — H2 database for rapid local development
- **Server-rendered UI** — Thymeleaf frontend with live WebSocket updates
- **Input validation** — Bean Validation on message payloads

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Java 17 |
| Framework | Spring Boot 3.1.3 |
| Real-time | Spring WebSocket (STOMP / SockJS) |
| ORM | Spring Data JPA / Hibernate |
| Database | MySQL (prod) / H2 (dev) |
| Templating | Thymeleaf |
| Build | Maven |

---

## Getting Started

### Prerequisites

- Java 17+
- Maven 3.6+
- MySQL 8.0+ (or use H2 for dev)

### Setup

```bash
git clone https://github.com/Murthyk6/chat-app-java.git
cd chat-app-java
```

**Option A — Dev mode (H2 in-memory, no setup needed):**

```properties
# application.properties
spring.datasource.url=jdbc:h2:mem:chatdb
spring.datasource.driver-class-name=org.h2.Driver
spring.jpa.hibernate.ddl-auto=create-drop
```

**Option B — MySQL:**

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/chat_db
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
```

Run:

```bash
./mvnw spring-boot:run
```

Open `http://localhost:8080` — open multiple tabs to test real-time messaging.

---

## How It Works

```
Browser (SockJS client)
        │
        │  STOMP over WebSocket
        ▼
Spring WebSocket Broker
        │
   /app/send  ──► @MessageMapping ──► business logic
        │
   /topic/messages ◄── @SendTo ──── broadcast to all subscribers
        │
        ▼
  All connected clients receive message in real time
```

---

## Project Structure

```
src/main/java/com/example/chat/
├── controller/     # @MessageMapping WebSocket handlers
├── model/          # Message entity + JPA mapping
├── repository/     # Spring Data repository
├── service/        # Message persistence logic
└── config/         # WebSocket + STOMP broker config
src/main/resources/
├── templates/      # Thymeleaf chat UI
└── application.properties
```

---

## Key Concepts Demonstrated

- WebSocket configuration with `WebSocketMessageBrokerConfigurer`
- STOMP message routing (`/app` → handler → `/topic` broadcast)
- SockJS fallback for environments blocking WebSocket
- JPA entity persistence alongside real-time message flow
- H2 in-memory database for zero-config local testing

---

> Built to explore event-driven, real-time backend architectures — patterns directly relevant to the SIP/RTP signaling and telecom infrastructure work at Ubona Technologies.
