# Socks5BalancerAsio-mini-build
the mini build for Socks5BalancerAsio.


---

follow is a fast copy-past deploy template for me (jeremie)

```
su jeremie
cd ~
git clone https://github.com/Lyoko-Jeremie/Socks5BalancerAsio-mini-build.git
chmod +x ~/Socks5BalancerAsio-mini-build/Socks5BalancerAsio-mini
exit

```


```

nano /home/jeremie/S5BA-config.json

{
  "listenHost": "::",
  "listenPort": 443,
  "stateServerHost": "127.0.0.1",
  "stateServerPort": 5010,
  "disableConnectTest": true,
  "disableConnectionTracker": true,
  "traditionTcpRelay": true,
  "multiListen": [
    {
      "host": "::",
      "port": 16600
    },
    {
      "host": "::",
      "port": 16601
    },
    {
      "host": "::",
      "port": 16602
    }
  ],
  "upstream": [
    {
      "name": "backend",
      "host": "127.0.0.1",
      "port": 10443
    }
  ]
}



nano /etc/systemd/system/S5BA.service




[Unit]
Description=Socks5BalancerAsio Service
Requires=network.target
After=network.target

[Service]
Type=simple
User=jeremie
Restart=always
AmbientCapabilities=CAP_NET_BIND_SERVICE
WorkingDirectory=/home/jeremie/Socks5BalancerAsio-mini-build/
ExecStart=/home/jeremie/Socks5BalancerAsio-mini-build/Socks5BalancerAsio-mini /home/jeremie/S5BA-config.json

[Install]
WantedBy=multi-user.target




systemctl start S5BA
systemctl enable S5BA
systemctl status S5BA
journalctl -exu S5BA


```

