# Bash Scripting
Bash scripting is when you put commands in a file. The file is read from top to bottom, and commands are executed one after another. Typically scripts will have a line on the top of the file that defines the command line interpreter (CLI) "She-Bang" /bin/bash

```bash
#!/bin/bash
```
This declares that the script that we are writing is written in bash syntax using bash commands. This could also reflect a different programming language like python or perl or something else.

There are 2 ways to call a script. You can either use the command line interpreter directly like this:

```bash
bash myscript.sh
```
Another way to call a script is to either give an absolute path to the script, or have the path to the script defined in the PATH variable. The directory ~/bin is in the student's PATH, so if a script is put in there it can be run by that user by name from anywhere.

```bash
[student@servera ~ ] mkdir ~/bin
[student@servera ~ ] vim ~/bin/scriptname
[student@servera ~ ] chmod +x ~/bin/scriptname
[student@servera ~ ] scriptname
output
```
As you can see in this example, execute privileges were granted to all users and this allowed the student user to run the script. It is not always necessary to supply execute privileges to all users and in practice it is better to allow access to only those who need that access.

## Loop Constructs
One form of loop construct is the "for loop". Basic syntax for a for loop is:

```bash
for VARIABLE in LIST; do
	actions;
done
```
The LIST can be given in a couple of different ways.

```bash
for USER in admin1 admin2 admin3; do
	usermod -aG admins $USER;
done


for  COUNTDOWN in {10..1}; do
	echo $COUNTDOWN ;
done


for DIRECTORY in Documents Downloads Desktop; do
	mkdir ~/${DIRECTORY};
done
```
### While Loop

The While loop will loop over and over as long as some condition remains true. There are many uses for this and it is used in many ways.

```bash
while true [[ <test_condition> ]]; do
	commands
done
```
As long as the test condition is true, it will continue to perform that same action over and over.

```bash
while true [[ -d /tmp/user ]]; do
	date >> logfile
	sleep 5
done
```
### Until Loop

An Until loop will loop through tasks as long as a condition is not true. As soon as the condition is no longer true, the script will complete.

```bash
until [[ <test_condition> ]]; do
	commands
done
```
```bash
until [[ -f /home/student/removeme ]]; do
	echo "What\'s causing this message? removeme"
	sleep 5
done
```
## Exit codes
Every command will produce an exit code whenever it finishes. This code let's the administrator know if it was successful or not. A return code of 0 indicates success and any positive number means failure. You could use this code to make a loop continue, or for a conditional statement. Here is an example where we search for user coby in the /etc/passwd file. If he is there, it will return 0 and if not a 1 or higher:

```bash
grep coby /etc/passwd
echo $?
1
```

If we were to repeat that same command for student, it should return a 0 since that user does exist.

```bash
grep student /etc/passwd
student:x:1000:1000:Student User:/home/student:/bin/bash
echo $?
0
```

Exit codes are also used with tests. You can test many different things. This is typically done with square brackets like these examples:

`[[ 1 -gt 0 ]]` → -gt is a numeric comparison operator meaning greater than

`[[ 1 -lt 2 ]]` → -lt is a numeric comparison operator meaning less than

`[[ 1 -gt 0 ]]` → -gt is a numeric comparison operator meaning greater than

`[[ 1 -ge 0 ]]` → -ge is a numeric comparison operator meaning greater than or equal to

`[[ 1 -le 0 ]]` → -le is a numeric comparison operator meaning less than or equal to

`[[ this != that ]]` → != is a string comparison operator meaning not equal to

`[[ this == this ]]` → == means equal to when comparing strings

```bash
#!/bin/bash
# Demonstrate case statement
echo "Who are you?"
read VARIABLE
case $VARIABLE  in
        jedi)
                echo "So you are a jedi. Keep helping others."
                ;;
        coby)
                echo "So you are the instructor... carry on."
                ;;
        student)
                echo "So you are a student? Keep up the good work"
                ;;
        *)
                echo "Choices are jedi coby or student. try one of those."
esac
```
