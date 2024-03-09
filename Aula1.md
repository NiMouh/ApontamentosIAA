# Aula 1 - Introdução a Integridade, Autenticação e Autorização

## Definições

- **Sujeito**: entidade que exibem uma atividade (processos, computadores, redes, etc.);
- **Objeto**: recurso que é alvo de uma ação (ficheiros, memória, etc.);

### Triple A

- **Autenticação**: verificar a identidade do sujeito;
- **Autorização**: verificar se o sujeito tem permissão para aceder ao objeto;
- **Accounting**: registar o acesso.

### Level of Assurance (LoA)

É composto por o **quanto** confiamos na identidade do sujeito.

## Controlo de acesso

São as **politicas** e **mecanismos** que **mediam o acesso** de um sujeito a um objeto.

Existem dois tipos de controlo de acesso:
- **Controlo de acesso discricionário (DAC)**: o dono do objeto / certos sujeitos decidem quem pode aceder ao objeto;
- **Controlo de acesso obrigatório (MAC)**: o sistema decide quem pode aceder ao objeto.

### ACL (Access Control List)

Lista de permissões associadas a um objeto. Normalmente, as ACLs estão armazenadas no objeto.

## Modelos de controlo de acesso

Existem dois tipos de acesso:
 - **Acesso físico**: contacto físico entre o sujeito e o objeto de acesso;
 - **Acesso eletrónico**: contacto orientado por um sistema eletrónico.

### Matriz de acesso
Tabela que define as permissões de acesso de cada sujeito a cada objeto. 

Exemplo:

|     | Objeto 1 | Objeto 2 | Objeto 3 |
| --- | -------- | -------- | -------- |
| S1  | R        | W        | R        |
| S2  | W        | -        | -        |
| S3  | -        | R        | W        |
| Sn  | -        | -        | -        |

### Capacidades vs Grupos

- **Capacidades** são um conjunto de permissões associadas a um sujeito;
- **Grupos** são um conjunto de sujeitos que partilham as mesmas permissões.

### RBAC (Role-Based Access Control)

Controlo de acesso baseado em funções. Cada sujeito tem uma ou mais funções, e cada função tem uma ou mais permissões.

Existem quatro variantes:
- **RBAC0**: não existe hierarquias, nem restrições;
- **RBAC1**: existe hierarquia (herança de permissões);
- **RBAC2**: existem restrições de acesso;
- **RBAC3**: RBAC1 + RBAC2.

### CBAC (Context-Based Access Control)

Controlo de acesso baseado em **eventos contextuais**.

Exemplo:
 - Stateful packet filtering: contêm o seguimento de todas as conexões da rede, e verifica se os pacotes são parte de uma conexão válida;

#### Chinese Wall Policy

Política que previne um sujeito de aceder a informação de duas entidades concorrentes (conflito de grupos).

### ABAC (Attribute-Based Access Control)

Controlo de acesso baseado em **atributos**, sendo estes, *tokens* que representam o acesso a um objeto.

Arquitetura OASIS XACML (eXtensible Access Control Markup Language):
 - *PEP* (Policy Enforcement Point): onde as políticas são aplicadas (ex: porta de entrada);
 - *PDP* (Policy Decision Point): onde as decisões das políticas são tomadas (ex: leitor de cartões);
 - *PAP* (Policy Administration Point): onde as políticas são definidas (ex: administrador);
 - *PIP* (Policy Information Point): onde as informações das políticas são armazenadas (ex: base de dados).

### Break Glass Model

Modelo que permite que um sujeito aceda a um objeto sem ter as permissões necessárias, em situações de emergência.

Nota: **Nunca** devem ser colocados sem **um processo de revisão**.

### Separação de funções

Princípio que previne que um sujeito tenha permissões para realizar todas as funções de um processo, fundamental para prevenir fraudes e erros.

**ISACA** (*Information Systems Audit and Control Association*).

## Principios de segurança

