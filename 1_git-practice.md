Perform below operations on private-repo from Git Bash:
1. Open Git Bash terminal
2. Git Initialization 

           git init
3. Generate ssh public key and private key using below command and add the public key in Git Hub account settings

           ssh-keygen

4. Add Private Remote Repository’s ssh url locally 

           git remote add origin ssh_url
           
5. Pull the changes from Remote Repository to sync Local Repository
            
           git pull origin master                
      
6. Create a new feature branch and checkout locally

           git branch feature_branch
           git checkout feature_branch
           

7. Create a testfile in working directory and add test data using vi editor

           touch testfile
           echo "hello world" >>testfile
       
8. Check git status and see if testfile is not indexed / untracked

           git status

9. Add testfile in staging area 
                        
           git add testfile
            
10. Check git status and see if testfile is indexed / tracked.

           git status
      
11. Commit file to store in Local Repository
            
           git commit -m "testfile commit"
      
          
           
12. Push the changes to feature branch of Remote Repository

           git push origin feature_branch
            
13. Modify existing file

           echo "This is test" >>testfile
           
14. Check the difference using below command

           git diff testfile
           
                OR
                
           git difftool testfile
           
           
