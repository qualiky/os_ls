# Labsheet 10: Processes in UNIX systems

___

## Objectives

1. To understand processes, syscalls, child and parent, forks, etc.
2. To understand process lifecycle and creation via C.

## Theory  
  
Each process in a Linux system is identified by its unique process ID, referred to as pid. Process IDs are 1-32768 numbers that are assigned sequentially by UNIX systems as new process are created. In MacOS, this value can be upto 99998 and is not tunable.

Every process also has a parent process (except init). Thus, we can think the processes in the Linux are arranged in a tree, with the init process at its root. The parent process ID, or ppid, is simply the process ID of the process's parent. Most of the process manipulation functions are declared in the header file <unistd.h>. A program can obtain the process ID of the process it's running with the getpid() system call, and it can obtain the process ID of its parent process with the getppid() system call.


## Activity

1. print_pid.c

    ```
    #include<stdio.h>
    #include<unistd.h>
    #include<stdlib.h>

    int main() {
        int pid, ppid;
        pid = getpid();
        ppid = getppid();
        printf(“The Process ID is %d \n”, pid);
        printf(“The Parent Process ID is %d \n”, ppid);
        return 0;
    }
    ```

2. syscalldemo.c

    ```
    #include<stdlib.h>
    int main() {
        int r_value;
        r_value = system(“ls -l /”);
        return r_value;
    }
    ```

3. forkmanager.c

    ```
    #include <stdio.h>
    #include <unistd.h>
    #include<stdlib.h>

    int main() {
        pid_t pid;
        pid = fork();

        if (pid < 0) {
            perror("fork() failed");
            return 1;
        } else if (pid == 0) {
            printf("I am the child process\n");
        } else {
            printf("I am the parent process\n");
        }
        return 0;
    }
    ```

4. forkingexmp.c

    ```
    #include < stdio.h>
    #include <unistd.h>

    int main() {
        int pid;
        printf(“The main program process ID is %d \n”, (int) getpid());
        pid = fork();
        if (pid != 0){
            printf(“This is the parent process, with id % d \n”, (int) getpid());
            printf(“The child process ID is %d \n”, pid);
        } else printf(“ This is the child process, with id %d\n”, (int) getpid());
        return 0;
    }
    ```
5. multipleforks.c

    ```
    #include<stdlib.h>
    int main() {

        for (int i=0;i<4;i++) {
            if(fork() == 0) {
                printf("[child] pid %d from [parent] pid %d\n",getpid(),getppid());
                exit(0);
            }
        }

        return 0;
    }
    ```
6. 






## Observation and Conclusion

Hence, we learned the basics of process management in UNIX systems.
