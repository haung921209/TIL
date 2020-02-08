3.1 Describe the differences among short-term, medium-term, and long-term scheduling.

Ans.

a. Short-term (CPU scheduler) - selects from jobs in memory those jobs that are ready to execute and allocates the CPU to them.
b. Medium-term - used especially with time-sharing systems as an intermediate scheduling level. A swapping scheme is implemented to remove partially run programs from memory and reinstate them later to continue where they left off.
c. Long-term (job scheduler) - determines which jobs are brought into memory for processing.

The primary difference is in the frequency of their execution. The short-term must select a new process quite often. Long-term is used much less often since it handles placing jobs in the system and may wait a while for a job to finish before it admits another one.

---

3.2 Describe the actions taken by a kernel to context-switch between processes

Ans. 

1. In response to a clock interrupt, the OS saves the PC and user stack pointer of the currently executing process, and transfers control to the kernel clock interrupt handler,
2. The clock interrupt handler saves the rest of the registers, as well as other machine state, such as the state of the floating point registers, in the process PCB
3. The OS invokes the scheduler to determine the next process to execute,
4. The OS then retrieves the state of the next process from its PCB, and restores the registers. This restore operation takes the processor back to the state in which this process was previously interrupted, executing in user code with user mode privileges.

- - -

3.4 Explain the role of the init process on UNIX and Linux systems in regard to process termination.

Ans.

Based on the relationship between a parent and child process, if a parent did not invoke wait() and simply terminated (making the child process an orphan), UNIX and Linux Systems assign these orphans the init process. This process periodically invokes wait(), where it will continue until these orphans finish their final statement before exiting using exit().


- - -

3.5 Including the initial parent process, how many processes are created by the program shown in Figure 3.32?

```c

#include <stdio.h>
#include <unistd.h>

int main(){
    int i;
    for(i = 0; i < 4; i++)
        fork();
    return 0;
}
/*Figure 3.32 code*/

```

Ans. 

16 processes are created. The program online includes printf() statements to better understand how many processes have been created.


- - -

3.6 Explain the circumstances under which the line of code marked printf("LINE J") in Figure 3.32 will be reached



```c

#include <sys/type.h>
#include <stdio.h>
#include <unistd.h>

int main(){
    pid_t pid;
    /*fork a child process*/
    pid = fork();
    if(pid<0){/* error occured */
        fprintf(stderr, "Fork Failed");
        return 1;
    }
    else if(pid == 0){
        execlp("/bin/ls","ls",NULL);
        printf("LINE J");
    }
    else{/* parrent process */
        /* parent will wait for the child to complete */
        wait(NULL);
        printf("Child Complete");
    }
    return 0;
}

/*Figure 3.32 code*/

```

Ans. 

The call to exec() replaces the address space of the process with the program specified as the parameter to exec(). If the call to exec() succeeds, the new program is now running and control from the call to exec() never returns. In this scenario, the line printf("Line J"); would never be performed. However, If an error occurs in the call to exec(), the function returns control and therefor the line printf("Line J"); would be performed.

- - -

3.7 Using the program in Figure 3.33, identify the values of pid at lines A, Bm, C, and D.(Assume that the actual pids of the parent and child are 2600 and 2603, respectively.)

```c
#include <sys/types.h>
#include <stdio.h>
#include <unistd.h>

int main(){
    pid_t pid, pid1;
    /* fork a child process */
    pid = fork();
    
    if(pid < 0){ /*error occured*/
        fprintf(stderr, "Fork Failed");
        return 1;
    }
    else if(pid == 0){/* child process */
        pid1 = getpid();
        printf("child: pid = %d", pid); /* A */
        printf("child: pid1 = %d", pid1); /* B */
    }
    else{ /* parent process */
        pid1 = getpid();
        printf("parent: pid = %d", pid); /* C */
        printf("parent: pid1 = %d", pid1); /* D */
        wait(NULL);
    }
    return 0;
}

/*Figure 3.33 code*/




```

Ans. A = 0, B = 2603, C = 2603, D = 2600

- - -

3.8 Give an example of a situation in which ordinary pipes are more suitable than named pipes and an example of a situation in which named pipes are more suitable than ordinary pipes.

