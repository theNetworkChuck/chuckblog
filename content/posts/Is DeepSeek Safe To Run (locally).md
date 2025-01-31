---
title: Is DeepSeek Safe To Run (locally)
date: 2025-01-31
draft: false
tags:
  - NetworkChuck
---
# Monitor Network Connections 

## Windows

```powershell
while($true) {
    Get-Process ollama | ForEach-Object { 
        $id = $_.Id
        Write-Host "`nConnections for Ollama process $id" -ForegroundColor Green
        Get-NetTCPConnection | Where-Object OwningProcess -eq $id | Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, State 
    }
    Start-Sleep -Seconds 2
    Clear-Host
}
```


## Mac

```bash
# One-time check
pid=$(pgrep ollama)
lsof -i -P -n | grep ollama

# For continuous monitoring
while true; do
    echo "$(date): Ollama Connections"
    lsof -i -P -n | grep ollama
    sleep 2
    clear
done

# Alternative using netstat
netstat -p tcp -v | grep ollama
```

## Linux

```bash
# One-time check
pid=$(pgrep ollama)
lsof -i -P -n | grep ollama

# Or for continuous monitoring
watch -n 2 "lsof -i -P -n | grep ollama"

# Alternative using netstat
netstat -np | grep ollama

# Or using ss (more modern)
ss -np | grep ollama
```



# Running Ollama Inside Docker

```bash
docker run -d \
--gpus all \
-v ollama:/root/.ollama \
-p 11434:11434 \
--security-opt=no-new-privileges \
--cap-drop=ALL \
--cap-add=SYS_NICE \
--memory=8g \
--memory-swap=8g \
--cpus=4 \
--read-only \
--name ollama \
ollama/ollama
```