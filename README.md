# TP 2 réseau

### Team
Raphaël, Ethan, Antonin

## Sommaire
- [Partie 1](#partie-1)
- [Partie 2](#partie-2)
    - [Exercice 1](#exercice-1)
    - [Exercice 2](#exercice-2)
    - [Exercice 3](#exercice-3)
    - [Exercice 4](#exercice-4)
    - [Exercice 5](#exercice-5) 
--------------------

## Partie 1
Configuration de deux VM chez Ethan (Cynosure, Mikoshi)
   Machine    | Cynosure     | Mikoshi      |
 |------------|--------------|--------------|
 | IPAdress   | 192.168.1.87 | 192.168.1.42 |
 | Mask       | 255.255.255.0 | 255.255.255.0 |

Ping :

![alt text](ping_cynosure_mikoshi.gif)

-------

## Partie 2
 | Machine    | Cynosure                         | Mikoshi                          |
 |------------|----------------------------------|----------------------------------|
 | puit       | ```./tsock -p 5667```            | ```./tsock -p 5668```            |
 | source     | ```./tsock -s 192.168.1.42 5668``` | ```./tsock -s 192.168.1.87 5667``` |

TCP :
![alt text](tsock_cynosure_mikoshi.gif)

UDP :
![alt text](tsock2_cynosure_mikoshi.gif)

### Exercice 1
a) UDP :

![alt text](tsock2_cynosure_mikoshi.gif)

b) On constate des pertes avec UDP :

![alt text](image_perte.png)

à l'inverse de TCP qui ne perd pas de packages :

![alt text](image_non_perte_tcp.png)

c) L'expérience consiste à saturer la communication UDP

````shell
# Mikoshi
./tsock -s 192.168.1.87 5667 -u -n 10000 -l 15000
# Cynosure
./tsock -p 5667 -u -15000
````
### Exercice 2
a) Avec UDP, on observe qu'aucun package part, mais pas d'erreur particulière :

![alt text](./2a_udp_cynosure_mikoshi.gif)

alors qu'en TCP, on observe une erreur d'ouverture de flux :

![alt text](./2a_tcp_cynosure_mikoshi.gif)

b) UDP n'a jamais reçu les packages, mais n'a pas relevé d'erreurs. Ce n'est pas un comportement souhaitable, ni acceptable, car il ne permet pas de savoir si la communication a fonctionné.

### Exercice 3
a)
![alt text](./3a_tcp_cynosure_mikoshi.gif)
b)
On peut voir le login avec TCP :
![alt text](./3b_tcp_cynosure_mikoshi.gif)
Log ici :

````shell
09:37:59.556289 IP 192.168.1.42.53801 > cynosure.nsca: Flags [S], seq 3811600990, win 64240, options [mss 1460,sackOK,TS val 3088549141 ecr 0,nop,wscale 7], length 0
09:37:59.556392 IP cynosure.nsca > 192.168.1.42.53801: Flags [S.], seq 3556977975, ack 3811600991, win 65160, options [mss 1460,sackOK,TS val 3686256413 ecr 3088549141,nop,wscale 7], length 0
09:37:59.556664 IP 192.168.1.42.53801 > cynosure.nsca: Flags [.], ack 1, win 502, options [nop,nop,TS val 3088549142 ecr 3686256413], length 0
09:37:59.556757 IP 192.168.1.42.53801 > cynosure.nsca: Flags [P.], seq 1:31, ack 1, win 502, options [nop,nop,TS val 3088549142 ecr 3686256413], length 30
09:37:59.556779 IP cynosure.nsca > 192.168.1.42.53801: Flags [.], ack 31, win 502, options [nop,nop,TS val 3686256455 ecr 3088549142], length 0
09:37:59.556814 IP 192.168.1.42.53801 > cynosure.nsca: Flags [F.], seq 31, ack 1, win 502, options [nop,nop,TS val 3088549142 ecr 3686256413], length 0
09:37:59.556906 IP cynosure.nsca > 192.168.1.42.53801: Flags [F.], seq 1, ack 32, win 502, options [nop,nop,TS val 3686256455 ecr 3088549142], length 0
09:37:59.557156 IP 192.168.1.42.53801 > cynosure.nsca: Flags [.], ack 2, win 502, options [nop,nop,TS val 3088549142 ecr 3686256455], length 0
````
c)
````shell

````
### Exercice 4
a,b,c,d) 
Pour TCP :
(*) Les adresses MAC ne sont pas les mêmes, car nous avons effectué le TP sur des machines réelles dans le cluster physique d'Ethan.
 | Machine    | Cynosure           | Mikoshi                          |
 |------------|----------------------------------|----------------------------------|
 | Adresse Mac       | 6c:4b:90:42:46:69 (*) | e8:6a:64:f3:0d:45 (*) |
 | Adresse IP     | 192.168.1.42  | cynosure.nsca (192.168.1.87) |
 | UDP/TCP     | (tos 0x0, ttl 64, id 43404, offset 0, flags [DF], proto TCP (6), length 60) | (tos 0x0, ttl 64, id 0, offset 0, flags [DF], proto TCP (6), length 40) |
 | Port du Puit     | 52027 | 52027 |
 | Port de la source     | 52027 | 52027 |


Pour UDP :
 | Machine    | Cynosure           | Mikoshi                          |
 |------------|----------------------------------|----------------------------------|
 | Adresse Mac       | 6c:4b:90:42:46:69 (*) | e8:6a:64:f3:0d:45 (*) |
 | Adresse IP     | 192.168.1.42  | cynosure.nsca (192.168.1.87) |
 | UDP/TCP     | (tos 0x0, ttl 64, id 26406, offset 0, flags [DF], proto UDP (17), length 38) | (tos 0x0, ttl 64, id 26406, offset 0, flags [DF], proto UDP (17), length 38) |
 | Port du Puit     | 56368 | 5667 |
 | Port de la source     | 56368 | 56368 |


### Exercice 5
a) La diffusion Broadcast envoie une communication à tous les appareils du réseau.   
b) Adresse de diffusion
![alt text](./broadcast_cynosure.gif)