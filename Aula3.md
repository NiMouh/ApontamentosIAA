# Aula 3 - Mecanismos de segurança

## Privilégios de gestão Linux

A filosofia do Linux em termos de privilégios é:
- O **root** pode fazer tudo (UID = 0);
- Os outros utilizadores estão sujeitos a verificação com base nos seus privilégios (UID != 0).

## Capabilities

Permite dividir os privilégios do **root** em diferentes grupos de privilégios.

São atributos *per-thread*, ou seja:
- Podem ser propagados para processos filhos (`fork`);
- Podem ser explicitamente herdados por processos filhos (`exec`).

Exemplos de *capabilities*:
- `CAP_CHOWN`: Alterar o dono de um ficheiro;
- `CAP_DAC_OVERRIDE`: Ignorar permissões de acesso a ficheiros;
- `CAP_DAC_READ_SEARCH`: Ignorar permissões de leitura e pesquisa de ficheiros;
- `CAP_KILL`: Enviar sinais a outros processos;
- `CAP_NET_ADMIN`: Executar operações de administração de rede;
- `CAP_SYS_ADMIN`: Executar operações de administração do sistema (mais genérico que `CAP_NET_ADMIN`).

São divididos em *sets*:
- **Efetivas**: usadas pelo kernel para verificar permissões;
- **Herdadas**: passadas para processos filhos;
- **Permitidas**: *superset* limitado;
- **Delimitadas** (*bounding*): limitar *capabilities* ganhas durante execução.
- **Ambiente**: são preservadas durante `exec` de um programa não-privilegiado.

Para ver as *capabilities* de um processo, usar o comando `getpcaps`.

Para definir as *capabilities* de um processo, usar o comando `setpcaps`.

Para saber listas de *capabilities* de um processo, usar o comando `capsh`.

Durante a execução do programa (como root):
- Caso o `EUID = 0` e `RUID = 0`, todas as *capabilities* são efetivas (1);
- Caso o `EUID = 0` e `RUID != 0`, as *capabilities* efetivas são limitadas;

## Control groups (`cgroups`)

Coleção de processos que são agrupados e geridos de forma a terem um conjunto de recursos limitados.

São organizados em hierarquias, onde cada nó pode ter um conjunto de limites de recursos.

Existem duas versões de *cgroups*:
- **v1**: *cgroups* originais;
- **v2**: *cgroups* unificados com *control groups*.

Exemplos de controladores:
- `cpu`: utilização de CPU;
- `memory`: utilização de memória;
- `pid`: # de processos;
- `devices`: acesso/criação a dispositivos.

## Linux Security Modules (LSM)

Framework que permite adicionar novas extensões de segurança (MAC ou *Mandatory Access Control*) ao kernel.

Exemplos de LSM:
- **AppArmor**: MAC p/ aplicações;
- **SELinux**: MAC p/ o *kernel*;
- **Smack**: MAC simplificada p/ o *kernel*;
- **TOMOYO**: MAC baseado em nomeação de objetos.
- **Yama**: MAC p/ controlo de execução de processos.
- **LoadPin**: MAC p/ controlo de carregamento de módulos.
- **SafeSetID**: MAC p/ controlo de `setuid` e `setgid`.

### *Namespaces*

Permitem criar ambientes isolados para processos.

Tipos de *namespaces*:
- **Mount**: Isola o sistema de ficheiros;
- **PID**: Isola a árvore de processos;
- **Network**: Isola a pilha de rede;
- **IPC**: Isola a comunicação entre processos;
- **User**: Isola a identidade do utilizador;
- **UTS**: Isola o nome do host.
- **Cgroup**: Isola o acesso a *cgroups*.

Exemplo de *namespaces* de rede:
```bash	
$ ip netns add namespace_1 # cria
$ ip netns exec namespace_1 iptables -P INPUT DROP # muda a política de entrada
$ ip netns exec namespace_1 iptables -L # lista as regras
```
