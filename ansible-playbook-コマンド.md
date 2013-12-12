## オプション

* -k, --ask-pass
  * SSH のパスワードを尋ねる(プロンプトが出る)
* -K, --ask-sudo-pass
  * sudo のパスワードを尋ねる(プロンプトが出る)
* -C, --check
  * インストールなどの変更は行わないが、条件の確認などは実行する
* -c CONNECTION, --connection=CONNECTION
  * local, ssh, paramiko から選択。デフォルトは paramiko。古い OpenSSH で ssh を指定する場合は ANSIBLE_SSH_ARGS="" と環境変数を空で上書きする必要がある
* -D, --diff
  * file や template の差分(diff)を表示する。--check と一緒に使うと便利
* -e EXTRA_VARS, --extra-vars=EXTRA_VARS
  * 追加の変数を key=value で指定する。playbook に書かれている変数の上書きはされない
* -f FORKS, --forks=FORKS
  * 並列実行する数(デフォルトは5)
* -h, --help
  * このヘルプメッセージを表示して終了する
* -i INVENTORY, --inventory-file=INVENTORY
  * インベントリファイルを指定する(デフォルトは /etc/ansible/hosts)
* -l SUBNET, --limit=SUBNET
  * 対象サーバーを指定のものだけに制限する
* --list-hosts
  * それぞれの playbook の対象ホスト一覧を表示して終了する。playbook の実行はされない
* --list-tasks
  * 各 playbook のタスク一覧を表示して終了する
* -M MODULE_PATH, --module-path=MODULE_PATH
  * モジュールファイルのディレクトリを指定する(デフォルトは /usr/share/ansible)
* --private-key=PRIVATE_KEY_FILE
  * SSH の秘密鍵ファイルを指定する
* --start-at-task=START_AT
  * 指定の task から開始する
* --step
  * ひとつの task ごとに "Perform task: タスク名 (y/n/c):" と確認される。y: (yes) 実行する、n: (no) 実行しない、c: (continue) 以降を確認なしで実行する
* -s, --sudo
  * 対象サーバーでの task を sudo で実行する
* -U SUDO_USER, --sudo-user=SUDO_USER
  * sudo での実行ユーザーを指定する(デフォルトは root)
* --syntax-check
  * playbook の文法チェックだけを行う
* -t TAGS, --tags=TAGS
  * 指定の tag が付けられた task のみを実行する
* -T TIMEOUT, --timeout=TIMEOUT
  * SSH のタイムアウトを指定する(デフォルトは10秒)
* -u REMOTE_USER, --user=REMOTE_USER
  * SSH で接続するユーザー名を指定する
* -v, --verbose
  * 冗長モード (-vvv でより冗長な出力になる)
* --version
  * バージョンを表示して終了する
