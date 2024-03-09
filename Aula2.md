# Aula 2 - OAuth 2.0

## OAuth

Permite uma aplicação aceder a recursos de utilizadores mantidos por um serviço/servidor, assumindo o papel de **Authorization Server**.

Neste fluxo de autenticação, temos:
- **Resource Owner**: Utilizador que possui/quer aceder os seus recursos;
- **Aplicação (Client)**: Aplicação que será a mediadora entre os **Resource Owner** e o **Resource Server**;
- **Authorization Server**: Servidor que irá autenticar o **Resource Owner** e emitir tokens (*) de acesso à aplicação;
- **Resource Server**: Servidor que possui os recursos que o **Resource Owner** quer aceder.

(*) Este token contém informação sobre a quais recursos o **Resource Owner** tem acesso e *timestamp* dos mesmos.

### *Authorization Endpoint*

É o endpoint que o **Resource Owner** acede para autenticar-se e autorizar a aplicação a aceder aos seus recursos diretamente pelo **Authorization Server**.

Exemplo: Iniciar sessão com o Google, Facebook, etc.

### *Redirection Endpoint*

É o endpoint que a aplicação (*client*) fornece ao **Authorization Server** para onde o **Resource Owner** será redirecionado após a autenticação.

## *Communication endpoints*

É um serviço que permite **autenticar** o *resource owner* (utilizador).

Delega o acesso a recursos protegidos a uma aplicação (*client*) e envia uma autorização **concedida** para um **endpoint de redirecionamento**. 

Existem 3 tipos de *endpoints*:
- **Authorization Endpoint**: Endpoint que o *resource owner* acede para autenticar-se e autorizar a aplicação a aceder aos seus recursos diretamente pelo **Authorization Server**.
- **Token Endpoint**: Endpoint que a aplicação (*client*) acede para obter um token de acesso.
- **Redirection Endpoint**: Endpoint que a aplicação (*client*) fornece ao **Authorization Server** para onde o **Resource Owner** será redirecionado após a autenticação.

## Tipos de Aplicações (*Clients*)

O tipo é relativo á **capacidade de manter confidencialidade das suas credenciais**.

### *Public Clients*

São aplicações que não conseguem manter segredo, como aplicações *web*, *mobile*, etc.

### *Confidential Clients*

São aplicações que conseguem manter segredo, como *secure servers*, etc.

## Perfis de Aplicações (*Clients*)

São relativas á **capacidade de interagir com o utilizador e obter autorização**.

Temos:
- **Web Application**: 
- **User Agent**:
- **Native Application**:

## Registo de Aplicações (*Clients*)

Os *clients* que acessam a servidores OAuth devem ser registados. 

Isto inclui tanto:
- **Informação legal** sobre a aplicação (termos de serviço, etc);
- **Informação operacional** sobre a aplicação (métodos de autenticação, etc).

## *Tokens* OAuth

É um conjunto de bytes aleatórios que fazem sentido apenas para o **Resource Server** e o **Authorization Server**.

- **Authorization grant**:
- **Access token**:
- **Refresh token**:

### *Bearer Tokens*

São *tokens* que são enviados pelo **Resource Owner** para o **Resource Server** para aceder aos recursos.

Nota: Os *clients* podem fornecer *tokens* de acesso a terceiros.

## OAuth flows

Existem vários fluxos de autenticação OAuth, sendo os mais comuns:
- **Authorization code flow**: 
- **Implicit flow**: 
- **Resource owner password credentials flow**: 
- **Client credentials flow**: 


# Prática 2 - Gestão de recursos e monitorização com *cgroups*

Controladores `cgroup` são utilizados para limitar recursos de um grupo de processos.

Para listar os controladores disponíveis:
```bash
cat /proc/cgroups
```

O armazenamento encontra-se dividido em **blocos** (conjuntos de bytes), onde uma partição representa um **conjunto desses blocos**. 

Um *mount* permite criar um **sistema de ficheiros** a partir de um bloco de armazenamento, ou seja, organizar os blocos de armazenamento.

O sistema de ficheiros é utilizado para **controlar como os dados são armazenados no dispositivo** ou fornecidos de uma forma virtual pela rede, ou outros serviços.

São um modo de hierarquia, que é criada fazendo `mount` aos controladores no sistema de ficheiros `/sys/fs/cgroup`.

A lista de `cgroups` montados pode ser vista com:
```bash
mount -t cgroup
```

Agora vamos criar um novo cgroup. Para isso vamos à pasta `/sys/fs/cgroup` e criamos uma pasta com o nome do cgroup que queremos criar (`p_limit` no caso).
```bash
sudo mkdir /sys/fs/cgroup/user.slice
cd /sys/fs/cgroup/user.slice/p_limit
```

Para verificar o tipo do cgroup:
```bash
cat cgroup.type
```

Para verificar os controladores disponíveis:
```bash
cat cgroup.controllers
```

Caso não tenha o controlador `pids` disponível, é necessário adicionar com o seguinte comando:
```bash
echo "+pids" > cgroup.controllers
```







