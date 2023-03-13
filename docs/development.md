---
layout: default
title: Development
nav_order: 4
---

# Development
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

# Set up environment

To start to contribute to FIM repositories you will need the following packages and dependencies:

*Generic dependencies for Linux systems*
- Git.
- GCC.
- RustC and Cargo.
- cURL.
- TAR.
- GZIP.

*For Debian based systems additional dependencies*
- devscripts
- equivs
- pkg-config
- libssl-dev

*For CentOS based systems additional dependencies*
- rpm-build
- openssl-devel

*Windows systems*
- Git.
- RustC and Cargo.
- Light and Candle from MSI toolset.

---

## Installing Rust
Install Rust in the mentioned systems can be performed following the next steps:

### Linux systems
1. Run `curl https://sh.rustup.rs -sSf | sh` to download and install Rust. Follow the required steps with recommended installation.
2. Reload terminal and try cargo with `cargo --version`.

---

### Windows systems
1. Download Rust from official [Rust page](https://www.rust-lang.org/tools/install).
2. Double click on installer and follow the UI steps.
3. Reload terminal and try cargo with `cargo --version`.

---

## Installing dependencies
The dependencies required for each system could be installed with:

### Debian dependencies
```
sudo apt update
sudo apt install -y git curl gcc tar gzip devscripts equivs pkg-config libssl-dev
```

### CentOS dependencies
```
sudo yum install -y git curl gcc tar gzip rpm-build openssl-devel
```

### Windows dependencies
1. Checkout and get Git from [Git downloads page](https://git-scm.com/downloads)
2. Checkout and get WIX Toolset from [WIX page](https://wixtoolset.org/docs/wix3/)

---

# Build FIM
FIM require to be compiled or packaged to run or install in the host. The repository provides tools to perform both options.

## Compile and run FIM
With the dependencies installed it will only require to fetch the repository source code and build with the following steps:
1. Fetch git repository with `git clone https://github.com/Achiefs/fim.git`.
2. Go to the repository `cd fim`.
3. Compile FIM `cargo build --release`.
4. Run FIM with `cargo run` (Unix systems).
5. Run FIM with `cargo run -- -f` to run FIM in foreground (Windows systems only)

{: .note}
> FIM executable is stored at `target/release` or `target/debug` folder, depending on cargo build performed `--release` or not.
