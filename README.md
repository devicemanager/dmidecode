dmidecode
=========

[![Build Status](https://github.com/devicemanager/dmidecode/workflows/CI/badge.svg?branch=master)](https://github.com/devicemanager/dmidecode/actions)

**devicemanager NOTES**

This dmidecode version supports Apple-specific table decoding as well
as native macOS SMBIOS reading through I/O Registry. Synced with
[upstream](git://git.savannah.gnu.org/dmidecode.git) up to a1a2258f.

**INTRODUCTION**

Dmidecode reports information about your system's hardware as described in
your system BIOS according to the SMBIOS/DMI standard. This information
typically includes system manufacturer, model name, serial number, BIOS
version, asset tag as well as a lot of other details of varying level of
interest and reliability depending on the manufacturer. This will often
include usage status for the CPU sockets, expansion slots (e.g. AGP, PCI,
ISA) and memory module slots, and the list of I/O ports (e.g. serial,
parallel, USB).

DMI data can be used to enable or disable specific portions of kernel code
depending on the specific hardware. Thus, one use of dmidecode is for kernel
developers to detect system "signatures" and add them to the kernel source
code when needed.

Beware that DMI data have proven to be too unreliable to be blindly trusted.
Dmidecode does not scan your hardware, it only reports what the BIOS told it
to.


**INSTALLATION**

The home web page for dmidecode is hosted on Savannah:
  http://www.nongnu.org/dmidecode/
You will find the latest version (including CVS) there, as well as fresh news
and other interesting material, such as a list of related projects and
articles.

This program was first written for Linux, and has since been reported to work
on FreeBSD, NetBSD, OpenBSD, BeOS and Solaris as well.

There's no configure script, so simply run "make" to build dmidecode, and
"make install" to install it. You also can use "make uninstall" to remove
all the files you installed. By default, files are installed in /usr/local
but you can change this behavior by editing the Makefile file and setting
prefix to wherever you want. You may change the C compiler and the
compilation flags as well.

Optionally, you can run "make strip" prior to "make install" if you want
smaller binaries. However, be aware that this will prevent any further
attempt to debug the programs.

Two parameters can be set in the Makefile file to make dmidecode work on
non-i386 systems. They should be used if your system uses the big endian
byte ordering (Motorola) or doesn't support unaligned memory accesses,
respectively. For example, compiling for a SPARC processor would require
both (but I am not aware of SPARC-based systems implementing SMBIOS).
Compiling for an IA64 processor requires the memory alignment workaround,
and it is enabled automatically.


**DOCUMENTATION**

Each tool has a manual page, found in the "man" subdirectory. Manual pages
are installed by "make install". See these manual pages for command line
interface details and tool specific information.

For an history of the changes made to dmidecode, see the NEWS file.

If you need help, your best chances are to visit the web page (see the
INSTALLATION section above) or to get in touch with the developers directly.
Have a look at the AUTHORS file and contact one of the maintainers.

If you want to help with the development of dmidecode, please consider
joining the dmidecode-devel discussion list:
  http://lists.nongnu.org/mailman/listinfo/dmidecode-devel


**COMMON PROBLEMS**

IA-64

Non-Linux systems are not yet supported.

MMAP

Note that mmap() is now used by default wherever possible, since this seems
to solve a number of problems. This default behavior can be changed in
config.h. Just to make sure this is clear, mmap() is not used for performance
reasons but to increase the number of systems on which dmidecode can be
successfully run.

CYGWIN

Dmidecode used to work under Cygwin. However the /dev/mem interface was
removed at some point in time so it no longer works.


**MISCELLANEOUS TOOLS**

Three other tools come along with dmidecode: biosdecode, ownership and
vpddecode. These tools are only useful on systems with a BIOS, so they
are not built on IA-64 by default.

BIOSDECODE

This one prints all BIOS related information it can find in /dev/mem.
It used to be part of dmidecode itself, but as dmidecode was growing,
we felt that the non-DMI part had to be moved to a separate tool.

OWNERSHIP

This tool was written on a request by Luc Van de Velde for use with Novell
tools in his company. It retrieves the "ownership tag" that can be set on
most Compaq computers. Since it uses the same mechanisms dmidecode and
biosdecode use, and could be of some use for other people as well, we
decided to make it part of the project.

VPDDECODE

This tool prints the contents of the "vital product data" structure as
found in most IBM and Lenovo computers. It used to have a lookup table
for the machine name, but it was unreliable and hard to maintain so it
was ultimately dropped. It has a command line interface.

Use -h flag for help.
