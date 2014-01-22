[戻る](ansible-note)

# git モジュール (ファイル・ディレクトリ操作)

git の clone や pull を行い、コードを最新に保ちます。

parameter | default | choices | comments
----------|---------|---------|----------
accept_hostkey | no | yes / no | ssh host key を受け入れるかどうか。初めてアクセスするサーバーの場合。(1.5で追加されました)
bare | no | yes / no | yes にすると bare repository を作成します。no の場合は workspace を持つ通常の repository となります
depth | | num | 履歴を指定の数に削った clone を作成します。指定可能な最小値は 1 です (1.2で追加されました)
**dest*** | | path | clone 先ディレクトリをしていする
executable | | path | git コマンドの path を指定します。PATH に入っていない場所のコマンドを使う場合、もしくはコマンド名が git でない場合に使います。(1.4で追加されました)
force | no | yes / no | yes にした場合、ローカルの変更は破棄されます。(0.7で追加されました。0.7までは常に yes でした)
reference | | | リファレンスリポジトリ (see "git clone --reference ...") (1.4で追加されました)
remote | no | origin | remote name
**repo*** | | | git, SSH, HTTP(s) プロトコルのリポジトリURI
update | yes | yes / no | yes の場合 remote リポジトリを使って更新します。no の場合はそのまま残します。(1.2で追加されました。1.2までは常に yes でした)
version | HEAD | hash値 / HEAD / tag名 / branch名 | チェックアウトする対象

**太字*** は必須

### 例
```yml
# Example git checkout from Ansible Playbooks
- git: repo=git://foosball.example.org/path/to/repo.git
       dest=/srv/checkout
       version=release-0.22

# Example read-write git checkout from github
- git: repo=ssh://git@github.com/mylogin/hello.git dest=/home/mylogin/hello

# Example just ensuring the repo checkout exists
- git: repo=git://foosball.example.org/path/to/repo.git dest=/srv/checkout update=no
```

リポジトリが SSH の場合、ターゲットホストの known_hosts にホストキーが登録されていない場合、プロンプトが表示されます。事前に /etc/ssh/ssh_known_hosts に追加しておくことでこれを回避できます。バージョン 1.5 からは accept_hostkey が使える？


