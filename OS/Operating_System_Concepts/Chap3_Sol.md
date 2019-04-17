3.1

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

Ans. The call to exec() replaces the address space of the process with the program specified as the parameter to exec(). If the call to exec() succeeds, the new program is now running and control from the call to exec() never returns. In this scenario, the line printf("Line J"); would never be performed. However, If an error occurs in the call to exec(), the function returns control and therefor the line printf("Line J"); would be performed.

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
















