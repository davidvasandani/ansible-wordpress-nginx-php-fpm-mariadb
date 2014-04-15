1. [Install Vagrant](http://www.vagrantup.com/)
2. [Install Ansible](http://docs.ansible.com/intro_installation.html)
3. Clone this repo
4. <code>cd ansible-wordpress-nginx-php-fpm-mariadb</code>
5. Run the following command:<br><code>ansible-playbook -i vagrant.hosts play_wordpress.yml -vv --extra-vars "vagrant=true"</code>
6. Add the following to your host file.<br><code>192.168.203.20  blog.you-local.com newblog.qa.blog.you-local.com newblog.blog.you-local.com</code>

Browse to http://blog.you-local.com/wp-admin/<br>
Login. Username: user Password: password
