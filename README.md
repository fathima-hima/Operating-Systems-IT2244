Operating Systems IT 2244 
Day 19 Practical 
31/05/2025

Exercise 01

IPC using message queue
read inputs from the parent process
Enter Name : him
Enter RegNo : 2021ict84
Enter Age : 23

message sent successfuly.

give the output from the child process

Received Name : him
Received RegNo : 2021ict84
Received Age : 23


Code :

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ipc.h>      // For IPC key generation
#include <sys/msg.h>      // For message queue functions
#include <unistd.h>       // For fork()
#define MAX 10            // Max size of message text

//structure for message queue
struct mesg_buffer {
    long mesg_type;
    char mesg_text[100];
} message;

int main() {
    int f = fork();  // ← FIXED semicolon

    if (f == 0) {
        // Child - Receive

        key_t key;
        int msgid;

        key = ftok("regno", 921);
        msgid = msgget(key, 0666 | IPC_CREAT);
        msgrcv(msgid, &message, sizeof(message.mesg_text), 1, 0);

        // Parse
        char name[30], regno[30], age[10];
        sscanf(message.mesg_text, "%s %s %s", name, regno, age);

        printf("\nReceived Name : %s\n", name);
        printf("Received RegNo : %s\n", regno);
        printf("Received Age : %s\n", age);

        msgctl(msgid, IPC_RMID, NULL);
    } 
	else 
	{
        // Parent - Send
        key_t key;
        int msgid;
 
        // Declare missing variables
        char name[30], regno[30], age[10];

        key = ftok("regno", 921);
        msgid = msgget(key, 0666 | IPC_CREAT);

        printf("Enter Name: ");
        scanf("%s", name);
        printf("Enter RegNo: ");
        scanf("%s", regno);
        printf("Enter Age: ");
        scanf("%s", age);

        message.mesg_type = 1;
        snprintf(message.mesg_text, sizeof(message.mesg_text), "%s %s %s", name, regno, age);

        msgsnd(msgid, &message, sizeof(message.mesg_text), 0);
        printf("\nMessage sent successfully.\n");
    }

    return 0;
}


Output :

[2021ict84@fedora ~]$ vi regno.c
[2021ict84@fedora ~]$ gcc regno.c -o regno
[2021ict84@fedora ~]$ ./regno
Enter Name: him
Enter RegNo: 2021ict84
Enter Age: 23

Message sent successfully.

Received Name : him
Received RegNo : 2021ict84
Received Age : 23
[2021ict84@fedora ~]$


Explanation :

Here,Both parent and child use the same key (ftok("regno", 921)) to access the queue.
The parent puts a message into the queue.
The child retrieves the message using msgrcv(). 


Standard I/O (stdio.h)
Memory and string handling (stdlib.h, string.h)
IPC functions and keys (sys/ipc.h, sys/msg.h)
Process creation using fork() (unistd.h)

mesg_type: required by System V message queues (used to filter messages).
mesg_text: the actual message content (up to 100 characters).

parent process:
Create a unique IPC key using ftok("regno", 921).
Create or get a message queue using msgget().
Take user input: Name, RegNo, and Age.
Combine the inputs into one string using snprintf().
Send the message using msgsnd().

child process:
Generate the same key with ftok().
Access the same message queue with msgget().
Use msgrcv() to receive the message (with type = 1).
Use sscanf() to split the message into Name, RegNo, and Age.
Print the received values.
Destroy the message queue using msgctl() to clean up.

