[Return](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/README.md) | [The Tolkien Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheTolkienRing.md) | [The Elfen Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheElfenRing.md) | [The Web Ring](#suricata) | [The Cloud Ring](#suricata) | [The Burning Ring of Fire](#suricata) | [Kringlecon](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/Kringlecon.md)

<h1 id="top">The Elfen Ring</h1>

#### Table of Contents

- [Clone with a Difference](#clone)
- [Prison Escape](#prison)
- [Jolly CI/CD](#jolly)

<h3 id="clone">Clone with a Difference</h3>

We just need you to clone one repo: `git clone git@haugfactory.com:asnowball/aws_scripts.git` this should be easy, right? This is:it does not seem to be working for me. This is a public repository through. I'm so confused! Please clone the repo and cat the READ.md file for me. To do this properly I will need to use the right syntax in order to clone the repository. `git clone <repository-url> <directory>` The command used is `git clone http://haugfactory.com/asnowball/aws`

![image1](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image1.jpg "Git Command: git clone <repository-url> <directory>")

![image2](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image2.jpg "Command: cd aws_scripts | ls | cat README.md")

Once the repo was cloned, I was able to go into the directory and find the README.md file. Here, I am able to cat or nano into the file and read its contents. Using the cat command, I was able to see what the last word within the contents which was Maintainer. `Command: cat README.md`.

<h3 id="prison">Prison Escape</h3>

Greetings Noble Player, 

Your yourself in a jail with a recently captured Dwarven Elf. He desperately asks your help in escaping for he is on a quest to aid a friend in a search for treasure inside a crypto-mine. If you can help him break free of his containment, he claims you would receive "MUCH GLORY!" 

The first step was to create a disk which I used the command `fdisk -l` but I also noticed that I had to be rooted in order to use the command. Next was to mount the drive using the command mount `/dev/vda /mnt`. Then moved into the `/mnt/` directory and be able to see what was inside.

![image3](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image3.jpg "Command: fdisk -l | mount /dev/vda /mnt | cd /mnt/ | ls")

The next step was to find out what was important and what was not relevant in order to move out of the container. I was able to find the jailer directory by moving directories for example `cd /mnt/home/` from here I was able to see the jailer directory. Next would be to move into the directory and see what hidden directories or files where available. The command used to do this was `cd /mnt/home/jailer/` then `ls -als` to see all hidden files in a list format.

![image4](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image4.jpg "Command: cd /mnt/home/jailer/ | ls -als | cat jail.key.priv")

Once I was able to see what files are avaliable I can catenate into jail.key.priv This file would be the private key for SSH, while the jail.key.pub would be the public key for SSH. The Hexadecimal value that was inside `jail.key.priv` was Hex value: `082bb339ec19de4935867`.
No alt text provided for this image
HEX VALUE: `082bb339ec19de4935867`

![image5](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image5.jpg "HEX VALUE: 082bb339ec19de4935867")

<h3 id="jolly">Jolly CI/CD</h3>

Greetings Noble Player, 

Many thanks for answering our desperate cry for help! You may have heard that some evil Sporcs have opened a webstore selling counterfeit banners and flags of the many noble houses found in the land of the North! They have leveraged some dastardly technology to power their storefront, and this technology is known as PHP! 

***gasp*** 

This storefront utilizes a truly despicable number of resources to keep the website up. And there is only a certain type of Christmas Magic capable of powering such a thing… an Elven Ring! Along with PHP there is something new we've not yet seen in our land. A technology called Continuous Integration and Continuous Deployment! Be wary! Many fair elves have suffered greatly but in doing so, they've managed to secure you a persistent connection on an internal network. BTW take excellent notes! Should you lose your connection or be discovered and evicted the elves can work to re-establish persistence. In fact, the sound off fans and the sag in lighting tells me all the systems are booting up again right now. Please, for the sake of our Holiday help us recover the Ring and save Christmas!

Using the clue that was given, I was able to clone the repository of the `gitlab.flag.net.internal` using the command `git clone git@gitlab.flag.net.internal/rings-of-powder/wordpress.flag.net.internal.git`

![image6](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image6.jpg "Command: git clone http://gitlab.flag.net.internal/rings-of-powder/wordpress.flag.net.internal.git")

![image7](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image7.jpg "Command: ls")

In order for me to mover further I would have to reference how to [start using git](https://docs.gitlab.com/ee/gitlab-basics/start-using-git.html) and [using git with ssh](https://docs.gitlab.com/ee/user/ssh.html). Once, I am in the cloned repository for `wordpress.flag.net.internal` I would be able to use the command git log in order to get a log of what commits where pushed to the Git-Lab repository.

![image8](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image8.jpg "Command: git log | shows the log of commits")

The next step is to check out a commit that looks interesting. The first commit that looks interesting is the whoops commit which is `[commit e19f653bde9ea3de6af21a587e41e7a909db1ea5]`. Using the command git show Hex value I would be able to see the contents of the commit. For the whoops commit it had ssh private and public keys attached but at the same time this was deleted out of the repo. So, the next step would be to check out the next commit which is `updated wp-config [commit abdea0ebb21b156c01f7533cea3b895c26198c98]`. Using the command `git show abdea0ebb21b156c01f7533cea3b895c26198c98`.

![image9](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image9.jpg "Command: git show abdea0ebb21b156c01f7533cea3b895c26198c98")

Now we have a commit with the right private and public keys that can be used to private to the other machine. The commands used to create a directory and files would be moving to the root directory. Then using command `mkdir .ssh` then moving into the directory and creating files named `id_rsa` and `id_rsa.pub` with command `touch id_rsa | touch id_rsa.pub`. Next, we will use the commit to move the contents from it to the `id_rsa` and `id_rsa.pub`. The commands used are `git show abdea0ebb21b156c01f7533cea3b895c26198c98:.ssh/.deploy > ~/.ssh/id_rsa` for the private key and then use command `git show abdea0ebb21b156c01f7533cea3b895c26198c98:.ssh/.deploy.pub > ~/.ssh/id_rsa.pub` for the public key. Which we will need both in order to connect to the other container. Next command is the `git push`. Command used `git push git@gitlab.flag.net.internal:/rings-of-powder/wordpress.flag.net.internal.git`. This will update the repo with anything that has changed. 

![image10](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image10.jpg "Command: git push git@gitlab.flag.net.internal:/rings-of-powder/wordpress.flag.net.internal.git")

Once that is updated, we will look for anything important in the logs like directory's or ssh login paths. This can be used in order to do a ssh season with another container. The directory found was `/etc/gitlab-runner/hhc22-wordpress-deploy` and the ssh connection path is `root@wordpress.flag.net.internal:/var/www/html`.

![image11](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image11.jpg "ssh -i /etc/gitlab-runner/hhc22-wordpess-deploy | root@wordpress.flag.net.internal:/var/www/html")

Here we will need to go into our repo and find a `.yml` file in order to write a script to get a listener. The best file to modify would be `.gitlab-ci.yml`. We will need to add a netcat listener to the script while add our own IP address in order to the listener to connect to which is `172.18.0.99`.

![image12](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image12.png "The local machines IP address - inet addr: 172.18.0.99")

We will need to use nano to edit the `.gitlab-ci.yml` file. Here we can add the netcat listener before the rsync script. If we do not add it before the listerner will not capture a connection. We need an advent to happen in order to get a connection to the container. Here is a snippet of the `.gitlab-ci.yml file`:

![image13](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image13.jpg ".gitlab-ci.yml script")

After that has been modified and saved in nano, the next step is to commit the file back to the repo. We will use the command `git commit -am "4GLORY"`. But we run into an issue, we will need to add the username and email address to the git config global. If we remember the last git show we did we can see the author and of the commit which we can use for the git config global command. The command we will use is `git config --global user.email "sporx@kringlecon.com" | git config --global user.name "knee-oh"`. Then we will `git commit -am "4GLORY"` one more time.

![image14](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image14.jpg "Command: git commit =am '4GLORY'")

`user.name: knee-oh | user.email: sporx@kringlecon.co`

![image15](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image15.png "Command: git config --global user.email 'sporx@kringlecon.com | git config --global user.name 'knee-oh'")

![image16](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image16.jpg "Command: git commit -am '4GLORY'")

The next step after it has been committed is to run the command `git push && nc -lvp 5555`

![image17](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image17.jpg "Command: git push && nc -lvp 5555")

Now that I have a listener established on the other container, I will be able to pivot from here to the gitlab-runner container.

![image18](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image18.jpg)

The next command I will need to run in order to pivot will be command `ssh -i /etc/gitlab-runner/hhc22-wordpress.deploy root@wordpress.flag.net.internal`. Once I have connection with this machine, I should have root over the wordpress server.

![image19](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image19.jpg)

Once connected I am in the root directory and will need to move into the next directory using command `cd /`. Here we can see that there is a flag.txt file that looks interesting. The command used to see what is inside that file is cat flag.txt.

![image20](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image20.jpg)
![image21](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheElfenRingImages/image21.jpg "Flag oI40zIuCcN8c3MhKgQjOMN8lfYtVqcKT")

Now we have captured the flag within WordPress Server.

[Top](#top)
