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

4. Testes

5. Considerações Finais;

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
|      grupo3VM1    | WEB         (web) | www.grupo3.turma924.ifalara.local   | -->
|      grupo3VM2    | BD           (bd) | bd.grupo3.turma924.ifalara.local    |

## 3. Implementação dos Serivços de Rede:

## 4. Testes

### Testes dig DNS Master (ns1);
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

### Testes dig DNS Slave (ns2);

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
### Testes nslookup ns1 (DNS Master);

```bash
administrador@ns1:~$ nslookup ns1 ns1
Server:         ns1
Address:        10.9.24.111#53

Name:   ns1.grupo3.turma924.ifalara.local
Address: 10.9.24.111
Name:   ns1.grupo3.turma924.ifalara.local
Address: 192.168.24.19
```
```bash
administrador@ns1:~$ nslookup ns2 ns1
Server:         ns1
Address:        10.9.24.111#53

Name:   ns2.grupo3.turma924.ifalara.local
Address: 192.168.24.20
Name:   ns2.grupo3.turma924.ifalara.local
Address: 10.9.24.122
```
```bash
administrador@ns1:~$ nslookup gw ns1
Server:         ns1
Address:        10.9.24.111#53

Name:   gw.grupo3.turma924.ifalara.local
Address: 192.168.24.17
Name:   gw.grupo3.turma924.ifalara.local
Address: 10.9.24.102
```
```bash
administrador@ns1:~$ nslookup samba ns1
Server:         ns1
Address:        10.9.24.111#53

Name:   samba.grupo3.turma924.ifalara.local
Address: 10.9.24.101
Name:   samba.grupo3.turma924.ifalara.local
Address: 192.168.24.18
```
```bash
administrador@ns1:~$ nslookup www ns1
Server:         ns1
Address:        10.9.24.111#53

Name:   www.grupo3.turma924.ifalara.local
Address: 10.9.24.215
```
```bash
administrador@ns1:~$ nslookup bd ns1
Server:         ns1
Address:        10.9.24.111#53

Name:   bd.grupo3.turma924.ifalara.local
Address: 10.9.24.216

```
## Testes nslookup id_sub-redes ns1 (DNS Master);

```bash
administrador@ns1:~$ nslookup 10.9.24.111 ns1
111.24.9.10.in-addr.arpa        name = ns1.grupo3.turma924.ifalara.local.
```
```bash
administrador@ns1:~$ nslookup 10.9.24.122 ns1
122.24.9.10.in-addr.arpa        name = ns2.grupo3.turma924.ifalara.local.
```
```bash
administrador@ns1:~$ nslookup 10.9.24.102 ns1
102.24.9.10.in-addr.arpa        name = gw.grupo3.turma924.ifalara.local.
```
```bash
administrador@ns1:~$ nslookup 10.9.24.101 ns1
101.24.9.10.in-addr.arpa        name = smb.grupo3.turma924.ifalara.local.
```
```bash
administrador@ns1:~$ nslookup 10.9.24.215 ns1
215.24.9.10.in-addr.arpa        name = www.grupo3.turma924.ifalara.local.
```
```bash
administrador@ns1:~$ nslookup 10.9.24.216 ns1
216.24.9.10.in-addr.arpa        name = bd.grupo3.turma924.ifalara.local.

```
## Testes nslookup ns2 (DNS Slave);

```bash
root@ns2:~# nslookup ns1 ns2
Server:         ns2
Address:        10.9.24.122#53

Name:   ns1.grupo3.turma924.ifalara.local
Address: 192.168.24.19
Name:   ns1.grupo3.turma924.ifalara.local
Address: 10.9.24.111
```
```bash
root@ns2:~# nslookup ns2  ns2
Server:         ns2
Address:        10.9.24.122#53

Name:   ns2.grupo3.turma924.ifalara.local
Address: 10.9.24.122
Name:   ns2.grupo3.turma924.ifalara.local
Address: 192.168.24.20
```
```bash
root@ns2:~# nslookup gw ns2
Server:         ns2
Address:        10.9.24.122#53

Name:   gw.grupo3.turma924.ifalara.local
Address: 192.168.24.17
Name:   gw.grupo3.turma924.ifalara.local
Address: 10.9.24.102
```
```bash
root@ns2:~# nslookup samba ns2
Server:         ns2
Address:        10.9.24.122#53

Name:   samba.grupo3.turma924.ifalara.local
Address: 192.168.24.18
Name:   samba.grupo3.turma924.ifalara.local
Address: 10.9.24.101
```
```bash
root@ns2:~# nslookup www ns2
Server:         ns2
Address:        10.9.24.122#53

Name:   www.grupo3.turma924.ifalara.local
Address: 10.9.24.215
```
```bash
root@ns2:~# nslookup bd ns2
Server:         ns2
Address:        10.9.24.122#53

Name:   bd.grupo3.turma924.ifalara.local
Address: 10.9.24.216
```

## Testes nslookup id_sub-redes ns2 (DNS Slave);

```bash
root@ns2:~# nslookup  10.9.24.111 ns2
111.24.9.10.in-addr.arpa        name = ns1.grupo3.turma924.ifalara.local.
```
```bash
root@ns2:~# nslookup  10.9.24.122 ns2
122.24.9.10.in-addr.arpa        name = ns2.grupo3.turma924.ifalara.local.
```
```bash
root@ns2:~# nslookup  10.9.24.102  ns2
102.24.9.10.in-addr.arpa        name = gw.grupo3.turma924.ifalara.local.
```
```bash
root@ns2:~# nslookup  10.9.24.101  ns2
101.24.9.10.in-addr.arpa        name = smb.grupo3.turma924.ifalara.local.
```
```bash
root@ns2:~# nslookup  10.9.24.215  ns2
215.24.9.10.in-addr.arpa        name = www.grupo3.turma924.ifalara.local.
```
```bash
root@ns2:~# nslookup  10.9.24.216  ns2
216.24.9.10.in-addr.arpa        name = bd.grupo3.turma924.ifalara.local.
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

Durante a realização do Trabalho final, assumimos o desafio de realizar o desenvolvimento da etapa final da matéria SRED, realizando as instalações, configurações e conexões dos serviços e servidores APACHE, BIND9, SAMBA, DNS, GATEWAY, BD e WEB. Todos os integrantes do grupo 3 participando direta ou indiretamente do desenvolvimento do projeto deram o seu máximo para alcançar as metas estabelecidas pelo professor Alaelson Jatobá.
Consideramos, sem dúvida que o grande "facilitador" durante todo o transcurso do trabalho foi a metodologia das aulas de “tira dúvidas” ministradas pelo professor.








