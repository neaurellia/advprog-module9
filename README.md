# advprog-module9

### 1. What is AMQP?

**AMQP (Advanced Message Queuing Protocol)** is an open standard protocol for message-oriented middleware.  
It allows **reliable, asynchronous communication** between services or components in a distributed system.  
It is widely used in messaging systems like **RabbitMQ**.

### 2. What does `guest:guest@localhost:5672` mean?

This is a **connection URI** commonly used when connecting to an AMQP broker like **RabbitMQ**.  
It is structured as: `amqp://<username>:<password>@<host>:<port>`

**`guest:guest`**
- **First `guest`** = **username**  
- **Second `guest`** = **password**  
These are default credentials for RabbitMQ when it's first installed. In production, these credentials are usually changed for security reasons.

**`localhost`**
- The **hostname or IP address** of the AMQP server (RabbitMQ broker).  
- `localhost` means the server is running on your **local machine**.

**`5672`**
- The **port number** RabbitMQ listens on for AMQP connections.  
- **Default AMQP port** = `5672`  
- **AMQPS (secured AMQP)** typically uses port `5671`.

---

### 3. How much data your publisher program will send to the message broker in one run?

The publisher sends **5 messages**, each containing a `UserCreatedEventMessage` struct with:

- `user_id: String` (e.g., `"1"`)
- `user_name: String` (e.g., `2306256261y-Amir`)

#### Estimated data size per message:

| Field           | Example Value             | Approx. Bytes |
|----------------|---------------------------|---------------|
| `user_id`      | `"1"` to `"5"`            | ~2 bytes      |
| `user_name`    | `"2306256261y-Amir"`      | ~20 bytes     |
| Borsh overhead | Struct encoding metadata  | ~5–10 bytes   |
| **Total/msg**  |                           | **~30–35 B**  |

#### Total for 5 messages:

**~150–175 bytes** (excluding protocol or RabbitMQ overhead)

### 4. The url of: `amqp://guest:guest@localhost:5672` is the same as in the subscriber program, what does it mean?

Both **publisher** and **subscriber** use the same connection URI, which means:

- **`guest:guest`** – Username and password (default RabbitMQ credentials).
- **`localhost`** – Both programs are connecting to a RabbitMQ broker on the same machine.
- **`5672`** – Default AMQP port used for messaging communication.

Publisher and subscriber are connected to **the same RabbitMQ instance**, so messages sent by the publisher can be received by the subscriber as long as:

- They're using **the same queue name or topic** ("user_created").
- The subscriber is properly subscribed to that action/topic.