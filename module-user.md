[戻る](ansible-note)

# user (ユーザーアカウントの管理)

ユーザーアカウントの管理をするモジュールです

parameter | default | choices | comments
----------|---------|---------|----------
append | no | yes / no | `yes` の場合、 `groups` への追加だけを行う。既存のグループから外れない
comment | | | アカウントのコメント (GECOS) を指定しる
createhome | yes | yes / no | `no` にしない場合はアカウント作成後にホームディレクトリを作成する
force | no | yes / no | `state=absent` の場合、 `userdel --force` として処理される
generate_ssh_key | no | yes / no | SSH key を作成するかどうか。既に存在する場合には上書きしません
group | | | ユーザーのプライマリグループをグループ名で指定する
groups | | | カンマ区切りのグループリストにユーザーを追加する。 `groups=` と、空文字列をしていするとプライマリグループ以外から削除します
home | | | ホームディレクトリの path を指定する
login_class | | | FreeBSD, OpenBSD, NetBSD 用の login class を指定する
**name*** | | | 操作対象のユーザー名を指定
non_unique | no | yes / no | ユニークでない uid を許可するかどうか
password | no | yes / no | ハッシュ化された文字列を指定することでパスワードを設定する
remove | no | yes / no | `state=absent` と同時に指定することで `userdel --remove` となり、ホームディレクトリも削除される
shell | | | ログインシェルを指定する
ssh_key_bits | 2048 | | 作成する SSH key の bit 数を指定する
ssh_key_comment | ansible-generated | | SSH key のコメントを指定する
ssh_key_file | $HOME/.ssh/id_rsa | | SSH key ファイルの path を指定する
ssh_key_passphrase | | | 作成する SSH key ファイルのパスフレーズ、指定しない場合はパスフレーズなしの key が作成される
ssh_key_type | rsa | | SSH key の暗号アルゴリズムを指定する、利用可能なものはそのホストの環境に依存する
state | present | present / absent | `absent` でユーザーを削除する
system | no | yes / no | システムアカウントとして作成する。既存のアカウントの設定を変更することはできない
uid | | | uid を指定する
update_password | always | always / on_create | パスワードの設定を常に行うか、作成時にのみ行うかを指定する (1.3 で追加された)

**太字*** は必須

`useradd`, `userdel`, `usermod` コマンドが必要

### 例

```
# 'johnd' という名前のユーザーを uid 指定で 'admin' グループで作成する
- user: name=johnd comment="John Doe" uid=1040 group=admin

# 'johnd' ユーザーを削除する、ホームディレクトリも削除する
- user: name=johnd state=absent remove=yes

# jsmith ユーザーを作成する、SSH key も作成する
- user: name=jsmith generate_ssh_key=yes ssh_key_bits=2048
```

パスワードなどは prompt を表示させて入力を変数にいれることでセキュリティを保つことができる。ハッシュ化には <a href="http://pythonhosted.org/passlib/">Passlib</a> モジュールが必要となる。CentOS 6 では `yum -y install python-passlib` で EPEL リポジトリがインストールできる

