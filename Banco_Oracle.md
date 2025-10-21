# Configuração do Banco de Dados MySQL na Oracle Cloud + Integração com Node-RED

## Virtual Cloud Network

IPv4 CIDR Block
```
10.0.0.0/16
```

## SUBNETs

IPv4 CIDR Block
```
10.0.2.0/24
```
Public Acess

## 1. Acesso ao Servidor
```
ssh -i C:\Users\renan\Downloads\Oracle\ssh-key-2025-10-078.key ubuntu@168.138.132.252
```
Se ocorrer erro de permissões, execute no PowerShell:
```
icacls "C:\Users\renan\Downloads\Oracle\ssh-key-2025-10-078.key" /inheritance:r
icacls "C:\Users\renan\Downloads\Oracle\ssh-key-2025-10-078.key" /grant:r "%USERNAME%:R"
icacls "C:\Users\renan\Downloads\Oracle\ssh-key-2025-10-078.key" /remove "Users"
icacls "C:\Users\renan\Downloads\Oracle\ssh-key-2025-10-078.key" /remove "Administrators
```

## 2. Instalação do MySQL Server
```
sudo apt update
sudo apt install mysql-server -y
sudo systemctl enable mysql
sudo systemctl start mysql
```
## 3. Criação do Usuário e Permissões
```
sudo mysql -u root
```
```
CREATE USER 'diretor'@'%' IDENTIFIED BY 'BRKM7480';
GRANT ALL PRIVILEGES ON *.* TO 'diretor'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
## 4. Acesso Remoto
```
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address = 0.0.0.0
```
## 5. Firewall
```
sudo apt install ufw
sudo ufw enable
sudo ufw allow 3306/tcp
sudo ufw reload
```
```
sudo apt-get install iptables-persistent
sudo iptables -I INPUT 5 -p tcp --dport 3306 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```
```
sudo systemctl restart mysql
```

## 6. Liberando porta 3306 na Oracle Cloud

No Oracle Cloud Console:
Vá em Networking → Virtual Cloud Networks (VCNs)
Acesse sua sub-rede (Subnet) → clique na Security List associada
Clique em Add Ingress Rule
Source CIDR: 177.181.6.159/32 (ou seu IP público)
Destination Port Range: 3306
Protocol: TCP

## NODE-RED

msg.topic = "INSERT INTO usuarios (nome, email, idade) VALUES ('Renan', 'renan@email.com', 25)";
return msg;
