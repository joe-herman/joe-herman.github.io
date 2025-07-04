---
layout: post
title: "Running Ollama on WSL and Open WebUI on a MBA for funsies"
---

## Summary
This post documents what worked for me to run an Ollama in WSL on Windows, while querying it from another machine using [Open WebUI](https://github.com/open-webui/open-webui).

This yields a ChatGPT-like service that runs privately and is still usable on underpowered clients.

## Prerequisites
* Server: WSL on Windows 11 22H1+ with a capable GPU
* Client: Macbook Air (or other thin client that struggles to run LLMs locally)
* Network: same local network

## Procedure

### **Server Setup**

1. Windows: Ensure `~/.wslconfig` has the following contents:
    ```ini
    [ws12]
    networkingMode = mirrored
    ```
1. Windows: if WSL was running make sure to shut it down to reload the above config:
    ```sh
    wsl --shutdown
    ```
1. Windows: In an **administrator Powershell session**, run:
    ```ps
    New-NetFirewallRule -DisplayName "Allow Ollama" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 11434
    ```
1. Windows: Open WSL:
    ```sh
    ubuntu
    ```
1. WSL: Note your NIC's IP, which should mirror your Windows host's IP (instead of some virtual adapter typically at `172.16.*.*`):
    ```sh
    ifconfig
    ```
    For example, my local IP was `192.168.1.204`.
1. WSL: Install `ollama` according to [instructions](https://ollama.com/download/linux)
    ```sh
    curl -fsSL https://ollama.com/install.sh | sh
    ```
1. WSL: Set the environment variable `OLLAMA_HOST` to listen to all network interfaces:
    ```sh
    export OLLAMA_HOST="0.0.0.0:11434"
    ```
1. WSL: Run `ollama` in the background:
    ```sh
    ollama serve &
    ```
1. Windows: Test to see if `ollama` is truly listening on the NIC instead of localhost:
    ```sh
    curl http://192.168.1.204/api/tags
    ```

### Client setup
1. Get the host IP from before 
1. Pick somewhere to store data like `/app/backend/data`
1. Export vars and run the docker container:
    ```sh
    export DATA_PATH="/app/backend/data"
    export OLLAMA_BASE_URL="http://192.168.1.204:11434"

    docker run -d -p 3000:8080 -e OLLAMA_BASE_URL -v open-webui-data:${DATA_PATH} --name open-webui ghcr.io/open-webui/open-webui:main
    ```
1. Wait forever for this thing to start up, check on it with:
    ```sh
    docker logs open-webui --follow
    ```
1. Open `http://localhost:3000`

That's everything!

## Why?
My poor Macbook Air (M1 with 16GB RAM/VRAM) can basically either run an LLM _or_ anything else due to the nature of limited shared memory. This setup offloads the LLM to the [greatest GPU of all time](https://www.youtube.com/watch?v=ghT7G_9xyDU), a GTX 1080 Ti (11GB VRAM).

I wanted to try a private LLM for reasons including avoiding contributing to future training data or [odd court mandates](https://arstechnica.com/tech-policy/2025/06/openai-says-court-forcing-it-to-save-all-chatgpt-logs-is-a-privacy-nightmare/). Also, it's fun to try things just because!

WSL allows the best of both Windows (hardware support) and Linux (UNIX-like app setup). Historically, WSL's NAT traversal and virtual adapters introduced annoyances for a server. I've always struggled with port mapping and firewalls on Windows, and no LLM could help me defeat WSL's NAT setup.

Luckily, [WSL now allows](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#configuration-settings-for-wslconfig) a `networkingMode = mirrored` setting, which magically rids us of NAT traversal and greatly simplifies setup with only minor caveats.

While I could run Ollama in a Docker container, I find the WSL GPU passthrough pretty seamless, and then I don't have to deal with orchestrating Ollama or Docker directly on Windows.

As to why I still have a Windows machine in 2025, I don't really know either.

## Why not?
Power usage is significantly better on ARM Macs.

*Additional* system power usage while generating a response based on my own power metering:

* **M1 Macbook Air:** ~17W
* **M1 Max Macbook Pro:** ~50W
* **7800x3D + GTX 1080 Ti via WSL:** ~240W

Also, response quality is generally worse than ChatGPT. I find myself having to clarify things to the LLM more often, which ultimately makes queries slower. This is probably due to a mix of several things including ChatGPT's base prompt, default context size, gpt-4o vs gemma3/qwen3 etc.

## Would I do this again?
Only for funsies, especially if new hardware is an option.

Honestly, the best new setup is likely a new Mac with tons of extra RAM. M1's efficiency is otherworldly compared to an 8 year old GPU, and more recent M-series chips are strictly faster still.

...But that's expensive. This lets me use my old 1080Ti as a modern appliance, and my slowly-aging Macbook Air as the thin client it excels at being—which is good enough for me!

## References
* [Open WebUI](https://github.com/open-webui/open-webui)
* [Ollama](https://github.com/ollama/Ollama)
* [.wslconfig reference](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#wslconfig)
* [WSL Configuration](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#configuration-settings-for-wslconfig)
