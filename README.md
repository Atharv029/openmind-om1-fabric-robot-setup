# Deploy Your First Robot on OpenMind Fabric Portal

In this guide, I will show you that how to install and run the **OM1 Agent** on a Linux system step-by-step.

---

##  1. Install Required Packages

```bash
screen -S openmind 
python3 -m venv .venv
source .venv/bin/activate
```

```bash
sudo apt update -y && sudo apt upgrade -y && sudo apt install -y \
portaudio19-dev python3-all-dev ffmpeg alsa-utils pipx && \
pipx install uv && \
sudo modprobe snd-dummy
```

---

## 2. Install UV

```bash
wget https://astral.sh/uv/install.sh
chmod +x install.sh
./install.sh
```

---

## 3. Clone the OM1 Repository

```bash
git clone https://github.com/openmind/OM1.git
cd OM1
```

---

## 4. Setup UV, Git, and Virtual Environment

```bash
pip install uv
git submodule update --init
uv venv
```

---

## 5. Get Your API Key

1. Visit [**OpenMind Fabric Portal**](https://portal.openmind.org/).  
2. log in with same account which you are using to do openmind testnet  
3. Click on **“Purchase Credits”** in the top-right menu and add **5 USDC**   
4. Click on **“Create API Key”** to generate your key.  
5. Copy and save it you **won’t be able to view it again** after closing the window.  

---

## 6. Add Your API Key to `.env`

```bash
cp env.example .env
nano .env
```

- Find the line: `OM-API-KEY=`  
- Paste your **OpenMind API key** after the equals sign.  
- Save and exit:  
> `CTRL + X → Y → ENTER`



---

## 7. Start the Node in a Screen Session

Run your node inside a `screen` session so it stays active even if you close your terminal.

```bash
uv run src/run.py conversation
```

Your OM1 agent is now running in the terminal.

---

## 8. Screen Commands

**Detach from screen:**
```bash
CTRL + A + D
```

**Reattach to screen:**
```bash
screen -r openmind
```

---

## Restart After Reboot or Crash

If the server or node restarts:

```bash
screen -r openmind
```

```bash
cd ~/OM1
source .venv/bin/activate
uv run src/run.py conversation
```

---

## Tips

- If you get **“401 Insufficient Balance”**, top up your balance and restart your node.  
- Always run OM1 inside a `screen` session to keep it active even after closing your terminal.  
- Use `screen -ls` to list active screen sessions if you have multiple nodes.

---

### License & Credits

This guide is based on official OpenMind installation instructions.  
For the latest setup updates, visit [OpenMind Fabric Portal](https://fabric.openmind.org/).
