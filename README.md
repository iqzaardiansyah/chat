<details>
<summary>Tutorial 2 Module 10</summary>

<details>
<summary>2.1. Original code of broadcast chat.</summary>

![2.1. Original code of broadcast chat. 1](https://i.ibb.co/PCYC7mx/Cuplikan-layar-2024-05-03-094202.png)
![2.1. Original code of broadcast chat. 2](https://i.ibb.co/DMzk4hW/Cuplikan-layar-2024-05-03-094221.png)
![2.1. Original code of broadcast chat. 3](https://i.ibb.co/VLXN7zJ/Cuplikan-layar-2024-05-03-094238.png)
![2.1. Original code of broadcast chat. 4](https://i.ibb.co/dpzNv3J/Cuplikan-layar-2024-05-03-094250.png)

First, we need to add this code to `Cargo.toml`
```
[[bin]]
name = "server"

[[bin]]
name = "client"
```

The reason we need to add the code to `Cargo.toml` is that Cargo needs to know that there are multiple binary targets in the project: `server` and `client`. By specifying them in the `Cargo.toml`, we're telling Cargo to build separate executables for each of these binaries when we run `cargo build` or `cargo run`.

To run the program and observe its behavior:

1. Navigate to the project directory containing `Cargo.toml`.
2. Run the server by executing: `cargo run --bin server`.
3. Run three clients by opening three separate terminal windows and executing: `cargo run --bin client`.
4. Each client will connect to the server and prompt us to type a message.
5. Type a message in each client terminal and press Enter.
6. Observe that the message is sent to the server, which broadcasts it to all connected clients.
7. We will see the messages received by each client, including the one sent by itself.

When we type text in each client, the text is sent to the server, which then broadcasts it to all connected clients. Each client receives the broadcasted message, including the message it sent, resulting in a chat-like interaction between all clients.
</details>

<details>
<summary>2.2. Modifying the websocket port</summary>

To modify the port to be 8080, we need to change the port number where the server binds and where the client connects. Here's what we need to modify:

### `src/bin/server.rs`:
Change the port number in the `TcpListener::bind` function call:

```
let listener = TcpListener::bind("127.0.0.1:8080").await?;
```

### `src/bin/client.rs`:
Change the URI to connect to the server on port 8080:

```
let (mut ws_stream, _) =
    ClientBuilder::from_uri(Uri::from_static("ws://127.0.0.1:8080"))
        .connect()
        .await?;
```

### WebSocket Protocol:
Both the server and client are using the WebSocket protocol, which is defined and implemented in the `tokio_websockets` crate. This crate provides the necessary abstractions and utilities for working with WebSocket connections in Tokio-based applications. The WebSocket protocol allows bidirectional communication between clients and servers over a single, long-lived connection.

After making these modifications, we should be able to run the server and clients on port 8080 successfully, maintaining the functionality of the chat application.
</details>

<details>
<summary>2.3. Small changes. Add some information to client</summary>

![2.3. Small changes. Add some information to client 1](https://i.ibb.co/xGxDgR9/Cuplikan-layar-2024-05-03-101655.png)
![2.3. Small changes. Add some information to client 2](https://i.ibb.co/7Kvrx1Q/Cuplikan-layar-2024-05-03-101703.png)
![2.3. Small changes. Add some information to client 3](https://i.ibb.co/yYNQbsR/Cuplikan-layar-2024-05-03-101712.png)

In the original implementation, the server was simply broadcasting the message received from a client without any additional information about the sender. Similarly, the client was receiving messages from the server without any details about who sent the message.

To add information about the sender to each client, we need to modify both the server and the client:

1. **Server Modification**:
    - In the server code, when handling a message from a client, we need to prepend information about the sender (in this case, the client's IP address and port) to the message before broadcasting it to all clients.
    - This modification ensures that each client receives messages along with details about who sent the message.

2. **Client Modification**:
    - In the client code, we need to extract and display the sender information along with the message content.
    - This modification allows each client to show messages along with details about the sender, providing context about the origin of each message.

By making these changes in both the server and client code, we ensure that information about the sender is included and displayed correctly in the chat application. It's essential to modify both sides of the communication to maintain consistency and ensure that each client receives and displays messages with sender information accurately.
</details>

</details>