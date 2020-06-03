# PickleTrick

This is a rewrite of TrickEmuS2, making it another Trickster Online Season 2 emulator. The goal of this project is to emulate the server of Trickster Online, but with better code than what TrickEmuS2 has. Unlike TrickEmuS2, PickleTrick is written with C# 8 features in mind, like `Span<T>`.

PickleTrick is in a very early stage. I'm currently considering different design choices before continuing on with the implementation of more features and servers.

Some obstacles to figure out:

* A way to do things asynchronously, especially database calls
* Whether the server core can handle a large number of connections with its current design
* Whether the config format is sufficient for the future
* Probably more.

### Progress

The code is barely tested. Unit tests are unlikely to be made due to the project being an emulator for another game. At the current moment, the only thing the server can do is send a server list packet with dummy data.

Development is pretty slow, too, as I only occasionally come back to work on this every now and then.

### Getting Started

Compile the projects and copy over the `*.toml` files to the folder the server binaries are present in. Edit the files to match your server's configuration.

You'll want to patch your client with the (very undetailed) instructions provided below in the "Client" section.

The server uses MySQL with development being done mostly with MariaDB. As there's no actual stuff going on with the database yet, there's no database schema or SQL file provided.

### Client

Like the original TrickEmuS2, PickleTrick will eventually also require a patch to enter the game. This is due to not having the original packet structures to send to the client. A vanilla client would crash from that.

Patch the jump instruction (jne/je) to jmp at `Trickster.0+0x74497`. `dummy` should be used as your password if you aren't able to patch the login code to use your actual password. This is due to Trickster's SSO system.