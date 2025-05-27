Operating Systems IT 2244
Day 15 Practical
22/05/2025


Code:

#include<stdio.h>
#include <unistd.h>
int main(){
        fork();
        fork();
        printf("Hello World!\n");
return 0;
}

Output :

[2021ict84@fedora ~]$ vi CPro1.c
[2021ict84@fedora ~]$ gcc CPro1.c -o CPro1
[2021ict84@fedora ~]$ ./CPro1
Hello World!
Hello World!
Hello World!
Hello World!

Explanation :

Calling fork() duplicates the current process. When fork() is called twice, the first call creates 2 processes (the original parent and a child), and the second call is executed by both of these processes, resulting in a total of 4 processes.

===========================================================================================

Code: 

#include<stdio.h>
#include<unistd.h>
int main(){
        int f=fork();
        if(f==0)
        {
                printf("I am child\n");
                printf("My parent ID is %d\n",getppid());
        }
        else
        {
                printf("I am parent\n");
                printf("My ID is %d\n",getpid());
                printf("My parent ID is %d\n",getppid());
        }

        return 0;
}

Output:

[2021ict84@fedora ~]$ vi first.c
[2021ict84@fedora ~]$ vi first.c
[2021ict84@fedora ~]$ gcc first.c -o first
[2021ict84@fedora ~]$ ./first
I am parent
My ID is 15949
My parent ID is 11223
I am child
My parent ID is 15949

Explanation :

This program uses fork() to create a child process.
int f = fork();
Creates a new process. f == 0 in child, f > 0 in parent.

If f == 0 (Child process):
Prints "I am child"
Prints its parent’s process ID using getppid()

Else (Parent process):
Prints "I am parent"
Prints its own process ID using getpid()
Prints its parent's ID using getppid() (usually the shell)

===========================================================================================


//print the numbers from 1 to 10
//1 to 5 should be print by child process and
//from 6 to 10 should be print by the parent process
//calculate the summation of those numbers


Code :

#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    int id = fork();
    int Csum = 0;
    int Psum = 0;

    if (id == 0) {
        
        printf("Child process:\n");
        for (int i = 1; i <= 5; i++) {
            printf("%d\n", i);
            Csum += i;
        }
        printf("Child sum: %d\n", Csum);
    } 

    else {
       
        wait(NULL); 
        printf("Parent process:\n");

        for (int i = 6; i <= 10; i++) {
            printf("%d\n", i);
            Psum += i;
        }

        printf("Parent sum: %d\n", Psum);

        int total = Psum + 15;

        printf("Total sum (Child + Parent): %d\n", total);

    }

    return 0;
}


Output:

[2021ict84@fedora ~]$ vi sum.c
[2021ict84@fedora ~]$ gcc sum.c -o sum
[2021ict84@fedora ~]$ ./sum
Child process:
1
2
3
4
5
Child sum: 15
Parent process:
6
7
8
9
10
Parent sum: 40
Total sum (Child + Parent): 55


Explanation :

This program uses fork() to create a child process and lets both child and parent calculate a sum.
In the Child Process (id == 0):
Prints numbers from 1 to 5
Calculates their sum (Csum = 15)
Prints "Child sum: 15"

In the Parent Process (id > 0):
Waits for the child to finish using wait(NULL)
Prints numbers from 6 to 10
Calculates their sum (Psum = 40)
Adds hardcoded child sum (15) to parent sum and prints the total (Total = 55)

