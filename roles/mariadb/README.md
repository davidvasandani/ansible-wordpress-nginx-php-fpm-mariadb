# MySQL Role
---

## Description

Installation and configuration of a MySQL server based upon a standardized configuration. The MySQL role will install all required RPMs and provide a standardized configuration for running a MySQL server. The MySQL role will also provide configuration management of the MySQL server.

## Requirements

The following are requirements for the server on which this role will be applied against.

* Access to the Warby Parker YUM repo.

## Playbook Usage

When making use of this role in a playbook, the best practice for obtaining the `mysql_root_new_password` value is to prompt for it with a private variable.

**Example:**

    vars_prompt:
      # This will reset the root password, this is used to secure the MySQL
      # instance.
      - name: "mysql_root_new_password"
        prompt: "Enter new MySQL root user password (optional)"
        private: yes

## Templates

The MySQL role contains a default set of configuration and provisioning tasks and templates used to establish a base setup.

As the need arises to parameterize the settings of the configuration file, the configurable values will be set as `defaults` and a variable placeholder will be added.

### Variables

* **`mysql_root_new_password`** - (String) New password to set for the root account
* **`mysql_ip`** - (String) IP address for the server to listen on
* **`mysql_port`** - (String) Service port for the server to listen on
* **`mysql_socket`** - (String) Unix socket location - absolute path to file
* **`mysql_server_id`** - (String) Server instance id - for replication
* **`innodb_buffer_pool_size`** - (String) The InnoDB buffer pool size
* **`innodb_data_file_path`** - (String) The InnoDB data file path
* **`install_dir`** - (String) Installation directory of MySQL

---
#### Notes

There's some tricky things here to allow this role to be idempotent. The trick is knowing that Ansible's `mysql_user` module will load a `~/.my.cnf` file if it finds one. As a result the playbook is structured with the following behavior:

* Upon the first run the installation of MySQL will provide a root user which by default has a blank password.
* Playbook's which utilize this role should prompt for the `mysql_root_new_password` variable. (See above)
* If left blank, the conditional task will not reset the MySQL root account user permissions, nor will it drop the `.my.cnf` file containing the credentials into the system `root` account (`/root/.my.cnf`).
* If a new password is set, then Ansible is able to use the credentials in the `.my.cnf` file to login to MySQL, update the password, and then update the `.my.cnf` file.
