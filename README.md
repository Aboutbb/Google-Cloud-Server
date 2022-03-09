**Change language [English](README.en.md).**

Покрокова інструкція як створити віртуальну машину google з безоплатним пробним періодом у 300$ (після 300$ гроші не зніматиме якщо не купляти підписку преміум)

**Потрібно буде вказати номер телефону та кредитну карточку** 

## Google cloud serivce:
1. Передйди: https://cloud.google.com/!
2. Залогінся в свій акаунт (або створи новий)
3. Нажми **Get Started For Free**
4. Зареєструйся (**Потрібно буде вказати номер телефону та кредитну карточку**) (*номер можна взяти тут https://receive-smss.com/*)
> 5. Compute engine => VM instances 
>> ![photo_2022-03-01_13-36-13 - Copy](https://user-images.githubusercontent.com/98760727/157469549-dd85283d-26dc-4b70-940c-88d32f28080b.jpg)

> 6. CREATE INSTANCE
>> ![photo_2022-03-01_13-36-15 - Copy](https://user-images.githubusercontent.com/98760727/157469573-e372ad5b-e8ef-48ce-815a-f50f81678858.jpg)
> - Region - будь-який з Europe
> - Machine type - *e2-highcpu-8(8 vCPU, 8 GB memory)*
>> ![photo_2022-03-01_13-36-16 - Copy](https://user-images.githubusercontent.com/98760727/157469599-584882e3-497d-4ed4-8b12-49c6d192dc17.jpg)
> - Boot disk => Change 
>> ![photo_2022-03-01_13-36-17 - Copy](https://user-images.githubusercontent.com/98760727/157469618-0e539d2f-41ad-40dc-a6af-eeb62dbaf0a1.jpg)
>> - Operating system - *Ubuntu*
>>> ![photo_2022-03-01_13-36-18 - Copy](https://user-images.githubusercontent.com/98760727/157469648-17521ca3-60f9-4551-9a23-1827df39c83f.jpg)
>- Firewall 
	- *allow http*
	- *allow https*
>> ![photo_2022-03-01_13-36-19 - Copy](https://user-images.githubusercontent.com/98760727/157469677-c782156a-0fde-439f-931e-745547c732eb.jpg)
> - Все решту не змінюєм

> 7. Connect => Open in browser window
>> ![photo_2022-03-01_13-36-20 - Copy](https://user-images.githubusercontent.com/98760727/157469700-3912dbcd-1438-47ee-984f-d459b639c12d.jpg)

## 0. VM terminal:
Пиши в термінал все що після `$`

Наприклад:
- @instance-2:~$ `sudo adduser apps`
- @instance-2:~/attacker$ `sudo git fetch`


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
	
якщо після `user@instance-2:~` не пише `/attacker`, заходим в `/attacker`:

    apps@instance-2:~$ cd attacker
		

Будуєм контейнери і атакуєм:

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
    
Можете відкривати декілька консолей щоб збільшити навантаження (не більше 3):

якщо перед `@` не пише `apps`, заходим в `apps`:

    user@instance-2:~$ su apps
    	-> Password: 
	
якщо після `user@instance-2:~` не пише `/attacker`, заходим в `/attacker`:

    apps@instance-2:~$ cd attacker
		
запускаєм атаку з python:

    apps@instance-2:~/attacker$ sudo git pull
    apps@instance-2:~/attacker$ sudo python3 attack.py 500
    

# Залишаєте на певний час, якщо побачити що більше не атакується:

		СTRL-C x2
    apps@instance-2:~/attacker$ sudo git pull
    	якщо docker-compose:
    apps@instance-2:~/attacker$ docker-compose up --build --scale attacker=5
    	якщо python:
    apps@instance-2:~/attacker$ sudo python3 attack.py 500
    
Якщо немає реакції на `CTRL-C`

- Закриваєм консоль
- Перезапускаєм серевер:
	- три крапки => `Stop` => чекаєм поки зупиниться (1-3 хв)
	- три крапки => `Start/Resume`
- Відкриваєм консоль

# Щоб почати атаку занову після виходу з консолі:

	user@instance-2:~$ su apps
    	-> Password: 
    apps@instance-2:~$ cd attacker
    apps@instance-2:~/attacker$ sudo git pull
	
### З docker-compose:

перевіряєм чи контейнери живі:
	
	apps@instance-2:~/attacker$ docker-compose logs
	
якщо немає логів або помилка перезапускаєм контейнери:

    apps@instance-2:~/attacker$ docker-compose up --build --scale attacker=5
	
### З python:

    apps@instance-2:~/attacker$ sudo python3 attack.py 500
	
