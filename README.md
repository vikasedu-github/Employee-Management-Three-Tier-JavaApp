# Employee-Management-Three-Tier-App

- sudo apt update and sudo apt upgrade -y
- sudo apt-get install mysql-server –y
- mysql -h "db endpoint" -U "username" -p
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
- vi Employee-Management-Three-Tier-App/springboot-backend/src/main/resources/application.properties and add dbip and port
	- spring.datasource.url=jdbc:mysql://localhost:3306/kube?createDatabaseIfNotExist=true&allowPublicKeyRetrieval=true&useSSL=false&user=tom$password=root
- /Employee-Management-Three-Tier-App/springboot-backend/
- mvn clean install
- /Employee-Management-Three-Tier-App/springboot-backend/target/
- java -jar -Djava.net.preferIPv4Stack=true jarfile &


Web

- sudo apt-get install npm
- sudo npm update npm -g
- vi /Employee-Management-Three-Tier-App/react-frontend/src/services/EmployeeService.js
	- const EMPLOYEE_API_BASE_URL = "http://localhost:8080/employees";
- cd /Employee-Management-Three-Tier-App/react-frontend/
- npm i
- npm start$
