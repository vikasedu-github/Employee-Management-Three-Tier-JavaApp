#For source reference visit https://github.com/14Rahul/Employee-Management-Three-Tier-App
# Employee-Management-Three-Tier-JavaApp
- Make VM for APP Server and Web Server including one MySQL database on AZURE or AWS.
- If you are creating multiple servers then we will need an Loadbalancer as well.
- Create one Loadbalancer and configure all the servers and Loadbalancer rules as per your requirements.
- We will place our VMs behind Loadbalancer
- Once VMs is created then login and follow the below steps to deploy this three tier App.
- Follow APP section for App VM and Web section for WEB VM.

**=========================== App VM Steps ===========================**   

- sudo apt-get install mysql-server -y
- mysql -h "db endpoint or db-name" -u root -p
- show databases;
- use kube;(your db name)
- create user 'tom'@'%' identified by 'root';
- GRANT ALL PRIVILEGES ON kube.* TO 'tom'@'%';
- \q
- git clone https://github.com/vikasedu-github/Employee-Management-Three-Tier-JavaApp.git
- sudo apt-get install maven default-jre
- sudo apt update
- sudo apt upgrade -y
- sudo nano Employee-Management-Three-Tier-JavaApp/springboot-backend/src/main/resources/application.properties
- You will see Output as below, Now change the "db-endpoint" with your database endpoint
  ```
  spring.datasource.url= jdbc:mysql://"db-endpoint":3306/kube?useSSL=false
  spring.datasource.username= tom
  spring.datasource.password= root
  spring.jpa.properties.hibernate.dialect= org.hibernate.dialect.MySQL5InnoDBDial>
  #Hibernate ddl auto (create, create-drop, validate, update)
  spring.jpa.hibernate.ddl-auto= update
  ```
- cd Employee-Management-Three-Tier-JavaApp/springboot-backend/
- sudo mvn clean install
- cd Employee-Management-Three-Tier-JavaApp/springboot-backend/target
- sudo nano /etc/systemd/system/app.service
- if it says folder does not exist then follow below steps under {} else skip this steps   
  {  
  -under Employee-Management-Three-Tier-JavaApp/springboot-backend/target/
  ```
  sudo mkdir etc
  ```
  -under Employee-Management-Three-Tier-JavaApp/springboot-backend/target/etc/
  ```
  sudo mkdir systemd
  ```
  -under Employee-Management-Three-Tier-JavaApp/springboot-backend/target/etc/systemd/
  ```
  sudo mkdir system
  ```
  -under Employee-Management-Three-Tier-JavaApp/springboot-backend/target/etc/systemd/system/
  ```
  sudo touch app.service
  ```
 }   
- sudo nano /etc/systemd/system/app.service
- if app.service file opened paste the following code
  ```
  [Unit]
  Description=app
  After=network.target

  [Service]
  User=root
  Group=root
  ExecStart=java -jar -Djava.net.preferIPv4Stack=true /home/vikas/Employee-Management-Three-Tier-JavaApp/springboot-backend/target/springboot-backend-0.0.1-SNAPSHOT.jar
  Restart=always

  [Install]
  WantedBy=multi-user.target
  ```
  -then save(ctrl+X) and exit(Enter).
  
- sudo chmod ugo+rwx /etc/systemd/system/app.service
- sudo systemctl start app.service
- sudo systemctl enable app.service
- sudo systemctl status app.service
- ss -nltp

now you can see app port on which it is up.


**=========================== Web VM Steps ===========================**

- sudo apt update
- sudo apt upgrade -y
- git clone https://github.com/vikasedu-github/Employee-Management-Three-Tier-JavaApp.git
- sudo nano Employee-Management-Three-Tier-JavaApp/react-frontend/src/Services/EmployeeService.js  
- change "Back-IP" with "LB-IP or Frontend Machine-IP"
- Save(ctrl+X) and Exit(Enter).
- cd Employee-Management-Three-Tier-JavaApp/react-frontend
- under Employee-Management-Three-Tier-JavaApp/react-frontend/  
   - sudo apt-get install npm
- once finished installing npm then  
   - npm i
- once above process done then under Employee-Management-Three-Tier-JavaApp/react-frontend/
   - sudo nano /etc/systemd/system/web.service
- if it says folder does not exist then follow the steps mentioned under {} else skip this step  
- {  
   -under Employee-Management-Three-Tier-JavaApp/react-frontend/
    ``` 
    sudo mkdir etc
    ```  
   -under Employee-Management-Three-Tier-JavaApp/react-frontend/etc/
   ```
   sudo mkdir systemd
   ```
   -under Employee-Management-Three-Tier-JavaApp/react-frontend/systemd/
   ``` 
   sudo mkdir system
   ```
   -under Employee-Management-Three-Tier-JavaApp/react-frontend/systemd/system/
   ```
   sudo touch web.service
   ``` 
}  
- sudo nano /etc/systemd/system/web.service
- if web.service file opened paste the following code
   ```
   [Unit]
   Description=web
   After=network.target

   [Service]
   User=root
   Group=root
   WorkingDirectory=/home/vikas/Employee-Management-Three-Tier-JavaApp/react-frontend/
   ExecStart=npm start
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```  
- then save(ctrl+X) and exit(Enter).
- sudo chmod ugo+rwx /etc/systemd/system/web.service
- sudo systemctl start web.service
- sudo systemctl enable web.service
- sudo systemctl status web.service
- ss -nltp   
    
now you can see app port on which it is up.  




