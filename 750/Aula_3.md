### Aula 03 - Instalação de Programas

Nesta aula, aprenderemos como configurar repositórios e gerenciar pacotes em distribuições como Debian e CentOS.

No dia a dia, é bastante comum precisarmos utilizar pacotes que eventualmente não estejam instalados nos sistemas que estamos operando.

Por isso é essencial que conheçamos meios de poder instalar os pacotes que precisamos, bem como instalar os repositórios de onde estes pacotes são disponibilizados.

#### Aula 3.1 Gerenciadores de Pacotes

![](assets/Aula_3-8d0494f3.png)

Existem 3 formas de instalar pacotes em sistemas Linux:

- Instalação via gerenciadores de pacotes como o apt(Debian), o yum(RedHat) e o zypper(OpenSuse), por exemplo;
- A partir de pacotes pré-compilados (arquivos com as extensões .deb ou .rpm);
- A partir do código fonte do pacote.

Existem gerenciadores de pacotes de alto nível (apt/yum/zypper) e de baixo nível (rpm/dpkg), os de alto nível são os que nos permitem maior comodidade durante a instalação de pacotes, pois tratam dependências e exige uma instalação "menos interativa" se comparados aos gerenciadores de baixo nível.

![](assets/Aula_3-4c96a498.png)

##### Afinal, o que é um gerenciador de pacotes?

Nada mais é do que um sistema que efetivamente gerencia os programas instalados numa distribuição Linux. A partir dele, podemos tanto instalar novos pacotes e suas respectivas dependências, como também podemos realizar atualização dos pacotes que já estão instalados no sistema, e por fim realizar a remoção destes mesmos pacotes, caso seja necessário.

Vamos verificar as características de se utilizar os gerenciadores de baixo e de alto nível:

  **Baixo nível** | **Alto Nível**
------|------
Instalação manual | Instalação automática
Não trata dependências | Trata dependências
Difícil manter compatibilidade de versões | Fácil manter compatibilidade de versões
Tendência a manter lixo no sistema | Remove pacotes deixando o sistema limpo

##### APT / YUM

A principal função dos gerenciadores de alto nível como o **apt** e o **yum** é realizar a pré-instalação dos pacotes. Primeiro fazem o download dos pacotes e suas dependências e auxiliam o DPKG e o RPM passando instruções para que realizem a instalação.

##### Ciclo de desenvolvimento Debian

![](assets/Aula_3-882283de.png)

As versoes de pacotes em desenvolvimento pela comunidade Debian, são basicamente distribuídos em 3 nichos, **Unstable(Sid)**, **Testing(Strench)** e **Stable(Jessie)**. Estas divisões servem para segregar os estágios de desenvolvimento de cada aplicação:

- **Unstable** - Últimas versões de programas, mas que ainda não foram homologadas;
- **Testing** - Versões recentes que já estão em homologação para as próximas versões;
- **Stable** - Não são necessáriamente as versões mais novas de cada programa, porém já foram testadas e homologadas pela comunidade.

###### Curiosidade Debian

Desde 1996, as versões do Debian são batizadas com o nome dos personagens do filme Toy Story. Essa ideia veio de Bruce Perens, que assumiu a liderança do Projeto Debian e trabalhava na Pixar, onde o filme foi produzido na época.

![](assets/Aula_3-7162fb72.png)

##### Repositórios Debian

No arquivo **/etc/apt/sources.list** estão listados os locais onde o **APT** buscará os pacotes que precisaremos instalar.
Em cada entrada do reposítorio estarão listados parâmetros relacionados a versão da distribuição (stable, testing, unstable) e a seção do repositório(main, non-free, contrib, non-US, etc).

O método de acesso ao repositório pode variar de acordo como a entrada é inserida, por exemplo:

- As entradas mais comuns possuem s string **"http://..."** indicando um repositório presente na internet;
- Caso o repositório seja um CD com pacotes, a entrada correspondente seria **"cdrom://"**;
- Por fim, existem também a opção de repositórios locais, que teria o método de entrada **file://**.


