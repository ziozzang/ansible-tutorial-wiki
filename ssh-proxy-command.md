[戻る](ansible-note)

## SSH Gateway 越しに対象サーバーに接続して Playbook を適用する

接続に paramiko ではなく、ssh を使うように `-c ssh` オプションを指定します。
また、ProxyCommand を設定するために ssh_config ファイルを ssh の `-F` オプションで指定するために ANSIBLE_SSH_ARGS 環境変数を設定します。

```
$ cat ssh_config
User ec2-user
IdentityFile ~/.ssh/id_rsa_aws
ProxyCommand ssh -W %h:%p -l ec2-user -i ~/.ssh/id_rsa_aws gateway-server
```

```
#!/bin/bash

export ANSIBLE_SSH_ARGS="-F ssh_config"
exec ansible-playbook -c ssh $*
```
