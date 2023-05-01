# binbash
# List the names of the users logged in and their total count without displaying any further details.
$ who -q
# Find out your terminal’s device name.
$ tty
# Display current date in the form dd/mm/yyyy.
$ date +%d/%m/%y
# Find out your machine’s name and the version of the operating system.
$ uname -nr
# Clear the screen and place the cursor at row 12, column 25.
$ clear
$ tput cup 12 25
# Find the decimal equivalent of 1101001.
$ echo "ibase=2; 1101001" | bc
# Find out the users who are idling.
$ w
# Ensure that bc displays the results of all divisions using three decimal places.
$ bc
scale=3
10/3
3.333
quit
# List all filenames starting with ‘a’ or ‘b’ or ‘m’.
$ find . -type f -name "[a-b-m]*"
# List all filenames that end with a digit.
$ find . -type f -name "*[0-9].*"
# List all files in the current directory whose second character is a digit.
$ find . -type f -name "?[0-9]*"
# Use command(s) to create a directory in your home directory called KeepOut whose contents can be read only by you.
$ cd ~
$ mkdir KeepOut
$ chmod 400 KeepOut
# List all the files beginning with the character "a" on the screen and also store them in a file called file1.
$ ls -1 | grep "^a" > file1
# List all the files with 3rd character "a" on the screen and also store them in a file called file1.
$ ls -1 | grep "^..a" > file1
# Sort the output of who and display on screen along with the total number of users. the same output except the number of users should be stored in a file file1.
$ who | sort | tee >(wc -l | awk '{print 1 " users"}' > file1)
# Double space a file.
$ sed G filename > outputfile
# Select lines 5 to 10 of a file.
$ sed -n '5,10p' filename
# e) Find the user name and group id from the file/etc/passwd using the cut command.

$ cut -d: -f1,4 /etc/passwd > outputfile
# f) Extract the names of the users from /etc/passwd after ignoring the first 10 entries.

$ tail -n +11 /etc/passwd | cut -d: -f1
# g) Sort the file /etc/passwd on GUID (primary) and UID (secondary) so that the users with the same GUID are placed together. User with a lower UID should be placed higher in the list.

$ sort -t: -k4,4 -k3,3n /etc/passwd
# h) List from etc/passwd the UID and the user having the highest UID.

$ awk -F: '{print 3, 1}' /etc/passwd | sort -n -r | head -1
# i) Device a sequence which lists the 5 largest files in the current directory.

$ ls -lS | head -5
# j) Remove duplicate lines from a file.

$ sort file.txt | uniq > file_unique.txt
# k) Count the frequency of occurences of words in a file.

$ grep -oE '[a-zA-Z]+' file.txt | sort | uniq -c | sort -nr
# l) Find "long" listing of the smallest 5 files in the /etc directory whose name contains the string ".conf", sorted by increasing file size.

$ find /etc -type f -name "\*.conf" -ls | sort -k7 | head -n 5
# m) Get a sorted list, with no duplicates, of all the users logged into the logged network.

$ who | cut -d' ' -f1 | sort | uniq
# n) Find all files in your home directory that are more than a week old and end with .bak.

$ find ~ -type f -name "\*.bak" -mtime +7
# o) How many total lines are contained in all the files ending in .c in the current directory, printing only the total number of lines.

$ find . -name "\*.c" -exec wc -l {} + | tail -n1 | awk '{print 1}'
# (i) Create two files.

$ touch file1 file2
# (ii) Combine the two files.

$ cat file1 file2 > combinedfile
# (iii) Search a specific word from any one of the file.

$ grep "word" file1
# (iv) Search a specific file from a directory.

$ find /path/to/dir -name "filename"
# 2. Under the same directory create 8 files with any extension of your choice but at least 3 file names must start with letter d and has extension .sh & 2 files with letter t. Note that no file should be empty.

$ echo "File 1" > d1.sh
$ echo "File 2" > d2.sh
$ echo "File 3" > d3.sh
$ echo "File 4" > t1
$ echo "File 5" > t2
$ echo "File 6" > file6.txt
$ echo "File 7" > file7.txt
$ echo "File 8" > file8.txt
# 3. Sort the output of who and display on screen along with total number of users. The same output except the number of users should be stored in a file file1.

