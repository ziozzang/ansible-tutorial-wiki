[戻る](ansible-note)

# copy モジュール

Ansible 実行サーバーからリモートサーバーにファイルをコピーするモジュールです。
このモジュールはディレクトリを再帰的にコピーすることができません。
(rsync コマンドを使う例が [delegation](http://www.ansibleworks.com/docs/playbooks2.html/#delegation) にあります)

```yml
# Playbook からの例
- copy: src=/srv/myfiles/foo.conf dest=/etc/foo.conf owner=foo group=foo mode=0644

# ntp.conf をコピーします。既に存在するファイルと差分がある場合は元のファイルをバックアップします
- copy: src=/mine/ntp.conf dest=/etc/ntp.conf owner=root group=root mode=644 backup=yes

# sudoers ファイルを dest の path にコピーする前に visudo コマンドでバリデーションを実行します
- copy: src=/mine/sudoers dest=/etc/sudoers validate='visudo -cf %s'
```

parameter | default | choices | comments
----------|---------|---------|---------
backup | no | yes / no | 既存ファイルと内容に差があった場合にバックアップ日時をファイル名に含むバックアップファイルを作成します
content | | | `src` の代わりに使用することで、ここに設定したデータがファイルの内容となります
**dest*** | | | コピー先の path
force | yes | yes / no | デフォルトは yes で、ファイルの内容に差があればコピーします。no の場合はファイルが存在すると上書きしません
src | | | コピーするファイルのpath。絶対pathでも相対pathでも可
validate | | | コピーする前に validation するコマンドを指定
その他 | | | [file モジュール](module-file) で指定可能なものすべてが使えます

**太字*** は必須