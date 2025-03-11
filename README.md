# How to setup
## 1. Clone this repository

Clone this repository with following command:

```bash
git clone git@github.com:fuku-inc/labcode-test-environment.git
```

## 2. Clone service repositories

Move into `labcode-test-environment` directory, run

```bash
bash clone_repositories.sh
```

Then, these repository is cloned:

1. `labcode-sim`
2. `labcode-log-server`
3. `labcode-web-app`

## 3. Edit environmental variables

Copy template file with following command:

```bash
cp labcode-web-app/app/.env.example labcode-web-app/app/.env
```

Then, edit `labcode-web-app/app/.env` and replace `your-google-client-id.apps.googleusercontent.com` with correct client ID.

## 4. Build containers

```bash
docker compose build
```

## 5. Run containers

```bash
docker compose up -d
```

## 6. (Only first time) setup database

```bash
docker compose exec log_server sh -c "python -m define_db.models"
```

## 7. Create user

1. Access to http://localhost:8000/docs#/users/create_users__post
2. Click "Try it out"
3. Enter email address to "email"
4. Click "Execute"
5. You will obtain response as follows:
```
{
  "id": 1,
  "email": "example@gmail.com"
}
```
6. Memo the value of "id" as user ID

## 8. Create Project

1. Access to http://localhost:8000/docs#/projects/create_projects__post
2. Click "Try it out"
3. Enter project name to "name"
4. Enter user ID obtained at user creation to "user_id"
5. Click "Execute"
6. You will obtain response as follows:

```{
  "id": 1,
  "name": "test_project",
  "user_id": 1,
  "created_at": "2025-02-25T10:44:18.911007",
  "updated_at": "2025-02-25T10:44:18.911017"
}
```
6. Memo the value of "id" as project ID.

## 9. Run experiment

1. Access to http://0.0.0.0:8080/docs#/default/run_experiment_run_experiment_post
2. Click "Try it out"
3. Enter project ID obtained at project creation to "project_id"
4. Enter protocol name to "protocol_name"
5. Enter user ID obtained at user creation to "user_id"
6. Upload `labcode-test-environment/protocol.yaml` to "protocol_yaml"
7. Upload `labcode-test-environment/manipulate.yaml` to "manipulate_yaml"
5. Click "Execute"

## 10. Access to Experiment tracking UI

Access to http://localhost:5173/

# How to access from another computer on the same network

## 1. Get the IP address of the computer running Experiment tracking ui

1. Open a terminal
2. Run the following command:

```bash
ip addr
```

Find the LAN IP address from the output:

(example)

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:1a:2b:3c:4d:5e brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.5/24 brd 192.168.1.255 scope global dynamic noprefixroute eth0
       valid_lft 86386sec preferred_lft 86386sec
```
In this example, 192.168.1.5 assigned to the eth0 (wired LAN) interface is the IP address within the LAN.
Look for an IP address with these characteristics:

Usually in the format of 192.168.xxx.xxx, 10.xxx.xxx.xxx, or 172.16.xxx.xxx to 172.31.xxx.xxx
Associated with eth0, eno1, enp0s3 (wired LAN) or wlan0, wlp2s0 (wireless LAN)
Displayed with scope global

## 2. Edit the hosts file on the computer you're using to access the Experiment tracking ui

### Linux

#### 1. Edit the hosts file with root or sudo privilleges

```
sudo nano /etc/hosts
```

#### 2. Add the hostname and IP address

```
192.168.1.5 labcode-web-app.com
```

(Replace 192.168.1.5 with the actual IP address of the web app server from the previous step)

### Windows

#### 1. Open Notepad with administrator privileges

Search for "Notepad" from the Start menu
Right-click on it and select "Run as administrator"

#### 2. Open `C:\Windows\System32\drivers\etc\hosts`

#### 3. Add the hostname and IP address

```
192.168.1.5 labcode-web-app.com
```

(Replace 192.168.1.5 with the actual IP address of the web app server from the previous step)


## 3. Access to Expeirment tracking ui

Access to http://labcode-web-app.com:5173