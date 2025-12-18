# Aula 30/10

```bash

    1  batcat /etc/passwd
    2  batcat /etc/group
    3  useradd

    // criando um usuário
    4  useradd -m -s /bin/bash -c "Maria Poliana P. de Paiva" poliana
    5  getent passwd poliana
    6  getent passwd poliana | sed 's/:/\n/g'
    7  getent passwd poliana | sed 's/:/\n/g'| nl
    8  getent gshadow poliana | sed 's/:/\n/g'| nl
    9  getent shadow poliana | sed 's/:/\n/g'| nl

    // criando a senha para meu usuário
   10  passwd poliana

   // criando grupos com meus dois sobrenomes
   11  groupadd pinheiro
   12  groupadd paiva
   13  groups

    // isso deu erro pq nao havia criado os usuários antes
   14  usermod -ag pinheiro maria.pinheiro
   15  usermod -aG pinheiro maria.pinheiro

   // criando os usuarios
   16  useradd maria.pinheiro

   // add os usuarios nos grupos
   17  useradd maria.pinheiro
   18  usermod -aG pinheiro maria.pinheiro
   19  useradd ana.pinheiro
   20  usermod -aG pinheiro ana.pinheiro
   21  useradd elisangela.pinheiro
   22  usermod -aG pinheiro elisangela.pinheiro
   23  getent group pinheiro
   24  useradd socorro.pinheiro
   25  usermod -aG pinheiro socorro.pinheiro
   26  getent group pinheiro
   27  getent group paiva
   28  useradd paula.paiva
   29  useradd antonio.paiva
   30  useradd eric.paiva
   31  useradd miro.paiva
   32  usermod -aG paiva paula.paiva
   33  usermod -aG paiva antonio.paiva
   34  usermod -aG paiva eric.paiva
   35  usermod -aG paiva miro.paiva

    // visualizar os grupos
   36  getent group paiva
   37  getent group
   38  grep paiva /etc/passwd
   39  grep silva /etc/passwd
   40  grep carneiro /etc/passwd

   // ver ip do terminal
   41  ip
   42  ip address
   43  ip -br a
   44  ip -br -4 a
```

chown e chgrp aceitam a opção -R


# Aula 04/05

```bash

getent passwd # lista usuário
getent group # lista grupos


# Propriedades
# Mudar a propriedade de um diretório e seu conteúdo recursivamente:
chown -v -R elisangela.pinheiro:pinheiro /srv/verde // sudo chown {opção} {usuario}:{grupo} {diretorio}

groupdel {grupo}

usermod -c "Maria Paula de Paiva Dias" paula.paiva 

```

Modo Octal (Numérico)
Cada permissão tem um valor numérico: r=4, w=2, x=1. A soma dos valores determina o nível de permissão para cada categoria (proprietário, grupo, outros). 

7 (rwx): Leitura, escrita e execução (4+2+1)
6 (rw-): Leitura e escrita (4+2)
5 (r-x): Leitura e execução (4+1)
4 (r--): Apenas leitura (4)
0 (---): Nenhuma permissão 


---
> pesquisar sobre osquery

# Aula 06/11


```bash
// mudar o que pertence ao grupo
sudo chgrp {grupo} {arquivo  ou diretorio}

ls -ld {caminho}


```
Para entrar em um diretorio, é preciso ter permisão de execução

SHEBANG: é a primeira linha que indica qual vai ser o interpretador

--- 

# Aula 25/11

1. Criar partições
2. Formatar partições
4. Montar e desmontar partições

- Buscar discos: `lsblk | grep disk` ou para entrar -> `fdisk -l /dev/<nome_disco>`
- Para editar: `fdisk /dev/<nome_disco>`
- Fazer uma fundação/formatar: `mkfs` escolhe um tipo...
    - Exemplo: `mkfs.ext4 /dev/<nome_particao>`      
- Montar: `mount <particao> <diretorio>`
- Montagem permanente: `<nome_editor> /etc/fstab`
   
## Comandos fsdisk
m: ajuda
p: exibir partições
n: criar nova partição
t: alterar o tipo da partição
q: sair sem salvar
w: sair e salvar 

## Partições

1. Primaria
2. Extendida

# Aula 11/12

## Processos
```bash
~ # pstree -p
init(1)-+-crond(627)
        |-getty(634)
        |-syslogd(337)
        `-udhcpc(431)
```
### Conceitos
BIOS -> Boot Manager -> Kernel -> init(1)

1. O processo cron (crond) no Linux é um daemon (serviço de sistema) usado para agendar a execução automática de comandos ou scripts em datas e horários específicos. Ele funciona como um gerenciador de tarefas que opera em segundo plano, permitindo a automação de rotinas repetitivas sem intervenção manual.
2. 

---

# Aula 16/12

- Fazer conexão ssh:
```bash
   6 apk add iproute2
   7 setup-apkrepos -c
   8 apk add iproute2
   9 apk add openssh
  10 service sshd start
  11 rc-update sshd
  12 rc-update add sshd
  13 apk add zsh
  14 ss -tl
  15 ip -br -c -4 address
  16 apk add gitea etckeeper
```
- Ativar o espelhamento da comunidade e iniciar o gitea:
```bash
echo 36 | setup-apkrepos -c # ja adiciona ao setup-apkrepos o espelho 36

service gitea start
rc-update add gitea
```
- Instalação do mariadb
```bash
  18 apk add mariadb mariadb-client
  19 mariadb-install-db --user=mysql --datadir=/var/lib/mysql
  20 service mariadb start
  21 rc-update add mariadb
  22 mariadb-secure-installation

```
- Configurar o maria db e iniciar o gitea:
```bash
  32 mariadb -u root -p

  33 micro /etc/gitea/app.ini
  34 micro /etc/my.cnf.d/mariadb-server.cnf

  35 service mariadb restart
  36 ss -tnl
  37 service gitea start
  38 rc-update add gitea
  39 service gitea stop
  40 service gitea start
```
```bash
  42 apk add caddy43 micro /etc/caddy/Caddyfile 
  44 ss -tnl
  45 rc-service caddy start
  46 ss -tnl
  47 micro /etc/gitea/app.ini 
  48 rc-service caddy restart
  49 micro /etc/gitea/app.ini 
  50 rc-service caddy restart
  51 micro /etc/gitea/app.ini 
  5  52 rc-service caddy restart
```

