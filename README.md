#For source reference visit https://github.com/14Rahul/Employee-Management-Three-Tier-App
# Employee-Management-Three-Tier-JavaApp

- sudo apt update and sudo apt upgrade -y
- sudo apt-get install mysql-server –y
- mysql -h "db endpoint" -u "username" -p
- sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
- Bind IP all
- sudo mysql -u root -p
- password - root
- create user 'tom'@'%' identified by 'root';
- create database kube;
- GRANT ALL PRIVILEGES ON kube.* TO 'tom'@'%';

App

- sudo apt-get install mysql-server -y
- mysql -h "db endpoint or db-name" -u root -p
- show databases;
- create user 'tom'@'%' identified by 'root';
- GRANT ALL PRIVILEGES ON kube.* TO 'tom'@'%';
- \q
- git clone https://github.com/vikasedu-github/Employee-Management-Three-Tier-JavaApp.git
- sudo apt-get install maven default-jre
- sudo apt update
- sudo apt upgrade -y
- sudo nano Employee-Management-Three-Tier-JavaApp/springboot-backend/src/main/resources/application.properties
- You will see Output as below, Now change the "db-endpoint" with your database endpoint
	- spring.datasource.url= jdbc:mysql://"db-endpoint":3306/kube?useSSL=false
        - spring.datasource.username= tom
        - spring.datasource.password= root
        - spring.jpa.properties.hibernate.dialect= org.hibernate.dialect.MySQL5InnoDBDial>
        - (HASH)Hibernate ddl auto (create, create-drop, validate, update)
        - spring.jpa.hibernate.ddl-auto= update
- cd Employee-Management-Three-Tier-JavaApp/springboot-backend/
- sudo mvn clean install
- cd Employee-Management-Three-Tier-JavaApp/springboot-backend/target
- sudo nano /etc/systemd/system/app.service
- if it says folder does not exist then follow below steps under {}
-{
  -under Employee-Management-Three-Tier-JavaApp/springboot-backend/target/
     - sudo mkdir etc
  -under Employee-Management-Three-Tier-JavaApp/springboot-backend/target/etc/
     - sudo mkdir systemd
  -under Employee-Management-Three-Tier-JavaApp/springboot-backend/target/etc/systemd/
     - sudo mkdir system
  -under Employee-Management-Three-Tier-JavaApp/springboot-backend/target/etc/systemd/system/
     - sudo touch app.service
-}
- sudo nano /etc/systemd/system/app.service
- if app.service file opened paste the following code
  -[Unit]
  -Description=app
  -After=network.target

  -[Service]
  -User=root
  -Group=root
  -ExecStart=java -jar -Djava.net.preferIPv4Stack=true /home/vikas/Employee-Management-Three-Tier-JavaApp/springboot-backend/target/springboot-backend-0.0.1-SNAPSHOT.jar
  -Restart=always

  -[Install]
  -WantedBy=multi-user.target

  -then save(ctrl+X) and exit(Enter).
  
- sudo chmod ugo+rwx /etc/systemd/system/app.service
- sudo systemctl start app.service
- sudo systemctl enable app.service
- sudo systemctl status app.service
- ss -nltp

now you can see app port on which it is up.


Web

- sudo apt-get install npm
- sudo npm update npm -g
- vi Employee-Management-Three-Tier-JavaApp/react-frontend/src/Services/EmployeeService.js
	- const EMPLOYEE_API_BASE_URL = "http://localhost:8080/employees";
- cd Employee-Management-Three-Tier-JavaApp/react-frontend/
- npm i
- npm start$
