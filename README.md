# AOT Operating System Lab Exam 2023
## Section 1: If-Else Condition

### Q.1 -> All arithmetic operations
```bash
read -p "Enter two numbers: " a b
read -p "Enter the operator: " op
# Important Notes
# -eq expects integer to be compared & == is used for char comparision
# You must write fi when you use if otherwise it will not work [if->then->fi]
# always use dollar for getting value
if [ $op == '+' ]; then echo $((a+b))
elif [ $op == '-' ]; then echo $((a-b))
elif [ $op == '*' ]; then echo $((a*b)) # This will create no problem in linux
elif [ $op == '/' ]; then echo $((a/b))
elif [ $op == '%' ]; then echo $((a%b))
fi
```
#### Output
```
Enter two numbers: 5 10
Enter the operator: +
15
```

### Q.2 -> Greatest & least of among 3 nos
```bash
read -p "Enter three numbers: " a b c
if [ $a -gt $b -a $a -gt $c ]; then echo "Greatest is $a"
elif [ $b -gt $a -a $b -gt $c ]; then echo "Greatest is $b"
else echo "Greatest is $c"
fi

if [ $a -lt $b -a $a -lt $c ]; then echo "Least is $a"
elif [ $b -lt $a -a $b -lt $c ]; then echo "Least is $b"
else echo "Least is $c"
fi
```
#### Output
```
Enter three numbers: 10 2 7 
Greatest is 10
Least is 2
```

### Q.3 -> Leap year
```bash
read -p "Enter the year: " year
if [ `expr $year % 4` -eq 0 ]
	then 
		if [ `expr $year % 100` -eq 0 ]
			then 
				if [ `expr $year % 400` -eq 0 ]; then echo "Leapyear"
				else echo "Not Leapyear"
				fi
		else echo "Leapyear"
		fi
	else echo "Not Leapyear"
fi
```
#### Output
```
Enter the year: 2020
Leapyear
Enter the year: 2020
Leapyear
Enter the year: 1900
Not Leapyear
Enter the year: 1753
Not Leapyear
```

### Q.4 -> Grade calculation (These are easy questions do it from your own)
### Q.5 -> Electric bill calculation (These are easy questions do it from your own)

## Section 2: While & for loop , command line argument

### Q.1 -> Fibonacci series (up-to range/term)
```bash
fib() {
	n=$1
	if [ $n -le 1 ]; then echo $n
	else echo $(( `fib $((n-1))` + `fib $((n-2))` ))
	fi
}
# Important Note: Function Calling Format `func arg` to return result we use echo
# Up-to term
read -p "Enter the terms: " n
for ((i=0; i<n; i++)) 
do
	echo -n "`fib $i` "
done
# Up-to range
read -p "Enter the range: " n
start=0
while [ `fib $start` -le $n ]
do
	echo -n "`fib $start` "
	start=$((start+1))
done
```
#### Output
```
Enter the terms: 6
0 1 1 2 3 5 
Enter the range: 50
0 1 1 2 3 5 8 13 21 34 
```
### Q.2 -> Palindrome no.
```bash
read -p "Enter a number: " n
reverse=0
original=$n
while [ $n -gt 0 ]
dor
	reverse=$((reverse*10 + n%10))
	n=$((n/10))
done
if [ $reverse -eq $original ]; then
echo "$original is a palindrome number"
else echo "$original is not a palindrome number"
fi
```
#### Output
```
Enter a number: 121
121 is a palindrome number
```

### Q.3 -> GCD & LCM
```bash
gcd () {
	if [ $2 -ne 0 ]; then echo `gcd $2 $(($1%$2))`
	else echo $1
	fi
} 
lcm () {
	echo $((($1 * $2) / `gcd $1 $2`))
}
read -p "Enter two numbers: " a b
echo `gcd $a $b`
echo `lcm $a $b`
```
#### Output
```
Enter two numbers: 3 5 
1
15
```

