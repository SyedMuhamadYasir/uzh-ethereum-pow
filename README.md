# UZH Ethereum PoW

Course support repository for the University of Zurich Ethereum Proof-of-Work hands-on.

This repository hosts prebuilt macOS Go-Ethereum v1.10.26 binaries for BCE 2026 so students do not need to compile the legacy client from source during the hands-on.

## macOS — BCE 2026

Install tmux:

```bash
brew install tmux
```

Create the course directory:

```bash
mkdir -p "$HOME/uzhethereum"
cd "$HOME/uzhethereum"
```

Download the correct prebuilt Geth binary automatically:

```bash
ARCH="$(uname -m)"

case "$ARCH" in
  arm64)
    URL="https://github.com/SyedMuhamadYasir/uzh-ethereum-pow/releases/download/bce26-v1.10.26/uzh-geth-macos-arm64-v1.10.26"
    ;;
  x86_64)
    URL="https://github.com/SyedMuhamadYasir/uzh-ethereum-pow/releases/download/bce26-v1.10.26/uzh-geth-macos-amd64-v1.10.26"
    ;;
  *)
    echo "Unsupported Mac architecture: $ARCH"
    exit 1
    ;;
esac

curl -fL --retry 3 "$URL" -o uzh-geth
chmod +x uzh-geth
./uzh-geth version
```

Download the UZH Ethereum PoW configuration and genesis files:

```bash
curl -fL --retry 3 \
  https://gitlab.uzh.ch/claudio.tessone/uzhethereum/-/raw/master/uzheth-config.toml \
  -o uzheth-config.toml

curl -fL --retry 3 \
  https://gitlab.uzh.ch/claudio.tessone/uzhethereum/-/raw/master/uzheth.json \
  -o uzheth.json
```

Then continue with the official hands-on:

```bash
./uzh-geth --networkid 702 --config uzheth-config.toml init uzheth.json
```

Run Geth inside the `pow` tmux session using:

```bash
./uzh-geth --networkid 702 --config uzheth-config.toml
```

Attach to the running node from the normal terminal using:

```bash
./uzh-geth --config uzheth-config.toml attach http://localhost:8545
```

## Linux / Windows with WSL2

No change is required. These platforms continue to use the existing Linux course binary and instructions.

## Release

Current BCE 2026 release:

- macOS Apple Silicon: `uzh-geth-macos-arm64-v1.10.26`
- macOS Intel: `uzh-geth-macos-amd64-v1.10.26`
