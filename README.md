# AWS_setup
simple instruction for environment setup on EC2 Linux 2 (64)


# 1. NODE JS
  ```
  curl --silent --location https://rpm.nodesource.com/setup_12.x | sudo bash -
  sudo yum -y install nodejs
  ```
  OR
  ```
  $ curl --silent --location https://rpm.nodesource.com/setup_10.x | bash -
  $ yum -y install nodejs
  ```
# 2. Apache2 - for php hosting sites
  ```
  sudo apt-get update
  sudo apt-get install apache2
  ```
# 3. MongoDB
  #3.1Create a /etc/yum.repos.d/mongodb-org-4.0.repo file 
  ```
  sudo touch /etc/yum.repos.d/mongodb-org-4.0.repo
  ```
  #3.2 Setup repository:
  ```
  sudo nano /etc/yum.repos.d/mongodb-org-4.0.repo
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

# 4. npm install in project folder with package.json in it

# 5. sudo npm install forever -g

# 6. NGINX AWS Extras
  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/amazon-linux-ami-basics.html#extras-library
  ```
  amazon-linux-extras list
  sudo amazon-linux-extras install nginx1.12
  ```
