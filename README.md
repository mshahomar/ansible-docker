# ansible-docker

### Assumption
This assumes your ansible master is running on CentOS or RHEL (or Amazon Linux)

### Usage
Execute this command:
<pre>
ansible-playbook main.yml
</pre>

Open this link on your browser: http://localhost


## Explanation
<pre>
├── docker
│   └── Dockerfile
└── main.yml
</pre>

### Docker
The directory docker contains a Dockerfile, which uses a base image of nginx (I use Nginx 1.15, this can be changed to :latest).  
This Dockerfile uses a root account to perform any command which requires privilege (i.e. to overwrite the /usr/share/nginx/html/index.html). 
It exposes TCP port 80 and finally the CMD runs nginx with a global directive "daemon off" to ensure Nginx runs in the foreground.

### Ansible
The main.yml is used by ansible playbook. It uses localhost as its host and to ensure that any tasks which require a root privilege, we use become and become_method. 

For the first two tasks, ansible will install pre-requisite package - PIP and docker-py from PIP package.

Third task will build a docker image using the Dockerfile in this path: docker/Dockerfile. The result will be a docker image named 'web-nginx'.

Fourth task will run docker-container with the name 'web-nginx' exposing TCP port 80 on host and port 80 on the docker container. To ensure that nginx server will always be available, we define the 'restart_policy' to 'always'.


