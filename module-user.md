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



