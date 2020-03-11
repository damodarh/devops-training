GIT Integration

1. Install git client on Jenkins server
 
       sudo apt-get install git
       which git
    
2. Copy git path and add in Jenkins Global Configurations from Managed Jenkins option

3. Git test connection

    a. Setup Jenkins freestyle job
    
    b. Checkout the remote git public repository
    
    c. Checkout the remote git private repository by configuring Github username and password in Jenkins credential manager
    
    
JDK and Maven Integration

1. Goto Manage Jenkins  --> Global Tool Configuration --> Choose JDK --> Create Oracle Account
2. Execute Jenkins job to install JDK
 
