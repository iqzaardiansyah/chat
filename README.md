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

</details>