# Bootnodes setup via Ansible


## Secret management

You'll need a [Keybase](https://keybase.io/) account and access to the `ethereum.devops.bootnodes` subteam under the `ethereum.devops` team. You can ask in the @Devops Discord room for access.

Once you've got access to the subteam, you'll need to have the [KeybaseFS](https://keybase.io/docs/kbfs) running on your machine.
Make sure that you can run `keybase fs ls /keybase/team/ethereum.devops.bootnodes/`


## First run

Make sure to run the `./install_dependencies.sh` script to make sure that you download all required ansible collections and roles.

If a machine has never been provisioned, then you should use the DevOps SSH key to establish the connection for the first time.
You can do this by appending `--private-key ~/.ssh/id_rsa_devops` to your ansible commands.

## Useful commands

Perform a quick connectivity test

```bash
$ ansible all -m ping
```

Executing the whole playbook

```bash
$ ansible-playbook playbook.yaml
```

Executing the playbook on a single target (Useful for rolling updates)

```bash
$ ansible-playbook playbook.yaml -l bootnode-aws-us-east-1-001
```

Executing parts of the playbook by using tags. e.g. Run the datadog agent role.
You can have a look at the playbook for more tags.

```bash
$ ansible-playbook playbook.yaml -t ethereum_node
```

Using `geth attach` to list all enodes

```bash
$ ansible mainnet_geth -b -m shell -a "docker exec geth geth --datadir /data attach --exec admin.nodeInfo | grep enode"
```

Same method to check the versions:
```bash
$ ansible mainnet_geth -b -m shell -a "docker exec geth geth --datadir /data attach --exec web3.version.node"
```
