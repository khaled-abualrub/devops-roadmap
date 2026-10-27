this is my nginx exercise 

what i built:
1- rented an ec2 instance from aws console
2-configured inbound rules to manage traffic 
3-ssh into ec2 instance
4-followed a detailed serious of commands to safely install and deploy nginx all put in my screenshots folder
5-linked the ec2 instance with my domain 

what i learnt:
1-how to rent and configure ec2 instance
2-how to safely install and run nginx 
3-how to configure a domain 
4-how to link ec2 instance to my domain

challenges i faced:
1-i needed to configure my TLS/SSL to flexible to allow https traffic cause it is was sit to full
2-i needed to configure an inbound rule inside ec2 instance cause cloudflare does not allow http on port 80 so we needed an https rules on port 443
