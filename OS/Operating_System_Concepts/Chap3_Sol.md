3.1

---

3.2 Describe the actions taken by a kernel to context-switch between processes

Ans. 
1. In response to a clock interrupt, the OS saves the PC and user stack pointer of the currently executing process, and transfers control to the kernel clock interrupt handler,
2. The clock interrupt handler saves the rest of the registers, as well as other machine state, such as the state of the floating point registers, in the process PCB
3. The OS invokes the scheduler to determine the next process to execute,
4. The OS then retrieves the state of the next process from its PCB, and restores the registers. This restore operation takes the processor back to the state in which this process was previously interrupted, executing in user code with user mode privileges.

- - -

3.3 construct a process tree similar to figure 3.8. to obtain process information for the UNIX or LINUX system, use the command ps -ael

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


```