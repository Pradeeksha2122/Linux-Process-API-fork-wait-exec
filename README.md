# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls

```
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main(void)
{	//variable to store calling function's process id
	pid_t process_id;
	//variable to store parent function's process id
	pid_t p_process_id;
	//getpid() - will return process id of calling function
	process_id = getpid();
	//getppid() - will return process id of parent function
	p_process_id = getppid();
	//printing the process ids

//printing the process ids
	printf("The process id: %d\n",process_id);
	printf("The process id of parent function: %d\n",p_process_id);
	return 0; 
}

```
gcc forkcheck.c -o forkcheck.o

chmod 755 forkcheck.o

./forkcheck.o












## OUTPUT
<img width="758" height="255" alt="image" src="https://github.com/user-attachments/assets/d2ce70f7-c184-41fa-a917-1c388d35e740" />










## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

nano exitwait.c
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execlp\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        exit(1);
    }
    wait(&status);
    
    printf("Done.\n");
    return 0;
}

```
gcc exitwait.c -o exitwait.o

chmod 755 exitwait.o

./exitwait.o

























## OUTPUT
<img width="480" height="276" alt="image" src="https://github.com/user-attachments/assets/22cba131-1922-478f-b4bc-66109159e3e4" />






















# RESULT:
The programs are executed successfully.
