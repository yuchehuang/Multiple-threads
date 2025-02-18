# Multiple-threads

* This project demonstrates the performance variation via operating the matrix multiplication by using different number of threads
* The work is acheived by C and adopts [windows.h](https://docs.microsoft.com/en-us/windows/win32/procthread/creating-threads) library to control and assign the task to each thread
* The result of the experiment is shown as the [report](https://github.com/yuchehuang/Multiple-threads/blob/master/Report/Thread%20performance%20analysis.pdf)

## Abstract

The technique of multi-threads has been widely used for solving multi-tasks such as matrix multiplication. The performance variation of the matrix operation by using the different number of threads is investigated in this project. The work demonstrates that multi-threads offers a faster performance due to the task is separated into several segments and operated simultaneously. However, the thread efficiency suffers from a lower utilization while using massive threads to execute the task due to each of it spends significant time on synchronization.


## Methodlolgy
The main point to improve the performance of multiplication operation is not only increasing the number of threads but also making sure tasks are equality assigned to each thread. With mapping equally, it prevents main thread from waiting a long time for one of thread still executing when others have completed their own tasks. Therefore, it leads in a lower CPU utilization and higher executing time. The work allocates tasks to each thread by the total number of elements which depend on the size of the matrix. In addition, to observe the multi-threading performance flexibly, dynamic memory allocation is adopted by the program to create the matrixes and threads by difference value of the input (as shown as the following figure). <br/>

![alt text](https://github.com/yuchehuang/Multiple-threads/blob/master/picture/equally%20assign.PNG)

To estimate the operating time of matrix multiplication accurately, the timer is only triggered while thread executing matrix multiplication. After checking threads and assigning tasks, the main function enable the timer after all of the threads start operating the calculation until all of them have been marked into finish state. As a result, the executing time can be more accurate and not affected by the other processes in the main program. 
<br/>

## Result

### Single thread
The following figure illustrates the matrix multiplication is complemented by only one thread and took up 1/8 of CPU utilisation. Due to the thread can be executed amount 8 physical cores, the task can be achieved without any time-consuming caused by synchronization and preemption. <br/>  


![alt text](https://github.com/yuchehuang/Multi-threading/blob/master/picture/1_thread_%20size_1000.jpg)
![alt text](https://github.com/yuchehuang/Multi-threading/blob/master/picture/1_thread_size_1000_core.jpg)


### Massive threads and its disadvantage 
By using multi-threading, the executing time decreases dramatically due the task is distributed equally to each thread to execute. However, there is a limitation of using massive threads. 
The following picture demonstrates an example that using 400 threads to execute the task. The result shows that although this strategy occupies almost 100% of CPU resource, each thread has only 3% of time to execute the task compared with 79% in synchronisation during the task.<br/> 

![alt text](https://github.com/yuchehuang/Multi-threading/blob/master/picture/400_thread_size_1000.png)
![alt text](https://github.com/yuchehuang/Multi-threading/blob/master/picture/400_thread_size_1000_core.JPG)


### Issue alleviation
By using the number of thread which equal to the physical cores, the issue of synchronisation will be eliminated and thread efficiency can be optimised due to none of the thread needs to wait for the other thread to finish its task. The result of this experiment is illustrated as the following picture which shown there are 93% of timeline in execution status.
<br/>

![alt text](https://github.com/yuchehuang/Multi-threading/blob/master/picture/8_thread_size_1000.JPG)
![alt text](https://github.com/yuchehuang/Multi-threading/blob/master/picture/8_thread_size_1000_core.JPG)

Moreover, this porject illustrates the variation of efficiency that using n^2 thread to accomplish the task compared with using only one thread. The result indicates that while using the number of thread taht more than physical cores, the gap of time-comsuming increases evidently due to each of thread starts spending time on synchorization. 
<br/>
![alt text](https://github.com/yuchehuang/Multi-threading/blob/master/picture/nxn%20in%20n%5E2%20thread.jpg)

The other experiment shows the difference of time-comusing by running the same task in different CPU. According to the picture below,
with a large number of logical cores (Xeon 2155 CPU, with 10 cores 2 physical threads in each core), it implies more and more threads are allowed to be allocated to each core in the same machine cycle. Therefore, the executing time can be dereased significantly compared with using intel 8550u (4 cores 2 physical threads in each core)
<br/>
![alt text](https://github.com/yuchehuang/Multi-threading/blob/master/picture/1000x1000_in_n_thread.jpg)
