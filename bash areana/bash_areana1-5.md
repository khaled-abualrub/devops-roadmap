#bash areana

level 1
Mission: Create a directory named Arena and then inside it, create three files: warrior.txt, mage.txt, and archer.txt. List the contents of the Arena directory.

1-run: mkdir Areana

2-run: cd /Areana

3-run: touch archer.txt  mage.txt  warrior.txt

4-run: ls


-----------------------------------------------


level 2
Mission: Create a script that outputs the numbers 1 to 10, one number per line.

1-run this script: 
#!/bin/bash



for (( i=1; i<11; i++ )); do

   echo "the number is: $i"
done


---------------------------------------------------


level 3
Mission: Write a script that checks if a file named hero.txt exists in the Arena directory. If it does, print Hero found!; otherwise, print Hero missing!.

1-run this script:
#!/bin/bash


if [[ -e "hero.txt" ]]; then

   echo "hero found!"
else 
   echo "hero missing!"
fi


-----------------------------------------------------


level 4
Mission: Create a script that copies all .txt files from the Arena directory to a new directory called Backup.

1- run this script: 
#!/bin/bash


for file in *.txt; do

   cp "$file" "backup"
   
   echo "the file that are being backedup are: $file"
done


--------------------------------------------------------


level 5
Mission: Combine what you've learned! Write a script that:

1. Creates a directory names 'Battlefield'
2. Inside Battlefield, create files named knight.txt, sorcerer.txt, and rogue.txt.
3. Check if knight.txt exists; if it does, move it to a new directory called Archive.
4. List the contents of both Battlefield and Archive.



1-run:
#!/bin/bash


mkdir Battlefield

touch knight.txt sorcerer.txt rogue.txt

mv knight.txt sorcerer.txt rogue.txt Battlefield

if [[ -e Battlefield/knight.txt ]]; then

   mkdir Archive
   mv Battlefield/knight.txt Archive
   echo "knight.txt exists and it is being moved to Archive directory"
else

   echo "knight.txt does not exist"
fi
ls Battlefield
ls Archive

