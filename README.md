# Flatcar App: WireGuard

A reference implementation for running **WireGuard VPN** on **Flatcar Container Linux** using **Butane**, **systemd**, and **Docker**.

This Flatcar App demonstrates how to deploy a secure, lightweight VPN service using a fully declarative configuration.

---

## Features

- Fully automated deployment using Butane
- Runs WireGuard inside a hardened container
- systemd service for automatic startup and recovery
- Supports multiple peers
- Works on cloud VMs or bare metal

---

## Repository Structure

```
flatcar-app-wireguard/
├── butane.yaml
├── docker-compose.yml
├── systemd/
│   └── wireguard.service
└── screenshots/   (optional)
```


---

## Requirements

- A Flatcar Container Linux machine
- Butane installed locally
- Docker (installed automatically by the config)
- WireGuard keys (generated locally)

---

## Deployment

### 1. Convert Butane to Ignition

```
butane --strict butane.yaml > ignition.json
```


### 2. Provision your Flatcar machine

Upload `ignition.json` using your cloud provider or provisioning tool.

---

## WireGuard Configuration

Place your WireGuard configuration in:

```
/etc/wireguard/wg0.conf
```


Example:

```
[Interface]
PrivateKey = <server-private-key>
Address = 10.0.0.1/24
ListenPort = 51820

[Peer]
PublicKey = <client-public-key>
AllowedIPs = 10.0.0.2/32
```


---

## Managing the Service

Start:

```
sudo systemctl start wireguard
```


Enable on boot:

```
sudo systemctl enable wireguard
```

Check logs:

```
sudo journalctl -u wireguard -f
```


---

## Verify Connectivity

From the client:

```
ping 10.0.0.1
```


If packets return, your VPN is working.

---

## Screenshots

Add screenshots here if you test the deployment.

---

## Contributing

Feedback and improvements are welcome!  
This app is part of the Flatcar Apps initiative.

---

## License

MIT