Exemplo de entrada do arquivo **"/etc/apt/sources.list"**:

```bash
 deb http://http.us.debian.org/debian stable main contrib non-free
```

Vamos checar o arquivo de configuração de repositório da nossa máquina Debian:

```bash
~ cat /etc/apt/sources.list
```

Caso os repositórios estejam configurados corretamente, para atualizar a lista de pacotes disponíveis no repositório, utilizamos o comando **apt** com o parâmetro **update**.

##### Configuração do repositório Debian

```bash
~ sudo apt update
```

Após atualizar a lista de pacotes disponíveis, podemos listar os pacotes instalados em nossa máquina que possuem atualizações disponíveis.

```bash
~ sudo apt list --upgradable
```

Para atualizar a distribuição do SO, utilizamos o comando **apt** com o parâmetro **dist-upgrade**.

```bash
~ sudo apt dist-upgrade
```

##### Repositórios RedHat

Para configurar reposítórios em distribuições baseadas em RedHat temos duas opções.

Adicionando as entradas correspondentes aos repositórios no arquivo **/etc/yum.conf** ou criando arquivos separados dentro do diretório **/etc/yum.repos.d/**. É importante saber que só se pode utilizar as configurações de repositório apenas em um desses locais.

Como se pode notar, a configuração de repositórios dentro de um sistema baseado em RedHat é diferente da configuração dos repositórios no Debian.

Enquanto no Debian se concentram todas as entradas de repositório no arquivo **/etc/apt/sources.list**, os sistemas RedHat concentram arquivos **.repo** separados para cada repositório que está adicionado na máquina.

Abaixo temos um exemplo de arquivo de configuração de repositório utilizado em sistemas baseados em RedHat.

```bash
[main]
cachedir=/var/cache/yum/$basearch/$releasever
keepcache=1
debuglevel=2
logfile=/var/log/yum.log
obsoletes=1
gpgcheck=1
```

Alguns outros parâmetros que também podem ser adicionados nos arquivos **.repo**.

- **name** — Nome descritivo, no exemplo: CentOS (versão da distribuição);
- **baseurl** — O endereço que contém a lista dos programas e os pacotes;
- **enabled** — Se o repositório está ativo ou não (1 significa sim, 0 significa não);
- **gpgcheck** — Se todos os pacotes devem ter sua autenticidade verificada (extremamente
recomendado, 1 significa sim, 0 significa não);
- **gpgkey** — Qual chave criptográfica utilizar para a verificação dos pacotes.

##### Configuração do repositórios RedHat / CentOS

Vamos listar as configurações dos arquivos **yum.conf** e do repositório base do CentOS.

```bash
~ cat /etc/yum.conf
~ cat /etc/yum.repos.d/CentOS-Base.repo
```

Após checar as configurações atuais, vamos instalar o repositório **EPEL Release**, bastante utilizado em distribuições RedHat.

```bash
~ sudo yum install epel-release
```

Após instalar o repositório EPEL, vamos realizar a atualização dos pacotes do sistema, a partir do comando **yum update**.

Caso a opção seja apenas atualizar um único pacote, basta citar o nome do pacote após o comando.

```bash
~ sudo yum update
~ sudo yum update vim
```

Diferentemente do **apt**, o **yum** atualiza a lista de pacotes dos repositórios todas as vezes em que uma instalação é executada. O gerenciador atualiza as listas dos repositórios, baixa os headers dos pacotes e calcula as dependências necessárias antes de confirmar a instalação.

Isso elimina a necessidade de realizar o *update* das listas manualmente antes de cada instalação ou upgrade de pacote.

##### Gerenciar Pacotes com o APT

Vamos checar primeiro as opções que o comando **apt** possui:

```bash
~ sudo apt --help
```

Depois de checar as opções vamos pesquisar e instalar um pacote que deixa a saída de logs do sistema colorida:
```bash
~ sudo apt search "log coloriser"
~ sudo apt show ccze
~ sudo apt install ccze
```

Depois de instalado, vamos testar o funcionamento da ferramenta redirecionando a saída dos logs para o comando ccze.
```bash
~ sudo tailf /var/log/messages | ccze
```

