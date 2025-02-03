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

alors qu'en TCP, on observe une erreur d'ouverture de flux :

b) UDP n'a jamais reçu les packages, mais n'a pas relevé d'erreurs. Ce n'est pas un comportement souhaitable, ni acceptable.

### Exercice 3
a)
b)
c)

### Exercice 4
a)
b)
c)
d)

### Exercice 5
a)
b)