$ who | sort > file1
$ wc -l file1
# 4. Write a shell script to implement a basic calculator (+,-,/,*)

#!/bin/bash

echo "Enter two numbers: "
read num1
read num2
echo "Enter an operator (+,-,*,/): "
read operator
if [ "$operator" = "+" ]; then
  result=$(($num1 + $num2))
elif [ "$operator" = "-" ]; then
  result=$(($num1 - $num2))
elif [ "$operator" = "*" ]; then
  result=$(($num1 * $num2))
elif [ "$operator" = "/" ]; then
  result=$(($num1 / $num2))
else
  echo "Invalid operator"
  exit 1
fi
echo "Result: $result"
# 5. Write and execute the following UNIX commands.
# (i) To view all the files and directories.

$ ls -al
# (ii) To view only the directories.

$ ls -d */
# (iii) To view only the files in a directory.

$ ls -p | grep -v /
# (iv) Display the working directory.

$ pwd
# (v) Rename file1 to file2. if file2 exists prompt for confirmation before overwriting it.

if [ -f file2 ]; then
  read -p "file2 already exists, overwrite? (y/n) " choice
  if [ "$choice" = "y" ]; then
    mv file1 file2
  fi
else
  mv file1 file2
fi
# 6. Write and execute the following UNIX commands.
# i. Create a directory SAMPLE under your home directory.

$ mkdir ~/SAMPLE
# ii. Create a sub-directory by name TRIAL under SAMPLE.

$ mkdir ~/SAMPLE/TRIAL
# iii. Change to SAMPLE.

$ cd ~/SAMPLE
# iv. Change to your home directory.

$ cd ~
# v. Change from home directory to TRIAL by using absolute and relative pathname.

$ cd ~/SAMPLE/TRIAL
$ cd ../TRIAL
# vi. Remove directory TRIAL.

$ rm -r ~/SAMPLE/TRIAL
# 7. Write and execute the following UNIX commands.
# i. start a script in your home directory

$ cd ~
$ touch script.sh
$ chmod +x script.sh
# ii. in your cs330 lab directory create three new directories named 'weather', 'assignment', and 'web' (if you do not have a cs330 lab directory then create it)

if [ ! -d cs330_lab ]; then
  $ mkdir cs330_lab
fi
$ cd cs330_lab
$ mkdir weather
$ mkdir assignment
$ mkdir web
# iii. change the permissions of the directory 'web' to -rwxr-xr-x using the octal form of chmod

$ chmod 755 web
# iv. change your working directory to weather

$ cd weather
# v. without using a text editor create three files called 'today', 'tomorrow', and 'deer'

$ touch today tomorrow deer
# vi. check the permissions with ls -l

$ ls -l
# vii. change the permissions of 'deer' to rwx r-- r--

$ chmod 744 deer
# viii. change the permissions of 'today' to -rw- r-- r--

$ chmod 644 today
# ix. check the permissions with ls -l

$ ls -l
# 8. Write a shell script which will take a filename as input and apply READ & EXECUTE permissions only for the owner and group.

#!/bin/bash

filename=$1
if [ ! -e $filename ]; then
  echo "Error: file $filename does not exist."
  exit 1
fi
chmod 550 $filename
echo "Success: READ and EXECUTE permissions added for owner and group on $filename"
# a) Find out the PID of your login shell.

$ echo "$SHELL"
$ ps
# b) Remove the header line from the ps output.

$ ps --no-headers
# c) List all processes that you are currently running on your machine, sorted by the command name in alphabetical order (i.e. a process running acroread should be listed before a process running zwgc). The output should consist only of the processes you are running and nothing else (i.e. if you are running 6 processes, the output should only have 6 lines).

$ ps|sort -d
# d) Display the files in the current directory that contain the string MCA HITK in either upper- or lowercase.

$ grep -i "MCA HITK" *
# e) Store in a variable the number of lines containing the word MCA in the files mca1, mca2 and mca3.

$ lines=$(grep -c "MCA" mca1 mca2 mca3)
# f) If you did not have the wc command, how would you use grep to count the number of users currently using the system?

$ who | grep -c ".*"
# g) Remove blank lines from a file using grep.

