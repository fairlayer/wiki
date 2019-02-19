# Development and private genesis

Look into `tools/genesis.js` to modify initial parameters such as Byzantine tolerance (you can set 0 and have single server building blocks, or 333 for a thousand).

You can increase blocktime or change gas cost along with other network settings.

## Local Simulation

`./install` then run `./simulate` to bootstrap local dev blockchain with 4 validators on different ports (8443, 8001, 8002, 8003) each having one Fair share. Other nodes 8004-8008 are regular user wallets. Demoapp is NodeJS demo exchange with deposit/withdraw functions.

![/img/pm2result.png](/img/pm2result.png)

To optimize the development `wallet` serves html for all other nodes and everyone runs the same code from src, only datadirs are different (each node executes blocks).

8443 is also a bank @main. At bootstrap there are various end-2-end tests performed on a live network, which is a great way to see if all components fit together. Different users at different times turn on different times and verify the result with setTimeout.

## Contribute

It's recommended to use Prettier, you can add it to Sublime Text (don't forget to `yarn global add prettier`)

## Using live network

Perfect way to run new code against old blockchain:

```sh
$ rm -rf fair
$ id=fair
$ f=Fair-1.tar.gz
$ mkdir $id && cd $id && curl https://fairlayer.com/$f -o $f
$ tar -xzf $f && rm $f
$ ln -s ~/work/fair/node_modules
$ ln -s ~/work/fair/wallet/node_modules wallet/node_modules
$ rm -rf ./src
$ cp -r ~/work/fair/src src
$ node fair -p8001
```

## Reading the codebase

Fairlayer has small codebase by design, about 5000 LOC. Less code, less bugs and technical debt.

`/bin` - binary tools

`/dist` - compiled wallet frontend

`/lib` - vendored 3rd party libraries

`/src` - core code and daemon functionality

`/tools` - random files to help the development or to showcase some concept

`/wallet` - Vue-based frontend for the daemon

`/wiki` - this Wiki, feel free to edit

Start with `/src/fair.js`.

# Runbook

## Deploy FL

```sh
$ ./deploy
```

Ensure https://fairlayer.com/ opens.

#### Troubleshooting

```sh
# prints FL logs
$ ./l
```

## Reconfigure caddy

```sh
$ vi Caddyfile
$ caddy -service restart
```

Ensure https://fairlayer.com/ opens.

#### Troubleshooting

```sh
# prints Caddy logs
$ journalctl --boot -u Caddy.service
```

# [2. Step by step](/11_step_by_step.md) / [Home](/README.md)
