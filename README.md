# mutex-and-spinlocks
A mini project to demonstrate the usage of mutex locks and spinlocks. 


We use pthreads here! (API)
Please use a VM with multiple cores!

How to run the code:

parallel_hashtable.c 
gcc -pthread parallel_hashtable.c -o parallel_hashtable
./parallel_hashtable <no of threads>

And you should see an output similar to the following: 
[main] Inserted 100000 keys in 0.006545 seconds 
[thread 0] 0 keys lost! 
[main] Retrieved 100000/100000 keys in 4.028568 seconds

With one thread the program is correct, but try it with more than one thread 
./parallel_hashtable 8
[main] Inserted 100000 keys in 0.002476 seconds [thread 7] 4304 keys lost! [thread 6] 4464 keys lost! [thread 2] 4273 keys lost! [thread 1] 3864 keys lost! [thread 4] 4085 keys lost! [thread 5] 4391 keys lost! [thread 3] 4554 keys lost! [thread 0] 4431 keys lost! [main] Retrieved 65634/100000 keys in 0.792488 seconds

TASK: (try it without referring to my solution code)
Modify the insert and retrieve functions so that you do not lose items when running the program with multiple threads.
You will likely need to use parts of the pthread library; things like pthread_mutex_t, pthread_mutex_init, pthread_mutex_lock, and/or pthread_mutex_unlock

Here, if we use multiple threads, no keys should be lost
parallel_mutex.c
gcc -pthread parallel_mutex.c -o parallel_mutex
./parallel_mutex <no of threads>

Same code using spinlocks: notice the differences
How to run it: 

parallel_spin.c
gcc -pthread parallel_spin.c -o parallel_spin
./parallel_spin <no of threads>

Let’s revisit your mutex-based code. When we retrieve an item from the hash table, do we need a lock? No, we don't. updated code so that multiple retrieve operations can run in parallel:
Also, let’s consider insertions. Describe a situation in which multiple insertions could happen safely (hint: what’s a bucket?). The answer is acquiring and releasing a lock only at the bucket itself and not the entire insertion process!!


Updated parallel_mutex_opt.c to handle this scenario.
parallel_mutex_opt.c
gcc -pthread parallel_mutex_opt.c -o parallel_mutex_opt
./parallel_mutex_opt <no of threads>


"Explanation.pdf" has the details of what exactly we can infer through this code implementation. 


