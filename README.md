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

<img width="1728" alt="Apache Ubuntu local host" src="https://user-images.githubusercontent.com/103472595/165990869-31792b52-4fc6-4335-b48e-246c74ef23b0.png">
           



<img width="1728" alt="Apache2 Ubuntu page" src="https://user-images.githubusercontent.com/103472595/165987376-ddac9c1c-df1a-4992-a036-fa1731fffce2.png">
