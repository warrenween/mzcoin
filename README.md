Mzcoin [![GoDoc](https://godoc.org/github.com/ShanghaiKuaibei/mzcoin?status.svg)](https://godoc.org/github.com/ShanghaiKuaibei/mzcoin) [![Go Report Card](https://goreportcard.com/badge/github.com/ShanghaiKuaibei/mzcoin)](https://goreportcard.com/report/github.com/ShanghaiKuaibei/mzcoin) 
=======

Mzcoin is children's education coin created by mzworld.

Installation
------------

*For detailed installation instructions, see [Installing mzcoin](../../wiki/Installation)*

## For linux:

```sh
$ sudo apt-get install curl git mercurial make binutils gcc bzr bison libgmp3-dev screen -y
```

## For OSX:

1) Install [homebrew](brew.sh), if you don't have it yet
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2) Install the latest version of golang
```
$ brew install go
```

3) Setup $GOPATH variable, add it to ~/.bash_profile (or bashrc). After editing, open a new tab
Add to `bashrc` or `bash_profile`
```sh
$ export GOPATH=/Users/<username>/go 
$ export PATH=$PATH:$GOPATH/bin

```

4) Install Mercurial and Bazaar
```
$ brew install mercurial bzr
```

5) Fetch the latest code of mzcoin from the github repository

```
$ go get github.com/ShanghaiKuaibei/mzcoin
```

6) Change your current directory to $GOPATH/src/github.com/ShanghaiKuaibei/mzcoin

```
$ cd $GOPATH/src/github.com/ShanghaiKuaibei/mzcoin
```

7) Install glock and sync all the dependencies 
```
$ go get github.com/robfig/glock
$ glock sync github.com/ShanghaiKuaibei/mzcoin
```

8) Run the node ;)
```
$ ./run.sh -h
```

9) Running Wallet

```
$ ./run.sh
```

Then open `http://127.0.0.1:6402` in a browser.

## Golang ENV setup with gvm

In China, use `--source=https://github.com/golang/go` to bypass firewall when fetching golang source

```
$ sudo apt-get install bison curl git mercurial make binutils bison gcc build-essential
$ bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
$ source $HOME/.gvm/scripts/gvm

$ gvm install go1.4 --source=https://github.com/golang/go
$ gvm use go1.4
$ gvm install go1.6
$ gvm use go1.6 --default
```

If you open up new terminal and the go command is not found then add this to .bashrc . GVM should add this automatically
```
$ [[ -s "$HOME/.gvm/scripts/gvm" ]] && source "$HOME/.gvm/scripts/gvm"
$ gvm use go1.6 >/dev/null
```


The mzcoin repo must be in $GOPATH, under "/src/github.com/ShanghaiKuaibei". Otherwise golang programs cannot import the libraries.

```
#pull mzcoin repo into the gopath
#note: puts the mzcoin folder in $GOPATH/src/github.com/ShanghaiKuaibei/mzcoin
$ go get github.com/ShanghaiKuaibei/mzcoin

#create symlink of the repo
$ cd $HOME
$ ln -s $GOPATH/src/github.com/ShanghaiKuaibei/mzcoin mzcoin
```

Dependencies
------------

```
$ go get github.com/robfig/glock
$ glock sync github.com/ShanghaiKuaibei/mzcoin
$ go get ./cmd/mzcoin
```

To update dependencies
```
$ glock save github.com/ShanghaiKuaibei/mzcoin/cmd/mzcoin
```

Running A mzcoin Node
----------------------

```
$ cd mzcoin
$ screen
$ go run ./cmd/mzcoin/mzcoin.go 
#then ctrl+A then D to exit screen
#screen -x to reattach screen
```

##Todo

Use gvm package set, so repo does not need to be symlinked. Does this have a default option?
```
$ gvm pkgset create mzcoin
$ gvm pkgset use mzcoin
$ git clone https://github.com/ShanghaiKuaibei/mzcoin
$ cd mzcoin
$ go install
```

##Cross Compilation

Install Gox:
```
$ go get github.com/mitchellh/gox
```

Compile:
```
$ gox --help
$ gox [options] cmd/mzcoin/
```

Local Server API
----------------

Run the mzcoin client then
```
http://127.0.0.1:6420/wallets
http://127.0.0.1:6420/outputs
http://127.0.0.1:6420/blockchain/blocks?start=0&end=500
http://127.0.0.1:6420/blockchain
http://127.0.0.1:6420/connections
```

```
http://127.0.0.1:6420/wallets
- to get your wallet seed. Write this down

http://127.0.0.1:6420/wallet/balance?id=2016_02_17_9671.wlt
- to get wallet balance (use wallet filename as id)
- TODO: allow addresses for balance check

http://127.0.0.1:6420/outputs to see outputs (address balances)

http://127.0.0.1:6420/blockchain/blocks?start=0&end=5000 to see all blocks and transactions.

http://127.0.0.1:6420/network/connections to check network connections

http://127.0.0.1:6420/blockchain to check blockchain head
```

Public API
----------

This is a public server. You can use these urls on local host too, with the mzcoin client running.
```
http://mzcoin-chompyz.c9.io/outputs
http://mzcoin-chompyz.c9.io/blockchain/blocks?start=0&end=500
http://mzcoin-chompyz.c9.io/blockchain
http://mzcoin-chompyz.c9.io/connections
```

Modules
-------

```
/src/cipher - cryptography library
/src/coin - the blockchain
/src/daemon - networking and wire protocol
/src/visor - the top level, client
/src/gui - the web wallet and json client interface
/src/wallet - the private key storage library
```

Meshnet
-------

```
$ go run ./cmd/mesh/*.go -config=cmd/mesh/sample/config_a.json
$ go run ./cmd/mesh/*.go -config=cmd/mesh/sample/config_b.json
```

Meshnet reminders
-----------------

- one way latency
- two way latency (append), latency between packet and ack
- service handler (ability to append services to meshnet)
- uploading bandwidth, latency measurements over time
- end-to-end route instrumentation

Rebuilding Wallet HTML
----------------------

```sh
$ npm install
$ gulp build
```
