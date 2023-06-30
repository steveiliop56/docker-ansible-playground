## Docker ansible playground

A simple and easy to set up ansible playground for deploying your playbooks on docker *"sevrers"*.

### Requirements

To begin with, you will need to have installed ``docker`` and ``docker-compose`` on your computer. You can install them with these commands:

``` Shellscript
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
rm -rf get-docker.sh
sudo apt install docker-compose -y
```

You will also need to have the command ``ssh-keygen`` available.

### Building

First you will need to build the 2 images required for the playground. The process is easy and fast.

- 1. Firstly generate the public and private ssh keys that are required to access your *"servers"*. You cand do this with this command:

``` Shellscript
ssh-keygen
```

When it prompts you to enter location and your current working direcotry. If you are on linux you can see it with this command ```pwd```.
Then it will ask you for passphrase just press enter as it is not needed.

- 2. Secondly you will need to build the node image with this command:

```Shellscript
sudo docker build -t steveiliop56/ansible-node Dockerfile-node
```

If your computer is fast it will take a minute or so.

- 3. Thirdly you will need to build the host image with this command:

```Shellscript
sudo docker build -t steveiliop56/ansible-host
```

This will take even less time.

### Running

Now it's time to run the docker-compose file with this command:

```Shellscript
sudo docker-compose up
```

This will create a vlan for your *"servers"* and your host and then create the containers.

To access the host you will need to type this command:

```Shellscript
sudo docker exec -it ansible-host bash
```

This will pop up a bash shell inside the container. Then it's time to create some magic with ansible.

The *"server"* nodes are:

```
Name: asnible-node1 Hostname: ansible-node1.local IP: 10.0.0.2
Name: ansible-node2 Hostname: ansible-node2.local IP: 10.0.0.3
```

And the host node is:

```
Name: ansible-host Hostname: asnible-host.local IP: 10.0.0.1
```

**Info:** When running your playbook make sure you are in the ``/root/`` direcotry because there are the ssh keys to access the *"server"* nodes. Morover the ``ansible-node1`` has the port 8081 exposed and mapped to the internal port 80 and the ``ansible-node2`` has the port 8082 exposed mapped to port 80 for creating web server projects with ansible.





