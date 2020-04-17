# atcf_hardware_bbc_grip

This is a grip repository, whose git subrepositories provide a full
BBC microcomputer implementation in CDL (an FPGA/silicon design
language).

The design works on the CDL simulation, running with a VNC framebuffer
to provide (slow) simulation of a BBC microcomputer. This is not
designed as an emulator, though; it is a full hardware implementation,
and so one can see inside the 6502 (for example) to see what is
happening.

The design also operates on FPGA boards, at more than 10x the original
speed if desired.

# Checking out the repository

It is simple to use this repository, but it does require some tools.

## Prerequisites

It repository requires the CDL tools to be installed; this is another grip
repository available at https://github.com/atthecodeface/cdl_tools_grip.git

The CDL tools repository includes grip itself - so once that is checked out
and configured, all is set up.

## Checkout process

The process assumes Ubuntu 16.04/18.04 (or similar) or OSX, with
appropriate packages.

The system packages required include: python3 automake

Python3 packages required include: toml

### Get grip

Grip is currently in a github repo. It is a Python3 utility that uses
a special 'grip.tom' file in a repository to describe subrepositories
which require cloning, where to clone them to, which git revisions
each requires, and the steps required to configure, build, run, test,
and so on the collection of repositories.

```
cd <where_to_put_stuff>
git clone  https://github.com/atthecodeface/grip.git
```

### Get and build CDL tools

The CDL tools grip repository, which is a github repo. It does not contain
the source for any tools - it is a grip repository whose git
subrepositories provide the tools or mechanisms for building the
tools.

```
cd <where_to_put_stuff>
git clone  https://github.com/atthecodeface/cdl_tools_grip.git
cd cdl_tools_grip
<where_to_put_stuff>/grip configure all
<where_to_put_stuff>/grip shell
... (this is in a new bash shell - with path set up by grip)
grip make install
```

The 'all' configuration of the cdl_tools_grip repository includes
grip, cdl, verilator, and GNU cross-compiler/assembler/linker for
RISC-V I32MC. The latter is installed using a download of GNU tarfiles
of a specific version of the tools.

The configure stage requires the download step for the GNU toolchain;
hence it is that step that grip ensures happens first.

### Get and set up atcf_hardware_bbc_grip

This is a grip repository, which is a github repo. It does not contain
the hardware descriptions or the source for any tools - the
subrepositories contain what is required.

The following assumes *grip* and *cdl* are on the PATH for the shell.

```
export ATCF_CDL_TOOLS_PATH=<where_to_put_stuff>/cdl_tools_grip/tools
cd <where_to_put_stuff>
git clone  https://github.com/atthecodeface/atcf_hardware_bbc_grip.git
cd atcf_hardware_bbc_grip
grip configure
```

# Using the repository

At present the best approach (since there are no global testing grip
targets, for example) is to use a grip shell.

The following assumes *grip* and *cdl* are on the PATH for the shell.

```
export ATCF_CDL_TOOLS_PATH=<where_to_put_stuff>/cdl_tools_grip/tools
cd <where_to_put_stuff>/atcf_hardware_bbc_grip
grip shell
```

This invokes a bash shell in which commands can be executed.

# Building and running the BBC simulator

There are grip make targets for running the simulator and the VNC RFB.
Use:

```
grip make run_bbc
```

and in another shell:

```
grip make run_vnc_rfb
```

This will create a VNC server on port 1080, which a regular VNC client
can connect to.

The build is put in atcf_hardware_bbc_grip/build.

