# Configuração do Banco de Dados MySQL na Oracle Cloud + Integração com Node-RED

## 1. Acesso ao Servidor
```
ssh -i C:\Users\renan\Downloads\Oracle\ssh-key-2025-10-078.key opc@168.138.132.252
```
Se ocorrer erro de permissões, execute no PowerShell:
```
icacls "C:\Users\renan\Downloads\Oracle\ssh-key-2025-10-078.key" /inheritance:r
icacls "C:\Users\renan\Downloads\Oracle\ssh-key-2025-10-078.key" /grant:r "%USERNAME%:R"
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
sudo systemctl restart mysql
```
## 5. Firewall
```
sudo ufw allow 3306/tcp
sudo ufw reload
```

**Renan Mendes**  
Guia técnico para conexão e automação no Oracle Cloud com Node-RED.
