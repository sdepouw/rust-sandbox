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

### "dlltool.exe" Error

After adding my first dependency, then making a change to `main.rs`, running `cargo build` resulted in this error:

```
> cargo build
   Compiling cfg-if v1.0.1
   Compiling zerocopy v0.8.26
   Compiling getrandom v0.3.3
   Compiling rand_core v0.9.3
error: Error calling dlltool 'dlltool.exe': program not found

error: could not compile `getrandom` (lib) due to 1 previous error
warning: build failed, waiting for other jobs to finish...
```

Attempting to resolve using [this StackOverflow post](https://stackoverflow.com/a/79640980/100534), as the question posed is very similar to my current setup.

- [Downloaded and installed MSYS2](https://www.msys2.org/) (installed to `C:\msys64`)
- In the MSYS2 terminal, ran the following command:

```
pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain \
    mingw-w64-ucrt-x86_64-nasm
```

- Added `C:\msys64\ucrt64\bin` to `PATH`
- Restarted Terminal, and re-ran `cargo build`. The application now compiles.

(Note: `mingw-w64-ucrt-x86_64-nasm` may have been for an unrelated package that the user on StackOverflow was using)

See also: [The Rust Book segment on Windows](https://rust-lang.github.io/rustup/installation/windows.html)
