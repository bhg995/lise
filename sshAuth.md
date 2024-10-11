# SSH Authentication Method, DigitalOcean

Debian, MacOs Monterey 12

### Generate SSH-key pair

    $ pwd
    $ ssh-keygen -b 4096 -t rsa

`ssh-keygen` generate, `-b 4096` **b**its. `-t rsa` algorithm. **t**ype. 

![Näyttökuva 2024-10-11 kello 5 13 52](https://github.com/user-attachments/assets/b0435699-478d-46d6-9976-c128768e86c8)

keypair location `~/user/.ssh/`. 

Public key file `~/.ssh/id_rsa.pub` private key file`~/.ssh/id_rsa` # keep the latter always hidden

### SSH-key Authentication Method  

Create droplet using SSH, choose `New SSH key`.

![Näyttökuva 2024-9-27 kello 14 46 00](https://github.com/user-attachments/assets/e85ee94a-a2c4-42e3-8489-f5da90c8ceb9)

![Näyttökuva 2024-9-27 kello 15 24 30](https://github.com/user-attachments/assets/85d4a6ce-5bbf-4401-9224-8d71fd08ea51)

content of `~/.ssh/id_rsa.pub`, to "SSH key content". 

- Name the public key in your server 
- `cat`-`less` `~/.ssh/id_rsa.pub`

### Login


Login in using SSH-key pair is more secure than a password. Passphrase is recommended to use. 

You can log in using SSH-key pair. 

    ssh user@xxx.xxx.xxx.x


First time connecting you'll get message `The authenticity of host 'xxx.xxx.xxx.x' can't be established`. 

Type `yes` to authenticate.

Enter the passphrase for the SSH-key pair for secure login.

### Copy your public key

You can copy your public key for another login.

    ssh-copy-id username@server_ip_address

Sources

- https://www.ibm.com/support/pages/steps-creating-ssh-keys
- https://stackoverflow.com/questions/51834225/why-use-t-rsa-b-4096-with-ssh-keygen
- https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server
- https://en.wikipedia.org/wiki/RSA_(cryptosystem)
