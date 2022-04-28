In order to use openstack to create your VMs for development and testing. Please go to  [link](http://cloud.torlab/dashboard/) (Please contact Li Liu for account creation)

# Login to the OpenStack
## login
[Login Portal](http://cloud.torlab/dashboard/project/instances/)
Use the provided username and password to login to the system. After login you should see panel as following:
![](https://gitlab.planetrover.ca/planetrover/knowledge/-/raw/master/img/after_login.png)
## Switch between projects
Click on the drop down list on the top left corner to switch between projects(You will likely be resided in the default project "sequoiaDP").

# Start VMs
Note: If there is not enough quota to start vms, please contact IT
- Click on the "Launch Instance" buttom.

![](https://gitlab.planetrover.ca/planetrover/knowledge/-/raw/master/img/launch_instance.png)

- In "Details" tab, fill in your instance name and number of VM you willing to create

![](https://gitlab.planetrover.ca/planetrover/knowledge/-/raw/master/img/instance_name.png)

- In "Source" tab, click "No" for "Craete New Volumn" option. Select the OS image you willing to use(e.g. centos7)

![](https://gitlab.planetrover.ca/planetrover/knowledge/-/raw/master/img/source_page.png)

- In "Flavor" tab, select the size of VM you want to create(e.g. m1.medium)

![](https://gitlab.planetrover.ca/planetrover/knowledge/-/raw/master/img/flavor_page.png)

- In "Key Pair" tab, if you don't have a key pair created. Please click on "Create Key Pair" buttom.

![](https://gitlab.planetrover.ca/planetrover/knowledge/-/raw/master/img/keypair.png)

- Fillin your key pair name and select "SSH Key" as the Key type. then click on "Create Keypair". Make sure you save the text from the box in a file on your local machine as a file name "key_pair_name.pem"

![](https://gitlab.planetrover.ca/planetrover/knowledge/-/raw/master/img/keypair3.png)

- Click on "Launch Intances" at right bottom corner. your VM should be starting now

- When you VM is starting, click on "Assiciate Floating IP" from the drop down list to assign a floating ip to it. This ip will the used to access the VM from outside

![](https://gitlab.planetrover.ca/planetrover/knowledge/-/raw/master/img/floating_ip.png)





