# Linux Server Configuration
### By Ian Agpawa
##### This repo is for my Linux server configuration project from Udacity's Full Stack Web Developer Nanodegree course.  The project used is my item catalog project from the same course.  The git repo of that project is located here: `https://github.com/ianagpawa/catalog.git`   


## Address and Port

####IP ADDRESS:
`35.165.176.112`
####SSH Port:   
`2200`

### Complete URL
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
1. Add user `grader` and grant sudo permissions:
    * Create file `/etc/sudoers.d/grader` and add the following line:
```
grader ALL=(ALL:ALL) ALL
```
2. Modify file `/etc/ssh/sshd_config` to only allow SSH (only via port 2200) and deny root access:
    * ```
    # What ports, IPs and protocols we listen for
    Port 2200
    ```
    * ```
    # Authentication:
    LoginGraceTime 120
    PermitRootLogin no
    ```
    * ```
    # Change to no to disable tunnelled clear text passwords
    PasswordAuthentication no
    ```
    * ```
    UsePAM yes
    AllowUsers grader
    ```

3. Configured UFW to only allow SSH (port 2200), HTTP (port 80), and NTP (port 123)

4. Changed local timezone to UTC

5. Configured and enabled new virtual host.  The following changes were made to `/etc/apache2/sites-available/catalog.conf `:


    * `ServerName 35.165.176.112`
    * `ServerAlias ec2-35-165-176-112.us-west-2.compute.amazonaws.com`
    * `ServerAdmin grader@35.165.176.112`
    * `WSGIScriptAlias / /var/www/catalog/catalog.wsgi`
    * `<Directory /var/www/catalog/catalog/>`
    * `Alias /static /var/www/catalog/catalog/static`
    * `<Directory /var/www/catalog/catalog/static/>`


6. Modified `/var/www/catalog/catalog.wsgi` with the following lines:
    * `sys.path.insert(0,"/var/www/catalog/")`
    * `from catalog import app as application`

7. Confirm PostgreSQL (file: `/etc/postgresql/9.3/main/pg_hba.conf`) does not allow remote connections (default settings).

8. Configure PostgreSQL:
    * Create Database `catalog`
    * Create User `catalog` and grant permission to database

9. Modified the following line in `main.py`, `db_setup.py`, and `loadsongs.py`, where `PASSWORD` is replaced by the password for PostgreSQL user `catalog`:
```
engine = create_engine('postgresql://catalog:PASSWORD@localhost/catalog')
```
10. File `main.py` was renamed to `__init__.py`.


## Third-party resources
* [Digital Ocean - Deploy Flask App](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)

* [Stack Overflow - make .git directory inaccessible ](http://stackoverflow.com/questions/6142437/make-git-directory-web-inaccessible)

* [Ubuntu - Change timezone to UTC](http://askubuntu.com/questions/138423/how-do-i-change-my-timezone-to-utc-gmt)

* [Ubuntu - Configure UFW](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-14-04)


## Creator

**Ian Agpawa**

[Github](https://github.com/ianagpawa)

agpawaji@gmail.com
