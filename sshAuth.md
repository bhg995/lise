# DigitalOcean SSH Authentication Method

### Generate SSH-key pair

    ssh-keygen -b 4096 -t rsa

Command `ssh-keygen` generates the key pair, we add `-b 4096` to specify number of bits for the key size. 4096 bits has higher security level compared to the default 2048 bit long key. **B**its. [1](https://www.ibm.com/support/pages/steps-creating-ssh-keys), [2](https://stackoverflow.com/questions/51834225/why-use-t-rsa-b-4096-with-ssh-keygen)

`-t rsa` specifies which type of algorithm is used. **T**ype. [2](https://stackoverflow.com/questions/51834225/why-use-t-rsa-b-4096-with-ssh-keygen)

Output:

![Näyttökuva 2024-9-27 kello 15 05 04](https://github.com/user-attachments/assets/2d9446ad-6894-4499-8cc6-785d010403b9)

If you know what you're doing, you can choose location other than the default. Otherwise stick with default location, as SSH-clients will automatically search this location for SSH-keys. 

Be careful! If you had previously generated SSH-keys, so the new key pair will be wiped out and new keys generated. [3](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)

![Näyttökuva 2024-9-27 kello 15 12 23](https://github.com/user-attachments/assets/69049c5d-913a-4b9d-a5d6-8569b03067ae)

Your keypair is created and is located in `~/user/.ssh/`. Public key is in file called `~/.ssh/id_rsa.pub` and your private key is in `~/.ssh/id_rsa`

### Choose SSH-key Authentication Method  

When creating a droplet on DigitalOcean, select the option that connects you to your droplet using SSH and choose `New SSH key`.

![Näyttökuva 2024-9-27 kello 14 46 00](https://github.com/user-attachments/assets/e85ee94a-a2c4-42e3-8489-f5da90c8ceb9)

![Näyttökuva 2024-9-27 kello 15 24 30](https://github.com/user-attachments/assets/85d4a6ce-5bbf-4401-9224-8d71fd08ea51)

You need to put the content of `~/.ssh/id_rsa.pub`, to where it says "SSH key content". 

To do this, you can and locate and open the file `~/.ssh/id_rsa.pub` in your computer, then copypaste it.

OR

Type and run command `cat ~/.ssh/id_rsa.pub` on your terminal, then copy the output and paste it.

Remember to name the public key you just pasted to your server, so you can differentiate SSH-keys for different projects.

### Using SSH method to log in to your server

You've generated SSH-key pair locally and copied the public key to your server, which means you are able to automate your login to your server. 

Login in using SSH-key pair is substantially safer than using a human-readable password. Passphrase is still recommended to use, in case attacker has access to your computer, virtually or physically, and generally for safety. 

Now you can log in to your server using only passphrase, after which your connection is authenticated by SSH-key pair.

![Näyttökuva 2024-9-27 kello 15 49 15](https://github.com/user-attachments/assets/d2c903cd-f7bb-42c7-9d57-eeb2e1af7fe0)

Since this is the first time connecting to your server via SSH from your computer, the promt says `The authenticity of host 'xxx.xxx.xxx.x' can't be established`

Type `yes` to add your ip address to list of known hosts. [3](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)

Then enter the passphrase for the SSH-key pair and you should be connected to your server securely.

Sources

1. https://www.ibm.com/support/pages/steps-creating-ssh-keys
2. https://stackoverflow.com/questions/51834225/why-use-t-rsa-b-4096-with-ssh-keygen
3. https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server
   https://en.wikipedia.org/wiki/RSA_(cryptosystem)
