AArch64 交叉編譯器 
======================

在這之前我們會先開始我們教學，你將需要一些工具，即時編譯AArch64架構的編譯器。


Before we could start our tutorials, you'll need some tools. Namely a compiler that compiles for the AArch64
architecture and it's companion utilities.

**重要筆記**: 這個不是描述一個一般執行交叉編譯的方式，而是關於編譯aarch64-elf為目標的編譯方法。
如果你有問題，請google "how to build a gcc cross-comiler"

**IMPORTANT NOTE**: this description is not about how to compile a cross-compiler in general. It's about how to
compile one specifically for the *aarch64-elf* target. If you have problems, google "how to build a gcc cross-compiler"
or ask on an appropriate support forum for your operating system. I can't and won't help you with your environment,
you have to solve that on your own. As I've said in the introduction I assume you know how to compile programs
(including the compilation of the cross-compiler).

Each directory has two Makefiles, one for the GNU gcc, and one for LLVM clang. Pick the one you prefer. I could have used makefile
variables and a common configuration, but it was important that each tutorial must be self-contained and dependency-free.

LLVM Compiler and Linker
------------------------

Clang by design is a cross-compiler, therefore you don't have to build a special version of it like with gcc. For
some (probably archaical) reason the corresponding linker uses a different target (no '-' in it), keep that in mind.

```
clang --target=aarch64-elf
ld.lld -m aarch64elf
```

Also note that you'll need other tools. You can find [llvm-objcopy](https://github.com/llvm-mirror/llvm/tree/master/tools/llvm-objcopy) here.

Build system
------------

To orchestrate compilation, we'll use GNU make. No need for cross-compiling this, as we are about to use it on the
host computer only, and not on the target machine. The reason I choosed this build system for the tutorials is that
GNU make is also required to compile the GNU compiler, so you'll need it anyway.

Download and unpack sources
---------------------------

First of all, download binutils and gcc sources. In this example I've used the latest versions as of writing.
You are advised to check the mirrors and modify filenames accordly.

```sh
wget https://ftpmirror.gnu.org/binutils/binutils-2.30.tar.gz
wget https://ftpmirror.gnu.org/gcc/gcc-8.1.0/gcc-8.1.0.tar.gz
wget https://ftpmirror.gnu.org/mpfr/mpfr-4.0.1.tar.gz
wget https://ftpmirror.gnu.org/gmp/gmp-6.1.2.tar.bz2
wget https://ftpmirror.gnu.org/mpc/mpc-1.1.0.tar.gz
wget https://gcc.gnu.org/pub/gcc/infrastructure/isl-0.18.tar.bz2
wget https://gcc.gnu.org/pub/gcc/infrastructure/cloog-0.18.1.tar.gz
```