### Q.4 -> Armstrong
```bash
read -p "Enter the number: " n
original=$n
countDigit=0
temp=0
while [ $n -gt 0 ]
do
	countDigit=$((countDigit+1))
	n=$((n/10))
done
n=$original #restore the original number
while [ $n -gt 0 ]
do
	remainder=$((n%10))
	ans=$((remainder ** countDigit))
	temp=$((temp + ans))
	n=$((n/10))
done
if [ $original -eq $temp ]; then echo "$original is an Armstrong Number"
else echo "$original is not an Armstrong Number"
fi
```
#### Output
```
Enter the number: 153
153 is an Armstrong Number
```

### Q.5 -> Pattern Questions
```
	  *				
   ***				
  *****				
 *******			
```

```bash
read -p "Enter the row number for first pattern: " n
for((i=1; i<=n; i++))
do
	# Calculation for spaces
	spaces=$((n-i))
	for((j=1; j<=spaces; j++))
	do
		echo -n " "
	done
	# Calculation for stars
	stars=$((2*i - 1))
	for((j=1; j<=stars; j++))
	do
		echo -n "*"
	done
	echo # for new line
done
```
```
****
***
**
*
```
```bash 
read -p "Enter the row number for second pattern: " n
for((i=4; i>=1; i--))
do
	for((j=1;j<=i;j++))
	do
		echo -n "*"
	done
	echo # for new line
done
```

## Section 4: bc calculator, function, recursion

### Q.1 -> Area of Triangle
```bash
# Use mycompiler.io to run this because replit doesn't support basic calculator
read -p "Enter the sides of triangle: " a b c
if [ $((a+b)) -le $c -o $((b+c)) -le $a -o $((c+a)) -le $b ]; then echo "Invalid Triangle"
else
	s=`echo "scale=3; $((a+b+c))/2" | bc`
	temp=`echo "scale=3; $s*($s-$a)*($s-$b)*($s-$c)" | bc`
	area=`echo "scale=3; sqrt($temp)" | bc`
	echo "The area of the triangle will be: $area"
fi
```
#### Output
```
Enter the sides of triangle: 4 5 7
The area of the triangle will be: 9.797
```

### Q.2 -> Factorial with recursion
```bash
fact() {
	n=$1
	if [ $n -le 1 ]; then echo 1
	else echo $((n*`fact $((n - 1))`))
	fi
}
read -p "Enter the number: " n
echo "$n! = `fact $n`"
```
#### Output
```
Enter the number: 5
5! = 120
```

### Q.3 -> Series f(x,n) = 1 + x^2/2! + x^4/4! +....+ x^2*n/(2*n)!
```bash
# Use mycompiler.io to run this because replit doesn't support basic calculator
fact() {
	n=$1
	if [ $n -le 1 ]; then echo 1
	else echo $((n*`fact $((n - 1))`))
	fi
}
f() {
	x=$1
	n=$2
	ans=0
	for((i=0; i<n; i++))
	do
		power=$((x ** (2*i)))
		factorial=`fact $((2*i))`
		ans=`echo "scale=3; $ans + ($power/$factorial)" | bc`
	done
	echo $ans
}
read -p "Enter the value of x, n respectively: " x n
echo `f $x $n`
```
#### Output
```
Enter the value of x, n respectively: 2 3
3.666
```

### Q.4 -> Pascal Triangle
```bash
calculate_coefficient() {
	row=$1
	col=$2
	result=1
	for ((i = 1; i <= col; i++)); do
		result=$((result * (row - i + 1) / i))
	done
	echo $result
}
print_pascals_triangle() {
	rows=$1
	for ((row = 0; row < rows; row++)); do
		for ((col = 0; col <= row; col++)); do
			coefficient=$(calculate_coefficient $row $col)
			echo -n "$coefficient "
		done
		echo
	done
}
read -p "Enter the number of rows: " rows
print_pascals_triangle $rows
```
#### Output
```
Enter the number of rows: 6
1 
1 1 
1 2 1 
1 3 3 1 
1 4 6 4 1 
1 5 10 10 5 1
```

