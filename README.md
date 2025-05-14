# advprog-module9

## 1. What is AMQP?

**AMQP (Advanced Message Queuing Protocol)** is an open standard protocol for message-oriented middleware.  
It allows **reliable, asynchronous communication** between services or components in a distributed system.  
It is widely used in messaging systems like **RabbitMQ**.

---

## 2. What does `guest:guest@localhost:5672` mean?

This is a **connection URI** commonly used when connecting to an AMQP broker like **RabbitMQ**.  

### `guest:guest`
- **First `guest`** = **username**  
- **Second `guest`** = **password**  
These are default credentials for RabbitMQ when it's first installed. In production, these credentials are usually changed for security reasons.

### `localhost`
- The **hostname or IP address** of the AMQP server (RabbitMQ broker).  
- `localhost` means the server is running on your **local machine**.

### `5672`
- The **port number** RabbitMQ listens on for AMQP connections.  
- **Default AMQP port** = `5672`  
- **AMQPS (secured AMQP)** typically uses port `5671`.
