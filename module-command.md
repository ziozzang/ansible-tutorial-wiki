# command モジュール (任意のコマンドを実行する)

`command` モジュールはスペース区切りの引数とともにコマンドを対象のサーバー上で実行します。ただし、このコマンドは shell に渡されるわけではないため "<", ">", "|", "&" や $HOME などの変数を使うことはできません。また、path は絶対パスで指定する必要があります。

pipe や redirect が必要な場合は `shell` モジュールを使います。

parameter | default | choices | comments
----------|---------|---------|----------
chdir | | | コマンドを特定のディレクトリで実行する必要がある場合に指定します (make とか rake とか)
creates | | | このコマンドの実行結果として、作成されるファイルの path を指定します。ファイルが存在する場合は実行済みとしてコマンドを実行しません
executable | | | subprocess.Popen の executable オプション
removes | | | このコマンドの実行結果として、削除されるファイルの path を指定します。ファイルが存在しない場合は実行済みとしてコマンドを実行しません
**実行するコマンド*** | | | 実行するコマンドをスペース区切りの引数付きで指定します

**太字*** は必須

`chdir`, `creates`, `removes` はコマンドの後ろに定義します。

### 例

```
# Example from Ansible Playbooks
- command: /sbin/shutdown -t now

# 指定したファイルが存在しなかった場合にのみコマンドを実行する
- command: /usr/bin/make_database.sh arg1 arg2 creates=/path/to/database
```
