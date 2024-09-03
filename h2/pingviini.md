# Command Line Basics

## Equipment

- **Screen: AOC G2490VXA, 24" QHD(1440p), 144Hz**
- **Raspberry Pi 4 model B 4 Gt**
- Operating Sytem: Raspbian OS (based on Debian)
- CPU: Broadcom BCM2711 SoC with a 1.8 GHz 64-bit quad-core ARM Cortex-A72 processor, with 1 MB shared L2 cache.
- Memory: 4 Gt
- Disk space: 32Gt
- Näytönohjain: Broadcom VideoCore VI @ 500 MHz

## x)Linux Commands

Linux uses commands that dates way back, even before internet was publicly available. Most of these if not all commands have stayed unchanged, 
and many generations have used the same commands to, navigate around directories, creating new content, deleting, updating and more.

In linux, some of the commands can be executed by the computer without root user permission. 
Root user being usually the administrator. For other commands, permission is needed, and you can confirm this by placing ’’sudo’’ before the command i.e. 

    $ sudo apt-get update
    
This command updates list of available packages.

    $ sudo apt-get upgrade
    
This command is used after the update command, to upgrade any and all available packages.

If command is about SSH or other type of either vulnerable or dangerous command, the system can ask for a password to execute the command

The most common commands include pwd, ls, cd, touch and mkdir.
With these command you can see the path to your current directory, list all the files and folders in a directory, 
move to different directory and create files with touch or directories(folders) respectively.

    $ pwd
    $ ls
    $ cd directoryA # or cd .. for previous directory
    $ touch NEWFOLDER
    $ mkdir NEWFILE

To remove you can use commands 

    $ rm NEWFILE
    $ rmdir NEWFOLDER 
    #if the directory has any content, you will need to run command $ rm -r NEWFOLDER

To open a remote access the commands is
    
    $ ssh xxx.xxx.xxx.x #change the X’s to your destination computers IP address

## History

You can check your command history, by typing simply history, and it will show you list of recently used commands

    $ mkdir NEWFILE

## Manual

An important command, for you to find information about how the different commands work, you can use the man command.

    $ man ls, 
    # this command shows you the manual page of the ls command. 
    # Changing the command after man, shows you the manual page for that requested command

## a) Installing Micro-editor

You can install the micro-editor simply by typing the command

    $ sudo apt-get install -y micro

![Näyttökuva 2024-9-3 kello 12 27 18](https://github.com/user-attachments/assets/9427a6e0-1a08-4dc6-b277-b3743c339637)

When you're downloading via command line, the -y option in the sudo apt-get install command is used to automatically answer "yes" to any prompts that might appear during the installation process.

For example. Install the micro package, and automatically answer 'yes' to any prompts that come up during the installation process.

## b) Installing multiple programs

To install multiple programs at once you can use the command for download, and then write the programs after the command with one space in between

    $ sudo apt update && sudo apt install htop ncdu cowsay tldr bat

![multiple](https://github.com/user-attachments/assets/3c067151-6cf4-41e5-8320-39f6b40984a6)

It looks like "htop" & "ncdu" came with the OS, so the terminal shows me that, it has both of them already in the system and they are the newest version.

### For this assignment I downloaded the following programs

"htop" which shows interactively running processes and usage of the resources in clear TUI.

![htop](https://github.com/user-attachments/assets/ce95dd51-853f-4469-abcc-6328ffdb51b8)


"ncdu" that shows systems size in memory usage, also helps you find large files and folders.

![ncdu](https://github.com/user-attachments/assets/f9cf26af-a34e-499f-8ee1-e04bdb1d6f80)


"cowsay", is funny little program that creates figure of cow and inserts your text to it speechbuble.

![cowsay](https://github.com/user-attachments/assets/9ca70c81-3b52-4ad5-873b-8edf345b0d39)

## c) Filesystem Hierarchy Standard

'/' on koko tietojärjestelmän juurikansio. Kaikki tiedostot ja hakemistot ovat tämän alaisuudessa

    $ ls /

'/home/'
