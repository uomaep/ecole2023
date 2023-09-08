## 1. Install Ubuntu
- select language
- set ip
- configure storage
- profile setup
- package update
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
#### 2. start service
```shell
sudo systemctl enable cockpit
sudo systemctl start cockpit
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

## 4. Install CloudPanel with Mysql
```shell
curl -sS https://installer.cloudpanel.io/ce/v2/install.sh -o install.sh; \
echo "3c30168958264ced81ca9b58dbc55b4d28585d9066b9da085f2b130ae91c50f6 install.sh" | \
sha256sum -c && sudo bash install.sh
```
