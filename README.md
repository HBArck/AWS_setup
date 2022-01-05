# AWS_setup
simple instruction for environment setup on EC2 Linux 2 (64)


# 1. NODE JS
  ```
  curl --silent --location https://rpm.nodesource.com/setup_14.x | sudo bash -
  sudo yum -y install nodejs
  ``` 
# 2. Apache2 - for php hosting sites
  ```
  sudo apt-get update
  sudo apt-get install apache2
  ```
# 3. MongoDB
  #3.1 Create a /etc/yum.repos.d/mongodb-org-4.4.repo file 
  ```
  sudo touch /etc/yum.repos.d/mongodb-org-4.4.repo
  ```
  #3.2 Setup repository:
  ```
  sudo nano /etc/yum.repos.d/mongodb-org-4.4.repo
  ```
  ```
  [mongodb-org-4.4]
  name=MongoDB Repository
  baseurl=https://repo.mongodb.org/yum/amazon/2/mongodb-org/4.4/x86_64/
  gpgcheck=1
  enabled=1
  gpgkey=https://www.mongodb.org/static/pgp/server-4.4.asc
  ```
  #3.3 Installing 
  ```
  sudo yum install -y mongodb-org
  ```
  #3.4 Running
    ```
    sudo service mongod start
    ```
  #3.5 Backup
    ```
    mongodump "--archive=./backups/XYZ-backup.gz" --gzip --db DB_NAME
    ```
  #3.6 Restore
    ```
    mongorestore "--archive=./backups/XYZ-backup.gz" --gzip --db DB_NAME
    ```

# 4. npm install in project folder with package.json in it

# 5. sudo npm install forever -g

# 6. NGINX AWS Extras DEPRECATED!
  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/amazon-linux-ami-basics.html#extras-library
  ```
  amazon-linux-extras list
  sudo amazon-linux-extras install nginx1.12
  ```
# 6. NGINX
  ```
  sudo yum clean metadata
 sudo yum -y install nginx
    
 nginx -v
  ```
  
# 7. REDIS
  ```
  sudo yum -y install gcc make # install GCC compiler
  cd /usr/local/src 
  sudo wget http://download.redis.io/redis-stable.tar.gz
  sudo tar xvzf redis-stable.tar.gz
  sudo rm -f redis-stable.tar.gz
  cd redis-stable
  sudo yum groupinstall "Development Tools"
  sudo make distclean
  sudo make
  sudo yum install -y tcl
  ```
  check if redis installed
  ```
  sudo make test
  ```
  ```
  sudo cp src/redis-server /usr/local/bin/
  sudo cp src/redis-cli /usr/local/bin/
  ```
  Launch redis
  ```
  sudo nano /etc/systemd/system/redis.service
  ```
  ```
  [Unit]
  Description=Redis In-Memory Data Store 
  After=network.target

  [Service]
  User=redis
  Group=redis
  ExecStart=/usr/local/bin/redis-server /etc/redis/redis.conf
  ExecStop=/usr/local/bin/redis-cli shutdown
  Restart=always

  [Install]
  WantedBy=multi-user.target
  ```
  ```
  sudo adduser --system --group --no-create-home redis
  ```
  ```
  redis-server
  sudo systemctl unmask  redis-server.service
  ```