$ grep -v '^$' file.txt
# h) List the ordinary files in your current directory that are not writable by the owner.

$ find . -type f ! -perm -200 -ls
# i) Locate lines ending and beginning with a dot and containing anything between them.

$ grep "^\..*\.$" file.txt
# j) Locate lines that are less than 100 characters in length.

$ grep "^.\{0,99\}$" *
# 1) Write a shell script to find out whether an integer input the keyboard is an odd number or an even number.

#!/bin/bash

echo "Enter an integer:"
read num

if [ $((num % 2)) -eq 0 ]; then
  echo "$num is an even number."
else
  echo "$num is an odd number."
fi
# 2) Write a shell script to find out whether any year input through the keyboard is a leap year or not. If no argument is supplied the current year should be assumed.

#!/bin/bash

if [ -z "$1" ]
then
    year=$(date +"%Y")
else
    year=$1
fi

if (( year % 4 == 0 && year % 100 != 0 || year % 400 == 0 ))
then
    echo "$year is a leap year"
else
    echo "$year is not a leap year"
fi
# 3) Write a shell script to find the maximum of three numbers provided as command line arguments.

#!/bin/bash

if [ $# -ne 3 ]; then
  echo "Error: Please provide exactly three integer arguments."
  exit 1
fi

num1=$1
num2=$2
num3=$3

if [ $num1 -ge $num2 ] && [ $num1 -ge $num3 ]; then
  echo "Maximum number is: $num1"
elif [ $num2 -ge $num1 ] && [ $num2 -ge $num3 ]; then
  echo "Maximum number is: $num2"
else
  echo "Maximum number is: $num3"
fi
# 4) Write a shell script to check whether a given number is prime or not.

#!/bin/bash

echo "Enter a number:"
read num

if [ $num -lt 2 ]; then
  echo "$num is not a prime number."
  exit 0
fi

for (( i=2; i<=num/2; i++ ))
do
  if [ $((num%i)) -eq 0 ]; then
    echo "$num is not a prime number."
    exit 0
  fi
done

echo "$num is a prime number."
# 1) Write a shell script to find the factorial value of any integer entered through the keyboard.

#!/bin/bash

echo "Enter a number:"
read num

fact=1
for (( i=1; i<=num; i++ ))
do
  fact=$((fact * i))
done

echo "The factorial of $num is: $fact"
# 2) Write a shell script to generate all combinations of 1, 2 and 3.

#!/bin/bash

for i in 1 2 3
do
  for j in 1 2 3
  do
    for k in 1 2 3
    do
      echo "$i$j$k"
    done
  done
done
# 3) Write a shell script to print all prime numbers in a given range.

#!/bin/bash

echo "Enter the range:"
read start end

for (( i=start; i<=end; i++ ))
do
  is_prime=true

  if [ $i -lt 2 ]; then
    is_prime=false
  fi

  for (( j=2; j<=i/2; j++ ))
  do
    if [ $((i%j)) -eq 0 ]; then
      is_prime=false
      break
    fi
  done

  if [ "$is_prime" = true ]; then
    echo $i
  fi
done
# 4) Write a shell script to calculate the sum of digits of any number entered through keyboard.

#!/bin/bash

echo "Enter a number:"
read num

sum=0
while [ $num -gt 0 ]
do
  digit=$((num%10))
  sum=$((sum + digit))
  num=$((num/10))
done

echo "The sum of digits is: $sum"
# 5) Rajesh's basic salary (BASIC) is input through the keyboard. His dearness allowance (DA) is 52% of BASIC. House rent allowance (HRA) is 15% of BASIC. Contributory provident fund is 12% of (BASIC + DA). Write a shell script to calculate his gross salary and take home salary using the following formula: Gross salary = BASIC + DA + HRA.

#!/bin/bash

echo "Enter Rajesh's basic salary:"
read BASIC

DA=$((52 * BASIC / 100))
HRA=$((15 * BASIC / 100))
CPF=$((12 * (BASIC + DA) / 100))
GROSS=$((BASIC + DA + HRA))
TAKE_HOME=$((GROSS - CPF))

echo "Rajesh's gross salary is: $GROSS"
echo "Rajesh's take home salary is: $TAKE_HOME"
# 1. Write a shell program that takes a number from user and prints the reverse of the number.

#!/bin/bash

read -p "Enter a number: " num
reverse=$(echo $num | rev)
echo "The reverse of $num is $reverse"
# 2. Write a shell script to determine whether two numbers input through keyboard are prime to each other.

#!/bin/bash

read -p "Enter the first number: " num1
read -p "Enter the second number: " num2
while [ $num2 -ne 0 ]
do
    temp=$num1
    num1=$num2
    num2=$((temp % num2))
done

if [ $num1 -eq 1 ]
then
    echo "$num1 and $num2 are prime to each other"
else
    echo "$num1 and $num2 are not prime to each other"
fi
# 3. Write a shell script to find whether a number is divisible by 11.

#!/bin/bash

read -p "Enter a number: " num
if [ $((num % 11)) -eq 0 ]
then
    echo "$num is divisible by 11"
else
    echo "$num is not divisible by 11"
fi
# 4. Write a shell script that produces a shell calculator to perform the following operations: addition, subtraction, multiplication, division

#!/bin/bash

add() {
    echo $(($1 + $2))
}
subtract() {
    echo $(($1 - $2))
}
multiply() {
    echo $(($1 * $2))
}
divide() {
    echo $(($1 / $2))
}

read -p "Enter the first number: " num1
read -p "Enter the operator (+, -, *, /): " op
read -p "Enter the second number: " num2

case $op in
    "+") result=$(add $num1 $num2);;
    "-") result=$(subtract $num1 $num2);;
    "*") result=$(multiply $num1 $num2);;
    "/") result=$(divide $num1 $num2);;
    *) echo "Invalid operator entered"; exit 1;;
