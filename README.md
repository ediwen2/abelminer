# AbelMine Pool-Account-Mechanism

## Prerequisite
The software has been tested on the Linux environment, mainly on
the Ubuntu 22.04 Release. The Nvidia CUDA Toolkit needs to be
installed and the machine needs to be restarted. To check if the
Nvidia CUDA driver has been properly installed, type

nvidia-smi

to see if the Nvidia GPU card information can be displayed. To
download the Nvidia CUDA Toolkit, please go to

https://developer.nvidia.com/cuda-toolkit


## Registration
To register an account:
1. copy your ABEL wallet address into ``abelmine.address``. If you do
   not have an ABEL wallet address, create one using the Abelian
   Desktop wallet which is available at https://www.abelian.info/downloads

2. use the following command

``` shell
./abelminer -U -P stratums://RegisteringAccountAbelMine:password@poolhost:27778
```

where the user needs to choose a ``password`` and specify the
``poolhost`` for the pool.

**Note:** A cert with name ``poolhost.cert`` must exist in
folder ``poolcerts``.

With such a command, abelminer will receive a username and directly
begin mining.

**Note:** The address and username will be written in a file,
``poolhost.abelmine.account``. 

This is one-off for each mining pool server. Namely, we need to register
once only for the pool server called Charlie, and we also need to register
once only for the other pool server called Dior if we want to use both
mining pools.

Each time this command can register only one ABEL wallet address, 
and if a user wants to register multiple addresses, he has to run
this command multiple times, and all the addresses and usernames
are stored in account files for the corresponding pool host.

Example:

``` shell
./abelminer -U -P stratums://RegisteringAccountAbelMine:MYPASSWORD_999@gpool-service-dior.abelian.info:27778
```


## Mine
While the above **registration** command registers and then mine, 
a user may stop **abelminer** and restart it later with a registered
address for some reason. For such a case, the user needs to type the
following to restart the mining.

``` shell
./abelminer -U -P stratums://username:password@poolhost:27778
```
**Note:** The registered username can be found in the account file
for the pool, say, ``poolhost.abelmine.account``, which is created
during the registration.

Example:

``` shell
./abelminer -U -P stratums://37e4128a053816f159acae13f363807ad06b1b56a50521672ce736ee3cd7e2a3:MYPASSWORD_999@gpool-service-dior.abelian.info:27778
```


## Multiple Pools
**abelminer** allows a user to specify multiple pools so that
once a connected pool disconnects, **abelminer** can switch to
the next one automatically.

``` shell
./abelminer -U -P stratums://RegisteringAccountAbelMine:password1@poolhost1:27778 -P stratums://RegisteringAccountAbelMine:password2@poolhost2:27778
```

``` shell
./abelminer -U -P stratums://username1:password1@poolhost1:27778 -P stratums://username2:password2@poolhost2:27778
```

## Mine by Getwork 
From v2.0.2, **abelminer** supports solo mining by **getwork**, which is supported by **abec-v0.11.9** and later versions.
The mine command is as below:
``` shell
./abelminer -P http://abec-host:port
```
where **abec-host** needs to enable the **getwork** supporting option, and the port is the specified port for supporting **getwork** solo mining.
We refer to the specification of **abec** for the configuration of supporting **getwork**.
Please note that on **abelminer**'s side, the above **getwork**-mining command does not need user or password, 
and it works only as an external miner of the connected **abec-host**.