### Principio do menor privilégio (Least Privilege Principle)

Um sujeito deve ter **apenas** as permissões necessárias para realizar o seu trabalho, **nada mais**. Isto é algo fácil de implementar, porém difícil de manter a longo prazo.

## Modelos de fluxo de informação

A autorização é aplicada a **fluxos de informação**. Tem como propósito prevenir que informação sensível/perigosa seja trocada.

### Multilevel Security (MLS)

Modelo que previne que informação de diferentes níveis de segurança seja trocada, onde os sujeitos (roles) têm um nível de segurança associado.

Níveis de segurança (p/ organizações militares):
- **Top Secret**: informação que pode causar danos graves;
- **Secret**: informação que pode causar danos moderados;
- **Confidential**: informação que pode causar danos leves;
- **Restricted**: informação que pode causar danos mínimos.
- **Unclassified**: informação que não pode causar danos.

Níveis de segurança (p/ organizações civis):
 - Toda a informação é confidencial (não existe maturidade para classificar informação).

### Categorias de segurança

Um objeto pode pertencer a diferentes categorias de segurança e pertencer a diferentes níveis de segurança (ex: um ficheiro pode ser confidencial e secreto).

#### Labels segurança

Informação que identifica o nível de segurança de um objeto;

É representado por: 

`Label = (Categoria, Nível)`

Nota: Não é por um sujeito ter um nível de segurança que ele pode aceder a informação de um nível inferior. A informação dentro do mesmo nível de segurança é **facilitada** e a informação entre níveis de segurança é **controlada**.

### Bell-LaPadula Model

Este modelo usa politicas de controlo de acesso para controlar fluxos de informação. Este usa um modelo de *state-transition*, onde a cada *state* estão sujeitos, objetos e uma matriz de acesso para a informação presente.

As regras são definidas por:
- **Simple Security Condition (no read up)**: S pode ler O se e só se L(S) >= L(O), o nível de segurança de S é maior ou igual ao nível de segurança de O;
- ***-Property (no write down)**: S pode escrever O se e só se L(O) >= L(S), o nível de segurança de O é maior ou igual ao nível de segurança de S.

### *Discretionary Security Model*

Modelo baseado em controlo de acesso discricionário (DAC).

### Strong Star Property

S pode ler O se e só se:
 - L(S) == L(O), o nível de segurança de S é igual ao nível de segurança de O.

### Principio de Tranquilidade (*Tranquility Principle*)

Segundo o principio de tranquilidade, o acesso a um objeto pode ter:
 - *Strong tranquility*: o nível de segurança de um objeto não pode ser alterado;
 - *Weak tranquility*: o nível de segurança de um objeto pode ser alterado, caso o sistema não seja comprometido.

### Biba Model

Semelhante ao Bell-La Padula, porém com as regras invertidas:
 - **Simple Integrity Condition (no read down)**: S pode ler em O se e só se L(S) <= L(O);
 - **-Property (no write up)**: S pode escrever O se e só se L(O) <= L(S).

Nota: Contêm uma propriedade de **invocação** que previne que um sujeito com um nível de segurança inferior possa invocar um sujeito com um nível de segurança superior.

### Clark-Wilson Model

Modelo que previne que um sujeito possa alterar um objeto de forma não autorizada, ou seja, feito por uma pessoa sem acesso e de modo **não integro**.

Contêm dois tipos de objetos:
 - **Constrained Data Item (CDI)**: objetos que são protegidos por regras de integridade;
 - **Unconstrained Data Item (UDI)**: objetos que não são protegidos por regras de integridade.

Pode ser feito através de:
 - **Transformation Procedure (TP)**: procedimentos que alteram os CDIs (recebe como input um CDI/UDI e devolve um CDI);
 - **Integrity Verification Procedure(IVP)**: procedimentos que verificam a integridade dos CDIs;

Existem dois conjuntos de regras:
 - Certificação;
 - Enforcement;
