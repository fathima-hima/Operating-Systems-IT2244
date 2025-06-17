Operating Systems IT 2244
Day 24 Practical
16/06/2025


1.Single threaded process.

Code :

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>


//A normal c function that is executed as a thread
//when its name is specified in pthread_create()
void *helloWorld(void *vargp)
{
   sleep(1);
   printf("Hello World\n");
   return NULL;
}

int main(){

   pthread_t thread_id;
   printf("Before Thread\n");
   pthread_create(&thread_id, NULL, helloWorld, NULL);
   pthread_join(thread_id,NULL);
   printf("After Thread\n");
   exit(0);

}

Output :

[2021ict84@fedora ~]$ vi threadexample.c
[2021ict84@fedora ~]$ gcc threadexample.c -o threadexample
[2021ict84@fedora ~]$ ./threadexample
Before Thread
Hello World
After Thread

Explanation :

This is a thread function named helloWorld.
The signature void *func(void *arg) is required by pthread_create.
Inside the function:
sleep(1); pauses the thread for 1 second.
Then it prints "Hello World\n".
Returns NULL (indicating the thread ends without any return value).

#include <pthread.h> is used to include the POSIX Threads library header, 
enabling the use of thread functions like pthread_create() and pthread_join().

int main(){
Entry point of the program.

   pthread_t thread_id;
Declare a variable thread_id of type pthread_t.
This will hold the identifier for the new thread.

   printf("Before Thread\n");
Print "Before Thread" before creating the new thread.

   pthread_create(&thread_id, NULL, helloWorld, NULL);
Create a new thread:

&thread_id — pointer to thread_id variable to store the thread ID.
NULL — default thread attributes.
helloWorld — the function the thread will run.
NULL — argument passed to helloWorld (no argument here).
After this call, a new thread starts and executes the helloWorld function concurrently.

   pthread_join(thread_id,NULL);
pthread_join waits for the thread identified by thread_id to finish before continuing.
This means the main thread will pause here until the helloWorld thread completes.

   printf("After Thread\n");
Once the thread finishes and pthread_join returns, print "After Thread".

   exit(0);
}
End the program successfully.

In conclusion,
The program prints "Before Thread".
Creates a new thread to run helloWorld().
The new thread sleeps for 1 second and then prints "Hello World".
main thread waits for helloWorld to finish (pthread_join).
After helloWorld completes, "After Thread" is printed.
Program exits.

===================================================================================================================

2. Multi-threaded process.

Code :

#include <stdio.h>
#include <pthread.h>

//function to be executed by the thread 
void* print_message(void* arg)
{
	char* message = (char*)arg;
	printf("%s\n",message);
	return NULL;
}

int main(){
	pthread_t thread1, thread2;
	
	//create first thread
	pthread_create(&thread1,NULL,print_message,"Hello from thread 1!");
	
	//create second thread
	pthread_create(&thread2,NULL,print_message,"Hello from thread 2!");
	
	//wait for both threads to finish 
	pthread_join(thread1,NULL);
	pthread_join(thread2,NULL);
	
	printf("Both threads completed.\n");
	return 0;
}


Output :
                 ^
[2021ict84@fedora ~]$ vi multithread.c
[2021ict84@fedora ~]$ gcc multithread.c -o multithread
[2021ict84@fedora ~]$ ./multithread
Hello from thread 1!
Hello from thread 2!
Both threads completed.

Explanation :

This C program demonstrates a multi-threaded process using POSIX threads.
It includes a function called print_message which takes a message as input and prints it.
In the main function, two threads (thread1 and thread2) are created using pthread_create.
Each thread runs the print_message function, printing a different message:
"Hello from thread 1!" and
"Hello from thread 2!".
The pthread_join function is then used to wait for both threads to finish execution.
After both threads complete their tasks, the main program prints "Both threads completed."
Since threads run concurrently, the order of the printed thread messages may vary each time the program runs.

===================================================================================================================

3. printing 
Thread 1 Says hi! in thread 1
Thread 2 Says Hello! in thread 2
Thread 3 Says hey! in thread 3

Code :

#include <stdio.h>
#include <pthread.h>

//function to be executed by the thread 
void* print_message(void* arg)
{
	char* message = (char*)arg;
	printf("%s\n",message);
	return NULL;
}

int main(){
	pthread_t threads[3]; //create array for threads
	char* messages[]={
		"Thread 1 Says hi!",
		"Thread 2 Says Hello!",
		"Thread 3 Says hey!"
	};
	
	//creating the thread
	for(int i=0; i<3; i++)
	{
		pthread_create(&threads[i],NULL,print_message,messages[i]);
	}
	

	//wait for both threads to finish 
	for(int i=0; i<3; i++){
		 pthread_join(threads[i],NULL);
		
	}
	
	printf("All threads done.\n");
	return 0;
}

Output:

[2021ict84@fedora ~]$ vi multithreadex.c
[2021ict84@fedora ~]$ gcc  multithreadex.c -o multithreadex
[2021ict84@fedora ~]$ ./multithreadex
Thread 1 Says hi!
Thread 2 Says Hello!
Thread 3 Says hey!
All threads done.

Explanation:

This program creates and runs three threads using the POSIX thread (pthread) library.
It defines a function print_message which takes a message as input and prints it.
In the main function, an array threads[3] is used to hold three thread identifiers, 
and an array messages[] stores the three messages each thread will print.
A for loop is used to create three threads using pthread_create.
Each thread is assigned a different message from the messages array.
After creating the threads, another for loop is used with pthread_join to make the main
program wait until all three threads have finished executing.
Once all threads complete, the main program prints "All threads done."
Since the threads run concurrently, the order of the printed thread messages may vary with each execution.

=========================================================================================================================

4. Using threads to compute parts of a sum (Parallel Sum)

Code :

#include <stdio.h>
#include <pthread.h>
#define SIZE 6

int arr[SIZE] ={1,2,3,4,5,6};
int sum1=0,sum2=0;

void* sum_part1(void* arg)
{
for(int i=0; i<SIZE/2; i++)
{
	sum1 += arr[i];
}
return NULL;
}

void* sum_part2(void* arg)
{
for(int i=SIZE/2; i<SIZE; i++)
{
	sum2 += arr[i];
}
return NULL;
}

int main(){
	
	pthread_t t1,t2;
	
	pthread_create(&t1,NULL,sum_part1,NULL);
	pthread_create(&t2,NULL,sum_part2,NULL);
	
	pthread_join(t1,NULL);
	pthread_join(t2,NULL);
	
	printf("Total  sum=%d\n",sum1+sum2);
	return 0;
}

Output :

[2021ict84@fedora ~]$ vi multithreadex2.c
[2021ict84@fedora ~]$ gcc  multithreadex2.c -o multithreadex2
[2021ict84@fedora ~]$ ./multithreadex2
Total  sum=12


Explanation :

This C program uses multi-threading to calculate the sum of an array by dividing the work between two threads.
An array arr of 6 integers {1, 2, 3, 4, 5, 6} is defined, and two global variables sum1 and sum2 are used to store partial sums.
Two thread functions are defined:
sum_part1 adds the first half of the array (1 + 2 + 3 = 6) and stores the result in sum1.
sum_part2 adds the second half of the array (4 + 5 + 6 = 15) and stores the result in sum2.
In the main function, two threads (t1 and t2) are created using pthread_create, and each one runs one of the sum functions.
The pthread_join function is used to wait until both threads complete their execution.
Finally, the program adds sum1 and sum2 and prints the total sum, which is 6 + 15 = 21.
