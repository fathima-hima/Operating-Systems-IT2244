Operating Systems IT 2244
Day 04 Practical
24/03/2025


  Implementation:
	1)Display the calander
	command: cal
	output:
	 cal                                                                                                                                                        ~
    	 April 2025
	 Su Mo Tu We Th Fr Sa
       	 1  2  3  4  5
         6  7  8  9 10 11 12
	 13 14 15 16 17 18 19
	 20 21 22 23 24 25 26
	 27 28 29 30

	2)Command to display the day of the month as a two-digit number
	---------------------------------------------------------------
	command: date +%d
	output: 
	{ Desktop }  » date +%d                                         
	24

	explanation of command:
	date -> Shows the date and time.
	+%d -> Displays only the day (01-31)

	3)Command to display the last two digits of the current year
	------------------------------------------------------------
	command: date +%y
	output: 
	{ Desktop }  » date +%y
	25

	explanation of command:
	date → Shows the date and time.
	+%y → Displays the last two digits of the year (00-99)

	4)Command to display the full weekday name
	------------------------------------------
	command: date +%A
	output: 
	{ Desktop }  » date +%A
	Monday

	explanation of command:
	date → Shows the date and time.
	+%A → Displays the full name of the weekday (eg: Sunday, Monday)

	5)Command to display the abbreviated weekday name
	-------------------------------------------------
	ommand: date +%a
	output: 
	{ Desktop }  » date +%a
	Mon

	explanation of command:
	date → Shows the date and time.
	+%a → Displays the abbreviated weekday name (e.g., Sun, Mon)

	6)Command to display the full month name
	----------------------------------------
	command: date +%B
	output: 
	{ Desktop }  » date +%B
	March

	explanation of command:
	date → Shows the date and time.
	+%B → Displays the full month name (e.g., January, February)

	7)Command to display the abbreviated month name
	-----------------------------------------------
	command: date +%b
	output: 
	{ Desktop }  » date +%b
	Mar

	explanation of command:
	date → Shows the date and time.
	+%b → Displays the abbreviated month name (e.g., Jan, Feb)

	8)Command to display the month as a two-digit number
	----------------------------------------------------
	command: date +%m
	output: 
	{ Desktop }  » date +%m
	03

	explanation of command:
	date → Shows the date and time.
	+%m → Displays the month as a two-digit number (01-12)

	9)Command to display the minute as a two-digit number
	-----------------------------------------------------
	command: date +%M
	output: 
	{ Desktop }  » date +%M
	18

	explanation of command:
	date → Displays the system date and time.
	+%M → Extracts and displays the current minutes (00-59)

	10)Command to display current hour in 24-hour format
	---------------------------------------------------
	command: date +%H
	output: 
	{ Desktop }  » date +%H
	22

	explanation of command:
	date → Displays the system date and time.
	+%H → Extracts and displays the current hour in 24-hour format (00-23)
	
	11)Getting user input in Linux
	------------------------------


	Example 01=>

	Open the terminal and type vi prgrm1.sh to create a new file using the vi command.
	Press i to enter INSERT mode and type the script, which prompts the user for their name and three numbers, then calculates the sum and average.
	After entering the code, press Esc, type :wq, and press Enter to save and exit the file.
	To verify whether the file is created, use the command ls -l prgrm1.sh, which will list the file along with its permissions.
	Grant full execution permissions to the file by running chmod 777 prgrm1.sh, allowing it to be executed.
	Check if the permissions are updated by using ls -l prgrm1.sh again, where it should display rwxrwxrwx.
	Execute the script using ./prgrm1.sh, which will:
	Prompt the user to enter their name and three numbers.
	Display a greeting message.
	Compute the sum and average of the numbers.
	Display the results.

	command:
	echo "Who are you?"
	read name
	echo "Enter Number 1"
	read x
	echo "Enter Number 2"
	read y
	echo "Enter Number 3"
	read z
	sum=$(($x+$y+$z))
	avg=$(($sum/3))

	echo "Hi" $name
	echo "Summation " $sum
	echo "Average " $avg

	output:
	{ Desktop }  »                                                
	\ 	echo "Who are you?"
	\       read name
	\       echo "Enter Number 1"
	\       read x
	\       echo "Enter Number 2"
	\       read y
	\       echo "Enter Number 3"
	\       read z
	\       sum=$(($x+$y+$z))
	\       avg=$(($sum/3))
	\
	\       echo "Hi" $name
	\       echo "Summation " $sum
	\       echo "Average " $avg
	\ 
	Who are you?
	Kamal
	Enter Number 1
	3
	Enter Number 2
	4
	Enter Number 3
	5
	Hi Kamal
	Summation  12
	Average  4

	explanation of the code:
	-echo prints "Who are you?" to the screen.
	-read name takes user input and stores it in the variable name
	-echo asks the user to enter three numbers.
	-read x, read y, and read z store the entered numbers into variables x, y, and z
	-The sum of x, y, and z is calculated using $(()) (arithmetic expansion).
	-The result is stored in the variable sum.
	-The sum is divided by 3 to get the average.
	-The result is stored in the variable avg.
	-Greets the user with "Hi" followed by their name.
	-Displays the calculated sum and average.

	Example 02=>

	Open the terminal and type vi prgrm2.sh to create a new file using the vi command.
	Press i to enter INSERT mode and type the script, which prompts the user to enter two numbers and then performs addition, subtraction, multiplication, and division.
	After entering the code, press Esc, type :wq, and press Enter to save and exit the file.
	To verify whether the file is created, use the command ls -l prgrm2.sh, which will list the file along with its permissions.
	Grant full execution permissions to the file by running chmod 777 prgrm2.sh, allowing it to be executed.
	Check if the permissions are updated by using ls -l prgrm2.sh again, where it should display rwxrwxrwx.
	Execute the script using ./prgrm2.sh, which will:
	Prompt the user to enter two numbers.
	Compute the sum, difference, product, and quotient of the numbers.
	Display the results.

	command:
	echo "Enter number 1:"
 	read p
	 echo "Enter number 2:"
 	read q
 	sum=$(($p+$q))
 	sub=$(($p-$q))
 	mul=$(($p*$q))
 	div=$(($p/$q))

	echo "Addition " $sum
	echo "subtraction " $sub
	echo "multiplication " $mul
	echo "division " $div

	output:
	{ Desktop }  »                                            
	\ echo "Enter number 1:"
	\  read x
	\  echo "Enter number 2:"
	\  read y
	\  sum=$(($p+$q))
 	\  sub=$(($p-$q))
 	\  mul=$(($p*$q))
 	\  div=$(($p/$q))

	\
	\ echo "Addition " $sum
	\ echo "subtraction " $sub
	\ echo "multiplication " $mul
	\ echo "division " $div
	\ 
	Enter number 1:
	20
	Enter number 2:
	3
	Addition  23
	subtraction  17
	multiplication  60
	division  6

	Explanation of code:
	-echo displays a message asking the user to enter numbers.
	-read x and read y take user input and store the values in variables x and y
	-Addition (sum): Adds p and q → sum = p + q
	-Subtraction (sub): Subtracts q from p → sub = p - q
	-Multiplication (mul): Multiplies p and q → mul = p * q
	-Division (div): Divides p by q → div = p / q (integer division)
