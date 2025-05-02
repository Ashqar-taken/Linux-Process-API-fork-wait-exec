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
```
Developed by: Ashqar Ahamed S.T
Register no: 212224240018
```
## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
	int pid = fork();
	
	if(pid == 0)
	{
		printf("I am child, my PID is %d\n", getpid());
		printf("My parent PID is: %d\n", getppid());
		sleep(30);
	}
	else
	{
		printf("I am parent, my PID is %d\n",getpid());
		wait(NULL);
	}
return 0;
}
```
## OUTPUT
![1(1)](https://github.com/user-attachments/assets/cf5b702a-241f-449c-ba5f-d997e0a2a617)
![1(2)](https://github.com/user-attachments/assets/69341356-c13d-4125-9f19-6fb92ee786e2)


## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main()
{
	int status;
	printf("Running ps with execl\n");
	if(fork() == 0) 
	{
		execl("ps","ps","-f",NULL);
		perror("execl failed");
		exit(1);
	}
	wait(&status);
	if(WIFEXITED(status))
		printf("Child exited with status: %d\n",WEXITSTATUS(status));
	else
		printf("Childdid not exit successfully\n");
	
	printf("Running ps with execlp (without full path\n");
	if(fork() == 0)
	{
		execlp("ps","ps","-f",NULL);
		perror("execlp failed");
		exit(1);
	}
	wait(&status);
	
	if(WIFEXITED(status))
		printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
	else
		printf("Child did not exit syscessfully\n");

	printf("Done.\n");
	return 0;
}
```

##  OUTPUT
![2](https://github.com/user-attachments/assets/9d99e4a8-fee7-4617-bac9-fff5b5bfaa15)



# RESULT:
The programs are executed successfully.
