# Two-tier-flask-app-deployment

this flask app that interacts with a mysql database.The app allow users to enter the messages,which are all stored in database and display messages as result in frontend.

## Prerequisites
 - Download Docker
 - Git

## Steps :
1. Create a EC2 instance in any cloud providers ( like.. AWS, AZURE, GCP )

2. Install and verify into your Docker account:
<pre>sudo apt update
sudo apt install docker.io
docker</pre>

3.Login into docker account:
<pre>docker login</pre>

4. Clone this repository:
<pre> git clone https://github.com/your-username/your-repo-name.git </pre>

5. Change the directory to ` your-repo-name ` in project
<pre>cd your-repo-name</pre>

6. Create a `.env` file in the project directory to store your MySQL environment variables:
<pre>touch .env</pre>

7.Build the docker container:
<pre>docker build -t two-tier-backend .</pre>

8.Create a custom network so flask app can interact with sql server:
<pre>docker network create two-tier -d bridge</pre>

9.Run docker network and configure a Mysql server container:
<pre>docker run -d --name mysql --network two-tier -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops mysql</pre>

10.Run docker flask container and configure with above container:
<pre>docker run -d -p 5000:5000 --network two-tier -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=root -e MYSQL_DB=devops two-tier-backend:latest</pre>

11. Change the Security groups and Edit inbound rules:
<pre>Create a new inbound rule and Select type "custom tcp" ,Set port range "5000" ,Set source "anywhere" and Save rule. </pre>

12. Now, you can see flask app on your localhost:
<pre>Local host = http://Public IPv4 address:5000</pre>