## Section: 5 case-menu driven
### Q.1 -> commands (pwd, ps, date etc.) using case
```bash
echo "Press 1 for pwd"
echo "Press 2 for date"
echo "Press 3 for ps"
echo "Press 4 for Exit"
while [ true ]; do
read -p "Enter the choice: " op
case $op in
1) ps;;
2) date;;
3) pwd;;
4) exit;;
esac
done
```
#### Output
```
Press 1 for pwd
Press 2 for date
Press 3 for ps
Press 4 for Exit
Enter the choice: 1
	PID TTY          TIME CMD
   4135 pts/1    00:00:00 bash
   4142 pts/1    00:00:00 ps
Enter the choice: 2
Thu 16 Nov 2023 06:04:28 PM UTC
Enter the choice: 3
/home/runner/OS-Lab
```

### Q.2 -> basic calculator (‘+’,’-’...case)
```bash
read -p "Enter two numbers: " a b
read -p "Enter the operator: " op
case $op in
'+') echo "Summation is $((a+b))";;
'-') echo "Subtraction is $((a-b))";;
'*') echo "Multiplication is $((a*b))";;
'/') echo "Division is $((a/b))";;
'%') echo "Remainder is $((a%b))";;
'^') echo "Power is $((a**b))";;
esac
```
#### Output
```
Enter two numbers: 5 10
Enter the operator: *
Multiplication is 50
```

### Q.3 -> given date is valid or not
```bash
read -p "Enter day month year seperately: " day month year
if [ $day -le 0 -o $month -le 0 ]
then echo "Invalid Date"
exit
fi
case $month in
1|3|5|7|8|10|12) 
if [ $day -gt 31 ]
then echo "Invalid Date"
exit
fi
;;
4|6|9|11) 
if [ $day -gt 30 ]
then echo "Invalid Date"
exit
fi
;;
2) 
if [ $((year%400)) -eq 0 -o $((year%4)) -eq 0 -a $((year%100)) -ne 0 ]
then 
	if [ $day -gt 29 ]; then
		echo "Invalid Date"
		exit
	fi
else
	if [ $day -gt 28 ]; then
		echo "Invalid Date"
		exit
	fi
fi
;;
esac
echo "Valid Date"
```
#### Output
```
Enter day month year seperately: 32 12 2025
Invalid Date

Enter day month year seperately: 24 04 2023
Valid Date
```

### Q.4 -> Number to Word conversion (Ex. i/p-123, o/p-One Two Three)
```bash
read -p "Enter the number: " n
# Note: To declare an array in bash we use arr=()
# Note: To push elements in array we can do arr+=($value)

# We need to use this array approach because if we have values with 
# trailing zeros then the answer will be wrong in reverse algorithm
# Enter the number: 1530
# Output: One Five Three [but actual answer should be One Five Three Zero]
arr=()
while [ $n -gt 0 ] 
do
	temp=$((n%10))
	arr+=($temp)
	n=$((n/10))
done
# Note: To get the values of an array we use ${arr[@]}
# Note: To get the size of an array we use ${#arr[@]}
# Note: To get a particular index value from array we can use ${arr[0]}
size=${#arr[@]}
for((i=size-1; i>=0; i--))
do
	temp=${arr[i]}
	case $temp in
		0) echo -n "Zero " ;;
		1) echo -n "One " ;;
		2) echo -n "Two " ;;
		3) echo -n "Three " ;;
		4) echo -n "Four " ;;
		5) echo -n "Five " ;;
		6) echo -n "Six " ;;
		7) echo -n "Seven " ;;
		8) echo -n "Eight " ;;
		9) echo -n "Nine " ;;
	esac
	n=$((n/10))
done
```
#### Output
```
Enter the number: 1503
One Five Zero Three
```

## Section 6: Array, IFS

### Q.1 -> Searching
```bash
IFS=" " read -p "Enter the numbers: " -a numbers # Without giving input size
read -p "Which number you want to search: " key
for number in ${numbers[@]}
do
	if [ $number -eq $key ]; then echo "Element Present"
	exit
	fi
done
echo "Element Absent"
```
#### Output
```
Enter the numbers: 10 8 9 1 3 5 2
Which number you want to search: 1
Element Present
```

