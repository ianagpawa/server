Create a new GitHub repository and add a file named README.md.
Your README.md file should include all of the following:

i. The IP address and SSH port so your server can be accessed by the reviewer.

ii. The complete URL to your hosted web application.

iii. A summary of software you installed and configuration changes made.

iv. A list of any third-party resources you made use of to complete this project.

Open your ~/.ssh/udacity_key.rsa file in a text editor and copy the contents of that file.
During the submission process, paste the contents of the udacity_key.rsa file into the "Notes to Reviewer" field.
# Linux Server Configuration
### By Ian Agpawa
##### This repo is for my Linux server configuration project from Udacity's Full Stack Web Developer Nanodegree course.  The project used is my item catalog project from the same course.  The git repo of that project is located here: `https://github.com/ianagpawa/catalog.git`   


## Address and Port

####IP ADDRESS:
`35.165.176.112`
####SSH Port:   
`2200`

## Complete URL
```
http://ec2-35-165-176-112.us-west-2.compute.amazonaws.com
```


## Installed software and configuration changes

####Software Installed:
`finger`
`apache2`
`libapache2-mod-wsgi`
`python-dev`
`postgresql`
`git`
`python-pip`
`virtualenv`
`Flask`
`python-psycopg2`
`python-flask`
`python-sqlalchemy`
`oauth1client`
`requests`
`httplib2`
`flask-seasurf`

####Configuration changes
1. Changed local timezone to UTC
2. Configured UFW to only allow SSH (port 2200), HTTP (port 80), and NTP (port 123).
3. Configured and enabled new virtual host.  The following changes were made to `/etc/apache2/sites-available/catalog.conf `

`ServerName 35.165.176.112`
`ServerAlias ec2-35-165-176-112.us-west-2.compute.amazonaws.com`
`ServerAdmin grader@35.165.176.112`
`WSGIScriptAlias / /var/www/catalog/catalog.wsgi`
`<Directory /var/www/catalog/catalog/>`
`Alias /static /var/www/catalog/catalog/static`
`<Directory /var/www/catalog/catalog/static/>`

4. Modified `/var/www/catalog/catalog.wsgi` with the following lines:
`sys.path.insert(0,"/var/www/catalog/")`
`from catalog import app as application`

5. Confirm PostgreSQL (file: `/etc/postgresql/9.3/main/pg_hba.conf`) does not allow remote connections (default settings).

6. Configure PostgreSQL:
-Create Database `catalog`
-Create User `catalog` and grant permission to database

7. Modified the following line in `main.py`, `db_setup.py`, and `loadsongs.py`, where `PASSWORD` is replaced by the password for PostgreSQL user `catalog`:
```
engine = create_engine('postgresql://catalog:PASSWORD@localhost/catalog')
```


## Third-party resources
