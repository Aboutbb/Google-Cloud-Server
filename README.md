Here is step-by-step instruction how to set up google virtual machine with 300$ free credits (with this settings enough for 1.5 month)

**phone and credit card needed!**

Dont Forget to unsubscribe after war is over!!!

## Google cloud serivce:
1. Go to: https://cloud.google.com/
2. Login to your account (or create new account)
3. Press button **Get Started For Free**
4. Set up account (**phone and credit card needed!**)
5. Compute engine => VM instances
6. CREATE INSTANCE
	- Region - any Europe
	- Machine type - *e2-highcpu-8(8 vCPU, 8 GB memory)*
	- Boot disk => Change 
	- Operating system - *Ubuntu*
	- Firewall 
	 - - *allow http*
	 - - *allow https*
	- Keep rest default

7. Connect => Open in browser window

## 0. VM terminal:
input in terminal everything that goes after `$`

like:
- @instance-2:~$`sudo adduser apps`
- @instance-2:~/attacker$ `sudo git fetch`

Dont use this commands yet!

## 1. Install Docker
     

    user@instance-2:~$ sudo adduser apps
    	-> ENTER x6
    user@instance-2:~$ sudo usermod -aG sudo apps
    user@instance-2:~$ su apps
    	-> Password:
    apps@instance-2:/home/user$ sudo ls
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

## 3. Install python:


    @instance-2:~$ sudo apt update
    @instance-2:~$ sudo apt install software-properties-common
    @instance-2:~$ sudo add-apt-repository ppa:deadsnakes/ppa
    	-> ENTER
    @instance-2:~$ sudo apt install python3.8
    	-> Y
    @instance-2:~$ sudo apt install python3-pip

## 4. Clone repo:


    @instance-2:~$ su apps
    @instance-2:~$ apps@instance-2:~$ sudo git clone https://github.com/Luzhnuy/attacker.git

## 5. Prepare and attack:

    

    @instance-2:~$ cd attacker
    @instance-2:~/attacker$ pip3 install -r requirements.txt
    @instance-2:~/attacker$ sudo python3 attack.py 500

## After exit:


    @instance-2:~$ cd attacker
    @instance-2:~/attacker$ sudo git fetch
    @instance-2:~/attacker$ sudo python3 attack.py 500
