#### 2.3 - Objetivos do aprendizado

No final do capítulo, deveremos ser capazes de:
- Explicar porque Linux exige a organização de um grande *Filesystem* e as considerações principais disso;
- Explicar a função do **FHS - File Hierarchy Standard**;
- Descrever o que deverá estar disponível no diretório **/** no momento do boot, e o que estará disponível uma vez que o sistema operacional tenha iniciado;
- Explorar cada um dos subdiretórios presentes no **/** e seus respectivos conteúdos.

#### 2.4 - Um grande sistema de arquivos

A estrutura de pastas de sistemas Linux (UNIX-based) de maneira geral, consistem em uma grande **"árvore"** de arquivos. Na verdade, é muito comum ser descrita como uma "árvore de ponta cabeça", onde o "**/**" é o topo da árvore.


#### 2.7 Layout do Diretório Principal


**Diretório** | **Faz parte do FHS?** | **Função**
------|------|------
/   |	 Sim |	Principal diretório dentro de toda a hierarquia do sistema de arquivos.
/bin | 	Sim |	Programas executáveis essenciais que devem estar disponíveis no modo *single user*.
/boot |	Sim |	Arquivos necessários para iniciar o sistema, como kernel(vmlinuz), initrd ou initramfs, assim como arquivos de configuração de boot e bootloaders.
/dev |	Sim |	Utilizado na interação entre hardware e software.
/etc |	Sim |	Arquivos de configuração do sistema.
/home |	Sim |	Diretórios pessoais dos usuários incluindo configurações e arquivos pessoais, etc.
/lib |	Sim |	Bibliotecas necessárias para executar binários presentes nos diretórios /bin e /sbin.
/lib64 |	Não |	Bibliotecas 64bit necessárias para executar binários presentes nos diretórios /bin e /sbin. Para sistemas que podem rodar programas 32 bits e 64 bits.
/media |	Sim |	Pontos de montagem para mídias removíveis como CDs, DVDs, Pen-Drives e HDs Externos etc.
/mnt |	Sim |	Sistemas de arquivos montados temporariamente.
/opt |	Sim |	Pacotes de software opcionais.
/proc |	Sim |	Pseudo-filesystem virtual que fornece informações sobre o sistema e processos em execução. Pode ser utilizado para alterar parâmetros do sistema.
/sys |	Não |	Segue o mesmo princípio do **/proc**.
/root |	Sim |	Diretório pessoal do usuário **root**.
/sbin |	Sim | Binários essenciais do sistema.
/srv |	Sim |	Dados fornecidos pelo sistema. Raramente utilizado.
/tmp |	Sim | 	Arquivos temporários; em muitas distribuições são perdidos durante o processo de reboot. Arquivos que podem ser executados em memória, e não no disco.
/usr |	Sim |	Aplicações, utilitários e dados multi-usuários; comumente sendo somente leitura.
/var |	Sim | 	Dados variáveis que mudam constantemente durante o funcionamento do sistema.
