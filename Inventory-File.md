Ansible では制御対象のサーバーのリストをインベントリファイルに書く必要があります。コマンドラインオプション(`-i`)で指定しない場合のデフォルトファイルは `/etc/ansible/hosts` です。この path は `ansible.cfg` ファイルにて設定可能です。
ansible.cfg はコマンド実行のカレントディレクトリ、環境変数の `ANSIBLE_CONFIG` 、`~/ansible.cfg` 、`/etc/ansible/ansible.cfg` の順に検索されます。

Best Practices のドキュメントには test, staging, production などによってインベントリファイルを使い分けるように書いてあります。
