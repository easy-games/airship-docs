# Server Management

Airship provides tools for creating and managing instances of game servers through the `Platform.Server.ServerManager` API.

## Creating Servers

You can create a server by calling `CreateServer()`. You can provide additional parameters to this function to define things like the starting scene, the access mode, and other custom configuration.

## Shutting Down Servers

Game servers with no players are automatically shut down after a few minutes, so you don't need to explicitly shut down a game server. If you do want to shut down a game server, you can use the `ShutdownServer()` function.

## Retrieving Server Data

You can retrieve basic server configuration information for any running game server using the `GetServer()` function.
