## rustup build trial (failed due to openssl libs/devel not present

```
$ pwd
/tmp/x/rustup
$ 
$ ls
build.rs    Cargo.toml    ci               doc       flake.nix       LICENSE-MIT  rustup-init.sh  tests           www
Cargo.lock  CHANGELOG.md  CONTRIBUTING.md  download  LICENSE-APACHE  README.md    src             triagebot.toml
$ 
$ cloc .
     242 text files.
     238 unique files.                                          
      19 files ignored.

github.com/AlDanial/cloc v 1.90  T=0.09 s (2593.9 files/s, 497053.6 lines/s)
--------------------------------------------------------------------------------
Language                      files          blank        comment           code
--------------------------------------------------------------------------------
Rust                             90           3597           2104          27516
Markdown                         27            700              0           2774
TOML                             50            307              8           1826
YAML                             15             57             87           1505
Bourne Shell                      5            105             91            566
CSS                               2            104            130            350
Bourne Again Shell                7             60             43            235
JavaScript                        1             28              6            182
HTML                              1             24              2            171
Python                            1             25             45            101
Dockerfile                       21             20              0             86
JSON                              2              0              0             30
Nix                               1              2              6             15
PowerShell                        1              4              3              9
--------------------------------------------------------------------------------
SUM:                            224           5033           2525          35366
--------------------------------------------------------------------------------
$ 
$ 
$ 
$ ls src/
bin     command.rs      currentprocess.rs  env_var.rs            install.rs        rust-key.pgp.ascii  toolchain.rs
cli     config.rs       diskio             errors.rs             lib.rs            settings.rs         utils
cli.rs  currentprocess  dist               fallback_settings.rs  notifications.rs  test.rs
$ 
$ 
$ cat Cargo.toml 
[package]
authors = ["Daniel Silverstone <dsilvers@digital-scurf.org>", "Diggory Blake <diggsey@googlemail.com>"]
build = "build.rs"
description = "Manage multiple rust installations with ease"
edition = "2021"
homepage = "https://github.com/rust-lang/rustup"
keywords = ["rustup", "multirust", "install", "proxy"]
license = "MIT OR Apache-2.0"
name = "rustup"
readme = "README.md"
repository = "https://github.com/rust-lang/rustup"
version = "1.25.2"

[features]
curl-backend = ["download/curl-backend"]
default = ["curl-backend", "reqwest-backend", "reqwest-default-tls", "reqwest-rustls-tls"]

reqwest-backend = ["download/reqwest-backend"]
vendored-openssl = ['openssl/vendored']

reqwest-default-tls = ["download/reqwest-default-tls"]
reqwest-rustls-tls = ["download/reqwest-rustls-tls"]

# Include in the default set to disable self-update and uninstall.
no-self-update = []

# Sorted by alphabetic order
[dependencies]
anyhow.workspace = true
cfg-if = "1.0"
chrono = "0.4"
clap = {version = "2", features = ["wrap_help"]}
download = {path = "download", default-features = false}
effective-limits = "0.5.5"
enum-map = "2.4.2"
flate2 = "1"
git-testament = "0.2"
home = "0.5.4"
lazy_static.workspace = true
libc = "0.2"
num_cpus = "1.15"
opener = "0.5.2"
# Used by `curl` or `reqwest` backend although it isn't imported by our rustup :
# this allows controlling the vendoring status without exposing the presence of
# the download crate.
openssl = {version = "0.10", optional = true}
pulldown-cmark = {version = "0.9", default-features = false}
rand = "0.8"
regex = "1"
remove_dir_all = {version= "0.8.1", features=["parallel"]}
same-file = "1"
scopeguard = "1"
semver = "1.0"
serde = {version = "1.0", features = ["derive"]}
sequoia-openpgp = { version = "1.13", default-features = false, features = ["crypto-rust", "allow-experimental-crypto", "allow-variable-time-crypto"] }
sha2 = "0.10"
sharded-slab = "0.1.1"
strsim = "0.10"
tar = "0.4.26"
tempfile.workspace = true
# FIXME(issue #1818, #1826, and friends)
term = "=0.7.0"
thiserror.workspace = true
threadpool = "1"
toml = "0.5"
url.workspace = true
wait-timeout = "0.2"
xz2 = "0.1.3"
zstd = "0.12"
trycmd = "0.14.12"

[dependencies.retry]
default-features = false
features = ["random"]
version = "1.3.1"

[dependencies.rs_tracing]
features = ["rs_tracing"]
version = "1.1.0"

[target."cfg(windows)".dependencies]
cc = "1"
winreg = "0.11"

[target."cfg(windows)".dependencies.winapi]
features = [
  "combaseapi",
  "errhandlingapi",
  "fileapi",
  "handleapi",
  "ioapiset",
  "jobapi",
  "jobapi2",
  "minwindef",
  "processthreadsapi",
  "psapi",
  "shlobj",
  "shtypes",
  "synchapi",
  "sysinfoapi",
  "tlhelp32",
  "userenv",
  "winbase",
  "winerror",
  "winioctl",
  "winnt",
  "winuser",
]
version = "0.3"

[dev-dependencies]
walkdir = "2"
once_cell = "1.17.1"
enum-map = "2.4.2"

[build-dependencies]
lazy_static = "1"
regex = "1"

[workspace]
members = ["download"]

[workspace.dependencies]
anyhow = "1.0.69"
lazy_static = "1"
tempfile = "3.4"
thiserror = "1.0"
url = "2.3"

[lib]
name = "rustup"
path = "src/lib.rs"

[profile.release]
codegen-units = 1
lto = true

# Reduce build time by setting proc-macro crates non optimized.
[profile.release.build-override]
opt-level = 0

$ 
$ pwd
/tmp/x/rustup
$ 
$ ls
build.rs    Cargo.toml    ci               doc       flake.nix       LICENSE-MIT  rustup-init.sh  tests           www
Cargo.lock  CHANGELOG.md  CONTRIBUTING.md  download  LICENSE-APACHE  README.md    src             triagebot.toml
$ 
$ 
$ cargo build
  Downloaded getrandom v0.2.8
  Downloaded autocfg v0.1.8
  Downloaded async-compression v0.3.15
  Downloaded bit-vec v0.6.3
  Downloaded aes-soft v0.6.4
  Downloaded bitvec v0.20.4
  Downloaded cfg-if v0.1.10
  Downloaded base64 v0.13.1
  Downloaded autocfg v1.1.0
  Downloaded bytes v1.4.0
  Downloaded crypto-mac v0.10.1
  Downloaded concolor v0.0.11
  Downloaded cipher v0.2.5
  Downloaded block-padding v0.2.1
  Downloaded lalrpop-util v0.19.8
  Downloaded hyper-rustls v0.23.2
  Downloaded is-terminal v0.4.4
  Downloaded pulldown-cmark v0.9.2
  Downloaded io-lifetimes v1.0.5
  Downloaded crossbeam-utils v0.8.14
  Downloaded jobserver v0.1.25
  Downloaded ctr v0.6.0
  Downloaded md-5 v0.9.1
  Downloaded normalize-line-endings v0.3.0
  Downloaded num-iter v0.1.43
  Downloaded normpath v1.1.0
  Downloaded cvt v0.1.1
  Downloaded os_pipe v1.1.3
  Downloaded serde_spanned v0.6.1
  Downloaded num-bigint-dig v0.6.1
  Downloaded remove_dir_all v0.8.1
  Downloaded retry v1.3.1
  Downloaded rustls-native-certs v0.6.2
  Downloaded shlex v1.1.0
  Downloaded semver v1.0.16
  Downloaded digest v0.9.0
  Downloaded crossbeam-deque v0.8.2
  Downloaded humantime-serde v1.1.1
  Downloaded cpufeatures v0.2.5
  Downloaded crc32fast v1.3.2
  Downloaded itertools v0.10.5
  Downloaded sha-1 v0.9.8
  Downloaded lock_api v0.4.9
  Downloaded crypto-mac v0.11.1
  Downloaded dirs-next v2.0.0
  Downloaded pkg-config v0.3.26
  Downloaded proc-macro2 v1.0.51
  Downloaded ed25519-dalek v1.0.1
  Downloaded dunce v1.0.3
  Downloaded scopeguard v1.1.0
  Downloaded regex v1.7.1
  Downloaded want v0.3.0
  Downloaded snapbox-macros v0.3.1
  Downloaded itoa v1.0.5
  Downloaded crunchy v0.2.2
  Downloaded concolor-query v0.1.0
  Downloaded aead v0.3.2
  Downloaded siphasher v0.3.10
  Downloaded similar v2.2.1
  Downloaded pin-utils v0.1.0
  Downloaded num-bigint v0.2.6
  Downloaded quote v1.0.23
  Downloaded filetime v0.2.20
  Downloaded miniz_oxide v0.6.2
  Downloaded fs_at v0.1.1
  Downloaded curl v0.4.44
  Downloaded rayon-core v1.10.2
  Downloaded funty v1.1.0
  Downloaded dbl v0.3.2
  Downloaded hmac v0.11.0
  Downloaded diff v0.1.13
  Downloaded sha2 v0.10.6
  Downloaded getrandom v0.1.16
  Downloaded mio v0.8.6
  Downloaded memoffset v0.7.1
  Downloaded rand_core v0.5.1
  Downloaded openssl-probe v0.1.5
  Downloaded openssl-macros v0.1.0
  Downloaded libm v0.2.6
  Downloaded sharded-slab v0.1.4
  Downloaded static_assertions v1.1.0
  Downloaded serde_urlencoded v0.7.1
  Downloaded reqwest v0.11.14
  Downloaded smallvec v1.10.0
  Downloaded futures-task v0.3.26
  Downloaded futures-sink v0.3.26
  Downloaded socket2 v0.4.7
  Downloaded glob v0.3.1
  Downloaded futures-io v0.3.26
  Downloaded fastrand v1.9.0
  Downloaded futures-core v0.3.26
  Downloaded spin v0.5.2
  Downloaded anyhow v1.0.69
  Downloaded flate2 v1.0.25
  Downloaded aho-corasick v0.7.20
  Downloaded hashbrown v0.12.3
  Downloaded http-body v0.4.5
  Downloaded foreign-types-shared v0.1.1
  Downloaded futures-util v0.3.26
  Downloaded ppv-lite86 v0.2.17
  Downloaded ed25519 v1.5.3
  Downloaded generic-array v0.14.6
  Downloaded form_urlencoded v1.1.0
  Downloaded mime v0.3.16
  Downloaded crossbeam-epoch v0.9.13
  Downloaded rayon v1.6.1
  Downloaded enum-map v2.4.2
  Downloaded httpdate v1.0.2
  Downloaded rand v0.8.5
  Downloaded rand_chacha v0.2.2
  Downloaded curve25519-dalek v3.2.1
  Downloaded byteorder v1.4.3
  Downloaded regex-syntax v0.6.28
  Downloaded cc v1.0.79
  Downloaded chrono v0.4.23
  Downloaded rustix v0.36.8
  Downloaded lalrpop v0.19.8
  Downloaded sys-info v0.9.1
  Downloaded strsim v0.10.0
  Downloaded httparse v1.8.0
  Downloaded foreign-types v0.3.2
  Downloaded env_proxy v0.4.1
  Downloaded ena v0.14.1
  Downloaded dirs-sys-next v0.1.2
  Downloaded content_inspector v0.2.4
  Downloaded h2 v0.3.16
  Downloaded syn v1.0.109
  Downloaded tar v0.4.38
  Downloaded threadpool v1.8.1
  Downloaded toml_datetime v0.6.1
  Downloaded tinyvec v1.6.0
  Downloaded tiny-keccak v2.0.2
  Downloaded tempfile v3.4.0
  Downloaded string_cache v0.8.4
  Downloaded new_debug_unreachable v1.0.4
  Downloaded enum-map-derive v0.11.0
  Downloaded hyper-tls v0.5.0
  Downloaded home v0.5.4
  Downloaded http v0.2.9
  Downloaded term v0.7.0
  Downloaded synstructure v0.12.6
  Downloaded sha2 v0.9.9
  Downloaded toml v0.5.11
  Downloaded subtle v2.4.1
  Downloaded tracing v0.1.37
  Downloaded time v0.1.45
  Downloaded thiserror v1.0.38
  Downloaded url v2.3.1
  Downloaded xattr v0.2.3
  Downloaded untrusted v0.7.1
  Downloaded thiserror-impl v1.0.38
  Downloaded slab v0.4.8
  Downloaded webpki v0.22.0
  Downloaded openssl v0.10.45
  Downloaded rand v0.7.3
  Downloaded ripemd160 v0.9.1
  Downloaded adler v1.0.2
  Downloaded radium v0.6.2
  Downloaded ansi_term v0.12.1
  Downloaded ascii-canvas v3.0.0
  Downloaded pem v0.8.3
  Downloaded opener v0.5.2
  Downloaded simple_asn1 v0.4.1
  Downloaded tokio-socks v0.5.1
  Downloaded unicode-bidi v0.3.10
  Downloaded signature v1.3.2
  Downloaded vec_map v0.8.2
  Downloaded precomputed-hash v0.1.1
  Downloaded aes v0.6.0
  Downloaded wait-timeout v0.2.0
  Downloaded bit-set v0.5.3
  Downloaded block-modes v0.7.0
  Downloaded wyz v0.2.0
  Downloaded typenum v1.16.0
  Downloaded trycmd v0.14.12
  Downloaded winnow v0.3.3
  Downloaded zeroize v1.3.0
  Downloaded yansi v0.5.1
  Downloaded xxhash-rust v0.8.6
  Downloaded version_check v0.9.4
  Downloaded zeroize_derive v1.3.3
  Downloaded zstd v0.12.3+zstd.1.5.2
  Downloaded zstd-safe v6.0.4+zstd.1.5.4
  Downloaded rustls-pemfile v1.0.2
  Downloaded serde_derive v1.0.152
  Downloaded either v1.8.1
  Downloaded ryu v1.0.12
  Downloaded dyn-clone v1.0.11
  Downloaded crypto-common v0.1.6
  Downloaded futures-channel v0.3.26
  Downloaded serde_json v1.0.93
  Downloaded crossbeam-channel v0.5.6
  Downloaded percent-encoding v2.2.0
  Downloaded git-testament v0.2.4
  Downloaded no-std-compat v0.4.1
  Downloaded git-testament-derive v0.1.14
  Downloaded fixedbitset v0.4.2
  Downloaded indexmap v1.9.2
  Downloaded block-buffer v0.10.3
  Downloaded parking_lot v0.12.1
  Downloaded num_cpus v1.15.0
  Downloaded num-traits v0.2.15
  Downloaded num-integer v0.1.45
  Downloaded once_cell v1.17.1
  Downloaded rand_core v0.6.4
  Downloaded parking_lot_core v0.9.7
  Downloaded digest v0.10.6
  Downloaded hyper v0.14.24
  Downloaded iana-time-zone v0.1.53
  Downloaded tokio-util v0.7.7
  Downloaded sct v0.7.0
  Downloaded time-macros v0.2.8
  Downloaded humantime v2.1.0
  Downloaded base64 v0.21.0
  Downloaded ipnet v2.7.1
  Downloaded unicode-normalization v0.1.22
  Downloaded opaque-debug v0.3.0
  Downloaded native-tls v0.2.11
  Downloaded pin-project-lite v0.2.9
  Downloaded block-buffer v0.9.0
  Downloaded openssl-sys v0.9.80
  Downloaded rand_chacha v0.3.1
  Downloaded tokio v1.25.0
  Downloaded serde v1.0.152
  Downloaded petgraph v0.6.3
  Downloaded eax v0.3.0
  Downloaded ecdsa v0.11.1
  Downloaded zstd-sys v2.0.7+zstd.1.5.4
  Downloaded idna v0.3.0
  Downloaded group v0.9.0
  Downloaded cmac v0.5.1
  Downloaded effective-limits v0.5.5
  Downloaded ff v0.9.0
  Downloaded cast5 v0.9.0
  Downloaded rustls v0.20.8
  Downloaded tracing-core v0.1.30
  Downloaded term_size v0.3.2
  Downloaded time v0.3.20
  Downloaded tokio-native-tls v0.3.1
  Downloaded tap v1.0.1
  Downloaded toml_edit v0.19.4
  Downloaded unicase v2.6.0
  Downloaded buffered-reader v1.1.4
  Downloaded unicode-ident v1.0.6
  Downloaded tinyvec_macros v0.1.1
  Downloaded time-core v0.1.0
  Downloaded der v0.3.5
  Downloaded const-oid v0.5.2
  Downloaded memsec v0.6.2
  Downloaded tokio-rustls v0.23.4
  Downloaded phf_shared v0.10.0
  Downloaded des v0.6.0
  Downloaded linux-raw-sys v0.1.4
  Downloaded tower-service v0.3.2
  Downloaded xz2 v0.1.7
  Downloaded x25519-dalek v1.2.0
  Downloaded unicode-xid v0.2.4
  Downloaded try-lock v0.2.4
  Downloaded snapbox v0.4.7
  Downloaded nix v0.26.2
  Downloaded encoding_rs v0.8.32
  Downloaded blowfish v0.7.0
  Downloaded rs_tracing v1.1.0
  Downloaded p256 v0.8.1
  Downloaded rsa v0.3.0
  Downloaded elliptic-curve v0.9.12
  Downloaded pkcs8 v0.6.1
  Downloaded twofish v0.5.0
  Downloaded spki v0.3.0
  Downloaded idea v0.3.0
  Downloaded bstr v1.3.0
  Downloaded lzma-sys v0.1.20
  Downloaded libz-sys v1.1.8
  Downloaded sha1collisiondetection v0.2.6
  Downloaded curl-sys v0.4.60+curl-7.88.1
  Downloaded ring v0.16.20
  Downloaded sequoia-openpgp v1.13.0
  Downloaded 277 crates (30.7 MB) in 9.95s (largest was `ring` at 5.1 MB)
   Compiling libc v0.2.139
   Compiling cfg-if v1.0.0
   Compiling autocfg v1.1.0
   Compiling version_check v0.9.4
   Compiling typenum v1.16.0
   Compiling proc-macro2 v1.0.51
   Compiling quote v1.0.23
   Compiling unicode-ident v1.0.6
   Compiling syn v1.0.109
   Compiling memchr v2.5.0
   Compiling generic-array v0.14.6
   Compiling pkg-config v0.3.26
   Compiling once_cell v1.17.1
   Compiling log v0.4.17
   Compiling jobserver v0.1.25
   Compiling cc v1.0.79
   Compiling bitflags v1.3.2
   Compiling serde_derive v1.0.152
   Compiling serde v1.0.152
   Compiling indexmap v1.9.2
   Compiling num_cpus v1.15.0
   Compiling pin-project-lite v0.2.9
   Compiling opaque-debug v0.3.0
   Compiling digest v0.9.0
   Compiling subtle v2.4.1
   Compiling spin v0.5.2
   Compiling unicode-xid v0.2.4
   Compiling itoa v1.0.5
   Compiling hashbrown v0.12.3
   Compiling bytes v1.4.0
   Compiling cipher v0.2.5
   Compiling socket2 v0.4.7
   Compiling getrandom v0.2.8
   Compiling tokio v1.25.0
   Compiling futures-core v0.3.26
   Compiling rand_core v0.6.4
   Compiling mio v0.8.6
   Compiling getrandom v0.1.16
   Compiling slab v0.4.8
   Compiling num-traits v0.2.15
   Compiling byteorder v1.4.3
   Compiling futures-task v0.3.26
   Compiling openssl-sys v0.9.80
   Compiling ring v0.16.20
   Compiling aho-corasick v0.7.20
   Compiling num-integer v0.1.45
   Compiling ppv-lite86 v0.2.17
   Compiling regex-syntax v0.6.28
   Compiling futures-util v0.3.26
   Compiling radium v0.6.2
   Compiling crossbeam-utils v0.8.14
error: failed to run custom build command for `openssl-sys v0.9.80`

Caused by:
  process didn't exit successfully: `/tmp/x/rustup/target/debug/build/openssl-sys-9e8b2102ad437148/build-script-main` (exit status: 101)
  --- stdout
  cargo:rustc-cfg=const_fn
  cargo:rustc-cfg=openssl
  cargo:rerun-if-env-changed=X86_64_UNKNOWN_LINUX_GNU_OPENSSL_LIB_DIR
  X86_64_UNKNOWN_LINUX_GNU_OPENSSL_LIB_DIR unset
  cargo:rerun-if-env-changed=OPENSSL_LIB_DIR
  OPENSSL_LIB_DIR unset
  cargo:rerun-if-env-changed=X86_64_UNKNOWN_LINUX_GNU_OPENSSL_INCLUDE_DIR
  X86_64_UNKNOWN_LINUX_GNU_OPENSSL_INCLUDE_DIR unset
  cargo:rerun-if-env-changed=OPENSSL_INCLUDE_DIR
  OPENSSL_INCLUDE_DIR unset
  cargo:rerun-if-env-changed=X86_64_UNKNOWN_LINUX_GNU_OPENSSL_DIR
  X86_64_UNKNOWN_LINUX_GNU_OPENSSL_DIR unset
  cargo:rerun-if-env-changed=OPENSSL_DIR
  OPENSSL_DIR unset
  cargo:rerun-if-env-changed=OPENSSL_NO_PKG_CONFIG
  cargo:rerun-if-env-changed=PKG_CONFIG_x86_64-unknown-linux-gnu
  cargo:rerun-if-env-changed=PKG_CONFIG_x86_64_unknown_linux_gnu
  cargo:rerun-if-env-changed=HOST_PKG_CONFIG
  cargo:rerun-if-env-changed=PKG_CONFIG
  cargo:rerun-if-env-changed=OPENSSL_STATIC
  cargo:rerun-if-env-changed=OPENSSL_DYNAMIC
  cargo:rerun-if-env-changed=PKG_CONFIG_ALL_STATIC
  cargo:rerun-if-env-changed=PKG_CONFIG_ALL_DYNAMIC
  cargo:rerun-if-env-changed=PKG_CONFIG_PATH_x86_64-unknown-linux-gnu
  cargo:rerun-if-env-changed=PKG_CONFIG_PATH_x86_64_unknown_linux_gnu
  cargo:rerun-if-env-changed=HOST_PKG_CONFIG_PATH
  cargo:rerun-if-env-changed=PKG_CONFIG_PATH
  cargo:rerun-if-env-changed=PKG_CONFIG_LIBDIR_x86_64-unknown-linux-gnu
  cargo:rerun-if-env-changed=PKG_CONFIG_LIBDIR_x86_64_unknown_linux_gnu
  cargo:rerun-if-env-changed=HOST_PKG_CONFIG_LIBDIR
  cargo:rerun-if-env-changed=PKG_CONFIG_LIBDIR
  cargo:rerun-if-env-changed=PKG_CONFIG_SYSROOT_DIR_x86_64-unknown-linux-gnu
  cargo:rerun-if-env-changed=PKG_CONFIG_SYSROOT_DIR_x86_64_unknown_linux_gnu
  cargo:rerun-if-env-changed=HOST_PKG_CONFIG_SYSROOT_DIR
  cargo:rerun-if-env-changed=PKG_CONFIG_SYSROOT_DIR
  run pkg_config fail: "`\"pkg-config\" \"--libs\" \"--cflags\" \"openssl\"` did not exit successfully: exit status: 1\nerror: could not find system library 'openssl' required by the 'openssl-sys' crate\n\n--- stderr\nPackage openssl was not found in the pkg-config search path.\nPerhaps you should add the directory containing `openssl.pc'\nto the PKG_CONFIG_PATH environment variable\nPackage 'openssl', required by 'virtual:world', not found\n"

  --- stderr
  thread 'main' panicked at '

  Could not find directory of OpenSSL installation, and this `-sys` crate cannot
  proceed without this knowledge. If OpenSSL is installed and this crate had
  trouble finding it,  you can set the `OPENSSL_DIR` environment variable for the
  compilation process.

  Make sure you also have the development packages of openssl installed.
  For example, `libssl-dev` on Ubuntu or `openssl-devel` on Fedora.

  If you're in a situation where you think the directory *should* be found
  automatically, please open a bug at https://github.com/sfackler/rust-openssl
  and include information about your system as well as this message.

  $HOST = x86_64-unknown-linux-gnu
  $TARGET = x86_64-unknown-linux-gnu
  openssl-sys = 0.9.80

  ', /home/gkamathe/.cargo/registry/src/github.com-1ecc6299db9ec823/openssl-sys-0.9.80/build/find_normal.rs:191:5
  note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
warning: build failed, waiting for other jobs to finish...
$ 
$ ls
build.rs    CHANGELOG.md     doc        LICENSE-APACHE  rustup-init.sh  tests
Cargo.lock  ci               download   LICENSE-MIT     src             triagebot.toml
Cargo.toml  CONTRIBUTING.md  flake.nix  README.md       target          www
$ 
$ ls target/
CACHEDIR.TAG  debug
$ 
$ ls target/debug/
build  deps  examples  incremental
$ 
$
```
