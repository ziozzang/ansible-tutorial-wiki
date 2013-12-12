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