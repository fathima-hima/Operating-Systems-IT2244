Operating Systems IT 2244
Day 18 Practical
30/05/2025

Inter-Process Communication Using Message Queues in C.
#include <sys/ipc.h>  - For IPC key generation.
#include <sys/msg.h>  - For message queue functions.
#define MAX 10        -  Max size of message text.
ftok() - Generates unique key based on a file and an ID.
msgget() - Creates or accesses message queue by key.
msgsnd() - Sends message (must specify message text size, not whole struct).
msgrcv() - Receives message of given type.
msgctl(..., IPC_RMID, NULL) - Deletes message queue.
