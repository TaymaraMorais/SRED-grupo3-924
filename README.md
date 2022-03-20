# Instituto Federal de Alagoas - Campus Arapiraca
Prof. Alaelson Jatobá

Turma: 924

Alunas:

Alice Julia

Angelina Oliveira

Kailane Santos

Taymara Morais


## Sumário

1. Introdução;

2. Definições Iniciais;

3. Implementação dos Serivços de Rede (Cada serviço uma sessão);

4. Considerações Finais;

## 1. Introdução

Este trabalho aborda os assuntos dados em aula pelo professor, Alaelson Jatobá. Apresenta dados sobre a instalação, configuração e conexão dos servidores SAMBA, GATEWAY,  DNS MASTER, DNS SLAVE, WEB e BD.

## 2. Definições Iniciais

<p><center> Tabela 1: Definições da rede interna </center></p>

| DESCRIÇÃO   | IP             |
|:------------|:---------------|
| rede        | 10.9.24.0      |
| máscara     | 255.255.255.0  |
| Gateway     | 10.9.24.102    |
| Broadcast   | 10.9.24.255/24 |
| NameServer1 | 10.9.24.111    |
| NameServer2 | 10.9.24.122    |
| Samba       | 10.9.24.101    |
| WEB         | 10.9.24.215    |
| BD          | 10.9.24.216    |


<p><center> Tabela 2: Definições do domínio: <b>grupo3.turma924.ifalara.local</b></center></p>

|        VM         |      Apelido      |               NOME                  |
|:------------------|:------------------|:------------------------------------|
|      aluno02      | gateway (gw)      | gw.grupo3.turma924.ifalara.local    |
|      aluno11      | nameserver1 (ns1) | ns1.grupo3.turma924.ifalara.local   |
|      aluno22      | nameserver2 (ns2) | ns2.grupo3.turma924.ifalara.local   |
|      aluno01      | hostsamba   (hs1) | samba.grupo3.turma924.ifalara.local |
|                   | WEB         (web) | www.grupo3.turma924.ifalara.local   | -->
|                   | BD           (bd) | bd.grupo3.turma924.ifalara.local    |

## 3. Implementação dos Serivços de Rede:

### 3.1 DNS MASTER (ns1);
```bash
@ns1:~$ dig ns1.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.6-Ubuntu <<>> ns1.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 11050
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;ns1.grupo3.turma924.ifalara.local. IN  A

;; ANSWER SECTION:
ns1.grupo3.turma924.ifalara.local. 0 IN A       10.9.24.111
ns1.grupo3.turma924.ifalara.local. 0 IN A       192.168.24.16

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sat Mar 19 20:25:21 UTC 2022
;; MSG SIZE  rcvd: 94
```
```bash
@ns1:~$ dig ns2.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.6-Ubuntu <<>> ns2.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 19783
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;ns2.grupo3.turma924.ifalara.local. IN  A

;; ANSWER SECTION:
ns2.grupo3.turma924.ifalara.local. 10800 IN A   192.168.24.20
ns2.grupo3.turma924.ifalara.local. 10800 IN A   10.9.24.122

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:14:59 UTC 2022
;; MSG SIZE  rcvd: 94

```
```bash
@ns1:~$ dig gw.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.6-Ubuntu <<>> gw.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 22856
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;gw.grupo3.turma924.ifalara.local. IN   A

;; ANSWER SECTION:
gw.grupo3.turma924.ifalara.local. 10800 IN A    192.168.24.17
gw.grupo3.turma924.ifalara.local. 10800 IN A    10.9.24.102

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:16:17 UTC 2022
;; MSG SIZE  rcvd: 93

```
```bash
@ns1:~$ dig samba.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.6-Ubuntu <<>> samba.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 43138
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;samba.grupo3.turma924.ifalara.local. IN        A

;; ANSWER SECTION:
samba.grupo3.turma924.ifalara.local. 10800 IN A 10.9.24.101
samba.grupo3.turma924.ifalara.local. 10800 IN A 192.168.24.18

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:14:00 UTC 2022
;; MSG SIZE  rcvd: 96

```
```bash
@ns1:~$ dig bd.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.6-Ubuntu <<>> bd.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 59413
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;bd.grupo3.turma924.ifalara.local. IN   A

;; ANSWER SECTION:
bd.grupo3.turma924.ifalara.local. 10800 IN A    10.9.24.216

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:16:53 UTC 2022
;; MSG SIZE  rcvd: 77

```
```bash
@ns1:~$ dig www.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.6-Ubuntu <<>> www.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 8439
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.grupo3.turma924.ifalara.local. IN  A

;; ANSWER SECTION:
www.grupo3.turma924.ifalara.local. 10800 IN A   10.9.24.215

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:39:21 UTC 2022
;; MSG SIZE  rcvd: 78

```
### 3.2 DNS SLAVE (ns2);
```bash
@ns2:~$ dig ns1.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.1-Ubuntu <<>> ns1.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 29250
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;ns1.grupo3.turma924.ifalara.local. IN  A

;; ANSWER SECTION:
ns1.grupo3.turma924.ifalara.local. 10800 IN A   10.9.24.111
ns1.grupo3.turma924.ifalara.local. 10800 IN A   192.168.24.19

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:42:14 UTC 2022
;; MSG SIZE  rcvd: 94

```
```bash
@ns2:~$ dig ns2.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.1-Ubuntu <<>> ns2.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34844
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;ns2.grupo3.turma924.ifalara.local. IN  A

;; ANSWER SECTION:
ns2.grupo3.turma924.ifalara.local. 10800 IN A   192.168.24.20
ns2.grupo3.turma924.ifalara.local. 10800 IN A   10.9.24.122

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:44:23 UTC 2022
;; MSG SIZE  rcvd: 94

```
```bash
@ns2:~$ dig gw.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.1-Ubuntu <<>> gw.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 40252
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;gw.grupo3.turma924.ifalara.local. IN   A

;; ANSWER SECTION:
gw.grupo3.turma924.ifalara.local. 4465 IN A     10.9.24.102
gw.grupo3.turma924.ifalara.local. 4465 IN A     192.168.24.17

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:46:31 UTC 2022
;; MSG SIZE  rcvd: 93

```
```bash
@ns2:~$ dig samba.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.1-Ubuntu <<>> samba.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16335
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;samba.grupo3.turma924.ifalara.local. IN        A

;; ANSWER SECTION:
samba.grupo3.turma924.ifalara.local. 5664 IN A  192.168.24.18
samba.grupo3.turma924.ifalara.local. 5664 IN A  10.9.24.101

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:48:52 UTC 2022
;; MSG SIZE  rcvd: 96

```
```bash
@ns2:~$ dig bd.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.1-Ubuntu <<>> bd.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 4724
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;bd.grupo3.turma924.ifalara.local. IN   A

;; ANSWER SECTION:
bd.grupo3.turma924.ifalara.local. 10800 IN A    10.9.24.216

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:50:25 UTC 2022
;; MSG SIZE  rcvd: 77

```
```bash
@ns2:~$ dig www.grupo3.turma924.ifalara.local
```
```bash
; <<>> DiG 9.16.1-Ubuntu <<>> www.grupo3.turma924.ifalara.local
;; global options: +cmd
;; Got answer:
;; WARNING: .local is reserved for Multicast DNS
;; You are currently testing what happens when an mDNS query is leaked to DNS
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 14608
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.grupo3.turma924.ifalara.local. IN  A

;; ANSWER SECTION:
www.grupo3.turma924.ifalara.local. 4330 IN A    10.9.24.215

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Sun Mar 20 00:51:48 UTC 2022
;; MSG SIZE  rcvd: 78

```
## Tabelas BD:
```bash
mysql> show databases;
+--------------------------------------+
| Database                             |
+--------------------------------------+
| bd_grupo3_turma924_projetofinal_serd |
| information_schema                   |
| mysql                                |
| performance_schema                   |
| sys                                  |
+--------------------------------------+
5 rows in set (0.02 sec)
```
```bash
mysql> use bd_grupo3_turma924_projetofinal_serd;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> select * from aluno;
+-----+--------------------------------+-------------------------+-----+
| UID | Nome                           | Email                   | GID |
+-----+--------------------------------+-------------------------+-----+
|   1 | Alice Julia Silva Costa        | ajsc1@aluno.ifal.edu.br |   3 |
|   2 | Angelina Nunes Silva Oliveira  | anso1@aluno.ifal.edu.br |   3 |
|  11 | Kailane Santos Calixto         | ksc1@aluno.ifal.edu.br  |   3 |
|  22 | Taymara Morais de Mendonça     | tmm2@aluno.ifal.edu.br  |   3 |
+-----+--------------------------------+-------------------------+-----+
4 rows in set (0.00 sec)
```
```bash
mysql> select * from host;
+-----+-------------+-----------------------------------+-----+
| HID | VMNome      | FQDNome                           | GID |
+-----+-------------+-----------------------------------+-----+
| 215 | Web grupo 3 | www.grupo3.turma924.ifalara.local |   3 |
+-----+-------------+-----------------------------------+-----+
1 row in set (0.00 sec)
```
```bash
mysql> select * from grupo;
+-----+---------+-------------------------------+
| GID | nome    | dominio                       |
+-----+---------+-------------------------------+
|   3 | Grupo 3 | grupo3.turma924.ifalara.local |
+-----+---------+-------------------------------+
1 row in set (0.00 sec)
```

## Considerações Finais







