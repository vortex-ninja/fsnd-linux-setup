# fsnd-linux-setup

List of configurations made:

### SSH SETUP

- create two key pairs locally: linux_setup_main and linux_setup_grader with ssh-keygen. One for myself and for the 'grader' account.
- install public key (linux_setup_main) for user ubuntu.
- remove default lightsail public key
 
- change ssh port in /etc/sshd/sshd_config from 22 to 2200
- update aws firewall to accept tcp connections on 2200 and block on 22

### AWS FIREWALL (from web interface)

 - add rule to allow 2200/tcp connections for ssh
 - remove rule allowing connections on port 22/tcp
 - add rule for 123/udp connections for ndp
 
 
### UFW SETUP
- sudo ufw default deny incoming: block all incoming traffic by default
- sudo ufw default allow outgoing: allow all outgoing traffic by default
- sudo ufw allow 2200/tcp: allow custom 2200 port over tcp for ssh connections
- sudo ufw allow www: allow 80 port over tcp for www connections
- sudo ufw allow 123/udp: allow 123 port over udp for ndp connections

### FIX THE PROBLEM WITH PERL LOCALES (IT WOULD INTERFER WITH POSTGRESQL INSTALL)

- sudo apt-get install language-pack-pl-base
- sudo dpkg-reconfigure locales
