[돌아가기](ansible-note)

## SSH Gateway를 통해 대상 서버에 연결되는 Playbook을 적용

연결에 paramiko 대신 ssh를 사용하도록 -c ssh 옵션을 지정합니다. 또한 ProxyCommand을 설정하기 위해 ssh_config 파일을 ssh의 -F 옵션에서 지정하는 ANSIBLE_SSH_ARGS 환경 변수를 설정합니다.

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
