
# Current status of China CI/CD setup

## k8s cluster for running gitlab runners
|Server|Role  |username|password|
|--|--|--|--|
|192.168.9.201|Master|root|sequoiadb  |
|192.168.9.202|worker1|root|sequoiadb  |
|192.168.9.203|worker2|root|sequoiadb  |
### Note
After the server is rebooted, the network between these hosts might become unavailable. please run command to fix the cluster issues
```
systemctl  stop firewalld
swapoff -a
```
**The gitlab runner is already setup and connected to gitlab.sequoiadb.com
Once the China gitlab is upgraded to the same version as Toronto gitlab, it should be able to run all the gitlab_ci scripts**

