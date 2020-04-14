/*********************************Pipeline script to host web app in Google bucket*************************************************/

                                    pipeline 
                   {
                       agent any    
                       tools
                       {
                           
                           nodejs  'node'

                       }
                       stages 
                        {
                          stage('Build') 
                          {
                           steps 
                            {
                              script
                              {   
                               cleanWs()
                               checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '${Repo_branch}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github_credential', url: 'https://github.com/vmgponly/react-web-app.git']]]
                             
                             sh '''
                             node --version
                             npm --version
                             
                             npm install
                             npm run build
                             ls -ltr
                             cd build/
                             tar -cvf frontend-${BUILD_NUMBER}.tar *
                             '''
                           }   
                            }
                          }
                           stage('Deploy') 
                          {
                           steps 
                            {

                                sh '''
                                cd build
                                tar -xvf frontend-${BUILD_NUMBER}.tar
                                rm -rf frontend-${BUILD_NUMBER}.tar
                                ls -ltr
                                gsutil acl ch -u AllUsers:R gs://test-vijayg
                                gsutil defacl set public-read gs://test-vijayg
                                gsutil web set -m index.html -e index.html gs://test-vijayg
                                gsutil cp -r * gs://test-vijayg/
                                gsutil setmeta -h "content-type: image/svg+xml" gs://test-vijayg/static/media/*.svg
                                '''
                             
                            }
                          }
                     }
                  }



Important Steps to host Static Website on Google Buckets 


1. Execute below Google SDK command to grant access to bucket for all users

        gsutil acl ch -u AllUsers:R gs://bucketname

2. To make bucket pubically accessible

        gsutil defacl set public-read gs://bucketname
        
3. To set or modify the website configuration for an existing bucket 

        gsutil web set -m index.html -e index.html gs://bucketname
        


Note: Execute below command to set metadata on bucket objects after copying the objects in bucket  
  
         gsutil setmeta -h "content-type: image/svg+xml" gs://bucketname/static/media/*.svg
