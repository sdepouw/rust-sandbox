# Rust Sandbox

Wanted to see what Rust is all about.

## Installing and Running Hello World

- Installed RustRover
- Installed the toolchain as prompted
- However, `link.exe` is associated with Git's version of it, on my machine
- Resolution: Using the GNU tools instead:

```
rustup toolchain install stable-x86_64-pc-windows-gnu
rustup default stable-x86_64-pc-windows-gnu
```

Confirming that it is the selected one (in Command Prompt, as Terminal will flash open a new window then close it):

```
rustup show
```

Output:

```
Default host: x86_64-pc-windows-msvc
rustup home:  C:\Users\DoctorBlue\.rustup

installed toolchains
--------------------
stable-x86_64-pc-windows-gnu (active, default)
stable-x86_64-pc-windows-msvc

active toolchain
----------------
name: stable-x86_64-pc-windows-gnu
active because: it's the default toolchain
installed targets:
  x86_64-pc-windows-gnu
```

## Random Notes

### Compile with Warnings as Errors

See [Lint Levels](https://doc.rust-lang.org/rustc/lints/levels.html). `-D` Deny allows overrides of lint things.
`-F` Forbid completely forbids it from being anything less than an error.

```
rustc .\main.rs -D warnings
```

Using Cargo (`clippy` is equivalent to `check`, but accepts the Deny flag):

```
cargo clippy -- -D warnings
```
