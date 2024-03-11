# Aula 2 - OAuth 2.0

## OAuth

Permite uma aplicação aceder a recursos de utilizadores mantidos por um serviço/servidor, assumindo o papel de **Authorization Server**.

Neste fluxo de autenticação, temos:
- **Resource Owner**: Utilizador que possui/quer aceder os seus recursos;
- **Aplicação (Client)**: Aplicação que será a mediadora entre os **Resource Owner** e o **Resource Server**;
- **Authorization Server**: Servidor que irá autenticar o **Resource Owner** e emitir tokens (*) de acesso à aplicação;
- **Resource Server**: Servidor que possui os recursos que o **Resource Owner** quer aceder.

(*) Este token contém informação sobre a quais recursos o **Resource Owner** tem acesso e *timestamp* dos mesmos.

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
- **Web Application**: Cliente que é executado num servidor *web*.
- **User Agent**: Cliente executa o programa numa *user agent* (navegador).
- **Native Application**: Cliente que é executado num dispositivo do utilizador.

## Registo de Aplicações (*Clients*)

Os *clients* que acessam a servidores OAuth devem ser registados. 

Isto inclui tanto:
- **Informação legal** sobre a aplicação (termos de serviço, etc);
- **Informação operacional** sobre a aplicação (métodos de autenticação, etc).

## *Tokens* OAuth

É um conjunto de bytes aleatórios que fazem sentido apenas para o **Resource Server** e o **Authorization Server**.

- **Authorization grant**: Permite, após autenticação do *resource over* e autorização, obter acesso a um recurso.
- **Access token**: Permite aceder a um recurso.
- **Refresh token**: Permite obter um novo *access token* sem a necessidade de autenticação do *resource owner*.

### *Bearer Tokens*

São *tokens* que são enviados pelo **Resource Owner** para o **Resource Server** para aceder aos recursos.

Nota: Os *clients* podem fornecer *tokens* de acesso a terceiros.

## OAuth flows



Existem vários fluxos de autenticação OAuth, estes têm alguns aspetos em comum:

| OAuth flows          | *frontend* | *backend* | interage com o *user* | *client secret* |
| -------------------- | ---------- | --------- | --------------------- | --------------- |
| Authorization code   | Sim        | Sim       | Sim                   | Sim             |
| Implicit grande      | Sim        | Não       | Sim                   | Não             |
| Password credentials | Sim        | Sim       | Sim                   | Sim             |
| Client credentials   | Não        | Sim       | Não                   | Sim             |

### *Authorization code flow*

Modelo mais seguro, que segue a arquitetura *3-legged* (*Client*, *Resource Owner*, *Authorization Server*).

Funciona da seguinte forma:
1. OAuth *server* autentica o *resource owner*: nome de utilizador e palavra-passe, ou outro método;
2. OAuth *server* autentica o *client*: ID do cliente + segredo do cliente + autorização HTTP;
3. *Client* autentica o OAuth *server*: Certificado + URL;

Nota: Para isto é necessário o armazenamento dos *tokens*, ID do cliente e segredo do cliente.

### *Implicit flow (grant)* 

Normalmente utilizado em *Single Page Applications* (SPA), onde não existe um *backend*. É uma maneira de obter um *access token* sem a necessidade de um *client secret*.

Funciona da seguinte forma:
1. *Browser* solicita um *access token* e é feito (se necessário) uma autenticação do utilizador;
2. *Browser* recebe o *access token* e pode aceder aos recursos.

### *Resource owner password credentials flow*

Normalmente utilizado em *confidential clients*. Existe a partilha das credenciais do *resource owner* com o *client* (para isto funcionar, o *client* deve ser confiável).

Funciona da seguinte forma:
1. *Client* solicita um *access token* com as credenciais do *resource owner*;
2. *Client* recebe o *access token*.
3. *Client* pode aceder aos recursos.

### *Client credentials flow*

Utiliza a arquitetura *2-legged* (*Client*, *Resource Server*). O *client* obtém um *access token* diretamente, **não necessitando de um *resource owner* para autenticação**.

Funciona da seguinte forma:
1. *Client* solicita um *access token* com as suas credenciais (ID do cliente + segredo do cliente);
2. *Client* recebe o *access token*;
3. *Client* pode aceder aos recursos.

### *Proof Key for Code Exchange* (PKCE)

É um método de segurança para o *Authorization Code Flow*. Utiliza um *code challenge*, sendo este um *hash* de um *code verifier*.

### *Device authorization grant*

Utiliza um segundo dispositivo para fazer a autenticação e autorizar o acesso a um recurso (e.g. *smartphone*, *tablet*).

# Prática 2 - Gestão de recursos e monitorização com `cgroups`

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







