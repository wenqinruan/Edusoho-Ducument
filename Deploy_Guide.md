Php hook script that can git pull, apc_clear_cache(), brew coffee etc

Intrigued to help a fellow developer and inspired by GitHub PHP webhook to auto-pull on repo push which I couldn’t get to work, I wrote my own gist.

Create a private/public SSH key pair, without passphrase.
Make sure the public key gets added in GitHub as a deploy key while the private key gets saved as /var/www/.ssh/id_rsa
With visudo insert “git ALL = (www-data) /usr/bin/git pull”.
Make www-data a part of the group that have access to the working tree.
Give www-data access to known_hosts by_ sudo touch /var/www/.ssh/known_hosts && sudo chown www-data /var/www/.ssh/known_hosts_
Update the known_hosts file by_ sudo -u www-data git pull_
Utilize the gist.
Update

Here is how I did it for a client recently.

Generate a new SSH key for Apache

su root
Create the folder

mkdir /var/www/.ssh
chmod 0700 /var/www/.ssh
chown -R www-data:www-data /var/www/.ssh
Create SSH key with an empty passphrase

su - www-data -c "ssh-keygen -t rsa"
chmod 0600 /var/www/.ssh/id_rsa
chmod 0600 /var/www/.ssh/id_rsa.pub
Add your SSH key to GitHub

help.github.com/articles/generating-ssh-keys#step-3-add-your-ssh-key-to-github

Make www-data a known_hosts file

touch /var/www/.ssh/known_hosts
chown www-data:www-data /var/www/.ssh/known_hosts
sudo -u www-data ssh github.com