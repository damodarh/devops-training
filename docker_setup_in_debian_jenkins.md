Refer below web link - https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-debian-9
First, update your existing list of packages:

sudo apt update
Next, install a few prerequisite packages which let apt use packages over HTTPS:

sudo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common
Then add the GPG key for the official Docker repository to your system:

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
Add the Docker repository to APT sources:

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
Next, update the package database with the Docker packages from the newly added repo:

sudo apt update
Make sure you are about to install from the Docker repo instead of the default Debian repo:

apt-cache policy docker-ce
You’ll see output like this, although the version number for Docker may be different:

Output of apt-cache policy docker-ce
docker-ce:
  Installed: (none)
  Candidate: 18.06.1~ce~3-0~debian
  Version table:
     18.06.1~ce~3-0~debian 500
        500 https://download.docker.com/linux/debian stretch/stable amd64 Packages
Notice that docker-ce is not installed, but the candidate for installation is from the Docker repository for Debian 9 (stretch).

Finally, install Docker:

sudo apt install docker-ce
Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:

sudo systemctl status docker
The output should be similar to the following, showing that the service is active and running:

Output
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2018-07-05 15:08:39 UTC; 2min 55s ago
     Docs: https://docs.docker.com
  Main PID: 21319 (dockerd)
   CGroup: /system.slice/docker.service
           ├─21319 /usr/bin/dockerd -H fd://
           └─21326 docker-containerd --config /var/run/docker/containerd/containerd.toml
           
Step 2 — Executing the Docker Command Without Sudo for Jenkins user

By default, the docker command can only be run the root user or by a user in the docker group, 
which is automatically created during Docker’s installation process. If you attempt to run the docker command without prefixing 
it with sudo or without being in the docker group, you’ll get an output like this:

Output
docker: Cannot connect to the Docker daemon. Is the docker daemon running on this host?.
See 'docker run --help'.        
1. Check if docker group is already exist or not by
cat /etc/groups
2. If it is not listed there, create a docker group..Btw, it supposed to be created already
sudo groupadd docker
3. Add jenkins user to the docker group.
sudo usermod -aG docker $USER
4. Log out and log back in so that your group membership is re-evaluated.

If testing on a virtual machine, it may be necessary to restart the virtual machine for changes to take effect.

On a desktop Linux environment such as X Windows, log out of your session completely and then log back in.

On Linux, you can also run the following command to activate the changes to groups:

newgrp docker

Note:restart the linux using below
sudo reboot
Now, you can execute docker login from jenkins.



