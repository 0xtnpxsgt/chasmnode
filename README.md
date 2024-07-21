# Chasm Node Setup
![image](https://github.com/user-attachments/assets/e9997d48-1190-4fd4-a74c-5d747873852e)

# Server Requirement : 
```bash
- Operating System: Ubuntu 22.04
- Min Requirement: 1 vCPU, 1GB RAM / 20GB Disk, Static IP
- Suggested Requirement: 2 vCPU, 4GB RAM / 50GB SSD, Static IP
```
# Listened Ports : 
![image](https://github.com/user-attachments/assets/96ba38ba-aa1c-4bb1-a280-3382b8b13987)

# Deployment:
- Update & Upgrade
```bash
sudo apt-get update && sudo apt-get upgrade -y
```
- Docker
```bash
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

# MINT
We need MNT Token for mint transaction. 0.20 Cent MNT : 0.35 MNT

# MINT SCOUT 
- Go to https://scout.chasm.net/private-mint / Connect your metamask wallet with MNT atleast 2 Token (Mantle Network) 

![image](https://github.com/user-attachments/assets/290ad42f-03ce-450c-9962-b7b08a4920f1)

# Create API KEY'S HERE:
- Save API KEY for later setup. 

- Groq : https://console.groq.com/keys
- OpenRouter : https://openrouter.ai/settings/keys
- OpenAI : https://platform.openai.com/api-keys

# Create .ENV FILE
```bash
nano .env
```

# EDIT
```bash
PORT=3001
LOGGER_LEVEL=debug

# Chasm
ORCHESTRATOR_URL=https://orchestrator.chasm.net
SCOUT_NAME=
SCOUT_UID=
WEBHOOK_API_KEY=
# Scout Webhook Url, update based on your server's IP and Port
# e.g. http://123.123.123.123:3001/
WEBHOOK_URL=

# Chosen Provider (groq, openai)
PROVIDERS=groq
MODEL=gemma2-9b-it
GROQ_API_KEY=

# Optional
OPENROUTER_API_KEY=
OPENAI_API_KEY=
```
--------------------------------------------------
- Scout Name : Your Node Name 
- Scout Cash ID : 
- WebHook IP : 
- Webhook URL: http://your-server-ıp:3001/
- Groq API : 
- Openrouter API : 
- OPENAI : 

# PORT
```bash
ufw allow 3001
```

# Docker Pull Chasm- Scout
```bash
docker pull johnsonchasm/chasm-scout .
```
```bash
docker run -d --restart=always --env-file ./.env -p 3001:3001 --name scout johnsonchasm/chasm-scout
```
```bash
source ./.env
curl -X POST \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $WEBHOOK_API_KEY" \
     -d '{"body":"{\"model\":\"gemma-7b-it\",\"messages\":[{\"role\":\"system\",\"content\":\"You are a helpful assistant.\"}]}"}' \
     $WEBHOOK_URL
```

# Test Connection 
```bash
curl localhost:3001
```
- Result : OK

# Check Logs
```bash
docker logs scout
```

Check Your Node Here: https://scout.chasm.net/leaderboard


