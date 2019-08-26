### Aula 01 - Comandos Essenciais

Inicialmente, vamos conhecer alguns comandos básicos usados no dia a dia.
Afinal, no cotidiano precisamos realizar atividades simples como navegar entre diretórios, criar, renomear ou deletar arquivos e não saber fazer essas ações limita completamente qualquer atividade a ser realizada via linha de comando.

#### Aula 1.1 Trabalhando na linha de comando

~ whoami

~ last - vai listar apenas os últimos evento de logins (como realização de SSH, logar na interface gráfica, etc) Abrir um outro shell com outro usuário numa sessão em que já se está logado, nao é considerado um evento de login mas sim uma escalação de privilégios.

~ passwd - realiza troca de senha de usuário ou grupo, o usuário pode alterar apenas a senha de sua própria conta. Para alterar a senha de outros usuários o perfil que está realizando a mudança precisa ter privilégios de root.

  passwd -d [login]    /- *[delete]* remove a senha da conta indicada;
  passwd -l [login]    /- *[lock]* trava a conta indicada;
  passwd -u [login]    /- *[unlock]* destrava a conta indicada.

~ hostname - exibe o nome do host da máquina onde se está executando o comando.

  hostname -f     /- *[fqdn]* - versão longa do hostname
  hostname -d     /- *[domain]* - nome de dominio
  hostname -i     /- *[ip-address]* - mostra todos os endereços ip do host


<ADVANCED>

~ hostnamectl - serve para exibir ou alterar informações do hostname.

</ADVANCED>


~ uname - exibe algumas informações relacionadas ao sistema e seu kernel.

Linux     benihime  5.0.0-23-generic  #24~18.04.1-Ubuntu SMP Mon Jul 29 16:12:28 UTC 2019   x86_64 x86_64 x86_64                         GNU/Linux
[kenrel] [nodename] [kernel-release]          [kernel-version]                              [machine - processor - hardware platform]   [SO]

  uname -a   /- exibe todas as informações (omite processador e plataforma se forem desconhecidos)
  uname -r   /- exibe a versão do lançamento do kernel
  uname -v   /- mostra a data em que o kernel foi criado
  uname -n   /- mostra o nome da máquina

As vezes precisamos executar comandos que exigem permissões que usuários comuns não possuem, nesses casos utilizamos o *sudo*.

~ sudo ifconfig - utilizamos o sudo para executar comandos com privilegio de administrador.

Para checar os usuários que estão configurados para executar o sudo, é necessário acessarmos o arquivo */etc/sudoers*

ex de entrada: tiago ALL=(ALL:ALL) ALL

## verificar configuração da minha maquina de casa para sudo nao exigir senha.

#### Aula 1.2 Documentação e Filtros

Listagem de arquivos

Dentro do shell, podemos utilizar os comandos *ls* e *pwd* para listar arquivos e checar em qual pastas estamos, respectivamente.

~ pwd

~ ls

  ls -d   /- lista os diretórios e não seu conteúdo (usar dois exemplo *ls /etc*)
  ls -a   /- lista todos os arquivos, inclusive os iniciados com ""**.**"", que são arquivos ocultos.
  ls -lh  /- -l indica a exibição em formato de lista, o h indica uma saída "mais legivel" para o operador.
  ls -lhrt  /- o r, indica uma inversão na ordem da exibição , o t ordena por horario de modificação, sendo os mais novos primeiro.
  ls -R   /- o R, indica uma listagem recursiva nos diretórios, serão listados todos os arquivos e diretórios dos diretórios subsequentes.


Caracteres coringa

(*****) - Coringa combina qualquer caractere conjunto de caracteres.

~ ls -l /dev/sda*   /- lista dispositivos que começam com **sda** e possuam qualquer caractere no restante do nome.

(**?**) - Coringa combina um único caractere.

~ ls -l /dev/sd??   /- lista dispositivos que iniciem com **sda** e possuam apenas mais dois caracteres no restante do nome.

(**[]**) - Coringa combina um intervalo de caracteres.

~ ls -l /dev/sda[15]  /- lista dispositivos iniciados com **sda** e possuam os caracteres 1 e 5 em seu nome.

(**{}**) - Coringa combina uma gama de expressões

~ ls -l /dev/sda{1..5}  /- lista dispositivos iniciados com **sda** e possuam os caracteres de 1 a 5 em seu nome.


Para realizarmos a criação de diretórios, utilizamos o comando **mkdir**:

~ mkdir /tmp/backup   /- cria o diretório backup dentro do diretório /tmp.


~ mkdir -p /tmp/backup/data/confs   /- cria a árvore de diretórios recursivamente. Caso um diretório pai não exista, ele será criado conforme a necessidade.
~ ls -R /tmp/backup/data


~ touch  - Serve para atualizar os horários de modificação e acesso de cada arquivo para o horário atual.

<!Usar o comando stat para verificar um arquivo e exibir os horarios do arquivo.>

  touch -a [arquivo]   /- altera apenas o horario de acesso ao arquivo
  touch -m [arquivo]   /- altera apenas o horario e modificação do arquivo



Para listar os arquivos e diretórios em formato de árvore, nós temos o comando tree. Ele exibe de forma hierárquica a estrutura de diretórios.

~ tree /tmp/backup

  tree -a [path]   /- lista todos os arquivos
  tree -d [path]   /- lista apenas diretórios


~ mkdir -m 777 arquivo1   /- cria o arquivo com as permissões préviamente definidas
~ mkdir -m 700 arquivo2

~ ls -ld arquivo1 arquivo2

<!listar arquivos para comparar as diferenças de permissão definidas nos comandos de criação de diretórios.>

~ stat arquivo1
~ stat arquivo2

No dia a dia é bastante comum movermos, copiar ou renomear arquivos e diretórios, para realizar essas ações, utilizamos coman

#### Aula 1.3 Localizar arquivos e expressões regulares

### Aula 02 - Editor de Textos e Shell
#### Aula 2.1 Conhecendo o Editor VIM
#### Aula 2.2 VIM Avançado
#### Aula 2.3 Configurar Shell e Timezone

### Aula 03 - Instalação de Programas
#### Aula 3.1 Gerenciadores de Pacotes
#### Aula 3.2 Gerenciar pacotes DPKG e RPM
#### Aula 3.3 Compilação de Pacotes

### Aula 04 -  Gerenciamento de Usuários
#### Aula 4.1 Administrando Usuários
#### Aula 4.2 Permissões Especiais
#### Aula 4.3 Configuração do Sudo
