
# Capitulo 1 - LFCS

## Courses Resources

- https://training.linuxfoundation.org/cm/LFS201
- Login: LFtraining
- Password: Penguin2014

# Capitulo 2

## FHS


By the end of this chapter, you should be able to:

    Explain why Linux requires the organization of one big filesystem tree, and what the major considerations are for how it is done.
    Explain the role played by the Filesystem Hierarchy Standard.
    Describe what must be available at boot in the root (/) directory, and what can be available only once the system has started.
    Explore each of the main subdirectory trees, explain their purposes, and examine their contents.



  2.5. Data Distinctions

    When talking about how files and data are organized in the one big directory tree, it is important to learn some taxonomy on what kind of information has to be read and written. In particular, there are two kinds of distinctions:

        Shareable vs. non-shareable
        Shareable data is that which can be shared between different hosts. Non-shareable data is that which must be specific to a particular host. For example, user home directories may be shareable, while device lock files are not.
        Variable vs. static
        Static data include binaries, libraries, documentation, and anything that does not change without system administrator assistance. Variable data is anything that may change even without a system administrator's help.


        2.7.a. Main Directory Layout I

        Linux distributors spend a lot of time making sure their filesystem layout is coherent and evolves correctly over time. Below is a list of the main directories which are normally found under /:.

        ####TABELA
        Directory 	In FHS? 	Purpose
        / 	 Yes 	Primary directory of the entire file system hierarchy.
        /bin 	Yes 	Essential executable programs that must be available in single user mode.
        /boot 	Yes 	Files needed to boot the system, such as the kernel, initrd or initramfs images, and boot configuration files and bootloader programs.
        /dev 	Yes 	Device Nodes, used to interact with hardware and software devices.
        /etc 	Yes 	System wide configuration files.
        /home 	Yes 	User home directories including personal settings, files, etc.
        /lib 	Yes 	Libraries required by executable binaries in /bin and /sbin.
        /lib64 	No 	64-bit libraries required by executable binaries in /bin and /sbin, for systems which can run both 32-bit and 64-bit programs.
        /media 	Yes 	Mount points for removable media such as CDs, DVDs, USB sticks etc.
        /mnt 	Yes 	Temporarily mounted filesystems.
        /opt 	Yes 	Optional application software packages.
        /proc 	Yes 	Virtual pseudo-filesystem giving information about the system and processes running on it. Can be used to alter system parameters.
        /sys 	No 	Virtual pseudo-filesystem giving information about the system and processes running on it. Can be used to alter system parameters. Similar to a device tree and is part of the Unified Device Model.
        /root 	Yes 	Home directory for the root user.
        /sbin 	Yes  	Essential system binaries.
        /srv 	Yes 	Site-specific data served up by the system. Seldom used.
        /tmp 	Yes 	Temporary files; on many distributions lost across a reboot and may be a ramdisk in memory.
        /usr 	Yes 	Multi-user applications, utilities and data; theoretically read-only.
        /var 	Yes  	Variable data that changes during system operation.
