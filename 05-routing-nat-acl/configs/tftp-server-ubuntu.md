# TFTP Server on Ubuntu (PC2)

A minimal TFTP server using `xinetd`, as built in the lab. TFTP has no authentication or encryption, so access is limited by the ACL on R2 to the wireless network only. Use it only on trusted lab networks.

## Install

```bash
sudo apt install xinetd tftpd tftp
```

## Configure `/etc/xinetd.d/tftp`

```
service tftp
{
    protocol    = udp
    port        = 69
    socket_type = dgram
    wait        = yes
    user        = nobody
    server      = /usr/sbin/in.tftpd
    server_args = /tftpboot
    disable     = no
}
```

## Create the shared folder

```bash
sudo mkdir /tftpboot
sudo chmod -R 777 /tftpboot      # the lab write-up used chown here by mistake
sudo chown -R nobody /tftpboot
```

`777` keeps the lab simple. On anything shared, use tighter permissions.

## Start and test

```bash
sudo systemctl restart xinetd
echo "hello" > /tftpboot/test.txt
tftp 127.0.0.1 -c get test.txt
```

From a wireless client, run the same `get` against PC2's address. From a client outside the wireless network, the request should time out, which confirms the R2 ACL is working.
