Operating Systems IT 2244
Day 22 Practical
09/06/2025


1.Area Calculation program

Circle => C
Triangle => T
Square = > S
Rectangle => Rectangle
Enter your choice : C

Circle area calculation

Enter the radius : 20.9
Area is: 1371.58

Code :

#include <stdio.h>
#include <stdlib.h>

#include <unistd.h>
#include <string.h>
#include <math.h>
#include <sys/wait.h>

// Function to calculate area
float calculateArea(char choice, float a, float b) {
    switch (choice) {
        case 'C':
            return M_PI * a * a; // Circle: a = radius
        case 'R':
            return a * b; // Rectangle
        case 'T':
            return 0.5 * a * b; // Triangle
        case 'S':
            return a * a; // Square
        default:
            return -1; // Invalid choice
    }
}

int main() {
    int ptc[2]; // Parent to Child pipe
    int ctp[2]; // Child to Parent pipe

    if (pipe(ptc) == -1 || pipe(ctp) == -1) {
        perror("Pipe creation failed");
        return 1;
    }

    pid_t pid = fork();

    if (pid < 0) {
        perror("Fork failed");
        return 1;
    }

    if (pid > 0) {
        // ===== PARENT PROCESS =====

        close(ptc[0]); // Close read end of ptc
        close(ctp[1]); // Close write end of ctp

        // Step 1: Get input from user
        char choice;
        float val1, val2;

        printf("\nArea Calculation program\n");
        printf("\nCircle => C\nTriangle => T\nSquare => S\nRectangle => R\n");
        printf("Enter your choice: ");
        scanf(" %c", &choice);

        switch (choice) {
            case 'C':
                printf("\nCircle area calculation\n");
                printf("Enter the radius: ");
                scanf("%f", &val1);
                val2 = 0; // not needed
                break;
            case 'R':
                printf("\nRectangle area calculation\n");
                printf("Enter length and width: ");
                scanf("%f %f", &val1, &val2);
                break;
            case 'T':
                printf("\nTriangle area calculation\n");
                printf("Enter base and height: ");
                scanf("%f %f", &val1, &val2);
                break;
            case 'S':
                printf("\nSquare area calculation\n");
                printf("Enter the side length: ");
                scanf("%f", &val1);
                val2 = 0; // not needed
                break;
            default:
                printf("\nInvalid choice!\n");
                return 1;
        }

        // Step 2: Send inputs to child
        write(ptc[1], &choice, sizeof(char));
        write(ptc[1], &val1, sizeof(float));
        write(ptc[1], &val2, sizeof(float));

        // Step 5: Read result from child
        float area;
        read(ctp[0], &area, sizeof(float));
        printf("\nArea is: %.2f\n", area);

        close(ptc[1]);
        close(ctp[0]);

        wait(NULL); // Wait for child to finish

    } else {
        // ===== CHILD PROCESS =====

        close(ptc[1]); // Close write end of ptc
        close(ctp[0]); // Close read end of ctp

        // Step 3: Read input from parent
        char choice;
        float a, b;

        read(ptc[0], &choice, sizeof(char));
        read(ptc[0], &a, sizeof(float));
        read(ptc[0], &b, sizeof(float));

        // Step 4: Perform calculation
        float result = calculateArea(choice, a, b);

        // Send result back to parent
        write(ctp[1], &result, sizeof(float));

        close(ptc[0]);
        close(ctp[1]);
    }

    return 0;
}


Output:
[2021ict84@fedora ~]$ gcc ex1.c-o ex1
[2021ict84@fedora ~]$ ./ex1

Area Calculation program

Circle => C
Triangle => T
Square => S
Rectangle => R
Enter your choice: C

Circle area calculation
Enter the radius: 5.3

Area is: 88.25


Explanation:

Two pipes:
ptc: Parent to Child
ctp: Child to Parent

This C program calculates the area of shapes like circle, triangle, rectangle, and square using parent-child communication.
It creates two pipes to allow communication between the parent and child processes:
One for sending data from parent to child
One for sending the result from child to parent
The program uses fork() to create a child process.

The parent process:
Asks the user to choose a shape and enter the required values (like radius or sides).
Sends the shape choice and values to the child through a pipe.
Waits to receive the calculated area from the child and prints it.

The child process:
Reads the shape and values sent by the parent.
Calculates the area using the values.
Sends the area back to the parent through another pipe.
The program then ends after both processes finish their work.
