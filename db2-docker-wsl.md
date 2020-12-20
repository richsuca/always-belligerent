# Install WSL, Docker to run DB2

## You will need 4 things
1. WSL (light weight system to run Linux from Windows)
2. Windows Terminal (for connecting to Linux)
3. Docker
4. DB2 Docker Container

## WSL
Follow steps 1-6 to install WSL (pick Ubuntu in Step 6)   
https://docs.microsoft.com/en-us/windows/wsl/install-win10#manual-installation-steps

*Remember* the password for the admin account, you will need it when you run `sudo` (Super User) commands.

## Windows Terminal
https://docs.microsoft.com/en-us/windows/wsl/install-win10#install-windows-terminal-optional

## Docker
I followed the steps from below website. The exact commands I used are listed below so you can skip the details.

https://docs.docker.com/engine/install/ubuntu/

Open Windows Terminal, start a Ubuntu session.

Commands:
```
sudo apt-get remove docker docker-engine docker.io containerd runc

sudo apt-get update

sudo apt-get install \
apt-transport-https \
ca-certificates \
curl \
gnupg-agent \
software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"
   
sudo apt-get install \
docker-ce \
docker-ce-cli \
containerd.io

sudo apt-get install \
docker-ce=5:20.10.0~3-0~ubuntu-focal \
docker-ce-cli=5:20.10.0~3-0~ubuntu-focal \
containerd.io

sudo service docker start

sudo docker run hello-world
```

If you see below, then Docker is working

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

## DB2 Docker
Got the command and steps from   
https://ajstorm.medium.com/installing-db2-on-your-coffee-break-5be1d811b052

Commands:

Set DB2 password by changing the value of `DB2INST1_PASSWORD`

```
mkdir ~/db2

sudo docker run -itd --name db2 --restart unless-stopped \
-e DBNAME=testdb -v ~/db2:/database -e DB2INST1_PASSWORD=YourSuperSecretPassword \
-e LICENSE=accept -p 50000:50000 --privileged=true ibmcom/db2
```

## Connect to DB2 server
Connect to the docker db2 server, run db2 (you can open multiple connections by starting another Ubuntu session from Windows Terminal
```
sudo docker exec -it db2 bash -c "su - db2inst1"
db2 connect to testdb
```

## Start/stop Docker service
When docker starts, it will start DB2 server.
```
sudo service docker start
sudo service docker stop
```

## (Optional) Install DBeaver
Install DBeaver on the Windows and connect to the DB2 instance

https://dbeaver.io/download/ (I recommended _Install from Microsoft Store_ option)

Get the IP Address of the Ubuntu running in WSL2 using
$ ip address | grep eth0 | grep inet

In DBeaver, use the IP address in the Host to connect (leave the port to default 50000)