### Q.2 -> Sorting
```bash
IFS=" " read -p "Enter the numbers: " -a arr # Without giving input size
n=${#arr[@]}
for((i=0; i<n-1; i++)); do
	for((j=0; j<n-i-1; j++)); do
		if [ ${arr[j]} -gt ${arr[j+1]} ]; then 
			temp=${arr[j]}
			arr[j]=${arr[j+1]}
			arr[j+1]=$temp
		fi
	done
done
echo ${arr[@]}
```
#### Output
```
Enter the numbers: 10 8 9 1 3 5 2
1 2 3 5 8 9 10
```

### Q.3 -> DOB calculation (using IFS)
```bash
read -p "Enter your date of birth: (dd/mm/yyyy)": dob
IFS="/"
set $dob
day=$1
month=$2
year=$3
currday=`date +%d` # Note: Don't use space after + otherwise it will not work
currmonth=`date +%m`
curryear=`date +%Y`
ageday=$((currday-day))
agemonth=$((currmonth-month))
ageyear=$((curryear-year))
if [ $ageday -lt 0 ]; then
	ageday=$((ageday+30))
	agemonth=$((agemonth-1))
fi
if [ $agemonth -lt 0 ]; then
	agemonth=$((agemonth+12))
	ageyear=$((ageyear-1))
fi
echo "Your age is: $ageyear years $agemonth months and $ageday days"
```
#### Output
```
Enter your date of birth: (dd/mm/yyyy):16/05/2002
Your age is: 21 years 6 months and 0 days
```

## Section 7: File permission, Count on file

### Q.1 -> Check & Change the file permission using chmod command
```bash
# Note: To check the permission of a given file we  use ls -l filename.sh
# The first character is the type of file - means it’s a regular file, a d means it’s a 
# directory. Then next 3 segments are respectively user, group & others permission.

# Note: To give the permission to a file we use chmod ABC filename.sh where ABC is defined 
# as user, group & others permission. [4 -> Only read, 2-> Only write, 1-> Only execute]

ls -l main.sh
# change the user permission to execute also
chmod 744 main.sh
ls -l main.sh
# revoke the execution permission from the user again
chmod 644 main.sh
ls -l main.sh
```
```
Output: bash main.sh
-rw-r--r-- 1 runner runner 10231 Nov 15 04:48 main.sh
-rwxr--r-- 1 runner runner 10231 Nov 15 04:48 main.sh
-rw-r--r-- 1 runner runner 10231 Nov 15 04:48 main.sh
```
### Q.2 -> Count the number of line, word & character of a file using wc command
```bash
if [ $# -eq 0 ]; then echo "No argument is given"; exit; fi
for i in $*; do
	# To check if it's actually file or not
	if [ -f $i ]; then
		echo "$i is a file"
		echo "Lines: $(cat $i | wc -l)" 
		echo "Chars: $(cat $i | wc -c)"  
		echo "Words: $(cat $i | wc -w)"  
	else echo "$i is a directory"
	fi
done
```
#### Input File (test.txt):
```
This is going to be a test file. 
We are using this file to test the word count question.
```

```
Output: bash main.sh test.txt Test
test.txt is a file
Lines: 2
Chars: 90
Words: 19
Test is a directory
```

## Section 8: File Read/Write

