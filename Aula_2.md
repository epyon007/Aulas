### Aula 02 - Editor de Textos e Shell
#### Aula 2.1 - Editores de Textos

- Vim
O "Vi" é o editor básico do GNU/Linux, e está disponível em grande parte das distribuições Linux, o
vim é uma versão mais completa e com mais recursos do que o "Vi", cujo seu significado é "Vim =
VI iMproved".

#### Outros Editores de Texto
●
Vi – Sem dúvida nenhuma o editor mais famoso de todos os tempos, presente em quase todas
as distribuições.
●
Nano – Editor padrão de muitas distribuições como Debian, CentOS, esse editor é diferente do
“vim” e é muito fácil de ser usado.
● Pico – Muito parecido com o “nano”, este está presente nas distribuições Slackware e Gentoo.
● Mcedit – Editor muito fácil e completo. Seu grande diferencial é a possibilidade da utilização do
mouse, mesmo no ambiente textual.
●
Ed – O editor de textos mais simples no mundo Unix, o “ed” é um editor de linha para terminais
aonde não é possível abrir uma janela de edição.

```bash
touch arquivo1.txt
cat arquivo1.txt
```

```bash
> arquivo2.txt
cat arquivo2.txt
```

```bash
touch -d '01 May 2010 'arquivo1.txt
stat arquivo1.txt
```

- Pico
O histórico, clássico editor de texto para Linux, chama-se "Pico" ("Pine Composer").
Consiste na sessão para edição de texto de um antigo cliente para e-mail (originalmente em Unix)
chamado "Pine“.
O Pine e o Pico, na realidade, não são softwares livres, foram desenvolvidos pelo
Departamento de Computação Aplicada à Comunicação da Universidade de Washington. No início
da Internet, quando a Web ainda não existia, o Pine era o principal cliente para mandar e receber e-
mails.

```bash
~ pico # Para iniciar o editor pico
GNU/LINUX is  OpenSource
```

```bash
CTRL + O
pico.txt <ENTER>
CTRL + X
```

Após inserir o texto desejado, basta seguir a orientação dada pelo menu para realizar ações como navegar dentro do arquivo, recortar e colar textos, salvar o documento, etc.

## Colar figura relacionada a janela de navegação do comando PICO.

Para salvar, basta teclar **'CTRL + O'**.

Após apertar as teclas, será solicitado o nome do arquivo a ser salvo, já que ele não foi atribuido no momento da abertura do arquivo.

Para sair sem salvar, basta teclar **'CTRL + X'**.

- nano

Nano é um editor de texto que deve ser executado a partir de um terminal, sua distinção
reside na simplicidade.
É um clone do antigo editor de texto Pico, o editor para o cliente de e-mail Pine, que foi muito
popular nos anos 1990, em UNIX e sistemas do tipo UNIX.
O Pine foi substituído pelo Alpine e o Pico pelo Nano, mas algumas coisas não mudaram -
assim como a simplicidade de edição com o Nano.

```bash
~ nano
GNU/LINUX is OpenSource
```

```bash
CTRL + O
nano.txt
CTRL + X
```

# Inserir figura de navegação do comando NANO

As teclas de atalho para realização de comandos dentro do NANO são basicamente as mesmas utilizadas no PICO

### Editor de texto Vim
O Vi é um dos mais antigos, (1976), editores de texto em linha de comando para Unix e
Linux. Derivado do Ed, do Ex, Joe e de outros editores de linha rudimentares.
O Vim (Vi Improved) é uma versão mais poderosa e maior em termos de espaço em disco e
requisitos de memória do editor de texto vi.


```bash
~ vimtutor # Utilizado para apresentar algumas funções do edtiro VIM, uma espécie de tutorial sobre o programa.
```
Para sair do tutor basta teclar **ESC** e em seguida digitar **:q!**

Outra maneira de acessar o tutor do vim é acessar o programa através do terminal digitando **vim** e em seguida **:help**.

Ao invocar o **“vim”**, este entra direto para o modo de “Visualização”. Para modificar o arquivo,
usam-se os modos de inserção, deleção e de substituição.
Para voltar ao modo de visualização, sempre se usa a tecla “ESC”, de forma que para entrar no
modo de inserção, use a tecla “i”.

