#  🛠 FAQ & Troubleshoot 🛠

</div>


# 1️⃣ How to Login or access  http://localhost:3000/ in VPS? 📶

* Open a new Terminal and login ur vps 

* Allow Incoming connection on VPS

```
sudo apt install ufw -y
sudo ufw allow 3000/tcp
```

* Enable ufw

```
sudo ufw enable
```

* Install cloudflared on the VPS

```
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
````

```
sudo dpkg -i cloudflared-linux-amd64.deb
```

* Check version

```
cloudflared --version
```

* Make sure your Node is running on port 3000 in Previous Screen

* Run the tunnel command

```
cloudflared tunnel --url http://localhost:3000
```

* Access the Link from your local machine

    
    ![image](https://github.com/user-attachments/assets/c5bdfec5-123d-4625-8da8-f46269700950)

* Now follow Login!
 
* Done!✅



# 2️⃣ Solution of OOM errors on MacBook (Memory/Cpu limit)

* Open -
 ```
nano ~/.zshrc
```

* Paste in the file

```
export PYTORCH_MPS_HIGH_WATERMARK_RATIO=0.0
export PYTORCH_ENABLE_MPS_FALLBACK=1
```
* Reload with

```
  source ~/.zshrc
```

# 3️⃣ How to get the Node Name?

* Check the image below to get your Node id!

![image](https://github.com/user-attachments/assets/728c6401-75c8-43b4-973c-e9d515c4b453)

# 4️⃣ Save your `swarm.pem` file (for future login)

* open a wsl window 

* If U have to copy this file to your local machine from VPS then Run this command from your local Terminal--

```
scp USERNAME@YOUR_IP:~/rl-swarm/swarm.pem ~/swarm.pem
```

It will save here in ur Terminal's Root Directory!


# 5️⃣ How To start the Next Day (Local Pc)

*
 ```
  cd rl-swarm
 ```

*
 ```
  python3 -m venv .venv
```

*
```
source .venv/bin/activate
```

*
```
./run_rl_swarm.sh
```


# 6️⃣ Node Stuck & getting errors like this? lets solve it! 

![image](https://github.com/user-attachments/assets/956c0691-b2da-40f1-825e-cd634c147d49)

* This error is coming for who's running on personal Device.

* Cause of error is old GPU or Low ram!

1) Stop your node with ctrl+c

2) Run `cd`

3) Open and Add this line at the end of the file (use up-down keys to move)

```
nano ~/.bashrc
```

```
export PYTORCH_MPS_HIGH_WATERMARK_RATIO=0.0
```

4) Reload with-

```
source ~/.bashrc
```

5) Open The Config file

For wsl/linux

```
nano ~/rl-swarm/hivemind_exp/configs/gpu/grpo-qwen-2.5-0.5b-deepseek-r1.yaml
```

For Mac

```
nano ~/rl-swarm/hivemind_exp/configs/mac/grpo-qwen-2.5-0.5b-deepseek-r1.yaml
```

🔺 Now Change- `vllm_gpu_memory_utilization: 0.2` to `0.4`  (check ss)

![image](https://github.com/user-attachments/assets/2d40c0dc-0438-4d80-85e4-c9fcfbbc58fc)


save with `cltr+x` , `Y` + `Enter`

6) Cut the Wsl or terminal and restart it!

7) Now start the node ( Check FAQ 5)

* It can be solve your issue, i think not for low GPU users!

---
# Troubleshooting:

### ⚠️ Upgrade viem & Node version in Login Page
1- Modify: `package.json`
```bash
cd rl-swarm
nano modal-login/package.json
```
* Update: `"viem":` to `"2.25.0"`

2- Upgrade
```bash
cd rl-swarm
cd modal-login
yarn install

yarn upgrade && yarn add next@latest && yarn add viem@latest

cd ..
```

### ⚠️ CPU-only Users: Ran out of input
Navigate:
```
cd rl-swarm
```
Edit:
```
nano hivemind_exp/configs/mac/grpo-qwen-2.5-0.5b-deepseek-r1.yaml
```
* Lower `max_steps` to `5`

Follow official Docs for more info and Errors!
Thank U! 👨🏻‍💻 Happy Coding💗
