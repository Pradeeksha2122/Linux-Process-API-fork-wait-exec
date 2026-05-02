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
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>   // <-- IMPORTANT

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2);
    } else { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    }

    return 0;
}




## OUTPUT

<img width="910" height="970" alt="image" src="https://github.com/user-attachments/assets/6f3f24b2-12bd-4242-9e73-97c5e0501b5c" />








## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() familyy
 
```bash
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    int status;

    printf("Running ps with execlp\n");

    if (fork() == 0) {
        execlp("ps", "ps", "ax", NULL);
        exit(1); // runs only if execlp fails
    }
    wait(&status);

    if (WIFEXITED(status))
        printf("Child exited with status %d\n", WEXITSTATUS(status));
    else
        printf("Child did not exit successfully\n");

    printf("Done.\n");

    printf("Running ps with full path\n");

    if (fork() == 0) {
        execl("/bin/ps", "ps", "ax", NULL);
        exit(1);
    }
    wait(&status);

    if (WIFEXITED(status))
        printf("Child exited with status %d\n", WEXITSTATUS(status));
    else
        printf("Child did not exit successfully\n");

    printf("Done.\n");

    return 0;
}





## Output
<img width="918" height="745" alt="image" src="https://github.com/user-attachments/assets/ed6a38c4-7283-4d3e-be47-3142f4afcca5" />
<img width="836" height="733" alt="image" src="https://github.com/user-attachments/assets/b638aebe-0a3c-4a9c-90c8-2e171ba44483" />
<img width="897" height="728" alt="image" src="https://github.com/user-attachments/assets/2c32f98c-5cac-4975-b34c-e33e356f2ff5" />
<img width="885" height="735" alt="image" src="https://github.com/user-attachments/assets/cccf534f-243d-4a2f-84eb-d141be2f8611" />
<img width="920" height="695" alt="image" src="https://github.com/user-attachments/assets/d906b410-c476-4616-92e2-eb23446685bb" />
<img width="924" height="682" alt="image" src="https://github.com/user-attachments/assets/23a844cf-ffd6-4510-a6c9-1e869eacc0f4" />
<img width="924" height="718" alt="image" src="https://github.com/user-attachments/assets/96f2ddf7-102e-47c0-8a1b-831e590d684e" />
<img width="921" height="736" alt="image" src="https://github.com/user-attachments/assets/f110dff7-ebeb-4fb9-ba4c-4c84fdbb7cda" />
<img width="913" height="250" alt="image" src="https://github.com/user-attachments/assets/0ace62ae-1a4f-4a87-937e-75be3c6df6c9" />








## C Program to execute Linux system commands using Linux API system calls exec() family
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}

## output

<img width="637" height="331" alt="image" src="https://github.com/user-attachments/assets/8a59ad7e-f724-4007-b64f-0c5bffe097c4" />

~~~









# RESULT:
The programs are executed successfully.