### Q.1 -> Grade calculation
```bash
fname=$1
if [ -f $fname ]; then
exec < $fname
# Note: > means overwrite all the contents of a file and >> means append content to file
echo "Roll  Name	     Result	 Grade" > grade.txt 
while read line; do
	set `echo $line` # To convert the line in array form
 	marks=$3
    if [ $marks -gt 100 -o $marks -lt 0 ]; then echo "Invalid Input"
	elif [ $marks -le 100 -a $marks -gt 90 ]; then echo "$1	  $2	 $3		 O" >> grade.txt
	elif [ $marks -le 90 -a $marks -gt 80 ]; then echo "$1	  $2	 $3		 E" >> grade.txt
	elif [ $marks -le 80 -a $marks -gt 70 ]; then echo "$1	  $2	 $3		 A" >> grade.txt
	elif [ $marks -le 70 -a $marks -gt 60 ]; then echo "$1	  $2	 $3		 B" >> grade.txt
	elif [ $marks -le 60 -a $marks -gt 50 ]; then echo "$1	  $2	 $3		 C" >> grade.txt
	elif [ $marks -le 50 -a $marks -gt 40 ]; then echo "$1	  $2	 $3		 D" >> grade.txt
	else echo "$1	  $2	 $3		 F" >> grade.txt
 	fi
done
cat grade.txt
else echo "This is not a file."
fi
```
#### Input File (result.txt):
```
001 Student1 81
002 Student2 95
003 Student3 74
004 Student4 69
005 Student5 57
006 Student6 40
007 Student7 34
008 Student8 85
009 Student9 91
```
#### Output File (grade.txt):
```
Roll  Name	     Result	 Grade
001	  Student1	 81		 E
002	  Student2	 95		 O
003	  Student3	 74		 A
004	  Student4	 69		 B
005	  Student5	 57		 C
006	  Student6	 40		 F
007	  Student7	 34		 F
008	  Student8	 85		 E
009	  Student9	 91		 O

```

### Q.2 -> Weekly Temperature Calculation
```bash
```
### Q.3 -> String Palindrome
```bash
# Function to check if a string is a palindrome
is_palindrome() {
	str=$1
	reversed=`echo "$str" | rev`
	[ $str == $reversed ]
}
# Extract and filter palindrome strings
echo "Palindrome Words" > output.txt # overwrite all the previous data of the file
echo "----------------" >> output.txt
grep -oE '[[:alpha:]]+' $1 | while read -r word; do
	if `is_palindrome $word`; then
		echo $word >> output.txt
	fi
done
cat output.txt
```

#### Input File (palin.txt):
```
mom; dad
liril@ 
Flower,
XYZ.
```
#### Output File (output.txt):
```
Palindrome Words
----------------
mom
dad
liril
```

## Section 9: tput cup command

### Q.1 -> Circle
```bash
read -p "Enter the radius value: " r
clear
for((i=0; i<=360; i++)); do
	th1=`echo "scale=3; 3.14/180*$i"|bc|awk '{print cos($1)}'`
	x=`echo "scale=3; $r*$th1"|bc|awk '{print int($1)}'`
	th2=`echo "scale=3; 3.14/180*$i"|bc|awk '{print sin($1)}'`
	y=`echo "scale=3; $r*$th2"|bc|awk '{print int($1)}'`
	x=$((5+x))
	y=$((20+y))
	tput cup $x $y
	echo "*"
done
```
```
Output:

  *****
 *     *
*       *
*       *
*       *
*       *
*       *
 *     *
  *****

```
### Q.2 -> Square
```bash
read -p "Enter the length of the side: " side
clear
for((i=0;i<side;i++)); do
	for((j=0;j<side;j++)); do
		if [ $i -eq 0 -o $i -eq $((side-1)) -o $j -eq 0 -o $j -eq $((side-1)) ]; then
			tput cup $i $j
			echo "*"
		fi
	done
done
```
```
Output:
*****
*   *
*   *
*   *
*****
```
### Q.3 -> Rectangle
```bash
read -p "Enter the two sides length of rectangle " x y
clear
for((i=0;i<x;i++)); do
	for((j=0;j<y;j++)); do
		if [ $i -eq 0 -o $i -eq $((x-1)) -o $j -eq 0 -o $j -eq $((y-1)) ]; then
			tput cup $i $j
			echo "*"
		fi
	done
done
```
```
Output:
$ bash main.sh 
Enter the length of height & width respectively: 5 6
******
*    *
*    *
*    *
******
```
### Q.4 -> Triangle
```bash
read -p "Enter the base of the triangle:" base
read -p "Enter the height of the triangle:" height
clear
for ((i = 1; i <= height; i++)); do
  spaces=$((height - i))
  for ((j = 1; j <= spaces; j++)); do
	tput cup $((i + 1)) $((j + 1))
	echo -n " " # Adding spaces here
  done
  for ((k = 1; k <= 2 * i - 1; k++)); do
	tput cup $((i + 1)) $((base - spaces + k))
	echo -n "*" # Adding stars here
  done
done
tput cup $((height + 2)) 0  # Move cursor to a new line after the triangle
```
```
 *
  ***
   *****
	*******
	 *********
	  ***********
	   *************
```
## Section 10: head & tail command


