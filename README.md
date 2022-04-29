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

