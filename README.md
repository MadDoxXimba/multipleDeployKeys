@author: Jonathan YUE CHUN

# Use multiple SSH Deploy keys on the same server (machine)

## Linux

1) create ssh key by attributing the commiting user identification (eg. email)

        ssh-keygen -t rsa -f ~/.ssh/id_rsa -C "your@email.com"

        ssh-keygen -t rsa -f ~/.ssh/id_rsa.repo1 -C "your@email.com"

2) in ~/.ssh  : create config file (touch config)

3) edit (eg. with vim: vim ~/.ssh/config) and add the following:


        Host github.com

                HostName github.com

                PreferredAuthentications publickey

                IdentityFile ~/.ssh/id_rsa
        
        Host github.com

                HostName github.com

                PreferredAuthentications publickey

                IdentityFile ~/.ssh/id_rsa.repo1
        
 4) ssh-add ~/.ssh/id_rsa
 5) ssh-add ~/.ssh/id_rsa.repo1
 6) if error while ssh-add, do: eval `ssh-agent -s` and run steps 4 & 5 again
 7) ssh-add -l  to check if keys are running as expected
 8) you might need to add ssh-add (key location) in ~/.bashrc for permanent change on shutdown/restart/etc...