### Q1 -> Student Database
1. Insert
2. Update
3. Delete
4. Display

```bash
insert() {
	read -p "Enter roll name & marks respectively: " roll name marks
	echo "$roll|$name|$marks" >> student.txt
	echo "Inserted $name at the end of the file successfully"
}

insert_at_position() {
	read -p "Enter roll name & marks respectively: " rollno name marks
	read -p "Enter the roll after which you wanna insert: " rollpos
	n=$(cat student.txt | wc -l)
	for((i=2; i<=n+1; i++)); do
		currline=`head -n $i student.txt | tail -n 1` # current line
		# Cut the line with respect to | character & -f is used to specifies fields to extract
		roll=`echo $currline | cut -d \| -f 1`
		if [ $roll -eq $rollpos ]; then
			head -n $i student.txt > temp.txt # written all previous values
			echo "$rollno|$name|$marks" >> temp.txt # written actual data to be inserted
			tail -n $((n-i)) student.txt >> temp.txt # write all remaining lines to temp.txt
			cat temp.txt > student.txt # overwritten the new data to student file
			break
		fi
	done
	echo "Inserted $name after roll number $rollpos successfully"
}

display() {
	cat student.txt
}

update() {
	read -p "Enter the roll you wanna update: " rollpos
	read -p "Enter the updated marks: " newmarks
	n=$(cat student.txt | wc -l)
	for((i=2; i<=n+1; i++)); do
		currline=`head -n $i student.txt | tail -n 1` # current line
		# Cut the line with respect to | character & -f is used to specifies fields to extract
		roll=`echo $currline | cut -d \| -f 1`
		name=`echo $currline | cut -d \| -f 2`
		if [ $roll -eq $rollpos ]; then
			head -n $((i-1)) student.txt > temp.txt # store all previous values
			echo "$roll|$name|$newmarks" >> temp.txt # store new data in temp file
			tail -n $((n-i)) student.txt >> temp.txt # store rest of the values
			cat temp.txt > student.txt
			break
		fi
	done
	echo "Updated Roll: $rollpos with new marks $newmarks successfully"
}

delete() {
	read -p "Enter the roll you wanna delete: " rollpos
	 n=$(cat student.txt | wc -l) 
	 for((i=2; i<=n+1; i++)); do
		 currline=`head -n $i student.txt | tail -n 1` # current line
		 # Cut the line with respect to | character & -f is used to specifies fields to extract
		 roll=`echo $currline | cut -d \| -f 1`
		 if [ $roll -eq $rollpos ]; then
			 head -n $((i-1)) student.txt > temp.txt # store all previous values
			 tail -n $((n-i)) student.txt >> temp.txt # store rest of the values
			 cat temp.txt > student.txt
			 break
		 fi
	 done
	 echo "Deleted Roll: $rollpos successfully"
}

echo "Press 1 for Insert at end"
echo "Press 2 for Insert at position"
echo "Press 3 for Display"
echo "Press 4 for Update a record"
echo "Press 5 for Delete a record"
echo "Press 0 for exit"

while [ true ]; do
	read -p "Enter your choice: " choice
	case $choice in
		1) insert ;;
		2) insert_at_position ;;
		3) display ;;
		4) update ;;
		5) delete ;;
		0) exit ;;
		*) echo "Invalid Option"
	esac
done
```

