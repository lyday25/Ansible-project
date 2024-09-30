
## RUN ON ANSIBLE CONTROLLER
ansible-playbook -i inventory startnginx.yaml

## RUN THIS ON TARGET MACHINES

sudo systemctl status nginx
curl localhost nginx

## TO RUN ANSIBLE PLAYBOOK ON CONTROLLER
ansible-playbook -i inventory name of file to run

## STOP the service
ansible-playbook -i inventory stopnginx.yaml

## To kill all the running process on the port 80

sudo apt-get install psmisc

 sudo fuser 80/tcp sudo lsof -i tcp:80 

sudo lsof -i tcp:80 -s tcp:listen 

sudo lsof -t -i tcp:80 -s tcp:listen | sudo xargs kill


=====

## To purge apache2

sudo apt-get purge apache2

## now run the ansible installation for apache 2


## And now run the 

sudo systemctl status apache2.service

# Troubleshooting

sudo journalctl -u apache2

