# Labsheet 13: CPU Scheduling

___

## Objectives

1. To understand what CPU scheduling is.
2. To use FCFS and SJF algorithm in C.

## Theory  
  
CPU scheduling is the process of determining which process or thread should be executed by the central processing unit (CPU) next. It is a fundamental aspect of operating systems, as it enables the efficient use of the CPU and the fair distribution of processing time among multiple processes or threads.

There are several different CPU scheduling algorithms, each with its own strengths and weaknesses. Some common algorithms include:

1. First-Come, First-Served (FCFS) scheduling, which runs processes in the order they are received
2. Shortest-Job-First (SJF) scheduling, which runs the process with the shortest expected run time next
3. Priority scheduling, which runs the process with the highest priority first
4. Round Robin scheduling, which runs each process for a fixed time quantum before switching to the next one.

The choice of scheduling algorithm depends on the specific requirements of the operating system and the system's usage.


## Activity

1. Define burst time, waiting time, and turnaround time.

    - Burst time is the amount of time a process requires to complete its execution.

    - Waiting time is the amount of time a process spends waiting in the ready queue for the CPU to be allocated to it.

    - Turnaround time is the total time from the process's arrival to completion of its execution. It is equal to the waiting time plus the burst time.

2.  Run program 8.1 to find out the waiting time (wt), turnaround time(tat), waiting time, average (wtavg) and turnaround time average (tatavg) for the following problem.

    - P0: 5
    - P1: 10
    - P2: 8
    - P3: 4
    - P4: 2

    ```

    Enter number of processes: maximum 20: 5
    Enter process burst time: 

    p[1]:: 5
    p[2]:: 10
    p[3]:: 8
    p[4]:: 4
    p[5]:: 2
         
    PROCESS        BURST TIME       WAITING TIME    TURNAROUND TIME

    P0              5               0               5

    Average Waiting Time -- 14.000000
    Average Turnaround Time -- 19.799999

    P1              10              5               15

    Average Waiting Time -- 14.000000
    Average Turnaround Time -- 19.799999

    P2              8               15              23

    Average Waiting Time -- 14.000000
    Average Turnaround Time -- 19.799999

    P3              4               23              27

    Average Waiting Time -- 14.000000
    Average Turnaround Time -- 19.799999

    P4              2               27              29
    
    Average Waiting Time -- 14.000000
    Average Turnaround Time -- 19.799999%         

3. SJF.c

#include<stdio.h>

    ```
    int main() {

        int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp;
        float avg_wt,avg_tat;
        printf("\nEnter number of process:");
        scanf("%d",&n);
    
        printf("\nEnter Burst Time - ");
        for(i=0;i<n;i++)
        {
            printf("p%d: ",i+1);
            scanf("%d",&bt[i]);
            p[i]=i+1;         
        }
    
        for(i=0;i<n;i++)
        {
            pos=i;
            for(j=i+1;j<n;j++)
            {
                if(bt[j]<bt[pos])
                    pos=j;
            }
    
            temp=bt[i];
            bt[i]=bt[pos];
            bt[pos]=temp;
    
            temp=p[i];
            p[i]=p[pos];
            p[pos]=temp;
        }
    
        wt[0]=0;            
    
    
        for(i=1;i<n;i++)
        {
            wt[i]=0;
            for(j=0;j<i;j++)
                wt[i]+=bt[j];
    
            total+=wt[i];
        }
    
        avg_wt=(float)total/n;      
        total=0;
    
        printf("\nProcess\tBurst Time\tWaiting Time\tTurnaround Time");
        for(i=0;i<n;i++)
        {
            tat[i]=bt[i]+wt[i];   
            total+=tat[i];
            printf("\np%d\t%d\t%d\t%d",p[i],bt[i],wt[i],tat[i]);
        }
    
        avg_tat=(float)total/n;    
        printf("\nAverage Waiting Time = %f",avg_wt);
        printf("\nAverage Turnaround Time = %f",avg_tat);
    }
    

    Output:

    Enter number of process:5

    Enter Burst Time - p1: 5
    p2: 10
    p3: 8
    p4: 4
    p5: 2

    Process Burst Time      Waiting Time    Turnaround Time
    p5      2       0       2
    p4      4       2       6
    p1      5       6       11
    p3      8       11      19
    p2      10      19      29
    Average Waiting Time = 7.600000
    Average Turnaround Time = 13.400000%  

    ```

3. Based on the output of question 2 and 3 which algorithm do you recommend to solve the above problem and why?

- I recommend using SJF to solve the above problem, since the average waiting and turnaround time are both lower than FCFS, however, the mileage may vary based on the type of problem.


## Observation and Conclusion

Hence, we learned how to use FCFS and SJF algorithm to calculate average waiting and turnaround time for processes in C.
