
###Scripts
```
#!/bin/bash

/usr/bin/perl
/bin/bash
/bin/csh
/usr/bin/python
/bin/sh


// bash scripts
# //comment. However, \# or #! is used as starting a script
\ // used at the end of a line to indicate continuation on the next line
; // used to interpret what follows as a new command
$ // indicates that follows is a variable

//example 1
#!/bin/bash
echo "Hello, please enter your name: "
read sname
echo "welcome " $sname


// split long commands over multiple line
scp abc@server1.linux.com:\
/var/ftp/pub/userdata/read \
abc@server2.linux.com:\
/opt/oradal/master/abc/
```

Putting multiple commands on a single line
```
$make ;make install; make clean // three commands will all execute even if the ones preceding them fail
$ make && make install && make clean // the subsequent commands will abort if one fails. && (and operator)
$cat file1 || cat file2 || cat file3 // or operator

```

Functions
```
function_name() {
    command...
}
```

Build-in shell commands
```
complied applications: rm, ls, df, vi, gzip
bash commands: cd, pwd, echo, read, logout, printf, let, ulimit

```

Command substitution
```
By enclosing the inner command with backticks(')
By enclosing the inner command in $()
```

Script parameters
```
$0 // script name
$1 // First parameter
$2, $3, etc // second, third parameter, etc
$* // all parameters
$# / number of arguments

//example
#!/bin/bash
echo "Hello, please enter your name: "
read sname

echo "welcome " $sname

echo "the script name is : " $0
echo "the first parameter is: " $1
echo "second parameter is : " $2
echo "third parameter is : " $3

//output redirection
file > /tmp/file.txt 

//input redirection
#!/bin/bash
echo "Line Count"
wd -l < /temp/test.txt

```

pass parameter to bash file from command line
```
=> p1=Joe p2=Swift bash test.sh
or => p2=Swift bash test.sh
or p2=Swift p1=joebash test.sh

//test.sh
#!/bin/bash
echo "start running bash file"
echo $p1
echo $p2
```

IF statement
```
// numerical or string comparisons
// return value of a command (0 for success)
// File existence or permissions

// file conditionals
-e file // check file existence
-d file // check if the file is a directory
-f file // check if file is a regular file
-s file // check if file is of non-zero size
-g file // check if file has sgrid set
-u file // check if the file has suid set
-r file // check if the file is readable
-w file // check if the file is writable
-x file // check if the file is executable

// string conditionals
string1 == string2 

// numerical conditionals
-eq //equal to
-ne // not equal to
-gt // greater than
-lt // less than
-ge // greater than or equal to 
-le // less than or equal to




if [condition]
then 
    statements
else 
    statements
fi

//Example: check file existence
#!/bin/bash
file=$1
if [-f $file ]
then
    echo -e "The $file exists"
else 
    echo -e "The $file does not exist"
fi


// Nested if statement
#!/bin/bash
echo "Enter the first number: "
read n1
echo "Enter the second number: "
read n2
echo "Choose calculation: 1 for addition, 2 for subtraction, 3 for multiplication"
read oper

if [ $oper -eq 1 ]
then 
    echo "Addition: " $(($n1 + $n2))
else 
    if [ $oper -eq 2 ]
    then
        echo "Subtraction: " $(($n1 - $n2))
    else
        if [ $oper -eq 3 ]
        then
            echo "Multiplication: " $(($n1 * $n2))
        else 
            echo "Invalid input"
        fi
     fi
fi


//Example: Elif
#!/bin/bash
echo "enter a number: "
read n

if [ $n -eq 100 ]
then 
    echo "Input is 100"
elif [ $n -gt 100 ]
then
    echo "Input is greater than 100"
else 
    echo "Input is less than 100"
fi
```


Arithmetic Expressions
```
expr 8+ 8
echo $(expr 8+8)

echo $((x+1))
let x=(1+2); echo $x
```

String Manipulation
```
[ string1 > string2 ] // compares the sorting order of string1 and string2
[ string1 = string2 ] // compares the characters in string1 with the characters in string2
myLen1 = ${#string1} // save tyhe length of string1 in the variable myLen1
${string1:0:5} // substring of string1; char 0 to 5
${string1#*.} // to extract all characters in a string after a dot
```


Boolean Expression
```
&& // AND
|| // OR
! // NOT
```

Case Statement
```
case expression in
    patter1) execute commands;;
    patter2) execute commands;;
    patter3) execute commands;;
    * )      execute some default commands or donothing;;
esac


//Example
#!/bin/bash
echo "Enter a letter"
read letter

case "$letter" in
    "a"|"A") echo "you have typed a vowel!" ;;
    "e"|"E") echo "you have typed a vowel!" ;;
    "i"|"I") echo "you have typed a vowel!" ;;
    "o"|"O") echo "you have typed a vowel!" ;;
    "u"|"U") echo "you have typed a vowel!" ;;
    * )      echo "you have types a consonant !";;
esac
exit 0
```

Looping Constructs
```
for
while
until

//For Loop
for variable-name in list
do
    commands
done


//While Loop
while [ condition-is-true]
do
    commands
done

//Until Loop
until [ condition-is-false]
do
    commands
done


//Example
#!/bin/bash

echo "Beginning for loop"
sum=0
for i in 1 2 3 4
do
    sum=$(($sum+$i))
done
echo "The sum of $i numbers if: $sum"
echo "Ending for loop"


echo "Beginning while loop"
no=5
fact=1
i=1
while [ $i -le $no ]
do
    fact=$(($fact * $i))
    i=$(($i + 1))
done
echo "the factorial of $no is $fact"
echo "Ending while loop"


echo "Beginning until loop"
echo "Number"
mn=1
mx=10
until [ $mn -gt $mx ]
do
    echo "$mn"
    mn=$(($mn + 2))
done
echo "the factorial of $no is $fact"
echo "Ending until loop"

```

Debugging
```
bash -x ./script_file 
// debug mode
//1. it traces and prefixes each command with the + character
//2. it displays each command before executingit
//3. Partially debug
set -x # turn on debugging
...
set +x # turn off debugging

//example
bash sample.sh > error.txt
```


```
TEMP=$(mktemp /tmp/tempfile.XXXXXXX) // to create a temporary file
TEMPDIR=$(mktemp -d /tmp/tempdir.XXXX) // to create a temporary directory
$fine / > /dev/null //Discarding output with /dev/null
$RANDOM // generate a random number
```
