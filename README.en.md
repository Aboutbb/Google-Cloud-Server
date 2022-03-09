**Змінити мову [Українська](README.md).**

Here is step-by-step instruction how to set up google virtual machine with 300$ free credits (you wont be charged after 300$ unless you manually subscribe to premium)

**phone and credit card needed!**

## Google cloud serivce:
1. Go to: https://cloud.google.com/
2. Login to your account (or create new account)
3. Press button **Get Started For Free**
4. Set up account (**phone and credit card needed!**) (*you can use number form here https://receive-smss.com/*)
5. Compute engine => VM instances
6. CREATE INSTANCE
- Region - any Europe
- Machine type - *e2-highcpu-8(8 vCPU, 8 GB memory)*
- Boot disk => Change 
- Operating system - *Ubuntu*
- Firewall 
	- *allow http*
	- *allow https*
- Keep rest default

7. Connect => Open in browser window

## 0. VM terminal:
input in terminal everything that goes after `$`

like:
- @instance-2:~$` sudo adduser apps`
- @instance-2:~/attacker$ `sudo git fetch`


## 1. Install Docker
     

    user@instance-2:~$ sudo adduser apps
    	-> Password:
    	-> ENTER x6
    user@instance-2:~$ sudo usermod -aG sudo apps
    user@instance-2:~$ su apps
    	-> Password:
    apps@instance-2:/home/user$ sudo ls // check
    [sudo] password for apps:
    apps@instance-2:/home/user$ exit
    user@instance-2:~$ su - apps
    	-> Password:
    apps@instance-2:~$ sudo ls
    apps@instance-2:~$ sudo apt-get -y update
    apps@instance-2:~$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    apps@instance-2:~$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    apps@instance-2:~$ sudo apt-get install -y docker-ce
    apps@instance-2:~$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    apps@instance-2:~$ sudo chmod +x /usr/local/bin/docker-compose
    apps@instance-2:~$ sudo usermod -aG docker $USER
    apps@instance-2:~$ exit
    user@instance-2:~$ su - apps
    	-> Password:
    apps@instance-2:~$ docker run hello-world
    	...
    	Hello from Docker!
    	This message shows that your installation appears to be working correctly.

## 2. Install git:

    user@instance-2:~$ sudo apt-get update
    user@instance-2:~$ sudo apt-get install git
    
## 3. Clone repo:

if there is not written `apps` before  `@`, login to `apps`:

    user@instance-2:~$ su apps
    	-> Password: 
	
if there is not written `/attacker` before  `user@instance-2:~`, change directory to `/attacker`:

    apps@instance-2:~$ cd attacker
		

Build containers and start the attack:

    apps@instance-2:~/attacker$ sudo git pull
    apps@instance-2:~/attacker$ docker-compose up --build --scale attacker=5


if this doesnt work, you may try to attack with Python:


# Attack with Python
## 1. Install python:

    apps@instance-2:~$ sudo apt update
    apps@instance-2:~$ sudo apt install software-properties-common
    apps@instance-2:~$ sudo add-apt-repository ppa:deadsnakes/ppa
    	-> ENTER
    apps@instance-2:~$ sudo apt install python3.8
    	-> Y
    apps@instance-2:~$ sudo apt install python3-pip

## 2. Prepare and attack:

    @instance-2:~$ cd attacker
    @instance-2:~/attacker$ pip3 install -r requirements.txt
    @instance-2:~/attacker$ sudo python3 attack.py 500

You can open more consoles to maximize output (but not more than 3:

if there is not written `apps` before  `@`, login to `apps`:

    user@instance-2:~$ su apps
    	-> Password: 
	
if there is not written `/attacker` before  `user@instance-2:~`, change directory to `/attacker`:

    apps@instance-2:~$ cd attacker
				
Start the attack:

    apps@instance-2:~/attacker$ sudo git pull
    apps@instance-2:~/attacker$ sudo python3 attack.py 500
    

# Leave it for a while. If progress stops:

	СTRL-C x2
    apps@instance-2:~/attacker$ sudo git pull
    	with docker-compose:
    apps@instance-2:~/attacker$ docker-compose up --build --scale attacker=5
    	or with python:
    apps@instance-2:~/attacker$ sudo python3 attack.py 500
    
if it doesnt react to `CTRL-C`

- Close the console
- Restart the machine:
	- three dots => `Stop` => wait till stop (1-3 min)
	- three dots => `Start/Resume`
- Open the console

# Starting the attack after exit:

	user@instance-2:~$ su apps
    	-> Password: 
    apps@instance-2:~$ cd attacker
    apps@instance-2:~/attacker$ sudo git pull
	
З docker-compose:

    apps@instance-2:~/attacker$ docker-compose up --build --scale attacker=5
	
З python:

    apps@instance-2:~/attacker$ sudo python3 attack.py 500
	
