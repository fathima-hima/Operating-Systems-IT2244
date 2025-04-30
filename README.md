Operating Systems IT 2244
Day 08 Practical
21/04/2025


Q1)Fibonacci Series 
Output: First 10 Fibonacci numbers
0 1 1 2 3 5 8 13 21 34

command:
a=0;
b=1;
for((i=1;i<=10;i++))
do
echo $a

c=$(($a+$b))
a=$b
b=$c
done


output:

[2021ict84@fedora ~]$ ./fibonacci.sh
0
1
1
2
3
5
8
13
21
34

Explanation:
Starts with a=0, b=1 (first two Fibonacci numbers)
In each loop:
Prints a
Calculates c = a + b (next Fibonacci number)
Shifts values:
a becomes b
b becomes c
Repeats 10 times to give:
0 1 1 2 3 5 8 13 21 34

============================================================================

Q2)Factorial
output: Factorial of 5 is: 120

command:
echo Enter number for find factorial:
read num
factorial=1;
for((i=1;i<=$num;i++))
do
factorial=$(($factorial * $i));
done

echo Factorial of $num: $factorial;

Output:

[2021ict84@fedora ~]$ ./factorial.sh
Enter number for find factorial:
5
Factorial of 5: 120

Explanation:
Reads a number (e.g., 5)
Initializes factorial = 1
Multiplies factorial by i from 1 to num
For 5:
1 × 2 × 3 × 4 × 5 = 120
Prints: Factorial of 5: 120

===========================================================================
Q3)Multiples of 3 between 1 and 50:
command:
for((i=1;i<=50;i++))
do
temp=$(($i%3));
if [ "$temp" -eq 0 ]; then
echo $i;
fi
done

output:

[2021ict84@fedora ~]$ ./multable.sh
3
6
9
12
15
18
21
24
27
30
33
36
39
42
45
48

Explanation:
Loops from 1 to 50
Uses modulus operator (%) to check divisibility by 3
If i % 3 == 0, then i is a multiple of 3
Prints all such numbers: 3 6 9 ... 48
