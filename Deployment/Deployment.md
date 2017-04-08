# Trading Server Deployment


## Install applications

```
sudo apt-get install -y build-essential 
sudo apt-get install -y python3-pip 
sudo apt-get install -y eric 
sudo apt-get install -y redis-server 
sudo apt-get install -y npm 

# Install jenkins
wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install -y jenkins

# Install redis commander
npm install -g redis-commander

# Open folder
mkdir logs
mkdir configs
mkdir workspace

# Link nodejs to node
ln -s /usr/bin/nodejs /usr/bin/node
```

## Set up startup service

Insert the following lines into file ```/etc/rc.local```.

```
/usr/local/bin/redis-commander --redis-host 127.0.0.1 --redis-port 16001 --port 8001 > /root/logs/redis-commander-$CURRDATE &

```

## Trading applications

```
sudo pip3 install pytest
sudo pip3 install bitcoinexchangefh
```

## Port usage

|Port  |Application     |
|------|----------------|
|6001  |Feed handler    |
|9999  |Unit test used  |
|8001  |Redis Commander |
|8080  |Jenkins         |
|6379  |Redis server    |