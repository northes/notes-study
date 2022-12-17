
```shell
docker run --name adguardhome\
    --restart unless-stopped\
    -v /root/adguardhome/workdir:/opt/adguardhome/work\
    -v /root/adguardhome/confdir:/opt/adguardhome/conf\
    -p 53:53/tcp -p 53:53/udp\
    -p 6767:67/udp -p 6868:68/udp\
    -p 8080:80/tcp -p 4433:443/tcp -p 4433:443/udp -p 3000:3000/tcp\
    -p 853:853/tcp\
    -p 784:784/udp -p 853:853/udp -p 8853:8853/udp\
    -p 5443:5443/tcp -p 5443:5443/udp\
    --network host\
    -d adguard/adguardhome
```