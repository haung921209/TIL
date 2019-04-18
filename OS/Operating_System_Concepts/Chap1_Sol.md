1.1 In a multiprogramming and time-sharing environment, several users share the system simultaneously. This situation can result in various security problems.

a. What are two such problems?
b. Can we ensure the same degree of security in a time-shared machine as in a dedicated machine? Explain your answer.

Ans.

a. Stealing or copying one’s programs or data; using system resources (CPU,memory, disk space, peripherals) without proper accounting.

b. Probably not, since any protection scheme devised by humans can inevitably be broken by a human, and the more complex the scheme, the more difficult it is to feel confident of its correct implementation.


- - -

1.2 The issue of resource utilization shows up in different forms in different types of operating systems. List what resources must be managed carefully in the following settings:

a. Mainframe or minicomputer systems
b. Workstations connected to servers
c. Handheld computers

Ans.

a. Mainframes: memory and CPU resources, storage, network bandwidth
b. Workstations: memory and CPU resources
c. Handheld computers: power consumption, memory resources


- - -

1.3 Under what circumstances would a user be better off using a timesharing system rather than a PC or a single-user workstation?

Ans.
When there are few other users, the task is large, and the hardware is fast, time-sharingmakes sense. The full power of the system can be brought to bear on the user’s problem. The problemcan be solved faster than on a personal computer. Another case occurs when lots of other users need resources at the same time. 
A personal computer is best when the job is small enough to be executed reasonably on it and when performance is sufficient to execute the program to the user’s satisfaction.

---

1.4 Describe the differences between symmetric and asymmetric multiprocessing. What are three advantages and one disadvantage of multiprocessor systems?

Ans.

Symmetric processing treats all processors as equals; I/O can be processed on any of them. 

Asymmetric processing designates one CPU as the master, which is the only one capable of performing I/O; the master distributes computational work among the other CPUs.

- advantages: Multiprocessor systems can save money, by sharing power supplies, housings, and peripherals. Can execute programs more quickly and can have increased reliability.
- disadvantages: Multiprocessor systems are more complex in both hardware and software. Additional CPU cycles are required to manage the cooperation, so per-CPU efficiency goes down.


---

1.5 How do clustered systems differ from multiprocessor systems? What is required for two machines belonging to a cluster to cooperate to provide a highly available service?

Ans.

Clustered systems are typically constructed by combining multiple computers into a single system to perform a computational task distributed across the cluster. Multiprocessor systems on the other hand could be a single physical entity comprising of multiple CPUs. A clustered system is less tightly coupled than a multiprocessor system. Clustered systems communicate using messages, while processors in a multiprocessor system could communicate using shared memory. In order for two machines to provide a highly available service, the state on the two machines should be replicated and should be consistently updated. When one of the machines fails, the other could then takeover the functionality of the failed machine


---

1.6 Consider a computing cluster consisting of two nodes running a database.Describe two ways in which the cluster software can manage access tothe data on the disk. Discuss the benefits and disadvantages of each.

Ans.

Consider the following two alternatives: **asymmetric cluster-ing and parallel clustering**. 
With asymmetric clustering, one host runsthe database application with the other host simply monitoring it.Ifthe server fails, the monitoring host becomes the active server. This isappropriate for providing redundancy. However, it does not utilize thepotential processing power of both hosts.With parallel clustering, the database application can run in parallel on bothh osts.The difficulty implementing parallel clusters is providing some form of distributedlocking mechanism for files on the shared disk


---

1.7 How are network computer different from traditional personal computers ? Describe some usage scenarios in which it is advantageous to use network computers ?

Ans.

A network computer relies on a centralized computer for most of its services. It can therefore have a minimal operating system to manage its resources. A personal computer on the other hand has to be capable of providing all of the required functionality in a standalone manner without relying on a centralized manner. Scenarios where administrative costs are high and where sharing leads to more efficient use of resources are precisely those settings where network computers are preferred.



---

1.8 What is the purpose of interrupts? What are the differences between a trap and an interrupt? Can traps be generated intentionally by a user program? If so, for what purpose? 

Ans.

An interrupt is a hardware-generated change of flow within the system. An interrupt handler is called to deal with the cause of the interrupt; control is then returned to the interrupted context and instruction. A trap is a software-generated interrupt. An interrupt can be used to signal the completion of an I/O to obviate the need for device polling. A trap can be generated intentionally by a user program. It can be used to call operating system routines or to catch arithmetic errors.


---

1.9 Direct memory access (DMA) is used for high-speed I/O devices in order to avoid increasing the CPU's execution load.

a. How does the CPU interface with the device to coordinate the transfer?
b. How does the CPU know when the memory operations are complete?
c. The CPU is allowed to execute other programs while the DMA controller is transferring data. Does this process interfere with the execution of user programs? If so, describe what forms of interference are caused.

Ans.

a. To initiate a DMA transfer, the CPU first sets up the DMA registers, which contain a pointer to the source of a transfer, a pointer to the destination of the transfer, and a counter of the number of bytes to be transferred. Then the DMA controller proceeds to place addresses on the bus to perform transfers, while the CPU is available to accomplish other work.
b. Once the entire transfer is finished, the DMA controller interrupts the CPU.
c. Both the CPU and the DMA controller are bus masters. A problem would be created if both the CPU and the DMA controller want to access the memory at the same time. Accordingly, the CPU should be momentarily prevented from accessing main memory when the DMA controller seizes the memory bus. However, if the CPU is still allowed to access data in its primary and secondary caches, a coherency issue may be created if both the CPU and the DMA controller update the same memory locations. 

---

1.10  Some computer systems do not provide a privileged mode of operation in hardware. Is it possible to construct a secure operating system for these computer systems? Give arguments both that it is and that it is not possible. 

Ans.

An operating system for a machine of this type would need to remain in control (or monitor mode) at all times. This could be accomplished by two methods:

a. Software interpretation of all user programs (like some BASIC, Java, and LISP systems, for example). The software interpreter would provide, in software, what the hardware does not provide. 
b. Require meant that all programs be written in high‐level languages so that all object code is compiler‐produced. The compiler would generate (either in‐line or by function calls) the protection checks that the hardware is missing. 


---

1.11 Many SMP systems have different levels of caches; one level is local to each processing core, and another level is shared among all processing cores. Why caching systems are designed this way?

Ans.

The different levels are based on access speed as well as size. In general, the closer the cache is to the CPU, the faster the access. However, faster caches are typically more costly. Therefore, smaller and faster caches are placed local to each CPU, and shared caches that are larger, yet slower, are shared among several different processors.



---

1.12 Consider an SMP system similar to the one shown in Figure 1.6 Illustrate with an example how data residing in memory could in fact have a different value in each of the local caches.

![Figure 1.6](/img/Figure1-6.png)


Ans.

Say processor 1 reads data A with value 5 from main memory into its local cache. Similarly, processor 2 reads data A into its local cache as well. Processor 1 then updates A to 10. However, since A resides in processor 1's local cache, the update only occurs there and not in the local cache for processor 2.


---