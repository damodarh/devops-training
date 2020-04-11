GIT Integration

1. Install git client on Jenkins server
 
       sudo apt-get install git
       
2. Copy installed git path using  below command

       which git
    
2. Add git path in Global Tool Configuration by going to Managed Jenkins

3. Test git connection

    a. Create new Jenkins freestyle job
    
    b. Configure Remote Git Private Repository
    
    c. Select configured GIT Credential
    
    d. Test by executing below shell command in build section
    
            ls -ltr         
    
JDK and Maven Configurations

1. Goto Manage Jenkins  --> Global Tool Configuration --> JDK --> JDK Installations
    Note: Need to create Oracle Account

2. Goto Manage Jenkins  --> Global Tool Configuration --> Maven--> Maven Installations
 
3. Create new Jenkins pipeline job and test the maven configuration by using below pipeline declarative script

                  pipeline 
                   {
                       agent any    
                       tools
                       {
                         maven 'maven' 
                         jdk 'jdk' 
                       }
                       stages 
                        {
                          stage('First stage') 
                          {
                           steps 
                            {
                             println "Hello World"
                             sh " mvn -version"
                            }
                          }
                        }
                   }






















