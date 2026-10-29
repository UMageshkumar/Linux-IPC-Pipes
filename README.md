# Linux-IPC--Pipes
Linux-IPC-Pipes


# Ex03-Linux IPC - Pipes

# AIM:
To write a C program that illustrate communication between two process using unnamed and named pipes

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - pipe(), fifo()

### Step 3:

Testing the C Program for the desired output. 

# PROGRAM:

## C Program that illustrate communication between two process using unnamed pipes using Linux API system calls

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/wait.h>

int main() {
    int p[2];
    pid_t pid;
    char message[] = "hello world";
    char buffer[100];

    if (pipe(p) == -1) {
        perror("pipe");
        return 1;
    }

    pid = fork();

    if (pid == 0) {
        close(p[1]);
        read(p[0], buffer, sizeof(buffer));
        printf("Message received: %s\n", buffer);
        close(p[0]);
    } else if (pid > 0) {
        close(p[0]);
        write(p[1], message, strlen(message) + 1);
        close(p[1]);
        wait(NULL);
    } else {
        perror("fork");
        return 1;
    }

    return 0;
}
```



## OUTPUT
<img width="2172" height="724" alt="01" src="https://github.com/user-attachments/assets/5ca19c7e-07b2-46c2-ab31-3207c0e8c13f" />


## C Program that illustrate communication between two process using named pipes using Linux API system calls

```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>

int main() {
    int res = mkfifo("/tmp/my_fifo", 0777);

    if (res == 0)
        printf("FIFO created\n");
    else
        perror("mkfifo");

    return 0;
}
```



## OUTPUT
<img width="1388" height="693" alt="image" src="https://github.com/user-attachments/assets/fb3fdf92-3ee8-473d-be20-3612971db062" />


# RESULT:
The program is executed successfully.
