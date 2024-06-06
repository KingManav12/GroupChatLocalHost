It handles connecting to the server, sending messages, and listening for incoming messages from the server.

Fields:

socket: The socket through which the client communicates with the server.
bufferedReader: Reads data from the server.
bufferedWriter: Sends data to the server.
username: The client's username.
Constructor:

Initializes the socket, input/output streams, and the username.
Handles any potential IOExceptions by closing all resources using closeEverything.
Methods:

sendMessage(): Sends the client's username initially and then continuously reads messages from the console to send to the server.
listenToMessage(): Runs a separate thread that listens for incoming messages from the server and prints them to the console.
closeEverything(): Closes the socket, BufferedReader, and BufferedWriter.
Main Method:

Prompts the user for a username.
Connects to the server on port 1234.
Creates a Client object, starts listening for messages, and begins sending messages.
ClientHandler Class
This class handles communication with each individual client. It runs on the server side and manages sending and receiving messages for a particular client.

Fields:

clientHandlers: A static list of all active ClientHandler instances (i.e., all connected clients).
socket: The socket for this specific client.
bufferedReader: Reads data from the client.
bufferedWriter: Sends data to the client.
clientName: The name/username of the client.
Constructor:

Initializes the socket and input/output streams.
Reads the client's username and adds the current instance to the clientHandlers list.
Broadcasts a message to all clients that a new client has joined.
Methods:

run(): Continuously listens for messages from the client and broadcasts them to all other clients.
broadCastMessage(): Sends a message to all clients except the sender.
removeClientHandler(): Removes the client from the clientHandlers list and broadcasts a message that the client has left.
closeEverything(): Closes the socket and input/output streams, and removes the client from the list of handlers.
myServer Class
This class represents the server-side of the chat application. It listens for incoming client connections and spawns a new ClientHandler thread for each connected client.

Fields:

serverSocket: The server socket that listens for incoming connections.
Constructor:

Initializes the server socket.
Methods:

startServer(): Continuously accepts new client connections and starts a new ClientHandler thread for each connection.
closeServerSocket(): Closes the server socket.
main(): Creates a server socket on port 1234, creates an instance of myServer, and starts the server.
Execution Flow
The server (myServer) starts and listens for client connections on port 1234.
When a client connects, a new ClientHandler is created to manage the connection.
The client (Client) connects to the server, sends its username, and starts listening for and sending messages.
Messages sent by any client are received by their respective ClientHandler, which then broadcasts the messages to all other clients.
If a client disconnects, its ClientHandler is removed from the list of handlers, and a disconnect message is broadcasted.
This setup enables multiple clients to join a chat, send messages to each other, and see notifications when users join or leave.
