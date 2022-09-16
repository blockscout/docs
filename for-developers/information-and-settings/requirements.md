# General Requirements / Blockscout Prerequisites

{% hint style="success" %}
Install the software below prior to Blockscout installation. For additional requirements see:

* [Database Storage Requirements](database-storage-requirements.md): Storage required for common chains to give a sense of needed storage
* [Node Tracing Requirements](node-tracing-json-rpc-requirements.md): JSON RPC methods&#x20;
* [Client Setting Requirements](client-settings.md): Settings related to client implementations (ie Geth, OpenEthereum, etc)
* [Hardware/Hosting Requirements](../../for-projects/resource-requirements.md): Base requirements for a hosted instance of Blockscout.
{% endhint %}

| Dependency                                                       | Mac                       | Linux                                                                                                                                                           |
| ---------------------------------------------------------------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Erlang/OTP 24](https://github.com/erlang/otp)                   | `brew install erlang`     | [Erlang Install Example](https://github.com/poanetwork/blockscout-terraform/blob/33f68e816e36dc2fb055911fa0372531f0e956e7/modules/stack/libexec/init.sh#L134)   |
| [Elixir 1.13.x](https://elixir-lang.org/)                        | `brew install elixir`     | [Elixir Install Example](https://github.com/poanetwork/blockscout-terraform/blob/33f68e816e36dc2fb055911fa0372531f0e956e7/modules/stack/libexec/init.sh#L138)   |
| [Postgres 10.3+,11,12, 13,14](https://www.postgresql.org/)       | `brew install postgresql` | [Postgres Install Example](https://github.com/poanetwork/blockscout-terraform/blob/33f68e816e36dc2fb055911fa0372531f0e956e7/modules/stack/libexec/init.sh#L187) |
| [Node.js 16.x.x](https://nodejs.org/en/)                         | `brew install node`       | [Node.js Install Example](https://github.com/poanetwork/blockscout-terraform/blob/33f68e816e36dc2fb055911fa0372531f0e956e7/modules/stack/libexec/init.sh#L66)   |
| [Automake](https://www.gnu.org/software/automake/)               | `brew install automake`   | [Automake Install Example](https://github.com/poanetwork/blockscout-terraform/blob/33f68e816e36dc2fb055911fa0372531f0e956e7/modules/stack/libexec/init.sh#L72)  |
| [Libtool](https://www.gnu.org/software/libtool/)                 | `brew install libtool`    | [Libtool Install Example](https://github.com/poanetwork/blockscout-terraform/blob/33f68e816e36dc2fb055911fa0372531f0e956e7/modules/stack/libexec/init.sh#L62)   |
| [Inotify-tools](https://github.com/rvoicilas/inotify-tools/wiki) | Not Required              | Ubuntu - `apt-get install inotify-tools`                                                                                                                        |
| [GCC Compiler](https://gcc.gnu.org/)                             | `brew install gcc`        | [GCC Compiler Example](https://github.com/poanetwork/blockscout-terraform/blob/33f68e816e36dc2fb055911fa0372531f0e956e7/modules/stack/libexec/init.sh#L70)      |
| [GMP](https://gmplib.org/)                                       | `brew install gmp`        | [Install GMP Devel](https://github.com/poanetwork/blockscout-terraform/blob/33f68e816e36dc2fb055911fa0372531f0e956e7/modules/stack/libexec/init.sh#L74)         |
| Make                                                             | -                         | `sudo apt install make`if Debian 9                                                                                                                              |
| G++ Compiler                                                     | -                         | `sudo apt install g++`if Debian 9                                                                                                                               |
| Rust                                                             | -                         | [Install Rust](https://www.rust-lang.org/tools/install)                                                                                                         |
| Cargo                                                            | -                         | Ubuntu - `apt-get install cargo`                                                                                                                                |
