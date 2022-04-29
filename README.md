# LAMP-Stack-Implementation-in-AWS
This is a project that implements the use of LAMP stack in AWS

## Creating EC2 instance
- Select region (the cl and launch a new EC2 instance of t2.micro family with Ubuntu Server 20.04 LTS (HVM)

Create a pair Key as the EC2 is created

Move into the folder where the pair key is downloaded and run the following command to connect to the instance

                      sudo chmod 0400 <private-key-name>.pem
                      
 Connect to the instance by running
                      
                      ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>
                      
 ## INSTALLING APACHE AND UPDATING THE FIREWALL
 
 Install Apache using Ubuntu’s package manager ‘apt’:

                                        #update a list of packages in package manager
                                        sudo apt update

                                        #run apache2 package installation
                                        sudo apt install apache2
  
  To verify that apache2 is running as a Service in our OS, use following command
  
                                      sudo systemctl status apache2
                                      
 First, let us try to check how we can access it locally in our Ubuntu shell, run


                                                    curl http://localhost:80
                                                    or
                                                     curl http://127.0.0.1:80
           

<img width="1728" alt="Apache Ubuntu local host" src="https://user-images.githubusercontent.com/103472595/165990869-31792b52-4fc6-4335-b48e-246c74ef23b0.png">

Testing our Apache HTTP server
                                      http://<Public-IP-Address>:80


<img width="1728" alt="Apache2 Ubuntu page" src="https://user-images.githubusercontent.com/103472595/165987376-ddac9c1c-df1a-4992-a036-fa1731fffce2.png">
  
  ## INSTALLING MYSQL
  
  Again, use ‘apt’ to acquire and install this software

                                    sudo apt install mysql-server
  
When prompted, confirm installation by typing Y, and then ENTER.

When the installation is finished, it’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Start the interactive script by running:

                                    sudo mysql_secure_installation
  
  When you’re finished, test if you’re able to log in to the MySQL console by typing:

                                                      sudo mysql
  
  <img width="561" alt="Start MySql" src="https://user-images.githubusercontent.com/103472595/165993144-a81c5c1e-9101-4735-9a64-cb9c2f2492fe.png">
  
  
  To exit the MySQL console, type:

                                                   exit
  
  ## INSTALLING PHP
  
  To install these 3 packages at once, run:

                                    sudo apt install php libapache2-mod-php php-mysql
  
  
Once the installation is finished, you can run the following command to confirm your PHP version:

                                                    php -v
  
  If everything is done correctly, it will display the picture below
  
  <img width="487" alt="To check the PHP installed is working" src="https://user-images.githubusercontent.com/103472595/165994043-1339d881-3d4e-4523-a123-1d2a75577238.png">
  
  
  ## CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
  
  Create the directory for projectlamp using ‘mkdir’ command as follows:

                                      sudo mkdir /var/www/projectlamp
  
Next, assign ownership of the directory with your current system user:

                                    sudo chown -R $USER:$USER /var/www/projectlamp
  
Then, create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor. Here, we’ll be using vi or vim (They are the same by the way):

                                    sudo vi /etc/apache2/sites-available/projectlamp.conf
  
  
This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:

                                        <VirtualHost *:80>
                                            ServerName projectlamp
                                            ServerAlias www.projectlamp 
                                            ServerAdmin webmaster@localhost
                                            DocumentRoot /var/www/projectlamp
                                            ErrorLog ${APACHE_LOG_DIR}/error.log
                                            CustomLog ${APACHE_LOG_DIR}/access.log combined
                                        </VirtualHost>
  
  To save and close the file, simply follow the steps below:

Hit the esc button on the keyboard
  Type :
  Type wq. w for write and q for quit
Hit ENTER to save the file
  
You can use the ls command to show the new file in the sites-available directory

                                      sudo ls /etc/apache2/sites-available
  
You will see something like this;

                                      000-default.conf  default-ssl.conf  projectlamp.conf
  
  You can now use a2ensite command to enable the new virtual host:

                                        sudo a2ensite projectlamp
  
   <img width="378" alt="Enabling our project lamp" src="https://user-images.githubusercontent.com/103472595/165995523-5489b4fc-7d1a-48bd-adfe-7a97a72a542e.png">
  
You might want to disable the default website that comes installed with Apache. This is required if you’re not using a custom domain name, because in this case Apache’s default configuration would overwrite your virtual host. To disable Apache’s default website use a2dissite command , type:

                                                    sudo a2dissite 000-default
 
  
To make sure your configuration file doesn’t contain syntax errors, run:

                                                sudo apache2ctl configtest
  
Finally, reload Apache so these changes take effect:

                                            sudo systemctl reload apache2
  
  Your new website is now active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:

                sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
  
Now go to your browser and try to open your website URL using IP address:
  

                                               http://<Public-IP-Address>:80
  
 
<img width="780" alt="Hello lamp html" src="https://user-images.githubusercontent.com/103472595/165995527-7203504c-ee4e-40d9-8a6f-42169006bb55.png">
  
  ## ENABLE PHP ON THE WEBSITE
  
  In case you want to change this behavior, you’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php 
  
  file is listed within the DirectoryIndex directive:

                                    sudo vim /etc/apache2/mods-enabled/dir.conf
  
                                    <IfModule mod_dir.c>
                                            #Change this:
                                            #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
                                            #To this:
                                            DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
                                    </IfModule>

  After saving and closing the file, you will need to reload Apache so the changes take effect:

                                              sudo systemctl reload apache2
  
  Create a new file named index.php inside your custom web root folder:

                                          vim /var/www/projectlamp/index.php
  
This will open a blank file. Add the following text, which is valid PHP code, inside the file:

                                                                    <?php
                                                                    phpinfo();

When you are finished, save and close the file, refresh the page and you will see a page similar to this:

<img width="1728" alt="PHP home page" src="https://user-images.githubusercontent.com/103472595/165996693-a8f1c73b-d710-42ad-ad07-660eb5f27579.png">

After checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use rm to do so:

                                          sudo rm /var/www/projectlamp/index.php

You can always recreate this page if you need to access the information again later.




  
  
  
  

