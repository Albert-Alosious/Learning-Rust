albertalosious@Alberts-MacBook-Air LearnRust % curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh 
info: downloading installer
warn: It looks like you have an existing rustup settings file at:
warn: /Users/albertalosious/.rustup/settings.toml
warn: Rustup will install the default toolchain as specified in the settings file,
warn: instead of the one inferred from the default host triple.

Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.

Rustup metadata and toolchains will be installed into the Rustup
home directory, located at:

  /Users/albertalosious/.rustup

This can be modified with the RUSTUP_HOME environment variable.

The Cargo home directory is located at:

  /Users/albertalosious/.cargo

This can be modified with the CARGO_HOME environment variable.

The cargo, rustc, rustup and other commands will be added to
Cargo's bin directory, located at:

  /Users/albertalosious/.cargo/bin

This path will then be added to your PATH environment variable by
modifying the profile files located at:

  /Users/albertalosious/.profile
  /Users/albertalosious/.bash_profile
  /Users/albertalosious/.bashrc
  /Users/albertalosious/.zshenv
  /Users/albertalosious/.tcshrc

You can uninstall at any time with rustup self uninstall and
these changes will be reverted.

Current installation options:


   default host triple: aarch64-apple-darwin
     default toolchain: stable (default)
               profile: default
  modify PATH variable: yes

1) Proceed with standard installation (default - just press enter)
2) Customize installation
3) Cancel installation
>1

info: profile set to default
info: default host triple is aarch64-apple-darwin
info: syncing channel updates for stable-aarch64-apple-darwin
info: latest update on 2026-07-16 for version 1.97.1 (8bab26f4f 2026-07-14)
info: downloading 6 components
        cargo installed                        8.47 MiB
       clippy installed                        3.02 MiB
    rust-docs installed                       22.82 MiB
     rust-std installed                       27.93 MiB
        rustc installed                       64.97 MiB
      rustfmt installed                        1.43 MiB                                                                                       info: default toolchain set to stable-aarch64-apple-darwin

  stable-aarch64-apple-darwin installed - rustc 1.97.1 (8bab26f4f 2026-07-14)


Rust is installed now. Great!

To get started you may need to restart your current shell.
This would reload your PATH environment variable to include
Cargo's bin directory ($HOME/.cargo/bin).

To configure your current shell, you need to source
the corresponding env file under $HOME/.cargo.

This is usually done by running one of the following (note the leading DOT):
. "$HOME/.cargo/env"            # For sh/bash/zsh/ash/dash/pdksh
source "$HOME/.cargo/env.fish"  # For fish
source "~/.cargo/env.nu"  # For nushell
source "$HOME/.cargo/env.tcsh"  # For tcsh
. "$HOME/.cargo/env.ps1"        # For pwsh
source "$HOME/.cargo/env.xsh"   # For xonsh