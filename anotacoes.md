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







