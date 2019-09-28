# easy-wg-quick
easy-wg-quick - Creates Wireguard configuration for hub and peers with ease

## Getting Started

These instructions will get you a copy of the project up and running on your
local machine. This machine (called hub) will act as VPN concentrator. All
other peers connects to hub (as in a "road warrior" configuration).

### Prerequisites

Install [Wireguard](https://www.wireguard.com/) for your operating system on
[local machine](https://www.wireguard.com/install/),
[router](https://openwrt.org/docs/guide-user/services/vpn/wireguard),
[VPS](https://en.wikipedia.org/wiki/Virtual_private_server) or
[container](https://github.com/activeeos/wireguard-docker). This will be your
hub.

As dependences `/bin/sh`, `wg`, `wg-quick`, `awk`, `grep` and `ip` commands
should be available on hub. If `ip` is not available user is required to set
`EXT_NET_IF` and `EXT_NET_IP` variables in script to external network interface
name and IP address (or edit `wg0.conf`). Optionally `qrencode` can be used
to generate [QR codes](https://en.wikipedia.org/wiki/QR_code) for mobile
applications.

```
sudo apt install wireguard mawk grep iproute2 qrencode
```

Peers also requires Wireguard installed.
[Android](https://play.google.com/store/apps/details?id=com.wireguard.android)
and [iOS](https://itunes.apple.com/us/app/wireguard/id1441195209?ls=1&mt=8)
are supported.

### Installing

Just download the script and make it executable with `chmod`.

```
wget https://raw.githubusercontent.com/burghardt/easy-wg-quick/master/easy-wg-quick
chmod +x easy-wg-quick
```

Or clone repository.

```
git clone https://github.com/burghardt/easy-wg-quick.git
```

## Usage

Script do not require any arguments. Just run it and it will create usable
Wireguard configuration for hub and one peer. Any sequential invocation creates
another peer configuration within same hub.

```
./easy-wg-quick
```

### Sample output

```
No seqno.txt... creating one!
No wgpsk.key... creating one!
No wghub.key... creating one!
No wg0.conf... creating one!
Wireguard hub address is 10.60.1.160:51820 on wlp2s0.
Note: customize [Interface] section of wg0.conf if required!
No wgclient10.conf... creating one!
█████████████████████████████████████████████████████████████████████
█████████████████████████████████████████████████████████████████████
████ ▄▄▄▄▄ █▄▄  ▄▀▀█ ▄▀▀ ▀█ ▀▀▀█▄▀█▀██▀  ▄ ▄▄█▄▄▀ ▀▀▄██  █ ▄▄▄▄▄ ████
████ █   █ █  ██▀██▄▀█▄██▀ █▀█▄ ▄▄ ▄▀▄▄█ ██▀ █▄▄▄▄██ ▄ ▄ █ █   █ ████
████ █▄▄▄█ █▄▄▄▄ ███▄ ██▄▀▀  ▀ ▀ ▄▄▄ █▀▀▀▀ ██ ██▄▀█▀██ ▄██ █▄▄▄█ ████
████▄▄▄▄▄▄▄█▄▀▄█▄█ █▄▀▄█▄▀▄█▄█▄▀ █▄█ █▄▀▄▀ █ █ █▄▀▄█▄█ █ █▄▄▄▄▄▄▄████
████ ▄▄ ▀█▄▀ █▄ ██ ▀█▄█ ▄ █▀ ▀▄▀   ▄▄█ █ █▀████ ▀  ▀ ▀██▄ ▀█  ▄█ ████
█████▀  ▀ ▄█ ▄   ▀  ▀▀█▀▄████▄▄▀█▀█ █▀█▀▀▄▄▀█▄ ▄▀▄▀ ▄▀▀▄█ ▄▄▄ ▀▀▀████
████ ███▀▄▄▄▄▀▄▀▄██  ▀▀▄███▄▀  ▄▀▀▀▀▀█▀▀▄  ▀█▀▄▀█▄  █▄▀▄█▄▄█▀▄▄██████
█████▄▀▄▄▀▄██▄ ▄  █▄ █▀██▀██▀▀▄▀ ▀▄ ▄ ▄█ ▀ ▀█▀▄██▄▀█▄▄▄▄▄▀  ▄▄ ▀ ████
████▄█ █▀▀▄ ▀▄ ▄▄█▄▄▀▀▄█▄   ▀▄▄█▀ ▄▄▀▄▀ ▄▀▄█▀▀█▀█▄▀ ▀▄ ▀▀▀▀▄█▄▀▄▄████
████ ▄▀▀▀▄▄█ ▄█ ▀█ ██▄▄▄▀ █▀▄▄▄  ▀▄▀▀█▀ ▄█▄▄▀ ▄ █ ▄▀▄▀▀▄ █▄▀ ▄█▄█████
████▄▄▄▀▀▄▄▀█▀█▄    ▀██ ▀▄▄▀▄ █▀▄█▄ ▀▄█▀ ▀█▀██▀█▄▄▄█▀▄▄  ▄  ▄  ▀▀████
████▄▄▄▄ ▄▄▄▄█ ▀▀▄█▄▄▄ ▀▄  ▀▀ █ ██▀▀█▀▀▀▀▀▄▀▀██  █ ▄▄▄▄  ██   ▀▀▄████
████▀▀   █▄ █▄▄ ▄█▄█▄█▄▀▀▄▄█▀▄▄▀█▀▀▄█▄▀ █ █ █▀ █▀██▄█▀▀▄▄▄▄▄█▄▄██████
████ █  ██▄█▀▀████▄▄▄▀▀▄ ▄▀▄█ ██▀▄▀▄▄▄██▀ ▄▀██▄ ▀██▄▀▄▄█▄▀  █▄  ▀████
████ ██▄ ▄▄▄ ▄  ▄▀▀▀▀██ █▀▀▄▀██▀ ▄▄▄  █▄▀▀█  ▀█▀█▄  █  █ ▄▄▄ █▀▀▀████
████ ███ █▄█ ▀█▄▄ ███▀█ ▀▄▀█▄▀ █ █▄█ ▄ ▄█▄▄▀█▀▀ ██▄▄ █▄▀ █▄█ ▀▀▀▄████
████▀█▄▄▄ ▄▄ ▄ ▀ █▄█    ▀ ▀▀▄█▀▀▄▄  ▄  ▀ ███▄ ▀█▄▀▄ ██▀▀▄  ▄▄▄ █▄████
██████▀   ▄▄▄ ▄▀▄▀▀▀▄▄█   ▀▄ ▀▀▄▀██ ████▀ ▄██▀▀█ ▄▀ █ ▄▄▀▄█▄██▄ █████
████▄▄▄▀▄▄▄█▄█ ▄▄▄ █ █▀▀▄▄█ ████▀ ▀ ▀▄███ █▄ ▀▀▀▀█▀█▀█▀▄ █▄▀▄▀▀▀▀████
████    ▀▄▄▀▀▄  ▀ ▄▄█▄▀ ▀██▀ ▄▄▀▀▀ ▄▀▀ █▀██▀▀▄█ █▄▀▄▀▀█ ██▀████ ▀████
████ █▀▀█ ▄▀███   ▄ ▀▄█▄█▀▀ ▄██ ▀███▄▀█▄▄█  ▀▄█▄▄▄█ ▄█▄█▀▄▄▀▀  ▀█████
█████  ██▄▄▀ ▄ ▀ █ ▀█▄▄█▀██▄▄ ▀█▄█▄▀█ █▄▀ █▀█▄ ▀████▄  ▀ █▄ ▀██▀▄████
████▄ █▀▀█▄█▀▀█▄██▀█  ▀██▀ ▀▄▄▀▄ ▄ ▄▀▀ ▀▄  ██ ▀  ▀█  ██  ▀█▀▄ ▀██████
████ ▄█▀█▄▄ ▀▄▄   ▀ ▀ ▄▀▄▄ ▀█▄▄ ▀▀▄ ▄▀█ ▀▀▄ ▀▄█ ▄ ▄ ▀▄█▄ █▀▄▄▀█▄▄████
████▄▄  ▀▄▄ ▄▄▄ █▄████▀▀██▄█ ▀█▄ ██▀▀█▀█▄▄▀ █▄▄█ █ ▄▄ ██▄▀█▄▀▄█▄▄████
████▀▀ ▄ ▄▄▀▄▄▄▄██  ▄▄█▄█ ██▄█   ▄█▀█ ▄ ▄▀▄▀█▄▀█▀▄  ▀ ▀ ▀  ▄▀▀▄▀▀████
████▄▄▄▄██▄█▀▄▀▀▀ ▄▄  ▀▀   █▀ █▄ ▄▄▄ █▀ ▄  ▄▄▄██▄▀█ █ ▄▀ ▄▄▄  ▀ █████
████ ▄▄▄▄▄ ██▀▄▄▀█▄ ▄ ▀ ▀▀▄▄▄▄█  █▄█ ▀▄▀█▀▀▄▀▄▄█▀ ▄ ▀▄▀  █▄█  ██▄████
████ █   █ █▀▄ █▀▄▄▄▄▄  ██ ▄▀█▄█▄ ▄ ▄▀  ▀██▄▄▀▄▀█▄ ▀  ▄█▄▄▄▄▄▀██ ████
████ █▄▄▄█ █ ▄ ██▄▄▄▀▀█▀▀███▀▄█▄ ███▀▄ ▄▄▄█▀ █▄▄ █▄▀▄▀█▀██▀ █▄█▄█████
████▄▄▄▄▄▄▄█▄███▄▄▄▄█████▄█▄▄█▄█▄▄▄▄▄▄█▄▄█▄▄▄▄▄██▄█▄▄▄███▄▄█▄█▄▄▄████
█████████████████████████████████████████████████████████████████████
█████████████████████████████████████████████████████████████████████
Scan QR code with your phone or use "wgclient10.conf" file.
Updating wg0.conf... done!

Important: Deploy updated wg0.conf configuration to wireguard with wg-quick:
  sudo wg-quick down ./wg0.conf # if already configured
  sudo wg-quick up ./wg0.conf
  sudo wg show # to check status

Note: passing argument to script creates symbolic link to created configuration
      to help remembering which config was for which device. If you didn't pass
      any argument you can still create a link manually with command:
  ln -vfs wgclient10.conf link_name.conf
```

### Using generated configuration

On hub configure Wireguard.

```
sudo wg-quick up ./wg0.conf
```

On peer scan QR code or copy `wgclient10.conf`.

Finally on hub check if everything works with `sudo wg show`.

```
interface: wghub
  public key: kbaG3HxSDz3xhqiTNXlo1fZkFa+V6oTl+w0cSAQKxwQ=
  private key: (hidden)
  listening port: 51820

peer: th8qYu0R0mgio2wPu1kz6/5OOgi6l8iy7OobK590LHw=
  preshared key: (hidden)
  endpoint: 10.60.1.150:37218
  allowed ips: 10.127.0.10/32
  latest handshake: 50 minutes, 22 seconds ago
  transfer: 32.64 MiB received, 95.24 MiB sent
```

## Fine tunning

### Enabling IPv6

If global unicast IPv6 address is detected on server tunnels will be created
with inner IPv6 addresses allocated. This allows hub's clients to connect over
hub's IPv6 NAT to IPv6 network.

To use outer IPv6 addresses (i.e. connect client to hub over IPv6) just set
`EXT_NET_IF` and `EXT_NET_IP` variables in script to external network interface
name and IPv6 address (or edit `wg0.conf`).

### Redirecting DNS

DNS redirection might be required to integrate with services like
[Pi-hole](https://pi-hole.net/) or
[Cloudflare DNS over TLS](https://github.com/qdm12/cloudflare-dns-server).
This could be achieved by using port 53 UDP/TCP redirection in `wg0.conf`.

```
PostUp = iptables -t nat -A PREROUTING -i %i -p udp -m udp --dport 53 -j DNAT --to-destination 1.1.1.1:53
PostUp = iptables -t nat -A PREROUTING -i %i -p tcp -m tcp --dport 53 -j DNAT --to-destination 1.1.1.1:53
PostDown = iptables -t nat -D PREROUTING -i %i -p udp -m udp --dport 53 -j DNAT --to-destination 1.1.1.1:53
PostDown = iptables -t nat -D PREROUTING -i %i -p tcp -m tcp --dport 53 -j DNAT --to-destination 1.1.1.1:53
```

When using IPv6 similar rules should be set independently with `ip6tables`.

## License

This project is licensed under the GPLv2 License - see the
[LICENSE](LICENSE) file for details.

## Acknowledgments

OpenVPN's [easy-rsa](https://github.com/OpenVPN/easy-rsa) was an inspiration
for writting this script.