- Criando um arquivo
A sintaxe para se criar um arquivo no vim é bem simples, sendo apenas o comando vim e o nome
do arquivo a ser criado, onde o mesmo será salvo no diretório corrente a sua criação.
Após digitar o texto, você precisará sair do modo de inserção para realizar qualquer outra ação,
para sair do modo de inserção digite ESC, assim como para salvar **:w**, salvar e sair **:wq**, e caso
queira forçar uma ação, adiciona um ponto de exclamação no final **:wq!** e **:q!** .

Antes de iniciar a prática com o vim, vamos copiar o arquivo **/etc/passwd** para o diretório **/tmp**.

```bash
~ cp /etc/passwd /tmp
~ vim /tmp/passwd
```

Dentro do vim, podemos trabalhar com dois modos de utilização, o **Modo de comando** e **Modo de inserção**:

- Para entrar no modo de inserção, basta teclar **i** enquando estiver no modo de comando;
- Para sair do modo de inserção e voltar ao modo de comando, basta teclar **ESC**.

### Comandos

- **gg** - Move o cursor para a primeira linha do documento;
- **G** - Move o cursor para a última linha do documento;
- **yy** - Copia a linha onde o cursor está posicionado;
- **cc** - Recorta a linha onde o cursor está posicionado;
- **pp** - Cola a(s) linha(s) que estão em buffer após cópias ou recortes de texto.


### Comando de pesquisa

- **/string** - O **/** permite realizar uma consulta dentro de um arquivo a partir de uma string definida pelo usuário;
- **?string** - O **?** também permite realizar uma consulta dentro de um arquivo a partir de uma string definida pelo usuario. No entanto, ele inverte o sentido da pesquisa. O **/** realiza a pesquisa do início para o fim do arquivo, o **?** realiza a pesquisa do final para o começo;
- **n** - Quando realizada a pesquisa a partir dos caracteres **?** ou **/**, o **n** vai para a próxima ocorrência da pesquisa realizada dentro do arquivo;
- **N** - Faz o oposto do **n**, e busca a ocorrência anterior da pesquisa realizada dentro do arquivo;


### Salvando e saindo de arquivos

Para salvar arquivos, o vim possui as opções **:wq**, **:x** ou **ZZ**, todas elas a serem utilizadas no Modo de Comando.

Para sair do arquivo sem realizar nenhuma operação de gravação, utiliza-se apenas a opção **:q**.

Para forçar a execução de algum destes comandos, basta utilizar o **!** após a execução deles (**:q!**,**:wq!**,**:x!**).

## Aula 2.2 VIM Avançado

### Objetivo:
Editar o arquivo **/etc/issue** para criar uma mensagem de login ao servidor customizada.

Utilizar comandos variados do vim para localizar, susbstituir e colar linhas dentro de um documento de texto.

Por segurança, antes de iniciar qualquer edição a arquivos de configuração, é importante realizar a cópia dos arquivos que editar para um diretório separado.

```bash
~ cp /etc/passwd /tmp
~ cp /etc/fstab /tmp
```

### Editar múltiplos arquivos

Após realizar a cópia dos arquivos, vamos utilizar a opção **-o** para abrir os dois arquivos que copiamos simultâneamente. Com a opção **-o**, a tela fica dividida horizontalmente.

```bash
~ vim -o /tmp/passwd /tmp/fstab
```
Utilizando a combinação de teclas < **CTRL + WW**> podemos alternar entre as duas janelas de arquivos abertos.

Para sair de todos os arquivos sem salvar, basta estar estar no Modo de Comando e teclar **:qa!**.

Para dividir a tela verticalmente, utiliza-se a opção **-O** e a navegação entre as janelas se dá da mesma forma que quando utilizada a opção **-o**, utilizando < **CTRL + WW** >.

Para salvar todos os arquivos e em seguida sair deles, utiliza-se a opção **:wqa** no Modo de Comando.

### Fazer substituições dentro de um arquivo de textos

Vamos editar o arquivo passwd que foi copiado anteriormente:

```bash
~ vim /tmp/passwd
```
Após acessar o arquivo, vamos utilizar expressões para editá-lo:

Para isso, no Modo de Comando devemos teclar **:% s/nologin/yeslogin/g**. O caractere **%** indica que a pesquisa deve ser realizada no arquivo inteiro, o **s** indica substituição dos textos e o **g** indica substituição global das strings, considerando não apenas as linhas e também as colunas.

Para voltar ao padrão anterior, devemos utilizar o comando **:% s/yeslogin/nologin/g**.

Em seguida, basta salvar o arquivo e sair teclando **:wq**.

```bash

```


```bash

```

#### Aula 2.3 Configurar Shell e Timezone
