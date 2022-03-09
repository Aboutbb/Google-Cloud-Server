**Change language [English](README.en.md).**

Покрокова інструкція як створити віртуальну машину google з безоплатним пробним періодом у 300$ (після 300$ гроші не зніматиме якщо не купляти підписку преміум)

**Потрібно буде вказати номер телефону та кредитну карточку** 

## Google cloud serivce:
1. Передйди: https://cloud.google.com/
2. Залогінся в свій акаунт (або створи новий)
3. Нажми **Get Started For Free**
4. Зареєструйся (**Потрібно буде вказати номер телефону та кредитну карточку**) (*номер можна взяти тут https://receive-smss.com/*)
5. Compute engine => VM instances
6. CREATE INSTANCE
	- Region - будь-який з Europe
	- Machine type - *e2-highcpu-8(8 vCPU, 8 GB memory)*
	- Boot disk => Change 
	 - - Operating system - *Ubuntu*
	
	
	- Firewall 
	 - - *allow http*
	 - - *allow https*
	- Keep rest default

7. Connect => Open in browser window

## 0. VM terminal:
Пиши в термінал все що після `$`

Наприклад:
- @instance-2:~$`sudo adduser apps`
- @instance-2:~/attacker$ `sudo git fetch`

Ці команди ще не пиши

## 1. Install Docker
     

    user@instance-2:~$ sudo adduser apps
    	-> Password:
    	-> ENTER x6
    user@instance-2:~$ sudo usermod -aG sudo apps
    user@instance-2:~$ su apps
    	-> Password:
    apps@instance-2:/home/user$ sudo ls
    	-> Password for apps:
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


    apps@instance-2:~$ sudo apt-get update
    apps@instance-2:~$ sudo apt-get install git
    
## 3. Clone repo:

	apps@instance-2:~$ exit
    user@instance-2:~$ su apps
		-> Password:
    apps@instance-2:~$ sudo git clone https://github.com/Luzhnuy/attacker.git
    
# Атакуєм з Docker-Compose:
якщо перед `@` не пише `apps`, заходим в `apps`:

    user@instance-2:~$ su apps
    	-> Password: 

Будуєм контейнери і атакуєм:

    apps@instance-2:~$ cd attacker
    apps@instance-2:~/attacker$ sudo git pull
    apps@instance-2:~/attacker$ docker-compose up --build --scale attacker=5


Якщо не виходить можете попробувати атакувати з Python

# Атакуєм з Python:
## 1. Install Python:


    apps@instance-2:~$ sudo apt update
    apps@instance-2:~$ sudo apt install software-properties-common
    apps@instance-2:~$ sudo add-apt-repository ppa:deadsnakes/ppa
    	-> ENTER
    apps@instance-2:~$ sudo apt install python3.8
    	-> Y
    apps@instance-2:~$ sudo apt install python3-pip


## 2. Prepare and attack:

 
    apps@instance-2:~$ cd attacker
    apps@instance-2:~/attacker$ pip3 install -r requirements.txt
    apps@instance-2:~/attacker$ sudo python3 attack.py 500
    

##
Залишаєте на певний час, якщо побачити що більше не атакується:

	СTRL-C
    apps@instance-2:~$ cd attacker
    apps@instance-2:~/attacker$ sudo git pull
    apps@instance-2:~/attacker$ sudo python3 attack.py 500


Можете відкривати декілька консолей щоб збільшити навантаження (не більше 3):
якщо перед `@` не пише `apps`, заходим в `apps`:

    user@instance-2:~$ su apps
    	-> Password: 
		
запускаєм атаку з python

    apps@instance-2:~$ cd attacker
    apps@instance-2:~/attacker$ sudo git pull
    apps@instance-2:~/attacker$ sudo python3 attack.py 500
