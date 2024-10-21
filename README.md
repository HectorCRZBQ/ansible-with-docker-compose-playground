# A playground to test Ansible with Docker Compose & Ubuntu

## Actions in the Host machine:

Launch containers
```bash
docker-compose up -d
```

![alt text](/images/image1.png)

Jump to the control node from host machine
```bash
docker-compose exec control bash
```

![alt text](/images/image2.png)

Cleanup
```bash
docker compose down

![alt text](/images/image3.png)
```

# Inside control node

Install ansible
```bash
sudo apt update
sudo apt-get install nano
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get install ansible
```

Setup ansible
```bash
sudo nano /etc/ansible/hosts
```

Content of host the file:
```
[servers]
server1 ansible_host=node1
server2 ansible_host=node2
server3 ansible_host=node3

[all:vars]
ansible_connection=ssh
ansible_user=root
ansible_ssh_pass=password
ansible_python_interpreter=/usr/bin/python3
```

Test conectivity

```bash
ansible-inventory --list -y
```

![alt text](/images/image4.png)

```bash
ansible all -m ping -u root
```

Sin haber conectado el nodo

![alt text](/images/image5.png)

Tras haber conectado el nodo.

![alt text](/images/image10.png)

```bash
ansible all -a "df -h" -u root
```

Sin haber conectado el nodo

![alt text](/images/image6.png)

Tras haber conectado el nodo.

![alt text](/images/image11.png)



Connect with nodes (ssh password is "password" without quotes):
```bash
ssh root@node1
```

![alt text](/images/image7.png)

```bash
ssh root@node2
```

![alt text](/images/image8.png)

```bash
ssh root@node3
```

![alt text](/images/image9.png)

Shared folder between host machine and control node:
```bash
cd /shared
```

We ejecute the yml with the tasks
```bash
ansible-playbook /shared/recipe-base.yml
```

![alt text](/images/image12.png)
![alt text](/images/image13.png)

We verify the conectivity of the nodes and ansible
```bash
ansible all -m setup -a 'filter=ansible_default_ipv4'
```

![alt text](/images/image14.png)

We test some examples inside a web explorer

---

Node 1 / Server 1

 - Port 7001: http://localhost:7001
  ![alt text](/images/image15.png)

 - Port 7002: http://localhost:7002
  ![alt text](/images/image16.png)

 - Port 7003: http://localhost:7003
  ![alt text](/images/image17.png)

---

Node 2 / Server 2

 - Port 8001: http://localhost:8001
   ![alt text](/images/image18.png)

 - Port 8002: http://localhost:8002
   ![alt text](/images/image19.png)

 - Port 8003: http://localhost:8003
   ![alt text](/images/image20.png)

---

Node 3 / Server 3

 - Port 9001: http://localhost:9001
   ![alt text](/images/image21.png)

 - Port 9002: http://localhost:9002
   ![alt text](/images/image22.png)

 - Port 9003: http://localhost:9003
   ![alt text](/images/image23.png)


# Other terminal

We assure that all containers are Up
```bash
docker ps
```
![alt text](/images/image24.png)


And thats all!!

### **Autor**: [HectorCRZBQ](https://github.com/HectorCRZBQ)

