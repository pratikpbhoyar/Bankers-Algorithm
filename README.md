# Banker's Algorithm

## 1.0. Aim/ Benefits of the Micro-Project
<p align="justify">Aim :  The aim of this project is to avoid DeadLock situation in Operating System.</p>
<p align="justify">Benefits :   It provides the benefit to process that can be schedule in proper sequence so that their process does not goes in infinite waiting state and avoid DeadLock condition. Banker's Algorithm provide Safety sequence of process execution.</p>

## 2.0. Course Outcome Addressed 
<p align="justify">a)  Apply the scheduling Algorithm to calculate turn around time and average waiting time.</p>
<p align="justify">b)  Execute process commands for performing process management operations.</p>

## 3.0. Drawback of  previous DeadLock in system :
<p align="justify">There are different drawback in previous DeadLock in system that has been overcomed by this algorithm in OS when deadlock occurs a process or thread enters a waiting state because a requested system resource is held by another waiting process, which in turn is waiting for another resource held by another waiting process this is called circular wait. When two different process wait for releasing each other occupied resorce it is called Hold and wait This drawback will be overcomed in this algorithm by giving future knowledge of resource requested.</p>

## 4.0. Explanation about Bankers algorithm :  
<p align="justify">Banker’s algorithm (Dead-lock avoidance algorithm) is applicable to a system with multiple resources of each type. It is less efficient than the resource-allocation graph scheme. The name was given because it can be used in a banking system to ensure that the bank never allocated its available cash in such a way that it could no longer satisfy the needs of all its customers. When a new process enters the system, it must declare the maximum number of instances of each resource type that it may need. This number may not exceed the total number of resources in the system. When a user requests a set of resources, the system must determine whether the allocation of these resources will leave the system in a safe state. If it will, the resources are allocated; otherwise, the process must wait until some other process releases enough resources.</p>

## 5.0. Four Necessory Conditions to Deadlock Avoidance
<p align="justify">Their are various drawback in privious deadlock prevention technique. For priventing deadlock we need to false at least one of four condition but, in some situations it is not possible to make this condition false see the  dorowback one by one :</p>
<p align="justify">Mutual exclusion : It will says make all the resource shareble , but is it possible to make all the resource sharebel. Let's take example with CPU we can easily share CPU one or more process but in case of printer it is not possible to share with two or more process, thats why it is not possible always make all the resource sharebel.</p>
<p align="justify">Hold and Wait : To ensure that the hold-and-wait condition never occurs in the system, we must guarantee that, whenever a process requests a resource, it does not hold any other resources. One protocol that we can use requires each process to request and be allocated all its resources before it begins execution. An alternative protocol allows a process to request resources only when it has none. A process may request some resources and use them. Before it can request any additional resources, it must release all the resources that it is currently allocated. To illustrate the difference between these two protocols, we consider a process that copies data from a DVD drive to a file on disk, sorts the file, and then prints the results to a printer. If all resources must be requested at the beginning of the process, then the process must initially request the DVD drive, disk file, and printer. It will hold the printer for its entire execution, even though it needs the printer only at the end. The second method allows the process to request initially only the DVD drive and disk file. It copies from the DVD drive to the disk and then releases both the DVD drive and the disk file. The process must then request the disk file and the printer. After copying the disk file to the printer, it releases these two resources and terminates. Both these protocols have two main disadvantages: First, resource utilization may be low, since resources may be allocated but unused for a long period. Second, starvation is possible. A process that needs several popular resources may have to wait indefinitely, because at least one of the resources that it needs is always allocated to some other process.</p>
<p align="justify">No Preemption : The third necessary condition for deadlocks is that there be no preemption of resources that have already been allocated. To ensure that this condition does not hold, we can use the following protocol: If a process is holding some resources and requests another resource that cannot be immediately allocated to it (that is, the process must wait), then all resources the process is currently holding are preempted. In other words, these resources are implicitly released. The preempted resources are added to the list of resources for which the process is waiting. The process will be restarted only when it can regain its old resources, as well as the new ones that it is requesting. Alternatively, if a process requests some resources, we first check whether they are available. If they are, we allocate them. If they are not, we check whether they are allocated to some other process that is waiting for additional resources. If so, we preempt the desired resources from the waiting process and allocate them to the requesting process. If the resources are neither available nor held by a waiting process, the requesting process must wait. While it is waiting, some of its resources may be preempted, but only if another process requests them. A process can be restarted only when it is allocated the new resources it is requesting and recovers any resources that were preempted while it was waiting. This protocol is often applied to resources whose state can be easily saved and restored later. It cannot generally be applied to such resources as mutex locks and semaphores.</p>
<p align="justify">Circular Wait : The fourth and final condition for deadlocks is the circular-wait condition. One way to ensure that this condition never holds is to impose a total ordering of all resource types and to require that each process requests resources in an increasing order of enumeration. Alternatively, we can require that a process requesting an instance of resource type Rj must have released any resources Ri such that F(Ri ) ≥ F(Rj). Note also that if several instances of the same resource type are needed, a single request for all of them must be issued. If these two protocols are used, then the circular-wait condition cannot hold. We can accomplish this scheme in an application program by developing an ordering among all synchronization objects in the system. It is also important to note that imposing a lock ordering does not guarantee deadlock prevention if locks can be acquired dynamically.</p>
<p align="justify">As I explen all four necessary conditions each one having some drowback arived while making one of four candition false.</p>
<p align="justify">Now, second method of protecting deadlock is deadlock avoidance. In deadlock avoidance generally two Algoritham are used one is Resource-Allocation Graph, but it is effective only for single instance resources and generally  system have multiple instances of same resource for that case we are using secound Algoritham that is Bankers Algorithm. Banker’s algorithm (Dead-lock avoidance algorithm) is applicable to a system with multiple resources of each type. When a new process enters the system, it must declare the maximum number of instances of each resource type that it may need. This number may not exceed the total number of resources in the system. When a user requests a set of resources, the system must determine whether the allocation of these resources will leave the system in a safe state. If it will, the resources are allocated; otherwise, the process must wait until some other process releases enough resources. The results of that Algorithm it will give safe sequence of process execution with the help of that system never enter into deadlock and we not need to make four nessary condition false which was not possible always.</p>

