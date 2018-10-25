# Tomcat8.5 Liferay7.1 CE MariaDB 10
This repo contains a dockerized Apache Tomcat 8.5 and a Liferay 7.1 installation. 
To preserve data a MariaDB database is preconfigured.


In this image, the Tomcat Manager GUI is enabled via the tomcat-users.xml.
To access the manager GUI 

    http://hostname:8080/manager/html
    
the following standard user (with all privileges) is created:
- User: jens
- PW: jenskohler


This image needs a standard MySQL or MariaDB database with

    User: root
    PW: jenskohler

and a database with name 'lportal'.

The following ports are exposed:
   
   - Tomcat 8080
   - Tomcat 8005
   - Tomcat 8009

If the containers are started for the first time, no additional configuration is required. 
In this case, the portal configuration page can be accessed at
    
    http://hostname:8080/liferay


Before the start of the containers, the following directories have to be created and
the respective files have to be extracted. 
These files just store the database and configuration files persistently. Furthermore, theses
files allow to change the configuration of the portal (or database) at runtime. 

    mkdir -p ${PWD}/persistent
    mkdir -p ${PWD}/mariadb_data

Extract the respective tar.gz archives into these directories

    tar -zxvf webapps.tar.gz -C ${PWD}/persistent/
    tar -zxvf mariadb_data.tar.gz -C ${PWD}/mariadb_data/ --strip-components=1




To start the container use:
    
    docker run --name my_mariadb -v ${PWD}/mariadb_data:/var/lib/mysql -p3306:3306 -e MYSQL_ROOT_PASSWORD=jenskohler -e -d finde/mariadb-liferay7

    docker run -it --link my_mariadb -v ${PWD}/persistent/webapps:/usr/local/tomcat/webapps -p8080:8080 -p8005:8005 -p8009:8009 finde/tomcat8-liferay7
    
   
    