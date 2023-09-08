## 1. Install Ubuntu
#### 1. select language
![image](https://github.com/uomaep/ecole2023/assets/114221785/1cd2e43c-6b56-405f-87c7-cf50829b29b7)
#### 2. set ip
![image](https://github.com/uomaep/ecole2023/assets/114221785/51f533bd-07e3-4149-9527-40957a93375b)
#### 3. configure storage(boot 1G, swap 4G, 나머지)
![image](https://github.com/uomaep/ecole2023/assets/114221785/934d784e-30b6-4534-b76d-b55eb9a434b2)
#### 4. profile setup
![image](https://github.com/uomaep/ecole2023/assets/114221785/95a95d5f-759c-4364-b050-6ac804e4b123)
#### 5. package update
```shell
sudo apt-get update
sudo apt upgrade
sudo reboot
```

## 2. Install Cockpit
- Linux용 브라우저 기반 관리 도구
- 공격자의 입장에서 ssh 연결이 아니라 Cockpit을 쓰는 것을 예상하기 힘들기 때문에 조금이라도 보안성을 높일 수 있음.
- Cockpit의 기본 포트를 사용하지 않고 다른 포트로 열면 더욱 보안을 높일 수 있음.
#### 1. install
```shell
sudo apt install cockpit
```
#### 2. service
```shell
sudo systemctl enable cockpit # enable은 부팅 시 service를 자동으로 시작하게 명령어
sudo systemctl start cockpit # start는 service를 시작시키는 명령어
sudo journalctl -u cockpit # service log를 확인하는 명령어
```

#### 3. allow port
```shell
sudo ufw allow 9090/tcp
```

#### 4. Cockpit 웹 접속
<img width="1526" alt="스크린샷 2023-09-09 오전 4 40 38" src="https://github.com/uomaep/ecole2023/assets/114221785/f3ad705e-dad4-48e2-9905-15c54d02d539">

## 3. netplan
- ubuntu 서버의 ip setting을 변경하고 싶으면 /etc/netplan의 config파일을 수정하면 된다.
```yaml
network:
  ethernets:
    enp4s0:
      dhcp4: no //DHCP 사용하지 않고, 고정 ip 할당 방식
      addresses:
      - 192.168.0.11/24
      gateway4: 192.168.0.1
      nameservers:
        addresses:
        - 8.8.8.8
        - 1.1.1.1
```
- 적용하기
```shell
sudo netplan apply
```

- 확인하기
```shell
ip addr
```
```shell
sudo apt install net-tools
ifconfig
```

## 4. Install CloudPanel with Mysql
```shell
curl -sS https://installer.cloudpanel.io/ce/v2/install.sh -o install.sh; \
echo "3c30168958264ced81ca9b58dbc55b4d28585d9066b9da085f2b130ae91c50f6 install.sh" | \
sha256sum -c && sudo bash install.sh
```

## 5. CloudPanel 접속
여러 웹 구성 요소를 관리, 서버를 제어하고 관리할 수 있게 된다.
