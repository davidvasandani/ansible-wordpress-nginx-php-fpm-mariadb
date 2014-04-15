1. [Install Vagrant](http://www.vagrantup.com/)
2. [Install Ansible](http://docs.ansible.com/intro_installation.html)
3. Clone this repo
4. cd into ansible-wordpress-nginx-php-fpm-mariadb directory
5. Run the following command:
    ansible-playbook -i vagrant.hosts play_wordpress.yml -vv --extra-vars "vagrant=true"
6. Add the following to your host file.
    192.168.203.20  blog.you-local.com newblog.qa.blog.you-local.com newblog.blog.you-local.com

# Browse to http://blog.you-local.com/wp-admin/
# Login. Username: user Password: password
