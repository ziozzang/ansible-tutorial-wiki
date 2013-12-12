# インベントリフィアル

Ansible では制御対象のサーバーのリストをインベントリファイルに書く必要があります。コマンドラインオプション(`-i`)で指定しない場合のデフォルトファイルは `/etc/ansible/hosts` です。この path は `ansible.cfg` ファイルにて設定可能です。
ansible.cfg はコマンド実行のカレントディレクトリ、環境変数の `ANSIBLE_CONFIG` 、`~/ansible.cfg` 、`/etc/ansible/ansible.cfg` の順に検索されます。

Best Practices のドキュメントには test, staging, production などによってインベントリファイルを使い分けるように書いてあります。

## グルーピング

インベントリファイルには対象ホストのホスト名もしくはIPアドレスを列挙します。 グルーピングすることができ、playbook の `hosts` 設定で対象を特定のグループに絞ったり、そのグループに属しているサーバーにのみ適用されるグループ変数を使うことができます。

グルーピングの例 ([Hosts and Groups](http://www.ansibleworks.com/docs/patterns.html#id2))
```ini
  [app-servers]
  app01
  app02
  app03
  
  [db-servers]
  db01
  db02
  db03
```

連番のサーバー名であれば次の様に書くこともできます
```ini
[webservers]
www[01:50].example.com

[databases]
db-[a:f].example.com
```

1つのホストが複数のグループに属すことも可能です

`&` や `!` などで複雑な指定も可能です ([Selecting Targets](http://www.ansibleworks.com/docs/patterns.html#id4))

## ホスト変数

インベントリファイルではホスト名、IPアドレスの後ろにそのサーバー用の変数を任意に複数指定できます

```
server1  listen_port=80 relay_server=relay1
server2 listen_port=81 relay_server=relay2
```

予約変数名
SSH の項目で説明しますが、SSH 関連で予約されている変数名があります

* ansible_ssh_host
  * あまり必要な場面がなさそうですが、イベントリのホスト名とSSH接続用のホスト名を分けたい場合に指定
* ansible_ssh_port
  * SSHポートが他と違う場合に指定する
* ansible_ssh_user
  * SSHのユーザー名が他と違う場合に指定する
* ansible_ssh_pass
  * SSHでパスワード認証する際のパスワードを指定
* ansible_connection
  * 対象サーバーへの接続方法 (local, ssh, paramiko)、デフォルトは paramiko
* ansible_ssh_private_key_file
  * SSHの秘密鍵が他と違う場合に指定
* ansible_syslog_facility
  * 対象サーバーで出力する syslog の facility
* ansible_python_interpreter
  * 対象サーバーでの Python の path を指定する。/usr/bin/python 以外を使いたい場合などに使う。/usr/bin/python が古い場合とか
* ansible_*_interpreter
  * 対象サーバーでの ruby とか perl の path を指定
