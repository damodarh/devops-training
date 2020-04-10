******Jenkins Installation on Debian Linux system using Jenkins official Repository*******

/* 
Check your os vendor by using cat /etc/os-release
*/

1. Switch to root user

         sudo su - root

2. Install Java version
    
        apt install -y openjdk-8-jdk && apt-get update
    
3. Import the GPG keys of the Jenkins repository using following wget command
    
         wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
        
4. Add the Jenkins official repository to debian system
    
         echo "deb http://pkg.jenkins.io/debian-stable binary/" >> /etc/apt/sources.list          
         apt-get update
                           
         apt-get install -y jenkins
    
5. Route Jenkins HTTP Port 8080 traffic to standard HTTP port 80

        iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080
         
         
6. Optional: Add --httpsPort=8443 in JENKINS_ARGS parameter under below file 
         
         vi /etc/default/jenkins

7. Optional: HTTPS Port 8443 to standard HTTPS port 443 using iptables.           
         
       iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 443 -j REDIRECT --to-port 8443

      
6. Set IST Timezone to get appropriate time in Jenkins console 

         cat /etc/timezone
         echo "Asia/Kolkata">/etc/timezone

7. Restart jenkins to reflect the changes.
       
        service jenkins restart
       
8. Now, you will be able to access jenkins via http or https using the below link
       
       http://${jenkins_public_ip}    OR     https://${jenkins_public_ip}
       
       cat /var/lib/jenkins/secrets/initialAdminPassword
       

       



