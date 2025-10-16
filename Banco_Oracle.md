# 🚀 Tutorial de Conexão SSH e Instalação do Node-RED no Oracle Cloud

## 🧩 1. Conectar ao Servidor Oracle Cloud
```bash
ssh -i C:\Users\renan\Downloads\ssh-key-2025-10-10.key ubuntu@136.248.115.35
```

> Se aparecer `Permission denied (publickey)`:
1. Corrigir permissões no PowerShell:
```bash
icacls "C:\Users\renan\Downloads\ssh-key-2025-10-10.key" /inheritance:r
icacls "C:\Users\renan\Downloads\ssh-key-2025-10-10.key" /grant:r "renan:R"
```
2. Tentar novamente o comando SSH acima.

---

## ⚙️ 2. Remover Instalação Antiga do Node-RED
```bash
sudo rm -rf ~/.node-red
sudo rm -rf /home/ubuntu/.nvm/versions/node/*/lib/node_modules/node-red
sudo npm cache clean --force
```

---

## 📦 3. Reinstalar o Node-RED
```bash
sudo npm install -g --unsafe-perm node-red
```

Verifique se funcionou:
```bash
node-red
```

Acesse no navegador:  
👉 [http://127.0.0.1:1880/](http://127.0.0.1:1880/)

---

## 🌐 4. Acessar de Qualquer Máquina
Edite o arquivo `settings.js` (geralmente em `~/.node-red/settings.js`):

Procure e altere:
```js
uiHost: "0.0.0.0",
uiPort: 1880,
```
Depois reinicie:
```bash
node-red-stop
node-red-start
```

No navegador de qualquer PC:  
👉 `http://<IP_PÚBLICO>:1880`  
Exemplo: [http://136.248.115.35:1880](http://136.248.115.35:1880)

---

## 🪪 5. Dica Extra – Rodar em Segundo Plano
```bash
node-red-start &
```

---

## 🧠 Autor
**Renan Mendes**  
Guia técnico para conexão e automação no Oracle Cloud com Node-RED.
