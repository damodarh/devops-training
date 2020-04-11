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
         
         
5. Install Jenkins 

         apt-get install -y jenkins
         
6. Open web-browser and hit below 

         http://PUBLIC-IP:8080
         
      Here, PUBLIC-IP is your VM Public IP address

7. Get Jenkins admin password from below file and do the login

        cat /var/lib/jenkins/secrets/initialAdminPassword
        
8. Install the suggested Jenkins plugins and configure your admin user        
    
9. Route Jenkins HTTP Port 8080 traffic to standard HTTP port 80

        iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080
         
         
10. Optional: Add --httpsPort=8443 in JENKINS_ARGS parameter under below file 
         
         vi /etc/default/jenkins

11. Optional: HTTPS Port 8443 to standard HTTPS port 443 using iptables.           
         
        iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 443 -j REDIRECT --to-port 8443

      
12. Set IST Timezone to get appropriate time in Jenkins console 

         cat /etc/timezone
         
         echo "Asia/Kolkata">/etc/timezone
         
                      OR
                     
          sudo dpkg-reconfigure tzdata
          

13. Restart jenkins to reflect the changes.
       
        service jenkins restart
        
        service jenkins status
       
14. Now, you will be able to access jenkins via http or https using the below link
       
        http://${jenkins_public_ip}    OR     https://${jenkins_public_ip}
       
         

       



