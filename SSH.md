Ansible はデフォルトでは SSH 接続に Python の paramiko を使う(RHEL 6 の OpenSSH は古くて ControlPersist 機能がないため?)、このためか ~/.ssh/config を読んではくれない。標準の path の秘密鍵以外を使いたい場合や 22 番以外のポートを使いたい場合はインベントリファイルにホスト毎、グループ毎、全体の変数を設定する。 Version 1.2.1 からは OpenSSH が ControlPersist をサポートしている場合は ssh で、そうでない場合は paramiko となる smart がデフォルトとなるようです

```ini
[group-a]
server1 ansible_ssh_port=2222
server2 ansible_ssh_user=bob

[group-b]
server3
server4

[group-b:vars]
ansible_ssh_port=3333

[all:vars]
ansible_ssh_port=1234
```

秘密鍵だけはコマンドラインオプションで指定できます

```
$ ansible --private-key=/path/to/key_file
```

この変数の強度は「host > group > all > コマンドラインオプション」の順

