
1. Execute below Google SDK command to grant access to bucket for all users

        gsutil acl ch -u AllUsers:R gs://bucketname

2. To make bucket pubically accessible

        gsutil defacl set public-read gs://bucketname
        
3. To set or modify the website configuration for an existing bucket 

        gsutil web set -m index.html -e index.html gs://bucketname
        


Note: Execute below command to set metadata on bucket objects after copying the objects in bucket  
  
         gsutil setmeta -h "content-type: image/svg+xml" gs://bucketname/static/media/*.svg
