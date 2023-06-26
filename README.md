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

- git clone https://github.com/vikasedu-github/Employee-Management-Three-Tier-JavaApp.git
- sudo apt-get install maven default-jre
- sudo nano Employee-Management-Three-Tier-JavaApp/springboot-backend/src/main/resources/application.properties
-  You will see Output as below, Now change the "db-endpoint" with your database endpoint
	- spring.datasource.url= jdbc:mysql://"db-endpoint":3306/kube?useSSL=false
        - spring.datasource.username= tom
        - spring.datasource.password= root
        - spring.jpa.properties.hibernate.dialect= org.hibernate.dialect.MySQL5InnoDBDial>
        - (HASH)Hibernate ddl auto (create, create-drop, validate, update)
        - spring.jpa.hibernate.ddl-auto= update
                    
- /Employee-Management-Three-Tier-JavaApp/springboot-backend/
- mvn clean install
- /Employee-Management-Three-Tier-JavaApp/springboot-backend/target/
- java -jar -Djava.net.preferIPv4Stack=true jarfile &


Web

- sudo apt-get install npm
- sudo npm update npm -g
- vi Employee-Management-Three-Tier-JavaApp/react-frontend/src/Services/EmployeeService.js
	- const EMPLOYEE_API_BASE_URL = "http://localhost:8080/employees";
- cd Employee-Management-Three-Tier-JavaApp/react-frontend/
- npm i
- npm start$
