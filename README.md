
The goal of the project was to set up and configure a Linux server to host an app that I had made. To do this an instance of an Ubuntu system was created using Amazon's Lightsail service. Once the Linux server was created, it was then configured to serve a Python app that used the Flask framework.

i. The public IP address for my lightsail instance is 54.245.49.118. SSH is set up to use port 2200.

ii. A Domain has not been registered, so the complete URL to my hosted web app is simply the public IP as stated in the previous point.


iii. Software installed:
        -To run the app Nginx, Gunicorn, PostgreSQL, Python and Flask were used on an Ubuntu operating system.
        -For a web server Nginx was chosen and installed.
        -Gunicorn was used in conjunction with Nginx to provide the ability to handle larger traffic loads than a Flask app can handle on it's own. PostgreSQL was the database used for this app. After postgreSQGL installation, the users and a database were created. SQLite was used during development, so a few modifications to the app and its setup files were necessary to allow for a connection to a PostgreSQL database rather than an SQLite database.
        -Last, but not least, Python and Flask were used to create the app.
    Configuration:
        -Update/upgrade any files:
            sudo apt-get update
            sudo apt-get upgrade
            sudo apt-get autoremove
        -Create users and grant sudo power:
            sudo adduser <user>
            sudo usermod -aG sudo <user>
        -Create .ssh/authorized_keys file and paste in the corresponding public key for each user. Key pairs generated locally
            ssh-keygen
        -Configure and enable firewall:
            sudo ufw default deny incoming
            sudo ufw default allow outgoing
            sudo ufw allow ssh
            sudo ufw allow www
            sudo ufw allow ntp
            sudo ufw enable
        -Install PostgreSQL, create users and database:
            sudo -i -u postgres
            psql
            CREATE USER <user> WITH PASSWORD '<password>';
            CREATE DATABASE <database> WITH OWNER <owner>;
        -Grant user that will be used by grader limited permissions to database:
            GRANT SELECT, INSERT, UPDATE, DELETE PRIVILEGES ON category TO grader;
            GRANT SELECT, INSERT, UPDATE, DELETE PRIVILEGES ON item TO grader;
            GRANT SELECT, INSERT, UPDATE, DELETE PRIVILEGES ON user TO grader;
iv. Third Party Resources:
    Many tutorials and forums were read in the process of setting up this Linux server to serve my web app. I had initially attempted to set up my system to run Apache -> mod_wsgi -> Python/Flask, but could not get it to run. After many, many different attempts and approaches with that set up I decided to try Nginx -> Gunicorn -> Python/Flask.
    This is the most influential source:
        https://realpython.com/blog/python/kickstarting-flask-on-ubuntu-setup-and-deployment/#add-a-new-user
    I adopted their approach and configured my system using nginx, gunicorn, python/flask, and supervisor.
    The other sources I learned from/used:
        Nginx/Gunicorn/Python/Flask:
            https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-gunicorn-and-nginx-on-ubuntu-16-04
        Apache/mod_wsgi/Python/Flask:
            https://stackoverflow.com/questions/30674644/installing-mod-wsgi-for-python3-on-ubuntu/30682386#3068238
            https://stackoverflow.com/questions/30642894/getting-flask-to-use-python3-apache-mod-wsgi
            https://www.jakowicz.com/flask-apache-wsgi/
            http://terokarvinen.com/2016/deploy-flask-python3-on-apache2-ubuntu
            https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
        Apache/Gunicorn/systemd/Python/Flask:
            https://www.vioan.eu/blog/2016/10/10/deploy-your-flask-python-app-on-ubuntu-with-apache-gunicorn-and-systemd/
        Nginx/Gunicorn/Python/Flask (using WSGI):
            https://www.digitalocean.com/community/tutorials/how-to-deploy-python-wsgi-apps-using-gunicorn-http-server-behind-nginx#glossary