Ans. 
    
Simple communication works well with ordinary pipes. For example, assume we have a process tha counts characters in a file. An ordinary pipe can be used where the producer writes the file to the pipe and the consumer reads the files and counts the number of characters in the file. Next, for an example where named pipes are more suitable, consider the situation where several processes may write messages to a log. When processes wish to write a message to the log, they write it to the named pipe. A server reads the messages from the named pipe and writes them to the log file.


- - -

3.9 Consider the RPC mechanism. Describe the undesirble consequences that could arise from not enforcing either the "at most once" or "exactly once" semantic. Describe possible uses for a mechanism that has neither of these guarantees.

Ans.

If an RPC mechanism cannot support either the “at most once” or “at least once” semantics, then the RPC server cannot guarantee that a remote procedure will not be invoked multiple occurrences. Consider if a remote procedure were withdrawing money from a bank account on a system that did not support these semantics. It is possible that a single invocation of the remote procedure might lead to multiple withdrawals on the server.

- For a system to support either of these semantics generally requires the server maintain some form of client state such as the timestamp described in the text.
- If a system were unable to support either of these semantics, then such a system could only safely
provide remote procedures that do not alter data or provide time-sensitive results. Using our bank account as an example, we certainly require “at most once” or “at least once” semantics for performing a withdrawal (or deposit!). However, an inquiry into an account balance or other account information such as name, address, etc. does not require these semantics.

- - -

3.10 Using the program shown in Figure 3.34, explain what the output will be at lines X and Y.

```c

#include <sys/types.h>
#include <stdio.h>
#include <unistd.h>

#define SIZE 5

int nums[SIZE] = {0, 1, 2, 3, 4};

int main(){
    int i;
    pid_t pid;
    pid = fork();
    
    if(pid == 0){
        for( i = 0 ; i < SIZE ; i++){
            nums[i] *= -i;
            printf("CHILD: %d ", nums[i]); /* LINE X */
        }
    }
    else if(pid > 0){
        wait(NULL);
        for (i = 0 ; i < SIZE; i++)
            printf("PARENT: %d", nums[i]); /* LINE Y */
    }
    return 0;
}


/*Figure 3.34 code*/


```

Ans. 

Because the child is a copy of the parent, any changes the child makes will occur in its copy of the data and won't be reflected in the parent. As a result, the values output by the child at line X are 0, -1, -4, -9, -16. The values output by the parent at line Y are 0, 1, 2, 3, 4.


- - -

3.11 What are the benefits and the disadvantages of each of the following? Consider both the system level and the programmer level.

    a. Synchronous and asynchronous communication
    b. Automatic and explicit buffering
    c. Send by copy and send by reference
    d. Fixed-sized and variable-sized messages
Ans.
    
a. Synchronous and asynchronous communication—A benefit of synchronous communication is that it allows a rendezvous between the sender and receiver. A disadvantage of a blocking send is that a rendezvous may not be required and the message could be delivered asynchronously. As a result, message-passing systems often provide both forms of synchronization.
    
b. Automatic and explicit buffering—Automatic buffering provides a queue with indefinite length, thus ensuring the sender will never have to block while waiting to copy a message. There are no specifications on how automatic buffering will be provided; one scheme may reserve sufficiently large memory where much of the memory is wasted. Explicit buffering specifies how large the buffer is. In this situation, the sender may be blocked while waiting for available space in the queue. However, it is less likely that memory will be wasted with explicit buffering. 
    
c. Send by copy and send by reference—Send by copy does not allow the receiver to alter the state of the parameter; send by reference does allow it. A benefit of send by reference is that it allows the programmer to write a distributed version of a centralized application. Java’s RMI provides both; however, passing a parameter by reference requires declaring the parameter as a remote object as well.
    
d. Fixed-sized and variable-sized messages—The implications of this are mostly related to buffering issues; with fixed-size messages, a buffer with a specific size can hold a known number of messages. The number of variable-sized messages that can be held by such a buffer is unknown. Consider how Windows 2000 handles this situation: with fixed-sized messages (anything < 256 bytes), the messages are copied from the address space of the sender to the address space of the receiving process. Larger messages (i.e. variable-sized messages) use shared memory to pass the message.













