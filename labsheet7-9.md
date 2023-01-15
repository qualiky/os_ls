# Labsheet 7-9: Shell Scripting in UNIX

___

## Objectives

1. To understand shell and it's rc files, history files, and environmental variables associated with the user.
2. To understand conditionals, loops, variables, and programs in shell script.

## Theory  
  
The shell is an interface that can be used to communicate with the user and kernel space of any UNIX system. It provides a text-based environment to create and run programs based on user input. Each operating system has it's own shell: Windows uses Command Prompt and Windows PowerShell, macOS uses bash/zsh while Linux systems usually come bundled with some form of bash shell.

## Activity

1. Printing environmental variables

    ```
    sandeepgautam@Sandeeps-MacBook-Pro bin % printenv

    __CFBundleIdentifier=com.apple.Terminal
    TMPDIR=/var/folders/p6/14j0qgkn7zjgvw9dphchh_yw0000gn/T/
    XPC_FLAGS=0x0
    TERM=xterm-256color
    SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.1MG7To3L0Z/Listeners
    XPC_SERVICE_NAME=0
    TERM_PROGRAM=Apple_Terminal
    TERM_PROGRAM_VERSION=447
    TERM_SESSION_ID=2180DD0E-B551-4B7D-A29D-74D040A63D8E
    SHELL=/bin/zsh
    HOME=/Users/sandeepgautam
    LOGNAME=sandeepgautam
    USER=sandeepgautam
    PATH=/opt/homebrew/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/sandeepgtm/Library/Android/sdk/platform-tools
    SHLVL=1
    PWD=/usr/bin
    OLDPWD=/Users/sandeepgautam/Apex/Sem_5/OS/lab/lab8
    JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-18.0.2.1.jdk/Contents/Home
    HOMEBREW_PREFIX=/opt/homebrew
    HOMEBREW_CELLAR=/opt/homebrew/Cellar
    HOMEBREW_REPOSITORY=/opt/homebrew
    MANPATH=/opt/homebrew/share/man::
    INFOPATH=/opt/homebrew/share/info:
    ANDROID_HOME=/Users/sandeepgautam/Library/Android/sdk
    LC_CTYPE=UTF-8
    _=/usr/bin/printenv
    ```

2. Shell script program to display list of users currently logged in.

    ```
    echo $w
    
     7:46  up 1 day, 10:36, 2 users, load averages: 1.57 1.49 1.43
    USER     TTY      FROM              LOGIN@  IDLE WHAT
    sandeepgautam console  -                Tue21   34:36 -
    sandeepgautam s000     -                 6:55       - w
    ```

3. Shell script program to display the long list of directories.

    ```
    cd /usr/bin && ls
    ```

4. Shell Script program to check whether the given number is even or odd.

    ```
    echo "Enter the number for odd/even test: "
    read number
 
    reminder=$(( $number % 2 ))
 
    if [ $reminder -eq 0 ]
    then
        echo "Entered number is even"
    else
        echo "Entered number is odd"
    fi
    ```

5. Shell Script program to take filename as input and delete the file.

    ```
    echo "Enter the file name to be deleted: "
    read filename

    if [ -f $file ]
    then 
        rm -f $filename
    else
        echo "File does not exist"
    fi
    ```

6. Shell script to add numbers from 1 to N.

    ```
    echo "Enter a number"
    read num
    i=1
    sum=0
    while [ $i -le $num ]
    do
        echo $i
        sum=$(($sum+$i))
        i=$(($i+1))
    done

    echo "Sum: $sum"
    ```

7. Shell script to find factorial of a number

    ```
    echo "Enter a number"
    read num

    fact=1

    while [ $num -gt 1 ]
    do
    fact=$((fact * num))  
    num=$((num - 1))      
    done

    echo $fact
    ```

8. Shell script for Arithmetic operation

    ```
    echo "Arithmetic operations in shell"
    echo "enter (a)="
    read a
    echo "enter (b)="
    read b
    echo "add=`expr $a + $b`"
    echo "mult=`expr $a \* $b`"
    echo "div=`expr $a / $b`"
    echo "mod=`expr $a % $b`"
    echo "sub=`expr $a - $b`"
    ```

9. Shell script for floating math

    ```
    echo "Arithemetic operations on
    floting point for decimal numbers"
    echo "enter two variables"
    echo "enter a"
    read a
    echo "enter b"
    read b
    sum=` echo $a + $b | bc `
    sub=` echo $a - $b | bc `
    div=` echo $a / $b | bc `
    mul=` echo $a \* $b | bc `
    mod=` echo $a % $b | bc `
    ```

10. Shell script for simple interest

    ```
    echo "simple interest"
    echo "enter p"
    read p
    echo "enter r"
    read r
    echo "enter t"
    read t
    echo "simple interest is"
    s=` expr $p \* $r \* $t `
    si=`echo $s / 100 | bc`
    echo "$si"
    ```

11. Shell script for circle geometry
    ```
    echo "Area of circle"
    echo "Enter the radius of the circle"
    read r
    a1= `echo $r \* $r \* 3.14 | bc`
    echo "$a1"
    echo "Area of rectangle"
    echo "Enter the length and the width of the rectangle"
    echo "enter the length"
    read l
    echo "enter width of rectangle"
    read b
    a2= `echo $l \* $b | bc `
    echo $a2
    echo "Area of square"
    echo "enter side of square a"
    read athen
    a3= `echo $a \* $a | bc `
    echo $a3
    ```

12. Shell script for positivity check

    ```
    echo "script to find given no is +ve ,-ve or 0"
    echo "enter value"
    read a
    if [ $a -gt 0 ]
    then
    echo "num is positive"
    else
    if [ $a -lt 0 ]
    then
    echo "num is negative"
    else
    echo "num is zero"
    fi
    ```


## Observation and Conclusion

Hence, we learned the basics of shell scripting in zsh/bash in UNIX systems.
