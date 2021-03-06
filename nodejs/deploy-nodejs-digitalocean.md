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
4. execute `apt update` and `apt upgrade`
5. go on nodejs website and copy the command line to install nodejs and paste on terminal to execute and install.
6. install yarn
7. install docker (we will use it for database and other uses)
8. give sudoer permission to user docker 
   1. `usermod -aG docker userdeploy`
9. configure the db (postgres):
   1.  `docker run --name database -e POSTGRES_PASSWORD=djfwbfkjwbdfjwfwrfwrfrr3333 -p 5432:5432 --restart always -d`
   2.  create a user in postgres db, because it's better than be using the postgres default user:
       1. navigate into postgres shell
       2. `CREATE TABLE nodedeploy`
       3. `CREATE USER dbcompany WITH ENCRYPTED PASSWORD 'defwfvwgvwljgfbljbg'`
       4. `GRANT ALL PRIVILEGES ON DATABASE nodedeploy TO dbcompany`
10. configure nodejs project in digital ocean machine
    1.  create .env file in the root of the project
         ```java
         PORT=2222
         NODE_ENV=development

         DB_HOST=localhost
         DB_USER=docker
         DB_PASS=docker
         DB_NAME=sqlnode

         ```
    2. in the config/database.js file, get the values by accessing env var:
        ```javascript
            module.exports = {
                dialect: 'postgres',
                host: process.env.DB_HOST,
                username: process.env.DB_USERNAME,
                password: process.env.DB_PASSWORD,
            }
        ```
    3. add the nodeenv dependency in the server.js file and the config/database.js
        `require('dotenv/config');`

11. Git clone the project in the machine

12. Copy the file .env.examaple to a new file .env and set the variables for the config in the machine
13. run node server.js
    