# 프로세스 생명 주기 요점 정리

---



## 1. 프로세스란?



`process is a program in execution`




![pcb](https://user-images.githubusercontent.com/14533484/56672022-a355bc80-66f0-11e9-96cc-d753efac4108.png)


(1) state와 flag의 특징



<img width="609" alt="스크린샷 2019-04-25 오전 8 31 09" src="https://user-images.githubusercontent.com/14533484/56700302-86db7380-6734-11e9-9eac-f75c13bc8a6e.png">


state의 경우, volatile long 자료형으로 선언된 변수입니다. 이 volatile의 경우에는, 이 선언된 변수는 최적화에서 제외하여 항상 메모리에 접근하도록 하는 자료형입니다.

예를 들면


~~~c
while (i < 10)
    i++;
~~~

와 같이 표현한 것을 컴파일러는

~~~c
int i=10;
~~~

과 같이 최적화 해버립니다.(i에 그냥 10을 할당해버림.)

volatile로 선언한다는 이야기는, 반복할 때마다 항상 i의 메모리에 접근해야 하므로, 컴파일러가 while 반복문을 없애지 않는다는 이야기와도 같습니다. 메모리 관리 등을 위해서라도 state에 대한 정확한 정보는 중요하기 때문에, volatile로 선언하여 안정성을 챙기는 것입니다.



<img width="621" alt="스크린샷 2019-04-25 오전 8 31 14" src="https://user-images.githubusercontent.com/14533484/56700301-86db7380-6734-11e9-8d7e-47b70a2f870b.png">

0보다 큰 process의 state에 대해서도 다음과 같이 정리해두었습니다. 이는 우리가 흔히 아는 프로세스 상태도에서 각 상태간의 번호에 대해서 이야기 해주고 있습니다. 즉 PCB에서는 프로세스가 어떤 상태인지 효과적으로 알려주기 위해서 위와 같이 일정 변수의 값을 이용하여 보여주는 방식으로 사용하고 있습니다.






다음은 flag입니다.


<img width="612" alt="스크린샷 2019-04-25 오전 8 42 37" src="https://user-images.githubusercontent.com/14533484/56700609-26e5cc80-6736-11e9-9df6-1247dc8e2ee3.png">

flag는 unsigned long으로 선언된 변수입니다. unsigned란, 0보다 작은 값을 배제하고 대신에 그 값에 할당할 수 있을 주소 값의 범위를 0보다 큰 범위에 할당하여, 그 범위에서 좀 더 다양한 값을 나타낼 수 있도록 한 값입니다. 아무래도 프로세스 자체의 상태를 나타내기는 하지만, state값과는 다르게, 프로세스가 정상적으로 다루어 진다는 전제 하에 그 상태를 나타내는 변수이기 때문에, 메모리에 안정적으로 접근하는 것이 아니라, 효율적으로 다룰 수 있는 것이 더 낫다라는 전제 하에 volatile을 사용하지 않은 것으로 보입니다.

다음은 flag의 값들입니다.

<img width="627" alt="스크린샷 2019-04-25 오전 8 42 46" src="https://user-images.githubusercontent.com/14533484/56700613-29482680-6736-11e9-9add-6e8fffce8484.png">

flag의 경우에는 변수는 하나이지만, 그 값들을 사용하는 경우에 여러 값을 동시에 나타낼 수 있도록 설계되어있습니다. 바로 비트 연산으로, 모든 경우의 수를 다 더하더라도, 자릿수가 정해져 있으므로 결과값에 어떤 상태 값이 더하여졌는지에 대해서는 언제나 알 수 있습니다. 추가로, 값의 다양성을 더 보여주기 위해 큰 범위가 필요했고, 그렇기 때문에 unsigned로 표현한 것도 있습니다..



(2) 자원 관리

<img width="612" alt="스크린샷 2019-04-25 오전 9 45 11" src="https://user-images.githubusercontent.com/14533484/56702416-daeb5580-673e-11e9-98f0-4e8d1712e6e0.png">

자원관리를 하는 변수에는 rlimit이 있습니다. 



이는 setrlimit() system call로 변경이 가능하고, kernel/sys.c파일에 sys_setrlimit() 함수로 구현이 되어 있습니다.


~~~c
setrlimit(int resource, const struct rlimit *rlp);
~~~

로 선언 되어있는 setrlimits는


<img width="605" alt="스크린샷 2019-04-25 오전 9 46 51" src="https://user-images.githubusercontent.com/14533484/56702449-12f29880-673f-11e9-9aa4-1d78d99b40b0.png">

아래와 같은 자원들을 조절하는데 도움을 줍니다.



~~~c

struct task_struct {

/* these are hardcoded - don't touch */

             volatile long state;            /* -1 unrunnable, 0 runnable, >0 stopped */

             long counter;

             long priority;

             unsigned long signal;

             unsigned long blocked;   /* bitmap of masked signals */

             unsigned long flags;        /* per process flags, defined below */

             int errno;

             long debugreg[8];  /* Hardware debugging registers */

             struct exec_domain *exec_domain;

/* various fields */

             struct linux_binfmt *binfmt;

             struct task_struct *next_task, *prev_task;

             struct task_struct *next_run,  *prev_run;

             unsigned long saved_kernel_stack;

             unsigned long kernel_stack_page;

             int exit_code, exit_signal;

             /* ??? */

             unsigned long personality;

             int dumpable:1;

             int did_exec:1;

             /* shouldn't this be pid_t? */

             int pid;

             int pgrp;

             int tty_old_pgrp;

             int session;

             /* boolean value for session group leader */

             int leader;

             int          groups[NGROUPS];

             /*

              * pointers to (original) parent process, youngest child, younger sibling,

              * older sibling, respectively.  (p->father can be replaced with

              * p->p_pptr->pid)

              */

             struct task_struct *p_opptr, *p_pptr, *p_cptr, *p_ysptr, *p_osptr;

             struct wait_queue *wait_chldexit;  /* for wait4() */

             unsigned short uid,euid,suid,fsuid;

             unsigned short gid,egid,sgid,fsgid;

             unsigned long timeout, policy, rt_priority;

             unsigned long it_real_value, it_prof_value, it_virt_value;

             unsigned long it_real_incr, it_prof_incr, it_virt_incr;

             struct timer_list real_timer;

             long utime, stime, cutime, cstime, start_time;

/* mm fault and swap info: this can arguably be seen as either mm-specific or thread-specific */

             unsigned long min_flt, maj_flt, nswap, cmin_flt, cmaj_flt, cnswap;

             int swappable:1;

             unsigned long swap_address;

             unsigned long old_maj_flt;             /* old value of maj_flt */

             unsigned long dec_flt;                   /* page fault count of the last time */

             unsigned long swap_cnt;                           /* number of pages to swap on next pass */

/* limits */

             struct rlimit rlim[RLIM_NLIMITS];

             unsigned short used_math;

             char comm[16];

/* file system info */

             int link_count;

             struct tty_struct *tty; /* NULL if no tty */

/* ipc stuff */

             struct sem_undo *semundo;

             struct sem_queue *semsleeping;

/* ldt for this task - used by Wine.  If NULL, default_ldt is used */

             struct desc_struct *ldt;

/* tss for this task */

             struct thread_struct tss;

/* filesystem information */

             struct fs_struct *fs;

/* open file information */

             struct files_struct *files;

/* memory management info */

             struct mm_struct *mm;

/* signal handlers */

             struct signal_struct *sig;

#ifdef __SMP__

             int processor;

             int last_processor;

             int lock_depth;                  /* Lock depth. We can context switch in and out of holding a syscall kernel lock... */

#endif   

};



~~~