###### Descrição dos comandos

- **apt search** — Busca pacotes relacionados a palavra-chave definida pelo usuário. O mesmo resultado por ser obtido pelo comando **apt-cache search**.
- **apt show** — Mostra informações detalhadas de um pacote. O mesmo resultado por ser obtido pelo comando **apt-cache show**.
- **apt install** — Realiza a instalação de um pacote.

Após checar o funcionamento da ferramenta ccze, vamos removê-la do nosso sistema e em seguida checar se ela realmente foi desinstalada.

```bash
~ sudo apt remove ccze
~ sudo dpkg -l | grep ccze
```

Podemos notar que apesar de desinstalarmos o pacote, ainda fica algo da instalação presente no sistema, para remover totalmente os dados é necessário utilizar a opção **--purge**:
```bash
~ sudo apt remove --purge ccze
~ dpkg -l | grep ccze
```

##### Descrição dos comandos
- apt remove
 — Remove um pacotes e suas dependências. A flag --purge remove
completamente o pacote incluindo arquivos de configuração.

##### Funcionalidades Avançadas

```bash
$ sudo apt clean # clean — Limpa o diretório de pacotes que são baixados para realizar uma instalação;
$ sudo apt autoremove # autoremove — Localiza e remove todos os pacotes “orfãos”;
$ sudo apt -f install # -f install — Aciona o sistema de resolução de problemas do APT;
$ sudo apt -f remove # -f remove — Similar ao “-f install”, porém ele dá preferência para remover os pacotes com problemas ao invés de tentar instalar;
Baixar o pacote no formato .DEB sem realizar a instalação
$ sudo apt -d install htop # -d - Baixa o pacote no formato .DEB sem realizar a instalação;
$ ls /var/cache/apt/archives # lista os arquivos baixados pelo apt.
```

##### Gerenciar pacotes com o yum

A exemplo do apt, vamos checar as opções disponíveis para o comando **yum** utilizando a flag **--help**.
```bash
~ sudo yum --help
```

Após checar as opções, vamos listar os repositórios que estão configurados em nossa máquina:
```bash
~ sudo yum repolist
```

Em seguida, vamos pesquisar e checar as informações relacionadas ao pacote "linux_logo".
```bash
~ sudo yum search "linux logo"
~ sudo yum info linux_logo
```

##### Descrição dos comandos
 - yum repolist — Valida quais repositórios estão sendo usados.
 - yum search — Busca pacotes relacionados a palavra-chave.
 - yum info — Mostra informações detalhadas de um pacote.

Depois de checadas as informações, podemos realizar a instalação do pacote e em seguida vamos testá-lo:

```bash
~ sudo yum install linux_logo
~ linux_logo -L23
```

Depois de utilizar o pacote, podemos removê-lo do sistema, utilizando o comando **yum remove**.

```bash
~ sudo yum remove linux_logo
```
Após realizar a remoção com o yum, vamos checar se realmente o pacote foi removido, utilizando o comando **rpm** com a opção **-qa**:

```bash
~ sudo rpm -qa | grep linux logo
```
##### Descrição dos comandos
- yum install — Instala um pacote.
- yum remove — Remove um pacotes e suas dependências.

##### Funcionalidades Avançadas

Limpar o diretório de pacotes através do comando yum clean all:
```bash
$ ls -R /var/cache/yum
$ sudo yum clean all # - clean all — Limpa o diretório de pacotes que são baixados para realizar uma instalação;
$ sudo yum upgrade # upgrade - Caso disponível atualiza a distribuição do CentOS;
$ sudo yum install ccze -y --downloadonly # --downloadonly — Plugin do Yum para realizar o download de pacotes sem realizar a instalação do mesmo.
```

Vamos listar se há pacotes do ccze baixados pelo yum no diretório de cache do gerenciador:
```bash
$ cd /var/cache/yum/x86_64/7/
$ ls epel/packages/ccze*
```
#### Aula 3.2 Gerenciar pacotes DPKG e RPM
#### Aula 3.3 Compilação de Pacotes
