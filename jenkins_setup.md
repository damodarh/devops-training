******Jenkins Installation*******

/* 
Check your os vendor by using cat /etc/os-release
*/

1. Create a Sudo User on Debian for Jenkins

   /* First, log in to your system as the root user */
   
       sudo su - root
       
   /* Create a new user account..below username is jenkins */   
       
       adduser jenkins
       
   /* To add a user to the sudo group use the usermod command..Here parameter -G = supplementary group, -a= To append  */
       
       usermod -aG sudo jenkins
       
   /* Test the sudo access by switching to the newly created user: */
   
       su - jenkins
       
   /* If the user has sudo access then the output of the below whoami command will be root */    
   
       sudo whoami
       
/* Note: You can now log in to your Debian server with this user account and use sudo to run administrative commands.        */
      
2. For Debian or Ubuntu system using Jenkins official Repository
    
        sudo apt install openjdk-8-jdk
        apt-get update
    
    /* Import the GPG keys of the Jenkins repository using the following wget command */
    
         wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
        
    /* Once the key is imported add the Jenkins repository to your system */
    
         echo "deb http://pkg.jenkins.io/debian-stable binary/" >> /etc/apt/sources.list
         apt-get install -y jenkins
    
3. Configure https using Jenkins startup script
 
   a. Jenkins startup script
        
        vi /etc/default/jenkins
        
   b. Configure https using self signed certificate. Create key and certificate. Provide information wherever asked.
        
        openssl req -newkey rsa:2048 -nodes -keyout jenkins.key -x509 -days 700 -out jenkins.crt
     /* The below command would ask you for password. Remember the same as that will be used during the configuration. */
        
        openssl pkcs12 -inkey jenkins.key -in jenkins.crt -export -out keys.pkcs12
        keytool -importkeystore -srckeystore keys.pkcs12 -srcstoretype pkcs12 -destkeystore /var/lib/jenkins/jenkins.jks
   
   c. Once the certificates are generated , configure the same in the /etc/default/jenkins file.
        
       JENKINS_ARGS="--webroot=/var/cache/$NAME/war --httpPort=-1 --httpsPort=8443 --httpsKeyStore=/var/lib/jenkins/jenkins.jks --httpsKeyStorePassword=<password>"
      /* Note: httpPort=-1 would disable http. If you wish to have both http and https , then provide the desired port.  */
      
4. Set Timezone to get appropriate time in Jenkins console

         cat /etc/timezone      

5. Once the above configuration is done, restart jenkins to reflect the change.
       
       sudo systemctl enable jenkins
       sudo systemctl start jenkins
       
       or
       
       sudo service jenkins enable
       sudo service jenkins start
       
6. Now, you will be able to access jenkins via https using the below link
       
       https://${jenkins_public_ip}:8443
       sudo cat /var/lib/jenkins/secrets/initialAdminPassword
       

       