## 6.0. Algorithm :
<p align="justify">1.	For P0 process avaible[R1=2, R2=3, R3=0] >= Need[R1=7, R2=4, R3=3] condition is false then check with next process.</p>
<p align="justify">2.	For P1 process avaible[R1=2, R2=3, R3=0] >= Need[R1=0, R2=2, R3=0] condition is true then allocate Avaible requard amount of resource to process and finish their execution and added P1 to safe sequence and after execution total Allocated resource to P1 process is released all resource and added to avaible resource that is : Avaible[R1=2, R2=3, R3=0] + Allocated[R1=3, R2=0, R3=2] = Avaible[R1=5, R2=3, R3=2].</p>
<p align="justify">3.	For P2 process avaible[R1=5, R2=3, R3=2] >= Need[R1=6, R2=0, R3=0] condition is false then check with next process.</p>
<p align="justify">4.	For P3 process avaible[R1=5, R2=3, R3=2] >= Need[R1=0, R2=1, R3=1] condition is true then allocate Avaible requard amount of resource to process and finish their execution and added P3 to safe sequence and after execution total Allocated resource to P3 process is released all resource and added to avaible resource that is : Avaible[R1=5, R2=3, R3=2] + Allocated[R1=2, R2=1, R3=1] = Avaible[R1=7, R2=4, R3=3].</p>
<p align="justify">5.	For P4 process avaible[R1=7, R2=4, R3=3] >= Need[R1=4, R2=3, R3=1] condition is true then allocate Avaible requard amount of resource to process and finish their execution and added P4 to safe sequence and after execution total Allocated resource to P4 process is released all resource and added to avaible resource that is : Avaible[R1=7, R2=4, R3=3] + Allocated[R1=0, R2=0, R3=2] = Avaible[R1=7, R2=4, R3=5].</p>
<p align="justify">6.	After the last process again goto first process that is for P0 process avaible[R1=7, R2=4, R3=5] >= Need[R1=7, R2=4, R3=3] condition is true then allocate Avaible requard amount of resource to process and finish their execution and added P0 to safe sequence and after execution total Allocated resource to P0 process is released all resource and added to avaible resource that is : Avaible[R1=7, R2=4, R3=5] + Allocated[R1=0, R2=1, R3=0] = Avaible[R1=7, R2=5, R3=5].</p>
<p align="justify">7.	for P2 process avaible[R1=7, R2=5, R3=5] >= Need[R1=6, R2=0, R3=0] condition is true then allocate Avaible requard amount of resource to process and finish their execution and added P2 to safe sequence and after execution total Allocated resource to P2 process is released all resource and added to avaible resource that is : Avaible[R1=7, R2=5, R3=5] + Allocated[R1=3, R2=0, R3=2] = Avaible[R1=10, R2=5, R3=7].</p>
<p align="justify">8.	After the all processes execution all Resources are released that is total instances of each type of resources  is equale to avaible instances of each type means : Avaible[R1=10, R2=5, R3=7] = Total[R1=10, R2=5, R3=7].</p>
<p align="justify">9.	At the last we will get safe sequence that is : P1 ->  P3 -> P4 -> P0 -> P2</p>

| Process no. | Allocation | Max | Need |
| --- | --- | --- | --- |
|  | R1 R2 R3 | R1 R2 R3 | R1 R2 R3 |
| P0 | 0 1 0 | 7 5 3 | 7 4 3 |
| P1 | 3 0 2 | 3 2 2 | 0 2 0 |
| P2 | 3 0 2 | 9 0 2 | 6 0 0 |
| P3 | 2 1 1 | 2 2 2 | 0 1 1 |
| P4 | 0 0 2 | 4 3 3 | 4 0 1 |

## 7.0. Output :
![image](https://github.com/pratikpbhoyar/Banker-s-Algorithm/assets/95959045/41a6034d-c5b2-4dab-9e53-e9b09b596efb)

![image](https://github.com/pratikpbhoyar/Banker-s-Algorithm/assets/95959045/ad032b75-0517-49cd-8169-040ba9c8cbd9)

![image](https://github.com/pratikpbhoyar/Banker-s-Algorithm/assets/95959045/ade53732-a2f9-4dbc-b7bb-78ea439ddb5d)



