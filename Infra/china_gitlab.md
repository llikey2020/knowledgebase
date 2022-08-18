# Current status of China CI/CD setup

## k8s cluster for running gitlab runners
|Server|Role  |username|password|
|--|--|--|--|
|192.168.9.201|Master|root|sequoiadb  |
|192.168.9.202|worker1|root|sequoiadb  |
|192.168.9.203|worker2|root|sequoiadb  |

### Note
I noticed after the server is rebooted, the network between these hosts might become unavailable. please run command to fix the cluster issues
```
systemctl  stop firewalld
swapoff -a
```


### Deploy gitlab runner on k8s cluster
use a config file with following contents

https://gitlab.planetrover.ca/planetrover/knowledge/-/blob/master/files/values.yaml

make sure replace the parameters in lines 68, 74

Run following command to deploy the gitlab runner

```
helm upgrade --install  --namespace gitlab-runner gitlab-runner -f values.yaml gitlab/gitlab-runner
```
Now go to the gitlab admin console, you should see the gitlab runner has connected to the system
Make the runner shared so that other projects can utilize it.


# Run a hello world gitlab ci job

In order to run CI jobs for a project, first create a file in the root directory named "**.gitlab-ci.yml**"
An example of the contents for this file:

```
build-job:
  stage: build
  script:
    - echo "Hello, $GITLAB_USER_LOGIN!"

test-job1:
  stage: test
  script:
    - echo "This job tests something"

test-job2:
  stage: test
  script:
    - echo "This job tests something, but takes more time than test-job1."
    - echo "After the echo commands complete, it runs the sleep command for 20 seconds"
    - echo "which simulates a test that runs 20 seconds longer than test-job1"
    - sleep 20
```

After commit this file, the gitlab ci should be triggered.

For the syntax of the ci file, please refer to https://gitlab.planetrover.ca/help/ci/quick_start/index.md



# What's missing?

Now the **k8s, gitlab runner, and gitlab have already been setup** in China internal network. However, since the China gitlab is 3 major versions behind Toronto gitlab, all the Toronto .gitlab-ci.yml scripts are not compatable in China gitlab.

To solve this, we need to upgrade the China gitlab to v14.5.2