esac

echo "Result: $result"
# 1. Write a shell script to print the pattern for any number of line.

      *
    * * *
  * * * * *
* * * * * * *
#!/bin/bash

read -p "Enter number of lines: " n
for ((i=1; i<=n; i++))
do
    for ((j=1; j<=n-i; j++))
    do
        echo -n "  "
    done
    for ((j=1; j<=2*i-1; j++))
    do
        echo -n "* "
    done
    echo ""
done
# 2. Write a shell script to test whether a given string is pallindrome.

#!/bin/bash

read -p "Enter a string: " str
rev_str=$(echo $str | rev)
if [ "$str" == "$rev_str" ]; then
    echo "The string is a palindrome."
else
    echo "The string is not a palindrome."
fi
# 3. Write a shell script which counts the number of consonants and vowel in a given sentence.

#!/bin/bash

read -p "Enter a sentence: " sentence
sentence=$(echo $sentence | tr '[:upper:]' '[:lower:]')
vowel_count=0
consonant_count=0
for ((i=0; i<${#sentence}; i++))
do
    char=${sentence:$i:1}
    case $char in
        [aeiou])
            vowel_count=$((vowel_count+1));;
        [bcdfghjklmnpqrstvwxyz])
            consonant_count=$((consonant_count+1));;
        *) ;;
    esac
done

echo "The sentence '$sentence' contains $vowel_count vowels and $consonant_count consonants."
# 4. Write a shell script to display the list of users as well as the number of users connected to the system.

#!/bin/bash

user_list=$(who | cut -d' ' -f1 | sort | uniq)
num_users=$(echo "$user_list" | wc -w)
echo "List of users connected to the system:"
echo "$user_list"
echo ""
echo "Number of users connected to the system: $num_users"
# 1. Write a shell script that displays a list of all files in the current directory to which you have read, write and execute permissions.

#!/bin/bash

