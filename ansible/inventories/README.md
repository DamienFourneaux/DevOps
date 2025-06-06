3.1

This inventory is here to connect directly to our server (damien.fourneaux.takima.cloud), seraching our key (beaucse we are giving the path for the ssh key).

The first command we use (ansible ping) is here to try the connection we try to establish with the server (it respond with a pong if ythe connection is succesful). In my case, it didn't work because the server was closed (due to too much time of my part).

The second command (ansible setup) is used to determine the Linux distribution running on each remote server.

The third and last command (ansible apt) instructs Ansible to connect to each machine listed in the inventories/setup.yml file, then invoke the apt module to remove the apache2 package with elevated (root) privileges.