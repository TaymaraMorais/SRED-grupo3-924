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

```
```bash
@ns1:~$ dig gw.grupo3.turma924.ifalara.local
```
```bash

```
### 3.2 DNS SLAVE (ns2);

### 3.3 SAMBA (samba);

### 3.4 GATEWAY (gw);

### 3.5 WEB (www);

### 3.6 BD (bd);

## Considerações Finais






