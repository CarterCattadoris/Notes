1: basic file IO
2: IP Address and port number
3: socket, bind and listen
4: socket and connect
5: connect accept and read

6:
```
#include <netdb.h>
#include <stdio.h>
#include <stdlib.h>
#include <arpa/inet.h>
int main(int argc, char **argv)
{
    struct hostent *hp = gethostbyname("ecs.syracuse.edu");
    if (hp != NULL)
    {
        printf("%s=\n", hp->h_name);
        unsigned int i = 0;
        while (hp->h_addr_list[i] != NULL)
        {
            printf("\t%s\n", inet_ntoa(*(struct in_addr *)(hp->h_addr_list[i]))); 
            i++;
        }
        printf("\n");
    }
}
```

7:
```
#include <stdio.h>
#include <arpa/inet.h>

int main() {
    struct in_addr addr;
    addr.s_addr = -1;
    printf("%s\n", inet_ntoa(addr));
    return 0;
}
```

8:
```
#include <stdio.h>
#include <arpa/inet.h>

int main() {
    struct in_addr addr;
    inet_aton("225.2.0.0", &addr);
    printf("%u\n", addr.s_addr);
    return 0;
}
```

9:

## Server.c
```
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

int port = atoi(argv[1]);

int listenfd, connfd1, connfd2;

struct sockaddr_in clientaddr;

socklen_t clientlen = sizeof(clientaddr);

char buf2[MAXLINE];

int n;

  

listenfd = open_listenfd(port);

  
  

connfd1 = accept(listenfd, (SA*)&clientaddr, &clientlen);

printf("Client 1 connected\n");

n = read(connfd1, buf2, MAXLINE - 1);

buf2[n] = '\0';

int num1 = atoi(buf2);

printf("Received from client 1: %d\n", num1);

close (connfd1);

  

connfd2 = accept(listenfd, (SA*)&clientaddr, &clientlen);

printf("Client 2 connected\n");

n = read(connfd2, buf2, MAXLINE - 1);

buf2[n] = '\0';

int num2 = atoi(buf2);

printf("Received from client 2: %d\n", num2);

close (connfd2);

printf("Sum: %d\n", num1 + num2);

  

close(listenfd);

return 1;

}
```


## client.c
```
#include "csapp.h"

#include <stdio.h>

#include <stdlib.h>

#include <sys/socket.h>

#include <unistd.h>

#include <strings.h>

#include <arpa/inet.h>

#include <netinet/in.h>

#include <netdb.h>

#define MAXLINE 8192 /* Max text line length */

typedef struct sockaddr SA;

  

int open_clientfd(char *hostname, int port) {

struct sockaddr_in serveraddr;

int clientfd = socket(AF_INET, SOCK_STREAM, 0);

  

struct hostent *hp = gethostbyname(hostname);

bzero((char *) &serveraddr, sizeof(serveraddr));

bcopy ((char *)hp->h_addr_list[0],

(char *)&serveraddr.sin_addr.s_addr, hp->h_length);

serveraddr.sin_port = htons(port);

serveraddr.sin_family = AF_INET;

connect(clientfd, (SA*)&serveraddr, sizeof(serveraddr));

return(clientfd);

}

  

int main(int argc, char **argv)

{

if (argc < 3) {

fprintf(stderr, "Usage: %s <host> <port>\n", argv[0]);

return 1;

}

  

int clientfd, port = atoi(argv[2]);

if (port <= 0) {

fprintf(stderr, "Invalid port: %s\n", argv[2]);

return 1;

}

  

char *host = argv[1];

char buf[MAXLINE];

clientfd = open_clientfd(host, port);

printf("Enter number: ");

fgets(buf, MAXLINE, stdin);

write(clientfd, buf, strlen(buf));

close(clientfd);

return 0;

}
```

![[Pasted image 20251202181829.png]]
