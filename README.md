# onboarding-docs for new engineers
This docs helps provide support for new engineers joining the team.

# Table of Contents
1. [Setting up VPN](#Setting up VPN)
2. [Authenticating with the proxy git account](#Authenticating with the proxy git account)

## Setting up VPN
First and foremost, the most important part of this onboarding process and while working with the client is to always have your VPN on. The default location should be set to `Seattle` but this can change and will be communicated on the slack channel. 

[`Express VPN`](https://www.expressvpn.com/) is the recommended choice of VPN but you can use anyone that works well for you.


#### Authenticating with the proxy git account
This steps allows use to use multiple account on your laptop. you will be adding the proxy git account to your laptop in addition to your personal account. This essense of doing this is so you can push to the client repository using the proxy credentials.

1. Generate a new ssh key.

    ```shell
    ssh-keygen -t rsa -C "email@work_mail.com" -f "work_user1"
	  ```
		
 2. Copy the public key using this command `pbcopy < ~/.ssh/work_user1.pub` and then log in to your personal GitHub account:

    Go to Settings, Select SSH and GPG keys from the menu to the left. Click on New SSH key, provide a suitable title, and paste the key in the box below.
    Click Add key — and you’re done
    
 3. Register the new SSH Keys with the ssh-agent command

   ```shell
   eval "$(ssh-agent -s)"
   ```
   
 4. Add the keys to the ssh-agent
    
    ```command
    ssh-add ~/.ssh/work_user1
    ```
    
 5. create the ssh config file

    ```command
    $ cd ~/.ssh/
    $ touch config           // Creates the file if not exists
    $ code config            // Opens the file in VS code, use any 
    ```
    
   Add the configuration entries for the relevant github account
   
   ```
    # Personal account, - the default config
    Host github.com
       HostName github.com
       User git
       IdentityFile ~/.ssh/id_rsa

    # Work account-1
    Host github.com-farogs   
       HostName github.com
       User git
       IdentityFile ~/.ssh/work_user1
   ```
  6. To make use of the proxy account, run the command below
     
     ```command
      ssh-add -D
      ssh-add ~/.ssh/work_user1
     ```
     At the stage, you can start cloning repos using ssh
     
  7. After cloning the repo, run the command below so commits can show the proxy username.
     
     ```command
       git config user.name "Farogs"   // Updates git config user name
       git config user.email "faarooq.arogundade@gmail.com"
     ```
