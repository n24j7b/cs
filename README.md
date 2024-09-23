java cAssignment №1
1 Simple Messanger
You need to develop the simplest instant messaging system (chat, messenger)
1.1 Server
Must receive messages from clients and send messages to all connected clients.
Use threads to work with multiple clients. The name of the binary ﬁle being
executed must be server. The server must have a console interface in the
parameters to which is transferred: port
1.2 Client
Each client must have own nickname, set by the user. When you receive a
message from another client, the screen should display the time of receiving the
message, the user-sender’s nickname, and the text of the message. An example:
{05:20} [John] Hi!
The client must have a console interface. The name of the client for binary
ﬁle. The client accepts the work options through the command line arguments
in the following order: server address, port, nickname.
To prevent the received (incoming) messages from interfering with the user’s
typing, it is suggested that a separate mode of sending a message, for example,
when the m key is pressed, the user enters his message, new messages from
other users are temporarily not displayed, after sending the message (by Enter)
the mode is automatically turned oﬀ.
1.3 Protocol
Client -> Server
Nickname size Nick Body size Body
4 bytes Nickname size bytes 4 bytes Body size bytes
Network format - Network format -
Server -> Client
Nickname size Nick Body size Body Date size Date
4 bytes
Nickname size
bytes
4 bytes Body size bytes 4 bytes
Data size
bytes
Network format - Network format - Network format -
11.4 Features that are not required of the server and the
client
• Client registration, authorization, authentication
• More than one channel of communication
• Keeping your correspondence history
• Processing time zones
• Working with languages other than English
1.5 Requirements
• The server and the c代 写program、C/C++
代做程序编程语言lient must be written in the language of the C
• Make should be used as an build system
• The code must be successfully compiled and worked for Linux and MacOS
• Valgrind and Google Thread Sanitizer should not ﬁnd errors in the code
server.c
1 #include 
2 #include 
3
4 #include 
5 #include 
6 #include 
7
8 #include 
9
10 int main(int argc, char *argv[]) {
11 int sockfd, newsockfd;
12 uint16_t portno;
13 unsigned int clilen;
14 char buffer[256];
15 struct sockaddr_in serv_addr, cli_addr;
16 ssize_t n;
17
18 /* First call to socket() function */
19 sockfd = socket(AF_INET, SOCK_STREAM, 0);
20
21 if (sockfd 
2 #include 
3
4 #include 
5 #include 
6 #include 
7
8 #include 
9
10 int main(int argc, char *argv[]) {
11 int sockfd, n;
12 uint16_t portno;
13 struct sockaddr_in serv_addr;
14 struct hostent *server;
15
16 char buffer[256];
17
18 if (argc h_addr, (char *) serv_addr.sin_addr.s_addr, (size_t) server->h_length);
43 serv_addr.sin_port = htons(portno);
44
45 /* Now connect to the server */
46 if (connect(sockfd, (struct sockaddr *) serv_addr, sizeof(serv_addr)) < 0) {
47 perror("ERROR connecting");
48 exit(1);
49 }
50
51 /* Now ask for a message from the user, this message
52 * will be read by server
53 */
54
55 printf("Please enter the message: ");
56 bzero(buffer, 256);
57 fgets(buffer, 255, stdin);
58
59 /* Send message to the server */
60 n = write(sockfd, buffer, strlen(buffer));
61
62 if (n < 0) {
63 perror("ERROR writing to socket");
64 exit(1);
65 }
66
67 /* Now read server response */
68 bzero(buffer, 256);
69 n = read(sockfd, buffer, 255);
70
71 if (n < 0) {
72 perror("ERROR reading from socket");
73 exit(1);
74 }
75
76 printf("%s\n", buffer);
77 return 0;
78 }
5

         
加QQ：99515681  WX：codinghelp
