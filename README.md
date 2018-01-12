@author: Jonathan YUE CHUN

# Use multiple SSH Deploy keys on the same server (machine)

## Linux

1) create ssh key by attributing the commiting user identification (eg. email)

        ssh-keygen -t rsa -f ~/.ssh/id_rsa -C "your@email.com"

        ssh-keygen -t rsa -f ~/.ssh/id_rsa.repo1 -C "your@email.com"

2) in ~/.ssh  : create config file (touch config)

3) edit (eg. with vim: vim ~/.ssh/config) and add the following:

### Default id_rsa
        Host github.com

                HostName github.com

                PreferredAuthentications publickey

                IdentityFile ~/.ssh/id_rsa
### repo1 id_rsa        
        Host github.com-repo1

                HostName github.com

                PreferredAuthentications publickey

                IdentityFile ~/.ssh/id_rsa.repo1
        
 4) ssh-add ~/.ssh/id_rsa
 5) ssh-add ~/.ssh/id_rsa.repo1
 6) if error while ssh-add, do: eval `ssh-agent -s` and run steps 4 & 5 again
 7) ssh-add -l  to check if keys are running as expected
 8) you might need to add ssh-add (key location) in ~/.bashrc for permanent change on shutdown/restart/etc...
 
        in ~/.bashrc
                eval `ssh-agent -s`
                ssh-add ~/.ssh/id_rsa
                ssh-add ~/.ssh/id_rsa.repo1
  9) Don't forget to add deploy keys on github repo (*.pub)
  10) In clone root directory for project repo1, change/add repository to:
                
                git remote set-url origin git@github.com-repo1:MadDoxXimba/tp_ri.git
  11) check if the key is working: ssh -T git@github.com-XXXX   where XXXX is repo1 in our scenario 


## Windows

 1) Install gitbash (https://desktop.github.com/)
 2) open gitbash cmd
 3) repeat same steps as for Linux
