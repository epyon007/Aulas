#### 2.3 - Objetivos do aprendizado

No final do capítulo, deveremos ser capazes de:
- Explicar porque Linux exige a organização de um grande *Filesystem* e as considerações principais disso;
- Explicar a função do **FHS - File Hierarchy Standard**;
- Descrever o que deverá estar disponível no diretório **/** no momento do boot, e o que estará disponível uma vez que o sistema operacional tenha iniciado;
- Explorar cada um dos subdiretórios presentes no **/** e seus respectivos conteúdos.

#### 2.4 - Um grande sistema de arquivos

A estrutura de pastas de sistemas Linux (UNIX-based) de maneira geral, consistem em uma grande **"árvore"** de arquivos. Na verdade, é muito comum ser descrita como uma "árvore de ponta cabeça", onde o "**/**" é o topo da árvore.


#### 2.7 Layout do Diretório Principal


**Directory** | **In FHS?** | **Purpose**
------|------|------
/   |	 Yes |	Primary directory of the entire file system hierarchy.
/bin | 	Yes |	Essential executable programs that must be available in single user mode.
/boot |	Yes |	Files needed to boot the system, such as the kernel, initrd or initramfs images, and boot configuration files and bootloader programs.
/dev |	Yes |	Device Nodes, used to interact with hardware and software devices.
/etc |	Yes |	System wide configuration files.
/home |	Yes |	User home directories including personal settings, files, etc.
/lib |	Yes |	Libraries required by executable binaries in /bin and /sbin.
/lib64 |	No |	64-bit libraries required by executable binaries in /bin and /sbin, for systems which can run both 32-bit and 64-bit programs.
/media |	Yes |	Mount points for removable media such as CDs, DVDs, USB sticks etc.
/mnt |	Yes |	Temporarily mounted filesystems.
/opt |	Yes |	Optional application software packages.
/proc |	Yes |	Virtual pseudo-filesystem giving information about the system and processes running on it. Can be used to alter system parameters.
/sys |	No |	Virtual pseudo-filesystem giving information about the system and processes running on it. Can be used to alter system parameters. Similar to a device tree and is part of the Unified Device Model.
/root |	Yes |	Home directory for the root user.
/sbin |	Yes | 	Essential system binaries.
/srv |	Yes |	Site-specific data served up by the system. Seldom used.
/tmp |	Yes | 	Temporary files; on many distributions lost across a reboot and may be a ramdisk in memory.
/usr |	Yes |	Multi-user applications, utilities and data; theoretically read-only.
/var |	Yes | 	Variable data that changes during system operation.
