# Aula 2 - OAuth 2.0

## OAuth

Permite uma aplicação aceder a recursos de utilizadores mantidos por um serviço/servidor, assumindo o papel de **Authorization Server**.

Neste fluxo de autenticação, temos:
- **Resource Owner**: Utilizador que possui/quer aceder os seus recursos;
- **Aplicação (Client)**: Aplicação que será a mediadora entre os **Resource Owner** e o **Resource Server**;
- **Authorization Server**: Servidor que irá autenticar o **Resource Owner** e emitir tokens (*) de acesso à aplicação;
- **Resource Server**: Servidor que possui os recursos que o **Resource Owner** quer aceder.

(*) Este token contém informação sobre a quais recursos o **Resource Owner** tem acesso e timestamp dos mesmos.

### Authorization Endpoint

É o endpoint que o **Resource Owner** acede para autenticar-se e autorizar a aplicação a aceder aos seus recursos diretamente pelo **Authorization Server**.

Exemplo: Iniciar sessão com o Google, Facebook, etc.

### Redirection Endpoint

É o endpoint que a aplicação (client) fornece ao **Authorization Server** para onde o **Resource Owner** será redirecionado após a autenticação.

## Tipos de Aplicações (Clients)

O tipo é relativo á **capacidade de manter confidencialidade das suas credenciais**.

### Public Clients

São aplicações que não conseguem manter segredo, como aplicações web, mobile, etc.

### Confidential Clients

São aplicações que conseguem manter segredo, como secure servers, etc.