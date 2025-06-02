Operating Systems IT 2244 
Day 20 Practical 
02/06/2025

Exercise 01

Code :

//writer process

#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <sys/shm.h>
#include <sys/ipc.h>

#DEFINE SHM_SIZE 1024  //size of shared memory segment

int main(){

key_t key=ftok("sharedmemo",84);//generate  unique key
int shmid = shmget(key,SHM_SIZE,IPC_CREAT|0666);//create shared memory segment
if(shmid==-1)
{
	perror("shmget");
	exit(1);
}

char *shmaddr = (char*) shmat(shmid,NULL,0); //Attached to shared memory
if(shmaddr == (char*)-1)
{
	perror("shmat");
	exit(1);
}

printf("Write data:"); 
fgets(shmaddr,SHM_SIZE,stdin);  //write data to shared memory


printf("Data written in memory: %s\n",shmaddr);

shmdt(shmaddr); //detach from shared memory

return 0;
}

//reader

#include <stdio.h>
#include <stdlib.h>
#include <sys/shm.h>
#include <sys/ipc.h>

#define SHM_SIZE 1024  // Size of shared memory segment

int main() {
    key_t key = ftok("sharedmemo", 84); // Same key as writer
    if (key == -1) {
        perror("ftok");
        exit(1);
    }

    int shmid = shmget(key, SHM_SIZE, 0666); // Access existing shared memory segment
    if (shmid == -1) {
        perror("shmget");
        exit(1);
    }

    char *shmaddr = (char *) shmat(shmid, NULL, 0); // Attach to shared memory
    if (shmaddr == (char *) -1) {
        perror("shmat");
        exit(1);
    }

    printf("Data read from memory: %s\n", shmaddr);

    shmdt(shmaddr); // Detach from shared memory

    // remove shared memory
    shmctl(shmid, IPC_RMID, NULL); // to delete shared memory

    return 0;
}


Output :

[2021ict84@fedora ~]$ vi sharedmemo.c
[2021ict84@fedora ~]$ gcc sharedmemo.c -o sharedmemo
[2021ict84@fedora ~]$ ./sharedmemo
Write data:helllo, this is shered memory
Data written in memory: helllo, this is shered memory

[2021ict84@fedora ~]$ vi reader.c
[2021ict84@fedora ~]$ gcc reader.c -o reader
[2021ict84@fedora ~]$ ./reader
Data read from memory: helllo, this is shered memory


Explanation :

In Writer Program,
The program includes necessary headers for input/output and shared memory operations.
It defines the size of the shared memory segment as 1024 bytes.
It generates a unique key using the ftok function based on a file named "sharedmemo".
It creates a shared memory segment or accesses an existing one with the generated key using shmget.
The shared memory segment is attached to the process’s address space with shmat, returning a pointer to it.
The program prompts the user to enter data.
It reads the user input from standard input and writes it into the shared memory.
It prints the data that was written to the shared memory as confirmation.
Finally, it detaches the shared memory segment from the process’s address space with shmdt.

In Reader Program,
The program includes necessary headers for input/output and shared memory operations.
It defines the shared memory segment size as 1024 bytes.
It generates the same unique key using ftok with the same file and ID as the writer.
It accesses the existing shared memory segment using shmget without the create flag.
It attaches the shared memory segment to its own process address space using shmat.
It reads the data stored in shared memory and prints it to the screen.
It detaches the shared memory segment using shmdt.
Optionally, it can remove the shared memory segment from the system with shmctl to clean up.

===========================================================================================

Exercise 02

Parent-Child Shared Memory Communication.
The child writes the message to shared memory.
The parent reads that message from shared memory and prints it.

Code :

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/mman.h>
#include <sys/wait.h>

int main(){
	size_t size=4096;
	char *shared_mem=mmap(NULL,size,PROT_READ|PROT_WRITE,MAP_SHARED|MAP_ANONYMOUS,-1,0);
	if(shared_mem==MAP_FAILED){
		perror("mmap failed");
		exit(1);
	}
	
	pid_t pid=fork();
	if(pid==0)
	{
		//child process
		sprintf(shared_mem, "Hello from child!");
		printf("Child wrote: %s\n",shared_mem);
		exit(0);
	}
	else if(pid>0)
	{
		//parent process
		wait(NULL);//wait for child to finish
		printf("Parent read: %s\n",shared_mem);
		munmap(shared_mem,size);
	}
	else
	{
		perror("fork failed");
		exit(1);
	}
	
	return 0;
}

Output :

