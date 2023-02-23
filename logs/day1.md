## Day 1 logs

```
$ curl --proto '=https' --tlsv1.3 https://sh.rustup.rs -sSf > sh.rustup.rs
$ 
$ file sh.rustup.rs 
sh.rustup.rs: POSIX shell script, ASCII text executable
$ 
$ wc -l sh.rustup.rs 
700 sh.rustup.rs
$ 
$ vim sh.rustup.rs 
$ 
$ 
$ sh sh.rustup.rs 
info: downloading installer

Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.

Rustup metadata and toolchains will be installed into the Rustup
home directory, located at:

  /root/.rustup

This can be modified with the RUSTUP_HOME environment variable.

The Cargo home directory is located at:

  /root/.cargo

This can be modified with the CARGO_HOME environment variable.

The cargo, rustc, rustup and other commands will be added to
Cargo's bin directory, located at:

  /root/.cargo/bin

This path will then be added to your PATH environment variable by
modifying the profile files located at:

  /root/.profile
  /root/.bash_profile
  /root/.bashrc

You can uninstall at any time with rustup self uninstall and
these changes will be reverted.

Current installation options:


   default host triple: x86_64-unknown-linux-gnu
     default toolchain: stable (default)
               profile: default
  modify PATH variable: yes

1) Proceed with installation (default)
2) Customize installation
3) Cancel installation
>1

info: profile set to 'default'
info: default host triple is x86_64-unknown-linux-gnu
info: syncing channel updates for 'stable-x86_64-unknown-linux-gnu'
info: latest update on 2023-02-09, rust version 1.67.1 (d5a82bbd2 2023-02-07)
info: downloading component 'cargo'
  6.6 MiB /   6.6 MiB (100 %)   4.2 MiB/s in  1s ETA:  0s
info: downloading component 'clippy'
info: downloading component 'rust-docs'
 19.3 MiB /  19.3 MiB (100 %)  16.0 MiB/s in  1s ETA:  0s
info: downloading component 'rust-std'
 29.3 MiB /  29.3 MiB (100 %)  20.5 MiB/s in  1s ETA:  0s
info: downloading component 'rustc'
 67.8 MiB /  67.8 MiB (100 %)   2.9 MiB/s in 25s ETA:  0s
info: downloading component 'rustfmt'
info: installing component 'cargo'
info: installing component 'clippy'
info: installing component 'rust-docs'
 19.3 MiB /  19.3 MiB (100 %)   5.6 MiB/s in  3s ETA:  0s
info: installing component 'rust-std'
 29.3 MiB /  29.3 MiB (100 %)   8.4 MiB/s in  3s ETA:  0s
info: installing component 'rustc'
 67.8 MiB /  67.8 MiB (100 %)   9.1 MiB/s in  7s ETA:  0s
info: installing component 'rustfmt'
info: default toolchain set to 'stable-x86_64-unknown-linux-gnu'

  stable-x86_64-unknown-linux-gnu installed - rustc 1.67.1 (d5a82bbd2 2023-02-07)


Rust is installed now. Great!

To get started you may need to restart your current shell.
This would reload your PATH environment variable to include
Cargo's bin directory ($HOME/.cargo/bin).

To configure your current shell, run:
source "$HOME/.cargo/env"
$ 
$ source "$HOME/.cargo/env"
$ 
$ 
$ rustc --version
rustc 1.67.1 (d5a82bbd2 2023-02-07)
$ 
$ 
$ cargo --version
cargo 1.67.1 (8ecd4f20a 2023-01-10)
$ 
$ 
$ vim main.rs
$ 
$ cat main.rs 
fn main() {
    println!("Hello, world!");
}
$ 
$ rustc main.rs 
error: linker `cc` not found
  |
  = note: No such file or directory (os error 2)

error: aborting due to previous error

$ 
$ which cc
/usr/bin/which: no cc in (/root/.cargo/bin:/root/.local/bin:/root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin)
$ 
$ 
$ dnf whatprovides cc
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

Last metadata expiration check: 1:52:37 ago on Wed 22 Feb 2023 07:08:46 PM EST.
gcc-11.3.1-4.3.el9.x86_64 : Various compilers (C, C++, Objective-C, ...)
Repo        : test-AppStream
Matched from:
Filename    : /usr/bin/cc

$ 
$ dnf install gcc
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

Last metadata expiration check: 1:52:43 ago on Wed 22 Feb 2023 07:08:46 PM EST.
Dependencies resolved.
=======================================================================================================================
 Package                               Architecture      Version                     Repository                   Size
=======================================================================================================================
Installing:
 gcc                                   x86_64            11.3.1-4.3.el9              test-AppStream             32 M
Installing dependencies:
 binutils                              x86_64            2.35.2-37.el9               test-BaseOS               4.6 M
 binutils-gold                         x86_64            2.35.2-37.el9               test-BaseOS               734 k
 cpp                                   x86_64            11.3.1-4.3.el9              test-AppStream             11 M
 elfutils-debuginfod-client            x86_64            0.188-3.el9                 test-BaseOS                40 k
 glibc-devel                           x86_64            2.34-60.el9                 test-AppStream             54 k
 glibc-headers                         x86_64            2.34-60.el9                 test-AppStream            556 k
 kernel-headers                        x86_64            5.14.0-265.el9              test-AppStream            4.9 M
 libmpc                                x86_64            1.2.1-4.el9                 test-AppStream             65 k
 libxcrypt-devel                       x86_64            4.4.18-3.el9                test-AppStream             32 k

Transaction Summary
=======================================================================================================================
Install  10 Packages

Total download size: 54 M
Installed size: 148 M
Is this ok [y/N]: y
Downloading Packages:
(1/10): glibc-devel-2.34-60.el9.x86_64.rpm                                             1.8 MB/s |  54 kB     00:00    
(2/10): glibc-headers-2.34-60.el9.x86_64.rpm                                            16 MB/s | 556 kB     00:00    
(3/10): kernel-headers-5.14.0-265.el9.x86_64.rpm                                        20 MB/s | 4.9 MB     00:00    
(4/10): libmpc-1.2.1-4.el9.x86_64.rpm                                                   10 MB/s |  65 kB     00:00    
(5/10): libxcrypt-devel-4.4.18-3.el9.x86_64.rpm                                        6.0 MB/s |  32 kB     00:00    
(6/10): cpp-11.3.1-4.3.el9.x86_64.rpm                                                   27 MB/s |  11 MB     00:00    
(7/10): binutils-gold-2.35.2-37.el9.x86_64.rpm                                          21 MB/s | 734 kB     00:00    
(8/10): elfutils-debuginfod-client-0.188-3.el9.x86_64.rpm                              4.3 MB/s |  40 kB     00:00    
(9/10): binutils-2.35.2-37.el9.x86_64.rpm                                               20 MB/s | 4.6 MB     00:00    
(10/10): gcc-11.3.1-4.3.el9.x86_64.rpm                                                  40 MB/s |  32 MB     00:00    
-----------------------------------------------------------------------------------------------------------------------
Total                                                                                   66 MB/s |  54 MB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                               1/1 
  Installing       : elfutils-debuginfod-client-0.188-3.el9.x86_64                                                1/10 
  Installing       : binutils-gold-2.35.2-37.el9.x86_64                                                           2/10 
  Installing       : binutils-2.35.2-37.el9.x86_64                                                                3/10 
  Running scriptlet: binutils-2.35.2-37.el9.x86_64                                                                3/10 
  Installing       : libmpc-1.2.1-4.el9.x86_64                                                                    4/10 
  Installing       : cpp-11.3.1-4.3.el9.x86_64                                                                    5/10 
  Installing       : kernel-headers-5.14.0-265.el9.x86_64                                                         6/10 
  Installing       : glibc-headers-2.34-60.el9.x86_64                                                             7/10 
  Installing       : libxcrypt-devel-4.4.18-3.el9.x86_64                                                          8/10 
  Installing       : glibc-devel-2.34-60.el9.x86_64                                                               9/10 
  Installing       : gcc-11.3.1-4.3.el9.x86_64                                                                   10/10 
  Running scriptlet: gcc-11.3.1-4.3.el9.x86_64                                                                   10/10 
  Verifying        : cpp-11.3.1-4.3.el9.x86_64                                                                    1/10 
  Verifying        : gcc-11.3.1-4.3.el9.x86_64                                                                    2/10 
  Verifying        : glibc-devel-2.34-60.el9.x86_64                                                               3/10 
  Verifying        : glibc-headers-2.34-60.el9.x86_64                                                             4/10 
  Verifying        : kernel-headers-5.14.0-265.el9.x86_64                                                         5/10 
  Verifying        : libmpc-1.2.1-4.el9.x86_64                                                                    6/10 
  Verifying        : libxcrypt-devel-4.4.18-3.el9.x86_64                                                          7/10 
  Verifying        : binutils-2.35.2-37.el9.x86_64                                                                8/10 
  Verifying        : binutils-gold-2.35.2-37.el9.x86_64                                                           9/10 
  Verifying        : elfutils-debuginfod-client-0.188-3.el9.x86_64                                               10/10 
Installed products updated.

Installed:
  binutils-2.35.2-37.el9.x86_64                  binutils-gold-2.35.2-37.el9.x86_64    cpp-11.3.1-4.3.el9.x86_64      
  elfutils-debuginfod-client-0.188-3.el9.x86_64  gcc-11.3.1-4.3.el9.x86_64             glibc-devel-2.34-60.el9.x86_64 
  glibc-headers-2.34-60.el9.x86_64               kernel-headers-5.14.0-265.el9.x86_64  libmpc-1.2.1-4.el9.x86_64      
  libxcrypt-devel-4.4.18-3.el9.x86_64           

Complete!
$ 
$ 
$ 
$ which cc
/usr/bin/cc
$ 
$ 
$ 
$ rustc main.rs 
$ 
$ ./main 
Hello, world!
$ 
$ file main
main: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=83e3122e8e0f0f95ab9cb9f80772b89e09837d52, for GNU/Linux 3.2.0, with debug_info, not stripped
$ 
$ 
$ 
$ 
$ cargo new hello_cargo
     Created binary (application) `hello_cargo` package
$ 
$ cd hello_cargo/
$ 
$ cat Cargo.toml 
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
$ 
$ 
$ cargo build
   Compiling hello_cargo v0.1.0 (/root/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.59s
$ 
$ 
$ ./target/debug/hello_cargo 
Hello, world!
$ 
$ cargo run 
    Finished dev [unoptimized + debuginfo] target(s) in 0.00s
     Running `target/debug/hello_cargo`
Hello, world!
$ 
$ 
$ cargo run -q
Hello, world!
$ 
$ 
$ 
```

