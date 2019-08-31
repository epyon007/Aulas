### Aula 04 -  Gerenciamento de Usuários

Ao administrar qualquer sistema de computação, seja em ambientes Windows ou Linux, é primordial saber gerenciar usuários e grupos de usuários.

A partir desse gerenciamento nos tornamos capazes de definir níveis de permissão e diferentes graus de acesso entre usuários e grupos, bem como automatizar ou padronizar a forma como estes usuários e grupos são criados.


#### Aula 4.1 Administrando Usuários

##### Objetivo da aula:
Aprender a criar e manipular configurações de usuários e grupos do sistema, bem como adicionar usuários, grupos e pastas departamentais definindo permissões específicas para seus respectivos usuários e grupos.

##### Arquitetura de arquivos na criação de um usuário

![](assets/Aula_5-21c98e02.png)

Dentro de sistemas Linux, temos alguns arquivos que possuem informações específicas sobre diferentes itens relacionados a gerenciamento de usuários, conforme vemos na figura acima.

No entanto, é bom conhecer quais arquivos armazenam quais itens, para facilitar a realização dessas tarefas diárias.



##### Componentes do arquivo /etc/passwd

O arquivo **/etc/passwd** é dividido em campos (separados por **:**). Cada campo do arquivo representa uma configuração diferente relacionado aos usuários, conforme descrito na imagem a seguir.

![](assets/Aula_5-aa2ecdfa.png)

Os **IDs** de usuários Linux seguem uma regra. Tanto em distribuições **Debian** como em baseadas em **RedHat**, os IDs numerados de **1** a **999**, são usuários de sistema (usuários específicos de aplicações que funcionam dentro do ambiente).

A partir do ID número **1000**, são identificados os IDs usuários comuns do sistema.

![](assets/Aula_5-5043f20a.png)

##### Componentes do arquivo /etc/shadow

![](assets/Aula_5-d0b4e477.png)

###### Arquivo /etc/shadow

As senhas dos usuários ficam armazenadas no arquivo **“/etc/shadow”** conhecido como “senhas sombras” (shadow passwords). As senhas ficam nele pois é um arquivo mais seguro que o arquivo
**“/etc/passwd”**. No arquivo **“/etc/passwd”** qualquer usuário poderia visualizá-las e copiá-las para outro diretório ou máquina remota, comprometendo a segurança.

Já o arquivo **“/etc/shadow”** tem permissões muito mais restritas, não permitindo que ele seja copiado e nem visualizado diretamente por um usuário comum.

Isso é uma grande ajuda na questão de segurança, pois se as senhas estivessem no próprio **”/etc/passwd”** seria muito fácil para um invasor com usuário comum, copiar esse arquivo para outro servidor e aplicar uma ferramenta de “brute force” para quebrar as senhas.


#### Coletando informaões de usuários existentes
Hora de praticar:

Na máquina **Storage**, vamos executar os comandos a seguir para verificar os arquivos **passwd** e **group** presentes no diretório /etc.

```bash
~ sudo getent passwd
~ sudo getent group
```

Vamos fazer um levantamento de informações sobre o usuário e grupo suporte:
```bash
~ sudo id suporte
~ sudo groups suporte
```

Vamos visualizar as informações do usuário suporte a partir do comando getent:
```bash
~ sudo getent passwd suporte
```

Vamos utilizar o comando **finger** para detalhar informações sobre o usuário suporte:
```bash
~ sudo finger suporte
```

Vamos utilizar também os comandos **who** e **w**, para verificar os usuários que estão conectados:
```bash
~ who
~ w
```

Por fim, vamos verificar as informações do usuário suporte no arquivo **/etc/shadow**:
```bash
~ sudo getent shadow suporte
```


###### Descrição dos comandos

- **sudo** — Permite a usuários comuns obter privilégios de outro usuário, em geral o root;
- **getent passwd** — Lista todos os usuários existentes no sistema;
- **getent group** — Lista todos os grupos existentes no sistema;
- **id** — Verifica o id de um usuário e seus respectivos grupos;
- **groups** — Verifica quais são os grupos aos quais um usuário está vinculado;
- **finger** — Exibe de maneira mais formatada as informações dos usuários;
- **who** — Permite verificar o nome do usuário logado;
- **w** — Verifica todos os usuários logados na máquina.


##### Adicionando usuários no sistema:

Para começar, vamos verificar as opções do comando **adduser** e adicionar o usuário **dexter**:

```bash
~ sudo adduser --help
~ sudo adduser dexter
```

Em seguida vamos adicionar um outro usuário e também definir a sua respectivas senha:

```bash
~ sudo adduser bryan.leah
~ sudo passwd bryan.leah
```

Vamos verificar se o novo usuário foi criado:

```bash
~ sudo tail -n 2 /etc/passwd /etc/group /etc/shadow
~ ls /home
```

#### Aula 4.2 Permissões Especiais




#### Aula 4.3 Configuração do Sudo
