[Return](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/README.md)

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
