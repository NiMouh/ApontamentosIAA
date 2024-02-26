# Cheat Sheet de comandos bash shell - Linux

## Comandos básicos

### Listar ficheiros

Comando para listar os ficheiros de um diretório.

Para listar todos os ficheiros de um diretório:
```bash
ls
```

Para listar todos os ficheiros de um diretório, incluindo os ficheiros ocultos:
```bash
ls -a
```

Para listar detalhes de todos os ficheiros de um diretório:
```bash
ls -l
```

Os acessos de leitura, escrita e execução são representados por:

| Tipo de Ficheiro | Owner rwx | Group rwx | Others rwx | Owner | Group | Size | Date | Name |

Os tipos de ficheiros podem ser:
- `-` para ficheiros normais
- `d` para diretórios
- `l` para links
- `c` para dispositivos de caracteres

### Diretórios

**Criar** um diretório:
```bash
mkdir diretório
```

**Apagar** um diretório:
```bash
rmdir diretório
```

**Mudar** de diretório:
```bash
cd diretório
```


### Redirecionamento

Para redirecionar a **saída** de um comando para um ficheiro:
```bash
comando > ficheiro
```

Para redirecionar a **entrada** de um ficheiro para um comando:
```bash
comando < ficheiro
```

Para redirecionar a **saída** de um comando para um ficheiro, **sem apagar o conteúdo do ficheiro** (*append*):
```bash
comando >> ficheiro
```

Para redirecionar a **saída de erro** de um comando para um ficheiro:
```bash
comando 2> ficheiro
```

Para redirecionar a **saída de um comando** para a **entrada de outro**:
```bash
comando1 | comando2
```

### Ficheiros

**Mover** um ficheiro:
```bash
mv ficheiro destino
```

**Apagar** um ficheiro:
```bash
rm ficheiro
```

**Copiar** um ficheiro:
```bash
cp ficheiro destino
```

**Criar** um ficheiro:
```bash
touch ficheiro
```

**Visualizar** o conteúdo de um ficheiro:
```bash
cat ficheiro
```

### Grupos

**Criar** um grupo:
```bash
groupadd grupo
```

**Adicionar** um utilizador a um grupo:
```bash
usermod -a -G grupo utilizador
```

**Remover** um utilizador de um grupo:
```bash
gpasswd -d utilizador grupo
```

**Listar** os grupos de um **utilizador**:
```bash
groups utilizador
```

**Listar** os utilizadores de um **grupo**:
```bash
getent group grupo
```

**Apagar** um grupo:
```bash
groupdel grupo
```

### Utilizadores

**Criar** um utilizador:
```bash
useradd utilizador
```

**Apagar** um utilizador:
```bash
userdel utilizador
```

**Alterar** a password de um utilizador:
```bash
passwd utilizador
```

**Entrar** como um utilizador:
```bash
su utilizador
```

## Controlo de acesso

### Permissões p/ Ficheiros

Comando para alterar as permissões de um ficheiro ou diretório.

Para adicionar permissões de execução a um ficheiro:
```bash
chmod +x ficheiro
```

Para remover permissões de execução a um ficheiro:
```bash
chmod -x ficheiro
```

Para atribuir permissões de leitura, escrita e execução a um ficheiro ao criador do ficheiro:
```bash
chmod u=rwx ficheiro
```

Para atribuir o `setuid` (permite que um ficheiro seja executado com os privilégios do dono) a um ficheiro:
```bash
chmod u+s ficheiro
```

Para atribuir o `setgid` (permite que um ficheiro seja executado com os privilégios do grupo) a um ficheiro:
```bash
chmod g+s ficheiro
```

A atribuições de permissão pode ser feita ao criador (`u`), a um grupo (`g`), ou a todos os utilizadores (`a`).

Nota: Caso não seja especificado o utilizador, o comando assume que é para todos os utilizadores.

### Permissões p/ Owners

Comando para alterar o dono de um ficheiro ou diretório.

Para alterar o dono de um ficheiro:
```bash
chown novo_dono ficheiro
```

Para alterar o dono e o grupo de um ficheiro:
```bash
chown novo_dono:novo_grupo ficheiro
```

### Permissões p/ Grupos

Comando para alterar o grupo de um ficheiro ou diretório.

Para alterar o grupo de um ficheiro:
```bash
chgrp novo_grupo ficheiro
```

### Lista de acessos especifica de um ficheiro

Comando para visualizar e alterar a lista de acessos de um ficheiro.

Para visualizar a lista de acessos de um ficheiro:
```bash
getfacl ficheiro
```

Para **alterar** a lista de acessos de um ficheiro:
```bash
setfacl -m u:utilizador:rwx ficheiro
```

Para **remover** a lista de acessos de um ficheiro de um utilizador:
```bash
setfacl -x u:utilizador ficheiro
```

Para **remover** todas as listas de acessos de um ficheiro:
```bash
setfacl -b ficheiro
```

Para **copiar** a lista de acessos de um ficheiro para outro:
```bash
getfacl ficheiro1 | setfacl --set-file=- ficheiro2
```

### Alterar o diretório raiz

Permite criar um ambiente isolado para um utilizador.

**Executar um comando** num diretório isolado:
```bash
chroot diretório comando
```