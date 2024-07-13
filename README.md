# Vprofile-project with containers
Repo for my Vprofile project

This project is the same as the vprofile project on my account, but it is redone using containers
so instead of having multiple VMs for the different services we use just one Vms but then create containers each providing it's on 
services and working together.

# Prerequisites
More or less the same as the original vprofile project, you can check the readme for that project for clarity.


# Deployment
After downloading all your prerequisites you can now start the deployment process as outlined below
1. Create a folder for the project
3. Download the files from the repo into that folder
4. run the vagrant up command and wait for the command to execute completely. (this will take a while!)
5. log into the VM using the vagrant ssh command.
6. switch to the root user using the sudo -i command.
7. create a compose folder using this command "Mkdir compose"
7. copy the compose file from the shared-folder into the compose folder using this command:- cp /vagrant_data/docker-compose.yml /root/compose.
8. cd into the compose folder and run this command:- docker compose up -d.
9. wait for the command to execute completely.
11. validate the webapp.


#Validation
to validate that the site you just deployed is working fine you have to take a few steps
firstly recall there are 5 containers, each container provides it own functionality for the site,
vprodb-1 - database (sql), vproapp-1 - application (tomcat), vprocache01-1 - caching (memecache), vpromq01-1 - queieing agent (rabbitmq)
vproweb-1 -  webserver (nginx). so these are all the components that make the application work. the steps to validate the
sites are outlined below.
1 - get the IP for the website either by running the ip addr show command to get an IP to use for testing (use oe of the 192.168.... IPs)
or by getting the private IP configured on the vagrantfile.
2. Input/paste that IP in your web browser, you will be taking to the HKH Infotech website, at this point
you have validated that the web and app containers are functional.
3. Try to login (username admin_vp, password admin_vp)
4. you will be logged into the account at this point you have verified that the database container is functional
5. click on the all users tab on the website, click on any user, you will see a data inserted into cache write up
above the user details. go back and click on the same user again, you will see a data retrieved from cache message
so the caching is working fine.
6. Go back to the IP/welcome page, click on the rabbitmq tab, you will see a rabbitmq initiated message, this is proof
that the queueing agent is working.
7. Website validated!