#over the wire bandit level 05 -> level 10

#bandit level 5 -> level 6

#goal: The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable 

#solotion

1- run: ls

2- run: cd inhere/

3- run: find ! -executable -size 1033c 2>/dev/null

#note: at first i looked at each file in each directory and checked the size and x by running ls -la in each directory until i found the correct one. i guess it is good practices lol.

#note: the ! means not, c in size =bytes, 2>/dev/null -> this will send all erros away so u get clean path to the password 

4- the password is: pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

--------------------------------------------

#bandit level 6 -> level 7

#goal: The password for the next level is stored somewhere on the server and has all of the following properties:

owned by user bandit7
owned by group bandit6
33 bytes in size

#solotion

1- run: find / -user bandit7 -group bandit6 -size 33c

#note: we start the find command with / what this means is to search from the root going all the way we need it cause we dont have any info on where the file is.

2- run: cat /var/lib/dpkg/info/bandit7.password

3- the password is: Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3

--------------------------------------------

#bandit level 7 -> level 8

#goal: The password for the next level is stored in the file data.txt next to the word millionth

#solotion

1- run: grep "millionth" data.txt

#note: at first i vim into data.txt and got into command mode ran the command /millionth and i got the result btw u cant copy paste from vim into note pad i tried yanking put it does not work what worked though is i ran the command:     :set mouse=a 
but the thing is this was a bad solution cause when u vim into file your using the memory and if a file is huge it could crash so the better solution is using the command grep  

2- the password is: VR1ljMayciFxbnUokuQmJFw6QC9VKtub 

--------------------------------------------

#bandit level 8 -> level 9

#goal: The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

#solotion

1- run: sort data.txt | unique -u

#note: the | it is the pipe command it means pass the output of sort data.txt into unique -u . now why do we need to sort first before executing unique -u is because unique operates with 2 lines maximum so when running unique -u without sorting it will compare the first line with the above and see they are different essentially it will print all the file but when u execute the sort command first unique then comes and see the first line and compare it to the bottom and see ahh identical and discard them cause they are not unique 

2- the password is: EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl

--------------------------------------------

#bandit level 9 -> level 10

#goal: The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

#solotion

1- strings data.txt | grep "=="
#note: the strings command basically remove the garbage data and prints the readable characters and then we pass it using | to grep "==" we use double == cause it is mentioned in the puzzle 

2- the password is: B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
--------------------------------------------






