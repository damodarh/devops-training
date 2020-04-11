GIT Integration

1. Install git client on Jenkins server
 
       sudo apt-get install git
       
2. Copy installed git path using  below command

       which git
    
2. Add git path in Global Tool Configuration by going to Managed Jenkins

3. Test git connection

    a. Setup Jenkins freestyle job
    
    b. Checkout the remote git private repository by configuring Github username and password in Jenkins credential manager
    
    
JDK and Maven Integration

1. Goto Manage Jenkins  --> Global Tool Configuration --> Choose JDK --> Create Oracle Account
2. Execute Jenkins job to install JDK
 
