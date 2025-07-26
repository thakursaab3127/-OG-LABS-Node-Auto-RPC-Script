


# 🚀 OG LABS Node Auto RPC Fetch Script  
**By Thakur Saab 🏆 – Gujarat, India**

A fully automated script to deploy and manage your **0G Storage Node** with one-click installation, custom RPC setup, and fast Flow DB sync. Built for node runners, decentralization supporters, and Web3 builders.

---

## 📌 Use Case

This script helps you:  
- 🔧 Auto-install 0G Storage Node on Ubuntu  
- 🔁 Fetch & apply a reliable custom RPC  
- ⚡ Sync faster using Flow DB snapshot  
- 🛠️ Control node via systemctl & screen  
- 🤖 Monitor status with a Telegram bot

---

## ✅ Server Requirements

- **OS**: Ubuntu 20.04 or 22.04  
- **CPU**: 4+ cores  
- **RAM**: 16 GB or more  
- **Storage**: 500GB–1TB SSD/NVMe  
- **Network**: Public IPv4 address

---

## 🛠 Installation Guide (All in One Flow)

### 🖥️ Start a screen session

```bash
screen -S og


📦 Update system & install git

sudo apt update && sudo apt install git -y

⚙️ Install 0G Storage Node (auto script)

bash <( curl -sL https://raw.githubusercontent.com/CodeDialect/0g-Storage-Node/main/0g_node_setup.sh \
     | sed '/^[ _|\\/()]\+$/d;/figlet/d;/toilet/d' ) \
     && echo && echo "============================================" \
     && echo "       Made by Thakur Saab, Gujarat " \
     && echo "============================================"

🌐 Apply custom RPC

bash <(curl -sL https://raw.githubusercontent.com/CodeDialect/0g-Storage-Node/main/change_rpc.sh)

Recommended RPC to use:

https://0g-evmrpc.sr20de.xyz/

⚡ Fast Sync with Flow DB Snapshot
🛑 Stop the node
bash
Copy code
sudo systemctl stop zgs
🧹 Remove existing flow DB
bash
Copy code
rm -rf $HOME/0g-storage-node/run/db/flow_db
📥 Download & extract snapshot
bash
Copy code
wget https://github.com/Naveenrawde3/0G-LABS-STORAGE-NODE-RUN-GUIDE-BY-NTEK/releases/download/v1.0/flow_db.tar.gz \
  -O $HOME/0g-storage-node/run/db/flow_db.tar.gz && \
  tar -xzvf $HOME/0g-storage-node/run/db/flow_db.tar.gz -C $HOME/0g-storage-node/r  ye ek line de

🔁 Restart node
bash
Copy code
sudo systemctl restart zgs


📡 Live Sync Status Checker
bash
Copy code
while true; do \
  response=$(curl -s -X POST http://localhost:5678 -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","method":"zgs_getStatus","params":[],"id":1}'); \
  logSyncHeight=$(echo $response | jq '.result.logSyncHeight'); \
  connectedPeers=$(echo $response | jq '.result.connectedPeers'); \
  echo -e "logSyncHeight: \033[32m$logSyncHeight\033[0m, connectedPeers: \033[34m$connectedPeers\033[0m"; \
  sleep 5; done

📈 Shows real-time logSyncHeight and connected peers
❌ Press Ctrl + C to stop

🧰 Node Management Commands

| 🔧 Action                | 🧪 Command                                                              |
| ------------------------ | ----------------------------------------------------------------------- |
| ✅ Check Node Status      | `sudo systemctl status zgs`                                             |
| 📜 View Logs             | `tail -f ~/0g-storage-node/run/log/zgs.log.$(date +%F)`                 |
| 🛑 Stop Node             | `sudo systemctl stop zgs`                                               |
| ❌ Remove Node Service    | `sudo systemctl disable zgs && sudo rm /etc/systemd/system/zgs.service` |
| 🧼 Delete All Node Files | `rm -rf $HOME/0g-storage-node`                                          |
| 🔁 Reattach to Screen    | `screen -r og`                                                          |