#### Input (student.txt):
```
Roll|Name|Marks
83|Student13|74
84|Student87|75
95|Student19|85
48|Student48|70
49|Student49|58
```
#### Output:
```
Press 1 for Insert at end
Press 2 for Insert at position
Press 3 for Display
Press 4 for Update a record
Press 5 for Delete a record
Press 0 for exit
Enter your choice: 1
Enter roll name & marks respectively: 81 Student81 81
Inserted Student81 at the end of the file successfully
Enter your choice: 2
Enter roll name & marks respectively: 85 Student85 85
Enter the roll after which you wanna insert: 84
Inserted Student85 after roll number 84 successfully
Enter your choice: 3
Roll|Name|Marks
83|Student13|74 
84|Student87|75 
85|Student85|85
95|Student19|85
48|Student48|70
49|Student49|58
81|Student81|81
Enter your choice: 4
Enter the roll you wanna update: 49
Enter the updated marks: 85
Updated Roll: 49 with new marks 85 successfully
Enter your choice: 5
Enter the roll you wanna delete: 95
Deleted Roll: 95 successfully
Enter your choice: 3
Roll|Name|Marks
83|Student13|74 
84|Student87|75 
85|Student85|85
48|Student48|70
49|Student49|85
81|Student81|81
Enter your choice: 0
```

#### Output File (student.txt):
```
Roll|Name|Marks
83|Student13|74 
84|Student87|75 
85|Student85|85
48|Student48|70
49|Student49|85
81|Student81|81
```

## Section 11: Process Creation

### Q.1 -> Child process creation using fork() system call
```c
#include <stdio.h>
#include <unistd.h>
int main() {
	pid_t pid; // Process ID
	pid = fork(); // Fork the current process
	// Code executed by the parent process
	if (pid > 0) {
		printf("Parent process (PID: %d)\n", getpid());
		printf("Child process ID: %d\n", pid);
	}
	// Code executed by the child process
	else if (pid == 0) {
		printf("Child process (PID: %d)\n", getpid());
	}
	return 0;
}
```
#### Output
```
Parent process (PID: 2801)
Child process ID: 2802
Child process (PID: 2802)
```

## Section 12: Inter Process Communication

### Any one process can send a number/string to the another process using pipe() system call.
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <string.h>
#define MAX 100
int main() {
	int option;
	printf("Press 1 for (Parent -> Child)\nPress 2 for (Child -> Parent)\nEnter an option: ");
	scanf("%d",&option);
	pid_t pid;
	int fd[2]; // fd means file descriptor
	char s1[MAX] = "Hello Pipe", s2[MAX];
	// Note: Always create pipe before fork() system call
	pipe(fd); // creating a pipe
	pid=fork(); // fork system call
	switch(option){
		case 1: 
			// Case 1: Parent process writes data to pipe and Child process reads from pipe
			if(pid == 0) { // child process
				read(fd[0], s2, MAX);
				close(fd[0]); // Close the read end in the child process
				printf("Child Process received: %s\n", s2);
			}
			else {
				write(fd[1], s1, strlen(s1)+1);
				close(fd[1]); // Close the write end in the parent process
				printf("Data written to pipe by parent process successfully. \n");
			}
			break;
		case 2:
			// Case 2: Child process writes data to pipe and Parent process reads from pipe
			if(pid == 0) { // child process	
				write(fd[1], s1, strlen(s1)+1);
				close(fd[1]); // Close the write end in the child process
				printf("Data written to pipe by child process successfully. \n");
			}
			else {
				read(fd[0], s2, MAX);
				close(fd[0]); // Close the read end in the parent process
				printf("Parent process received: %s\n", s2);
			}
			break;
		default:
			printf("Invalid Option\n");
	}
	return 0;
}
```
#### Output for Case 1 (Parent to Child)
```
Press 1 for (Parent -> Child)
Press 2 for (Child -> Parent)
Enter an option: 1
Data written to pipe by parent process successfully. 
Child Process received: Hello Pipe
```

#### Output for Case 2 (Child to Parent)
```
Press 1 for (Parent -> Child)
Press 2 for (Child -> Parent)
Enter an option: 2
Data written to pipe by child process successfully. 
Parent process received: Hello Pipe
```
