#over the wire bandit level 15 -> level 20

#bandit level 15 -> level 16

#goal: The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

#solotion


1- run: cat /etc/bandit_pass/bandit15 | openssl s_client -quiet -ign_eof -connect localhost:30001

#note: same as nc we pipe down the password but the twist we need to establish a secure connection so we use openssl , s_client means( standard client). -quite what it does it makes the printing of certification on the screen not visible so it is smoother on our screen now for -ign_eof this is a crucial option it means (ignore end of file) why we need it is cat is so fast so by the time the openssl makes the certification and performing a handshake with the server and waiting for a response cat reaches end of file which is after cat done it is job it says iam done system so when openssl sees the cat is ended by deafault it says okay fine close the socket thats why we need to make openssl ignores the eof and continue it is job and prints out the password from the server.


2- the password is: kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V 


---------------------------------------------------

#bandit level 16 -> level 17

#goal: The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

#solotion

1- run: nmap -sV -p 31000-32000 localhost
#note: nmap will scan the ports to check which is open(avaliable), now -sV will give the service/version now some of them will say echo that means they just echo what u type and some will say ssl/unkown that is the target now general knowledge is make it a habit to specify the port and then the destination
#note: nc -v localhost 31970 the -v means verbose now what will this say is if the port is live 

2- run: cat /etc/bandit_pass/bandit16 | openssl s_client -quiet -ign_eof -connect -p 31790 localhost 


Correct!
-----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----

---------------------------------------------------------

#bandit level 17 -> level 18

#goal: There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

#solotion


1- first we ssh -i to the level as we did a couple of levels before 

2- run: diff -u passwords.old passwords.new 
#note: the -u will label the old lines with a - and for the new lines with + 

3- the password is: OQxXZjELndr90zuhOTDYBEomI0SZITXI



---------------------------------------------------------

#bandit level 18 -> level 19

#goal: The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

#solotion

1- run: ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme

#note: first we need to understand how ssh works it creates a connection to the machine we want to gain access to, now after u log in automatically the shell file gets executed in this case bash.rc file which in this challenge has an exit command in it so by default when u login the bash.rc gets called cause it needs to setup the environment for you. we bypass that with the command we want so we tell ssh just get in there and read this file without calling the bash.rc file.
#note: there is another solution which is  ssh -t bandit18@bandit.labs.overthewire.org -p 2220 /bin/sh
now what this command do is it calls a pseudo terminal which is /bin/sh (the bourne shell) so bash.rc never gets called so we bypass the bash.rc file and the -t it forces the ssh to call a pseudo terminal to interact  

-3 the password is: KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI



---------------------------------------------------------

#bandit level 19 -> level 20

#goal: To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

#solotion

1- run: ./bandit20-do cat /etc/pass_bandit/bandit20

#note: now what happens and what setuid does actually: it gives a temporary access to the user who owns the files, and how u know if u type ls -la u will see a file with an r-w-s that means it has an s bit.

#note: so when u run ./bandit20-do cat /etc/pass_bandit/bandit20 the bandit-do is owned by bandit20 and we are bandit19 but when cat /etc/pass_bandit/bandit20 it inherited the euid(effective user id) of bandit20 so thats why it works, so we temporary gained bandit20 user privilege.

#note: setuid is a powerful tool and we use it to change passwords for example and only root can give and create s files and give setuid privilege

#note: u need execute permission to gain access to the file 

#note: sudo is built it on setuid, we need to understand the process but we dont use setuid and infact we disable it in containers to not let anyone abuse misconfigured binaries and we need to understand to audit misconfigured binaries 

2- the password is: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA



