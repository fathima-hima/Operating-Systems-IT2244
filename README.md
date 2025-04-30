Operating Systems IT 2244
Day 06 Practical
04/04/2025

1.Get the calander and date
command: 
cal
date +%d

Output:
{ ~ }  » cal                                                                  ~
     April 2025
Su Mo Tu We Th Fr Sa
       1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30

{ ~ }  » date +%d                                                             ~
06

Explanation:
1. cal:
This command displays a calendar in the terminal.
it shows the current month's calendar.

2. date +%d:
The date command displays the current date and time.
The +%d part is an option that formats the output to only show the day of the month.
%d represents the day of the month, from 01 to 31.

===========================================================================================
2.Get the student name and marks for the 3 subjects from user then calculate the total and average
    Output:
    Enter the name: Isuru
    Enter the mark for subject1:
    Enter the mark for subject1:
    Enter the mark for subject1:
    Total:
    Average:

command:
echo Enter the name:
read name
echo Enter the mark for subject1:
read mark1
echo Enter the mark for subject2:
read mark2
echo Enter the mark for subject3:
read mark3
total=$(($mark1+$mark2+$mark3))
average=$(($total/3))
echo Total: $total
echo Average: $average

Output:
Enter the name:
zaheeda
Enter the mark for subject1:
3
Enter the mark for subject2:
4
Enter the mark for subject3:
5
Total: 12
Average: 4

Explanation:
First, a new file was created using the command vi ghi.sh. The given code was typed into the file,
and then it was saved and closed by typing :wq. After that, the file’s permission was changed to 
777 using the command chmod 777 ghi.sh, so that anyone could read, write, and run the file.
The script was then run using ./ghi.sh. It asked the user to enter their name and marks for three subjects.
Once the user entered the information, the script calculated and displayed the total and average marks on the screen.

================================================================================================

3.Create calculator with arithmetic operations.
command:
echo Enter the first number:
read num1
echo Enter the second  number:
read num2
sum=$(($num1+$num2))
sub=$(($num1-$num2))
div=$(($num1/$num2))
mul=$(($num1*$num2))
echo Summation:$sum
echo Subtraction:$sub
echo Division:$div
echo Multiplication:$mul

output:
{ ~ }  » ./prgrm4.sh                                                          ~
Enter the first number:
45
Enter the second number:
4
Summation: 49
Substraction: 41
Division: 11
Multiplication: 180

Explanation:
First, a new file was created using the command vi prgrm4.sh The provided code was typed into the file, 
and it was then saved and closed using the command :wq. To ensure the script could be executed by anyone, 
its permission was changed to 777 using the command chmod 777 prgrm4.sh 
The script was then run using ./prgrm4.sh . It prompted the user to enter the first number, and after input, 
asked for the second number. Once both values were entered, the script performed four arithmetic operations: 
addition, subtraction, division, and multiplication.

Finally, it displayed the results for each operation:

The sum of the two numbers,
The difference (first minus second),
The quotient (first divided by second),
The product of the two numbers.

==========================================
4.Get the days based on the use input numbers

command:
echo Enter the number:
read num
if [ "$num" -lt 8 ]; then
 if [ "$num" -eq 1 ]; then
        echo "Monday"
 elif [ "$num" -eq 2 ]; then
        echo "Tuesday"
 elif [ "$num" -eq 3 ]; then
        echo "Wednesday"
 elif [ "$num" -eq 4 ]; then
        echo "Thursday"
 elif [ "$num" -eq 5 ]; then
        echo "Friday"
 elif [ "$num" -eq 6 ]; then
        echo "Saturday"
 elif [ "$num" -eq 7 ]; then
        echo "Sunday"
 fi
else
 echo "Invalid Number"
fi

output:
{ ~ }  » ./prgrm5.sh  
Enter the number:
3
Wednesday

Explanation:
First, a new file was created using the command vi prgrm5.sh. The provided code was typed into the file, 
and it was then saved and closed using the command :wq. 
To ensure the script could be executed by anyone, its permission was changed to 777 using the command chmod 777 prgrm4.sh.
The script was then run using ./prgrm4.sh. It prompted the user to enter a number, which was stored in a variable. 
The script checked if the entered number was less than 8, ensuring it was within the range of 1 to 7.
If the input was valid (eg: from 1 to 7), the script compared the number to each weekday and printed the corresponding day
If the input number was 8 or more, the script displayed the message "Invalid Number".
This allowed the user to quickly get the name of the day based on the number they entered.

=======================================================
5.Verify wether your username is correct or not 
command:
echo Enter user name:
read name
username=$(whoami)
if [ "$name" = "$username" ]; then
        echo username is correct
else
        echo username is incorrect
fi

output:
{ ~ }  » ./prgrm6.sh                                                          
Enter username:
skyline
username is correct

Explanation:
First, a new file was created using the command vi prgrm6.sh. The given code was typed into the file, and it was then saved and closed by typing :wq. 
After that, the file’s permission was changed to 777 using the command chmod 777 checkuser.sh, allowing anyone to read, write, and execute the file.
The script was then run using ./prgrm6.sh.sh. It prompted the user to enter a username, and the input was stored in the variable name.
Next, the script used the whoami command to fetch the currently logged-in user's actual username, storing it in the variable username.
The script then compared the input (name) with the actual system username (username):
If both matched, the script printed: "username is correct"
Otherwise, it printed: "username is incorrect"

===============================================
6.Output: Enter two numbers:
command:
echo Enter two numbers:
read num1 num2

if [ "$num1" -gt "$num2" ]; then  
echo $num1 is greater than $num2
elif [ "$num1" -eq "$num2" ]; then 
echo $num1 is equal to $num2
else
echo $num1 is less than $num2
fi

output:
{ ~ }  » ./prgrm7.sh
Enter two numbers:
10 5
10 is greater than 5

Explanation:
The script was then run using ./compare.sh. It prompted the user to enter two numbers, which were stored in the variables num1 and num2.
The script then compared the two numbers using conditional statements:
If the first number was greater than the second (-gt), it printed:
"[num1] is greater than [num2]"
If both numbers were equal (-eq), it printed:
"[num1] is equal to [num2]"
If the first number was less than the second (else), it printed:
"[num1] is less than [num2]"

===================================================================================================================================

7.Create simple calculator using "expr" command as same as the Question 03
command:
echo Enter the first number:
read num1
echo Enter the second  number:
read num2
sum=$(expr $num1 + $num2)
sub=$(expr $num1 - $num2)
div=$(expr $num1 / $num2)
mul=$(expr $num1 \* $num2)
echo Summation:$sum
echo Subtraction:$sub
echo Division:$div
echo Multiplication:$mul

output:
{ ~ }  » ./prgrm8.sh
Enter the first number:
10
Enter the second  number:
5
Summation:15
Subtraction:5
Division:2
Multiplication:50

Explanation:
First, a new file was created using the command vi calc2.sh. The given code was typed into the file, and then it was saved and closed using the command :wq. 
After that, the file’s permission was changed to 777 using the command chmod 777 calc2.sh, so that anyone could read, write, and execute the file.
The script was then run using ./calc2.sh. It first prompted the user to enter the first number
, and then to enter the second number. These values were stored in the variables num1 and num2.
Using the expr command, the script performed four arithmetic operations:
Addition of the two numbers, stored in sum
Subtraction (first minus second), stored in sub
Division (first divided by second), stored in div
Multiplication, stored in mul (note: * was escaped with a backslash \ to avoid shell interpretation)
Finally, the script displayed the results of all four operations: Summation,Subtraction,Division,Multiplication.
