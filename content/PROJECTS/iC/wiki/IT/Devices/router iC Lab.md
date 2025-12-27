pwd: ProdejVajec03

Připojovací IP adresa: 212.47.16.33
Maska: 255.255.255.240
výchozí brána: 212.47.16.46
DNS1: 193.85.1.100
DNS2

port forwarding is in format external->internal

# Gauss
gauss: 212.47.16.33:9022
## port forwarding
80->4080 lets encrypt2 gauss
443->4060 let's encrypt 443

4060->4060 footfall recording
4080->8080 CVAT

tensorboad/free
7006->6006
7007->6007
7008->6008
7009->6009
7010->6010
7011->6011
7012->6012

9022->22 ssh


gauss-jupyterlab 212.47.16.33:6613

# Fourier
fourier: 212.47.16.33:8022

# port forwarding
8022->22
9030->8080

# Euler
euler: 212.47.16.33:8282`
## port forwarding
1322->1322 euler filip super-gradient docker ssh

4000 -> 4000 Nomachine

5501->5501 euler MartinV docker

tensorboard/free
6006->6006
6007->6007
6008->6008
6009->6009
6010->6010
6011->6011 euler jupyter

8282->22
8201 -> 8201    free
8202 -> 8202   free



# m2c sensor 
- AP z iC Labu z POE switche

# footfall64-iclab
- ssh -p 1422 icsapl@212.47.16.33
- 192.168.0.190
- -p 1422