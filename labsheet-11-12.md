# Labsheet 11-12: Processes in UNIX systems

___

## Objectives

1. To understand how inter-process communication works in C.
2. To understand pipes, descriptors and more in IPC.

## Theory  
  
Inter-process communication (IPC) is a method for different processes to communicate with each other and synchronize their actions. IPC mechanisms vary depending on the operating system, but common methods include pipes, message queues, semaphores, and shared memory. These mechanisms allow processes to share data and communicate with each other, even if they are running on different processors or in different address spaces. IPC is an essential feature of modern operating systems, as it enables the concurrent execution of multiple processes and the sharing of resources.


## Activity

1. ipcmgmt.c

    ```
    #include<stdio.h>
    #include<unistd.h>
    #include<stdlib.h>

    int exflag = 0;
    char pipeline[2];

    int main() {
        char c, bfr;
        pipe(pipeline);
        if(!fork()){
            printf("Press a key!");
            scanf("%c", &c);
            write(pipeline[0], &c, 1);
            printf("Written successfully!"); 
            exit(2);
        } else {
            read(pipeline[1], &bfr, 1);
            printf("Character received: %c", bfr);
            exit(3);
        }

    }
    ```

2. pipebomb.c

    ```
    #include<stdio.h>
    #include<stdlib.h>
    #include<unistd.h>

    int exflags = 0;

    int main() {
        int pfd[2];
        pipe(pfd);
        if(pipe(pfd)<0) printf("Error");
        if(!fork()){
            char data;
            printf("Child: press a key to exit!\n");
            scanf("%c", &data);
            write(pfd[0], &data, 1);
            printf("exiting child..");
            exflags = 1;
        } else {
            while(exflags == 0);
            char data;
            printf("Parent: reading pipe..\n");
            read(pfd[1], &data, 1);
            printf("value from child is: %c", data);	
            exit(0);
        };
    }
    ```

3. msgsz.c

    ```
    #include<stdio.h>
    #include<stdlib.h>
    #include<unistd.h>

    int main(){
        char *msg1 = "hello1";
        char *msg2 = "hello2";
        char *msg3 = "hello3";

        char inbuf[16];

        int p[2], j;

        pipe(p);

        write(p[1],msg1, 6);
        write(p[1], msg2, 6);
        write(p[1], msg3, 6);

        for(j=0;j&lt;3;j++){
            read(p[0],inbuf,msgsz);
            printf(“%s\n”,inbuf);
        }
        exit(0);
    }
    ```

4. Modifying to change parent & child data R-W order in program 2, we get

    ```
    #include<stdio.h>
    #include<stdlib.h>
    #include<unistd.h>

    int exflags = 0;

    int main() {
        int pfd[2];
        pipe(pfd);
        if(pipe(pfd)<0) printf("Error");
        if(!fork()){
            char data;
            printf("Child: press a key to exit!\n");
            scanf("%c", &data);
            write(pfd[1], &data, 1);
            printf("exiting child..");
            exflags = 1;
        } else {
            while(exflags == 0);
            char data;
            printf("Parent: reading pipe..\n");
            read(pfd[0], &data, 1);
            printf("value from child is: %c", data);	
            exit(0);
        };
    }
    ```

5. Descriptor.c

    ``` 
    int main() {

        char *msg=”hello1”;
        char inbuf[msgsz];
        int p[2],pid,j;
        pipe(p);

        pid=fork();

        if(pid>0) {
            close(p[0]);
            write(p[1],msg1,msgsz);
            write(p[0], msg1, msgsz); // fails, p[0] is closed
        }

        if(pid==0) {
            close(p[1]);
            read(p[0],inbuf,msgsz);
            printf(“%s\n”,inbuf);
        }
        exit(0);
    }
    ```
Here, the descriptors are working just as intended.


## Observation and Conclusion

Hence, we learned how pipes, IPC, and close() work in C in *NIX systems.












