# Where to access OpenStack?
Please refer to document https://gitlab.planetrover.ca/planetrover/knowledge/-/blob/master/onboarding/OpenStack.md
For regular usage of openstack

# What if something went wrong?
## Restart all the OpenStack services
login to the control plane server and restart all the services
```
> ssh li@192.168.5.56         #ask for password from sys admin
> sudo su stack
> cd /opt/stack/devstack
> ./restart_services.sh
```
## In case restart all the service won't work
### Back up the openstack database(login to the control plane as last step)
```
mysqldump -u root -p --all-databases > mysql.dump  ## Password is "supersecret"
```
**Download the mysql.dump to a safe place(e.g. your laptop)**
### Restore the control plane VM to a previous snap shot
Login to [VMware](https://192.168.5.100/ui/)
Ask system admin for username and password
Find the control plane VM and restore to the snap shot named "0524-2021-good"
![enter image description here](https://gitlab.planetrover.ca/planetrover/knowledge/-/raw/master/img/restore_snapshot.png)
### Restore the database contents
Upload the "mysql.dump" to the control plane VM and run following command
```
mysql -u root -p < mysql.dump
```
Now, the OpenStack should be back and working

## Change Openstack Quota for project
Examples
```
openstack quota set --cores 150 sequoiaDP
openstack quota set --ram 300000 sequoiaDP
```
