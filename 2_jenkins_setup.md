******Jenkins Installation on Debian Linux system using Jenkins official Repository*******

/* 
Check your os vendor by using cat /etc/os-release
*/

1. Switch to root user

         sudo su - root

2. Install Java version
    
        apt install openjdk-8-jdk
        apt-get update
    
3. Import the GPG keys of the Jenkins repository using following wget command
    
         wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
        
4. Add the Jenkins official repository to debian system
    
         echo "deb http://pkg.jenkins.io/debian-stable binary/" >> /etc/apt/sources.list
         
         apt-get update
         
         apt-get install -y jenkins
    
5. Optional - Configure https using Jenkins startup script
 
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
      
6. Set IST Timezone to get appropriate time in Jenkins console 

         cat /etc/timezone
         echo "Asia/Kolkata">/etc/timezone

7. Restart jenkins to reflect the changes.
       
        sudo service jenkins start
       
8. Now, you will be able to access jenkins via http or https using the below link
       
       http://${jenkins_public_ip}:8080    OR     https://${jenkins_public_ip}:8443
       
       cat /var/lib/jenkins/secrets/initialAdminPassword
       

       



