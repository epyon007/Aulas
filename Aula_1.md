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
[kernel] [nodename] [kernel-release]          [kernel-version]                              [machine - processor - hardware platform]   [SO]

  uname -a   /- exibe todas as informações (omite processador e plataforma se forem desconhecidos)
  uname -r   /- exibe a versão do lançamento do kernel
  uname -v   /- mostra a data em que o kernel foi criado
  uname -n   /- mostra o nome da máquina

As vezes precisamos executar comandos que exigem permissões que usuários comuns não possuem, nesses casos utilizamos o *sudo*.

~ sudo ifconfig - utilizamos o sudo para executar comandos com privilegio de administrador.

Para checar os usuários que estão configurados para executar o sudo, é necessário acessarmos o arquivo */etc/sudoers*

Exemplo de entrada:

```shell
tiago ALL=(ALL:ALL) ALL
```

ex de entrada para suprimir senha:
```shell
tiago ALL=(ALL:ALL) NOPASSWD: ALL
```





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

```bash
~ tree /tmp/backup
```


######  tree -a [path]   /- lista todos os arquivos
######  tree -d [path]   /- lista apenas diretórios


~ mkdir -m 777 arquivo1   /- cria o arquivo com as permissões préviamente definidas
~ mkdir -m 700 arquivo2

~ ls -ld arquivo1 arquivo2

<!listar arquivos para comparar as diferenças de permissão definidas nos comandos de criação de diretórios.>

~ stat arquivo1
~ stat arquivo2

No dia a dia é bastante comum movermos, copiar ou renomear arquivos e diretórios, para realizar essas ações é necessário conhecer os comandos corretos de forma a facilitar o trabalho.

Para copiar arquivos e diretórios, utilizamos o comando 'cp':
``` bash
~ cp /etc/hosts /tmp
```

<!Usar o 'cat' para exibir o conteúdo do arquivo para mostrar aos alunos que o arquivo foi realmente copiado>

#### Opções úteis

```bash
cp -p [origem] [destino] # Preserva os atributos dos arquivos como modo, dono do arquivo, horarios de acesso e/ou modificação etc.

cp -r ou -R [origem] [destino] # Copia diretórios recursivamente

cp -v [origem] [destino] # Exibe o status de progresso da cópia, listando os arquivos que estão sendo copiados naquele momento.

cp -i /etc/hosts /tmp # O -i é um parâmetro de interatividade, onde o sistema pergunta para se você realmente deseja realizar a operação.
```

Para renomear e mover arquivos, utilizamos o 'mv':

```bash
~ mv /tmp/hosts .
~ mv hosts /tmp/servers
```

#### Opções úteis

```bash
~ mv -f [origem] [destino] # Não pergunta ao usuário antes de sobrescrever um arquivo.
~ mv -i [origem] [destino] # Pergunta ao usuário antes de sobrescrever um arquivo.
~ mv -n [origem] [destino] # Não sobrescreve um arquivo existente.
~ mv -v [origem] [destino] # Exibe o status de progresso da movimentação de arquivos, listando o que está sendo movido naquele momento.
```

Para realizar a remoção de arquivos, utilizamos o comando 'rm'. Para remover diretórios, utilizamos o 'rmdir'.

Antes de realizar a remoção, vamos fazer um backup do arquivo que vamos remover:

```bash
~ mkdir /tmp/confs
~ cp /etc/*.conf /tmp/confs
```

Agora que fizemos a cópia, vamos remover os arquivos e diretórios utilizando os comandos 'rm' e 'rmdir', respectivamente:

##### Importante: O comando 'rmdir' remove apenas diretórios vazios

```bash
~ rm /tmp/confs/*.conf
~ rmdir /tmp/confs
```
Obs:

#### Opções úteis do comando 'rm'

```bash
~ rm -f [arquivo] # Força a remoção de arquivos, ignorando arquivos inexistentes.
~ rm -i [arquivo] # Questiona o usuário antes e realizar a remoção dos arquivos.
~ rm -r [arquivo] # Remove diretórios e seus conteúdos recursivamente.
~ rm -v [arquivo] # Exibe o status de progresso da remoção dos arquivos/diretórios.
```

```bash
~ rmdir -v [diretório] # Exibe o status de progresso da remoção do(s) diretório(s).
~ rmdir -p [diretório] # Faz a remoção do diretório especificado e de seus diretórios pais, quando informado o caminho correspondente.
```

##### Criação de links

Dentro de um sistema Linux, podemos criar links simbólicos e links físicos, conhecidos respectivamente como softlinks e hardlinks.

- Links simbólicos (softlinks): São links que equivalentes a atalhos para arquivos, estes links podem ter como alvos diretórios ou arquivos que estejam em filesystems distintos.
  - O tamanho de um arquivo de link simbólico é exatamente igual a quantidade de caracteres do caminho do alvo.
  - O link será quebrado apenas se o arquivo/diretório alvo for movido/apagado.

Para realizar a criação de um link simbólico, devemos utilizar o comando 'ln' com a opção '-s', conforme a sintaxe abaixo:

ln -s [caminho arquivo original] [caminho arquivo softlink]

A seguir temos um exemplo prático, a criação de um link simbólico para o diretório '/var/log'.

```bash
~ ln -s /var/log /opt/log
```