for file in ./*; do
    if [ -r "$file" ] && [ -w "$file" ] && [ -x "$file" ]; then
        echo "$file"
    fi
done
# 2. Write a shell script that lists files by modification time when called with lm and by access time when called with la. By default, the script should show the listing of all files in the current directory.

#!/bin/bash

case $1 in
    lm) ls -lt;;
    la) ls -lut;;
    *) ls -l;;
esac
# 3. Write a shell script to display the files created or updated within fourteen days from the current date.

#!/bin/bash

find . -type f -atime -14 -mtime -14 | sort -u
# 4. Develop a shell script which displays all files with all attributes those have been created or modified in the month of November.

#!/bin/bash

current_year=$(date +%Y)
find . -type f -newermt "$current_year-11-01" ! -newermt "$current_year-12-01" -ls
# 1. Write a shell script to print last twenty commands issued by the user. The user name is supplied as a command line argument to the script (use bash-history file).

#!/bin/bash

username=$1
history_file="/home/$username/.bash_history"

if [ ! -f $history_file ]; then
    echo "Error: history file for user $username not found"
    exit 2
fi

tail -n 20 $history_file
# 2. Write a shell program, which displays the message "welcome" and prints the date when you login to your system.

To display a welcome message and print the date when you login to your system, you can add the following lines to your .bashrc file:

#!/bin/bash

echo "Welcome"
echo "Today is $(date)"
The .bashrc file is executed every time you open a new terminal or login to your system.

# 3. Accept a string from the terminal and echo a suitable message if it doesn't have at least ten characters.

#!/bin/bash

echo "Enter a string:"
read string

if (( ${#string} < 10 )); then
  echo "The string is too short."
else
  echo "The string is at least ten characters long."
fi
# 4. Write a shell script which receives either the LOGNAME or the UID supplied at the command prompt and finds out at how many terminals this user has logged in.

#!/bin/bash

if [ "$1" == "-u" ]; then
  user=$(getent passwd "$2" | cut -d: -f1)
else
  user=$1
fi

num_terminals=$(who | grep "$user" | wc -l)
echo "$user is logged into $num_terminals terminal(s)."
# 5. Write a shell script, which gets executed the moment a user logs in. It should display the message "GOOD MORNING" or "GOOD AFTERNOON" or "GOOD EVENING" depending upon the time at which the user logs in.

nano ~/.bashrc
hour=$(date +%H)

if [ $hour -lt 12 ]; then
  echo "GOOD MORNING"
elif [ $hour -lt 18 ]; then
  echo "GOOD AFTERNOON"
else
  echo "GOOD EVENING"
fi
# 1. Write a shell script, which reports names and sizes of all files in a directory (directory should be supplied as an argument to the shell script) whose size exceeds 100 bytes. The filenames should be printed in decreasing order of their sizes. The total number of such files should also be reported.

#!/bin/bash

dir=$1
count=0

if [ -d $dir ]; then
    find $dir -type f -size +100c -printf "%s %p\n" | sort -nr | while read -r size filename
    do
        echo "$filename: $size bytes"
        ((count++))
    done
    echo "Total number of files: $count"
else
    echo "Error: directory not found"
fi
# 2. Write a shell script that shows the names of all the non-directory files in the current directory and calculates the sum of the size of them.

#!/bin/bash

sum=0
for file in *
do
    if [ -f "$file" ]; then
        echo "$file"
        size=$(stat -c %s "$file")
        ((sum+=size))
    fi
done
echo "Total size: $sum bytes"
# 3. Write a shell script to list the name of files under the current directory that starts with a vowel.

#!/bin/bash

for file in [aeiou]* *[AEIOU]*
do
    if [ -f "$file" ]; then
        echo "$file"
    fi
done
# 4. Write a shell script which receives two filenames as arguments and checks whether the two file's contents are same or not. If they are same then the second file should be deleted.

#!/bin/bash

if cmp -s "$1" "$2"; then
    rm "$2"
    echo "Files have same contents. Second file deleted."
else
    echo "Files have different contents."
fi
# 1. Write a shell script to check if a given file (filename supplied as command line argument) is a regular file or not and find the total number of words, characters and lines in it.

#!/bin/bash

file=$1

if [ -f "$file" ]; then
    echo "Regular file"
    wc "$file"
else
    echo "Not a regular file"
fi
# 2. Write a shell script which reads a directory name and compares the current directory with it (which has more files and how many more files).

#!/bin/bash

dir=$1

if [ -d "$dir" ]; then
    num_files_dir=$(ls "$dir" | wc -l)
    num_files_cur=$(ls | wc -l)

    if [ $num_files_dir -gt $num_files_cur ]; then
        echo "$dir has more files than the current directory by $(expr $num_files_dir - $num_files_cur) files."
    elif [ $num_files_dir -lt $num_files_cur ]; then
        echo "The current directory has more files than $dir by $(expr $num_files_cur - $num_files_dir) files."
    else
        echo "Both directories have the same number of files."
    fi
else
    echo "Error: directory not found"
fi
# 3. Write a shell script to check whether the given file is a blank file or not. If not found blank then display the contents of the file.

#!/bin/bash

file=$1

if [ -f "$file" ]; then
    if [ -s "$file" ]; then
        echo "Contents of $file:"
        cat "$file"
    else
        echo "$file is a blank file."
    fi
else
    echo "File not found."
fi
# 4. Write a shell script to concatenate two files and count the number of characters, number of words and number of lines in the resultant file.

#!/bin/bash

file1=$1
file2=$2
outfile="output.txt"

cat "$file1" "$file2" > "$outfile"
echo "Number of characters: $(wc -m "$outfile" | cut -d ' ' -f 1)"
echo "Number of words: $(wc -w "$outfile" | cut -d ' ' -f 1)"
echo "Number of lines: $(wc -l "$outfile" | cut -d ' ' -f 1)"
# 5. Write a shell script that accepts two directory names, say mca1 and mca2 as arguments and deletes those files in mca2 which have identical named files in mca1.

#!/bin/bash

dir1=$1
dir2=$2

if [ -d "$dir1" ] && [ -d "$dir2" ]; then
    for file in "$dir2"/*
    do
        if [ -f "$file" ]; then
            filename=$(basename "$file")
            if [ -f "$dir1/$filename" ]; then
                rm "$file"
                echo "$file deleted."
            fi
        fi
    done
else
    echo "Error: directory not found"
fi
# 1. A file called list consists of several words. Write a shell script which will receive a list of filenames, the first of which would be list. The shell script should report all occurrences of each word in list in the rest of the files supplied as arguments.

#!/bin/bash

if [ $# -eq 0 ]
then
	echo "please give filenames"
	exit
fi
p= $1
shift
for var1 in $*
do
	for var2 in `cat $p`
		do
			echo "Occurence of $var2 in $var1 is : `grep -c $var2 $var1`"
		done
done
# 2. Write a shell script which deletes all lines containing the word UNIX in the files supplied as arguments to this shell script.

#!/bin/bash

if[$# -eq 0]
then
	echo "please give  filenames"
	exit
fi
p="UNIX"
for file in $*
do
	sed "/$p/d" $file | tee tmp
	mv tmp $file
done
# 3. Write a shell script which would receive a log name during execution, obtain information about it from password file and display this information on the screen in easily understandable format.

#!/bin/bash

if [ $# -ne 1 ]
then
    echo  "Enter your login name only"
    exit
fi
IFS=:
if [ $? -eq 0 ]
then
    set -- `grep -w "$1"  "/etc/passwd"
    echo "Login name:$1"
    echo "Password:$2"
    echo "UID:$3"
    echo "GUID:$4"
    echo "HOME:$5"
    echo "Login Shell:$7"
else
    echo "User Does not exist"
fi
# 4. Write a shell script, which will receive either the filename or the filename with its full path during execution. This script should print information about the file as given by Is command and display it in an informative manner.

#!/bin/bash

if [ $# -ne 1 ]
then
    echo  "Enter a file name: "
    exit
fi
set -- `ls -1 $1`
echo "File permission: "$1
echo "Links: "$2
echo "Username: "$3
echo "Groupuser name: "$4
echo "Size: "$5
echo "Month: "$6
echo "Date: "$7
echo "Time: "$8
# 1. Write a shell script that takes a list of names and displays all information in the password file, where login names are the members of the list.

#!/bin/bash

if [ $# -eq 0 ]
then
    echo "Please provide a list of login names as arguments."
    exit 1
fi

while [ $# -gt 0 ]
do
    login_name=$1
    shift
    echo "Information for login name $login_name:"
    grep -w "$login_name" /etc/passwd
    echo
done
# 2. Write a shell script that periodically count the number of users logged into the system. Send the number of minutes at which to check as parameter.

#!/bin/bash

if [ $# -ne 1 ]
then
    echo "Please provide a single argument indicating the number of minutes between checks."
    exit 1
fi

interval=$1
while true
do
    num_users=$(who | wc -l)
    timestamp=$(date +"%Y-%m-%d %H:%M:%S")
    echo "[$timestamp] Number of users logged in: $num_users"
    sleep ${interval}m
done
# 3. Write a shell script to count the number of words of different length present in a given text.

#!/bin/bash

if [ $# -ne 1 ]
then
    echo "Please provide a single argument indicating the file containing the text."
    exit 1
fi
file=$1
declare -A counts
while read -ra words; do
  for word in "${words[@]}"; do
    len=${#word}
    ((counts[len]++))
  done
done < "$file"
echo "Word Length    Count"
echo "-----------   -----"
for len in "${!counts[@]}"; do
  printf "%-12s %s\n" "$len" "${counts[$len]}"
done
# 4. Write a shell script to count the frequency of different words used in a file. A shell script receives even number of filenames. Suppose four filenames are supplied then the first file should get copied into the second file, the third file should get copied into the fourth file, and so on. If odd number of filenames is supplied then no copying should take place and an error message should be displayed.

#!/bin/bash

if [ $# -ne 2 ]
then
    echo "Please provide two arguments: the input file and the output file."
    exit 1
fi
input_file=$1
output_file=$2
if [ $(( $# % 2 )) -ne 0 ]
then
    echo "Error: odd number of filenames supplied."
    exit 1
fi
for ((i=1; i<=$#; i+=2))
do
    cp "${!i}" "${!((i+1))}"
done
declare -A word_counts
while read -r line
do
    for word in $line
    do
        ((word_counts[$word]++))
    done
done < "$input_file"
for word in "${!word_counts[@]}"
do
    printf "%s: %d\n" "$word" "${word_counts[$word]}" >> "$output_file"
done
# Devise a menu-driven shell program that accepts values from 1 to 4 and performs action depending upon the number keyed in:
# 1. List of users currently logged in
# 2. Present date
# 3. Present working directory
# 4. Quit

#!/bin/bash

while true
do
    echo "Please select an option:"
    echo "1. List of users currently logged in"
    echo "2. Present date"
    echo "3. Present working directory"
    echo "4. Quit"
    read choice

    case $choice in
        1)
            who;;
        2)
            date;;
        3)
            pwd;;
        4)
            exit;;
        *)
            echo "Invalid choice.";;
    esac
done
# Write a shell script to make a password based menu-driven program, which will give a maximum of three chances to enter the password. If the given password is correct then the program will show the
# 1. Number of users currently logged in.
# 2. Calendar of current month.
# 3. Date in the format: dd/mm/yyyy.
# 4. Quit
# The menu should be placed approximately in the centre of the screen and should be displayed in bold.

#!/bin/bash

# Define the correct password
PASSWORD="mypassword"

# Define the menu options
OPTIONS=("Number of users currently logged in" "Calendar of current month" "Date in the format: dd/mm/yyyy" "Quit")

# Define the maximum number of password attempts
MAX_ATTEMPTS=3

# Initialize the attempt counter
attempts=0

# Loop until the correct password is entered or maximum attempts are reached
while [ "$attempts" -lt "$MAX_ATTEMPTS" ]; do
  # Prompt for password
  read -s -p "Enter password: " input_password

  # Check if the password is correct
  if [ "$input_password" = "$PASSWORD" ]; then
    # Password is correct, show the menu
    clear
    printf "\033[1m" # Bold text
    printf "%*s\n" $(((${#OPTIONS[@]} + 13) / 2)) "Menu"
    printf "%*s\n" $(((${#OPTIONS[@]} + 4) / 2)) "------"
    printf "\033[0m" # Reset text formatting
    select opt in "${OPTIONS[@]}"; do
      case $opt in
        "${OPTIONS[0]}")
          who | wc -l
          ;;
        "${OPTIONS[1]}")
          cal
          ;;
        "${OPTIONS[2]}")
          date +"%d/%m/%Y"
          ;;
        "${OPTIONS[3]}")
          exit 0
          ;;
        *)
          echo "Invalid option selected."
          ;;
      esac
    done
  else
    # Password is incorrect, increment the attempt counter
    attempts=$((attempts + 1))
    echo "Incorrect password. Attempts remaining: $((MAX_ATTEMPTS - attempts))"
  fi
done

# Maximum number of attempts reached, exit with error status
echo "Maximum number of attempts reached. Exiting."
exit 1
