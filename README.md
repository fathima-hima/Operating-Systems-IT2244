Operating Systems IT 2244 Day 01 Practical Windows Commands PRACTICAL

1.Practical No: 01

2.Problem Specification: Writing a Batch Script to Create Folder Structures

3.Implementation:

Steps to Create the Batch Script: 1)Open a Text Editor: 2)Write the Script: In the text editor, type the following script. This script uses basic batch commands like mkdir to create folders and cd to navigate between them

mkdir Criteria_1 cd Criteria_1 mkdir Standard_1 mkdir Standard_2 mkdir Standard_3

cd.. mkdir Criteria_2 cd Criteria_2 mkdir Standard_1 mkdir Standard_2 mkdir Standard_3 mkdir Standard_4 mkdir Standard_5 cd.. mkdir Criteria_3 cd Criteria_3 mkdir Standard_1 mkdir Standard_2 mkdir Standard_3

cd.. mkdir Criteria_4 cd Criteria_4 mkdir Standard_1 mkdir Standard_2 mkdir Standard_3 mkdir Standard_4 mkdir Standard_5 mkdir Standard_6 cd.. mkdir Criteria_5 mkdir Criteria_6 mkdir Criteria_7

3)How to run the Batch Script:

1.Save the Script: After writing the script, save it with a .bat extension (e.g., createFolders.bat) 2.Run the Script: Find the .bat file in File Explorer. Double-click it to execute. The script will automatically create the folder structure in the same location as the .bat file.

4.Explanation of Commands Used:

mkdir: Creates new folders.

cd: Navigates between folders

cd.. – Goes up one folder level

5.Conclusion: In this practical, we created a batch script to automatically set up a folder structure. By using commands like mkdir, cd, and cd.. , to organize the directories.

1.Practical No: 02

2.Problem Specification: Writing a Batch Script to Calculate Age

3.Implementation:

Steps to Create the Batch Script:

1)Open a Text Editor: 2)Write the Script: In the text editor, type the following script. This script asks for the user's birth year, then calculates and displays their age based on the current year.

@echo off set /p birth_year=Enter your birth year: set /a age=%date:~10,4% - %birth_year% echo Your age is: %age% pause

3)How to Run the Batch Script: Save the Script: After writing the script, save it with a .bat extension (e.g., calculateAge.bat). Run the Script: Find the .bat file in File Explorer. Double-click it to execute. The script will ask you to enter your birth year and then show your calculated age.

4.Explanation of Commands Used:

set /p: Asks the user to input their birth year.

%date:~10,4%: Retrieves the current year from the system date. set /a: Performs arithmetic (calculates the age).

echo: Displays the result.

pause: Pauses the script so you can see the result before closing.

5.Conclusion:

In this practical, we created a batch script to calculate a user's age based on their birth year and the current year. By using basic commands like set, echo, and pause, we were able to interact with the user and perform a simple calculation.

1.Practical No: 03

2.Problem Specification: Writing a Batch Script to Display System Information

3.Implementation:

Steps to Create the Batch Script:

1)Open a Text Editor: 2)Write the Script: In the text editor, type the following script. This script will display the username, system version, current date, and time.

@echo off echo Username : %username% echo Version : ver

echo Date : %date%

echo Time : time

pause

3)How to Run the Batch Script:

Save the Script: After writing the script, save it with a .bat extension (e.g., systemInfo.bat). Run the Script: Find the .bat file in File Explorer. Double-click it to execute. The script will show your username, system version, current date, and time.

4.Explanation of Commands Used:

@echo off: Hides the command execution details for cleaner output.

echo: Displays information to the user.

%username%: Displays the current user's username.

ver: Shows the system version.

%date%: Displays the current date.

time: Displays the current system time.

pause: Pauses the script so you can view the results before closing the window.

5.Conclusion:

In this practical, we created a batch script that shows system information such as the username, version, date, and time. By using simple commands like echo, %username%, ver, and pause, we can easily display useful system details.

1.Practical No: 04

2.Problem Specification: Change the text and background color of CMD

3.Implementation:

Syntax

color xy

x - represents the color of the Terminal’s background

y - represents the color of the font on the Command Prompt Terminal.

0 = Black       8 = Gray
1 = Blue        9 = Light Blue
2 = Green       A = Light Green
3 = Aqua        B = Light Aqua
4 = Red         C = Light Red
5 = Purple      D = Light Purple
6 = Yellow      E = Light Yellow
7 = White       F = Bright White
Replace 'x' with 'f' for a white background and 'y' with 'd' for a light purple font.

color fd

4.Conclusion: The color fd command changes the Command Prompt background to white and the text to light purple. This shows how we can easily change the look of the terminal using color codes.

How to Open PuTTY and Connect to a Server

1.Open PuTTY – Search for PuTTY on your computer and open it.

2.Enter Server IP – Type 172.16.140.150 in the Host Name box.

3.Start Connection – Click Open to connect.

4.Login – Enter your username and password (password is hidden when typing). (Password used: 789*asd)

5.Connected! – You are now logged into the server.
