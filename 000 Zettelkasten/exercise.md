## Server.c
added a numConnections variable that is incremented after a connection in the while loop, which returns once it is equal to 2 (inititialized at 0)


#include "csapp.h"

#include <stdio.h>

#include <stdlib.h>

#include <sys/socket.h>

#include <unistd.h>

#include <strings.h>

#include <netinet/in.h>

#include <netdb.h>

#define MAXLINE 8192 /* Max text line length */

typedef struct sockaddr SA;

  

int open_listenfd(int port) {

struct sockaddr_in serveraddr;

int listenfd = socket(AF_INET, SOCK_STREAM, 0);

bzero((char *) &serveraddr, sizeof(serveraddr));

serveraddr.sin_port = htons((unsigned short)port);

serveraddr.sin_family = AF_INET;

bind(listenfd, (SA*)&serveraddr, sizeof(serveraddr));

listen(listenfd, LISTENQ);

return(listenfd);

}

  

int main(int argc, char **argv)

{

int port = atoi(argv[1]), numConnections;

int listenfd, connfd;

struct sockaddr_in clientaddr;

socklen_t clientlen = sizeof(clientaddr);

listenfd = open_listenfd(port);

while(1) {

connfd = accept(listenfd, (SA*)&clientaddr, &clientlen);

printf("Socket connected: %d\n", connfd);

if(numConnections++ == 2) {

close(listenfd);

return 0;

}

}

return 1;

}
