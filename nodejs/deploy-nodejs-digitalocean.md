## Deploying a nodejs application in Digital Ocean

1. Create the machine on DigitalOcean website
2. connect ssh via terminal into the machine created
3. create a new user
   1. command `addsuer userdeploy`
   2. give permission to userdeploy to be a sudoer: command `usermod -aG sudo userdeploy`
   3. copy the keys ssh that are set for root into userdeploy user folder.
      1. `cd /home/userdeploy/.ssh`
      2. `cp ~/.ssh/autorized_keys /home/userdeploy/.ssh/`
      3. `chmod 600 authorized_keys`
      4. `cd ..`
      5. `chmod 700 .ssh/`
