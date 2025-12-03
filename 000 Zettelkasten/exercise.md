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

![[Pasted image 20251202181829.png]]