[2021ict84@fedora ~]$ vi sharedmem.c
[2021ict84@fedora ~]$ gcc sharedmem.c -o sharedmem
[2021ict84@fedora ~]$ ./sharedmem
Child wrote: Hello from child!
Parent read: Hello from child!

Explanation :

This C program demonstrates inter-process communication (IPC) using shared memory between a parent and child process.
1. Shared Memory Creation
char *shared_mem = mmap(NULL, size, PROT_READ | PROT_WRITE, MAP_SHARED | MAP_ANONYMOUS, -1, 0);
It creates a shared memory region of 4096 bytes using mmap().
PROT_READ | PROT_WRITE: both processes can read from and write to it.
MAP_SHARED: changes are visible to all processes sharing it.
MAP_ANONYMOUS: no file is backing this memory—it's purely in RAM.

2. Child Process
pid_t pid = fork();
if (pid == 0)
After fork(), if pid == 0, this is the child process.
It writes a message "Hello from child!" directly into the shared memory using sprintf().
Then it prints the message and exits.

3. Parent Process
else if (pid > 0)
The parent waits for the child to complete using wait(NULL).
After that, it reads the message written by the child from the shared memory.
It prints the message: "Parent read: Hello from child!".
Finally, it unmaps the shared memory using munmap() to release resources.

4. Error Handling
If mmap() or fork() fails, the program prints an error and exits.

In conclusion,
The child writes data to shared memory.
The parent waits, then reads that data from the same memory.
This shows how two processes can communicate without using files or pipes.

===========================================================================================

Exercise 03

The parent takes two inputs n and r from the user.
The parent sends these integers to the child via shared memory.
The child calculates factorials of n and r.
The child sends the factorial results back to the parent via shared memory.
The parent calculates and prints nCr and nPr using those factorials.

Code :
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/mman.h>
#include <sys/wait.h>

int main() {
    size_t size = 3 * sizeof(long);
    long *shared_mem = mmap(NULL, size, PROT_READ | PROT_WRITE, MAP_SHARED | MAP_ANONYMOUS, -1, 0);
    if (shared_mem == MAP_FAILED) {
        perror("mmap failed");
        exit(1);
    }

    int n, r;
    printf("Enter value for n: ");
    scanf("%d", &n);
    printf("Enter value for r: ");
    scanf("%d", &r);

    pid_t pid = fork();

    if (pid < 0) {
        perror("fork failed");
        exit(1);
    } else if (pid == 0) {
        printf("Child process started (PID: %d)\n", getpid());

        long factorial(int num) { 
            long fact = 1;
            for (int i = 1; i <= num; i++)
                fact *= i;
            return fact;
        }

        shared_mem[0] = factorial(n);
        shared_mem[1] = factorial(r);
        shared_mem[2] = factorial(n - r);

        printf("Child calculated factorials and stored them in shared memory.\n");
        exit(0);
    } else {
        wait(NULL);
        long fact_n = shared_mem[0];
        long fact_r = shared_mem[1];
        long fact_n_r = shared_mem[2];

        long ncr = fact_n / (fact_r * fact_n_r);
        long npr = fact_n / fact_n_r;

        printf("Parent process started (PID: %d)\n", getpid());
        printf("Factorial of %d: %ld\n", n, fact_n);
        printf("Factorial of %d: %ld\n", r, fact_r);
        printf("NCR (%dC%d): %ld\n", n, r, ncr);
        printf("NPR (%dP%d): %ld\n", n, r, npr);

        munmap(shared_mem, size);
    }

    return 0;
}

Output :

[2021ict84@fedora ~]$ vi shrm1.c
[2021ict84@fedora ~]$ gcc shrm1.c -o shrm1
[2021ict84@fedora ~]$ ./shrm1
Enter value for n: 5
Enter value for r: 2
Child process started (PID: 19740)
Child calculated factorials and stored them in shared memory.
Parent process started (PID: 19493)
Factorial of 5: 120
Factorial of 2: 2
NCR (5C2): 10
NPR (5P2): 20

Explanation :

This C program demonstrates inter-process communication using shared memory and the fork() system call. It starts by allocating a shared memory region using mmap() to store three long integers—factorials of n, r, and n-r. The user is prompted to enter values for n and r. After that, the process forks into a child and a parent. The child process defines and uses a local factorial function to compute n!, r!, and (n−r)!, and stores the results in the shared memory. Once done, the child exits. The parent process waits for the child to complete using wait(), then reads the factorial values from the shared memory. It computes nCr using the formula n! / (r! * (n−r)!) and nPr using n! / (n−r)!, and prints the results. Finally, it unmaps the shared memory before terminating.

mmap() allocates shared memory for communication,
munmap() deallocates it once it's done being used.
