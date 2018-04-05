# fsnd-linux-setup

### IP, URL

http://18.197.34.81/
http://acidninja.com/

For the google oauth to work correctly please use http://acidninja.com/

### SOFTWARE INSTALLED

- apache2
- libapache2-mod-wsgi
- postgresql
- pipenv
- virtualenv

### LIST OF CONFIGURATIONS MADE

##### SSH SETUP

- create two key pairs locally: linux_setup_main and linux_setup_grader with ssh-keygen. One for myself and for the 'grader' account
- install public keys for user ubuntu and grader
- remove default lightsail public key
 
- change ssh port in `/etc/sshd/sshd_config` from 22 to 2200
- set `PermitRootLogin no` to disallow remote root login
- set `PasswordAuthentication no` to force key-based authentication

### AWS FIREWALL (from web interface)

 - add rule to allow 2200/tcp connections for ssh
 - remove rule allowing connections on port 22/tcp
 - add rule for 123/udp connections for ndp
 
 
### UFW SETUP
- `sudo ufw default deny incoming` - block all incoming traffic by default
- `sudo ufw default allow outgoing` -  allow all outgoing traffic by default
- `sudo ufw allow 2200/tcp` - allow custom 2200 port over tcp for ssh connections
- `sudo ufw allow www` - allow 80 port over tcp for www connections
- `sudo ufw allow 123/udp` - allow 123 port over udp for ndp connections

### FIX THE PROBLEM WITH PERL LOCALES (IT WOULD INTERFER WITH POSTGRESQL INSTALL)

- `sudo apt-get install language-pack-pl-base`
- `sudo dpkg-reconfigure locales`

### PIPENV AND VIRTUALENV

- add commands to `app.wsgi` file to activate virtual environment
- set permissions for `activate_this.py` and all the folders above so apache can run this file

## SET ENVIRONMENT VARIABLES WITH `SetEnv`

- set variables with `SetEnv` in configuration file `/etc/apache2/sites-available/test_catalog.conf`
- use those variables in wsgi file when defining application

### GOOGLE OAUTH

- create a static ip for my instance
- point a domain at the ip
- add domain urls to google allowed redirect addresses
- make path to `client_secrets.json` absolute (why is this needed?)

### DATABASE SETUP

 - `create role catalog with login password 'catalog';` - create a role 'catalog'
 - `grant select, update, insert, delete on all tables in schema public to catalog;` - set needed permissions
 - `grant usage, select on all sequences in schema public to catalog` - set needed permissions