- Links físicos (hardlinks): São um ou mais nomes que possuem como alvo um 'inode' de um sistema de arquivos, estes links não podem ter um diretório como alvo, apenas arquivos. Além disso, não podem ter como alvo arquivos que estão em um filesystem distinto.
    - Hardlinks para um mesmo inode, possuem o mesmo tamanho do arquivo para o qual ele está apontando.
    - Os arquivos não são apagados enquando existir links que possuem como alvo um inode específico.

Para realizar a criação de um link físico, basta utilizar o comando 'ln' sem qualquer opção e informar os caminhos correspondentes:

ln [caminho arquivo original] [caminho hardlink]

Exemplo prático para criação de hardlink para o arquivo '/etc/hosts'.

```bash
~ ln /etc/hosts /home/tiago/link_fisico
```

#### Aula 1.2 Documentação e Filtros

É muito comum ter alguma dúvida com relação a comandos a serem utilizados no shell, especialmente quando não se está acostumado a executar alguns comandos específicos.

Para isso, podemos utilizar algumas ferramentas de apoio fornecidas pelo sistema.

Um exemplo disso é o comando 'man', que exibe manuais de comandos do sistema.

No comando a seguir, exibiremos um manual do comando 'ls', onde é exibida uma descrição da função do comando, bem como suas opções correspondentes, além de outras informações.

```bash
~ man ls
```

Podemos também consultar uma descrição resumida relacionada a um comando especifico,

```bash
~ man -k vim
```

Para atualizar a base de dados de manuais, é necessário utilizar o comando mandb. Ele atualiza o banco de dados relacionado aos manuais de comandos do sistema

```bash
~ mandb
```

Além do comando 'man', temos também como ferramenta de apoio o comando 'help', que também exibe descrição sobre a função do comando consultado, bem como suas respectivas opções.

```bash
~ help
~ help unset
```

Existem também um comando que possui a mesma função do **'man -k [comando]'**, o comando 'apropos'.

```bash
apropos unset
```

Além destas ferramentas já citadas, podemos utilizar também a opção **--help** nos comandos que utilizarmos.

```bash
~ passwd --help
~ vim --help
```

##### Redirecionamento

<!Checar conhecimento dos alunos sobre dispositivos de entrada e saída>

<!Realizar o desenho exemplificando entrada e saída padrão>

Ao utilizar qualquer computador, nós precisamos de alguns dispositivos que permitam esta interação com o computador, são os chamados 'Dispositivos de entrada e saída'.

Enquanto trabalhamos, estes dispositivos e enviam e recebem sinais, sendo as entradas enviadas por meio de mouse ou teclado e as saídas recebidas em monitores ou impressoras.

Fundamentalmente, existem 3 tipos de sinais:

- stdin (Standard Input) - Entrada de dados a serem processados pelo computador, utilizando mouse, teclado, scanner, etc. Dentro do shell, o dispositivo de entrada padrão é o teclado;

- stdout (Standard Output) - Informações de saída que são resultado de processamentos de comandos enviados a partir da entrada padrão, a saída pode ser vista a partir de monitores, impressoras, etc;

- stderr (Standard Error) - Informações de saída de erros que são resultado de processamentos enviados a partir da entrada padrão. Assim como no **stdout**, seu destino também é o monitor, mas este erro padrão também pode ser redirecionado para um arquivo, se necessário.

Conhecendo este conceito, podemos agora falar sobre redirecionadores, que servem para nos auxiliar na manipulação de entradas e saídas dentro de sistemas Linux.

Vamos começar com um exemplo prático:

```bash
~ ls /etc/*.conf > /tmp/lista.txt
```
No comando acima, nós listamos todos os arquivos que estão no diretório **/etc** e que terminam com os caracteres **.conf**, após a realização do comando todos os dados processados pelo computador foram inseridos no arquivo **/tmp/lista.txt**.

Ao utilizar o redirecionador **'>'**, toda a saída do comando sobrescreverá o arquivo para o qual ela foi enviada, não preservando dados que já estavam naquele arquivo.

Caso o administrador não queira que os dados anteriores sejam sobrescritos, ele deverá utilizar um redirecionador diferente, o **'>>'**. Ao utilizar **'>>'**, a saída do comando será adicionada ao final do arquivo, logo após os dados que já estavam salvos.

```bash
~ ls /var/log/*.log >> /tmp/lista.txt
~ cat /etc/passwd | wc -l
```
O caractere PIPE ( **'|'** ), serve para redirecionarmos a saída de um comando como entrada de outro.

Por exemplo, abaixo podemos utilizar o comando 'cat' no arquivo **/etc/passwd** e contar quantas linhas o arquivo possui com o comando **wc** e a opção **-l**, apenas em uma linha de comando.

```bash
~ cat /etc/passwd | wc -l
```

```bash
cat /etc/passwd | tr [:lower:] [:upper:]
cat /etc/passwd | tr [a-z] [A-Z]
```

```bash
cut -d : -f 1 /etc/passwd
cut -d : -f 1 /etc/passwd | sort | tr [:lower:] [:upper:]
```

```bash
awk -F : '{print $1}' /etc/passwd
```

```bash

```
```bash

```
```bash

```
```bash

```
```bash

```
```bash

```
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
