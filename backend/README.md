# Backend

Source code: https://github.com/bmpi-dev/deprecated-github-backend

Download: https://github.com/bmpi-dev/logseq.xyz/releases/download/backend/logseq.jar

## Start Service

```
mkdir logseq
cd logseq
wget https://github.com/bmpi-dev/logseq.xyz/releases/download/backend/logseq.jar
sudo mkdir -p /app/logs/
sudo chown -R ubuntu:ubuntu /app/logs/
sudo cp logseq.service /etc/systemd/system/logseq.service
sudo systemctl daemon-reload
sudo systemctl enable logseq.service
sudo systemctl start logseq.service
sudo systemctl status logseq.service
```
