[戻る](ansible-note)

# yum モジュール (yum でのパッケージ管理)

parameter | default | choices | comments
----------|---------|---------|----------
conf_file | | | 対象ホストで /etc/yum.conf 以外を使う場合に指定
disable_gpg_check | no | yes / no | パッケージのシグネチャチェックを無効にする
disablerepo | | | 実行時に無効にしたいリポジトリを指定する。カンマ区切りで複数指定可能
enablerepo | | | デフォルトで無効にしているが実行時に有効にしたいリポジトリを指定する。カンマ区切りで複数指定可能
list | | | ansible-playbook ではなく ansible コマンド用。冪等でない。例を見よと書いてあるが例に載ってない...
**name*** | | | パッケージ名 state=latest で name=* の場合は yum -y update を意味する。rpm ファイルを指定することも可能
state | present | present / latest / absent | present はインストールされていること、最新は求めない。lastest は最新に更新する。absent はインストールされていない状態にする (installed も使える)

**太字*** は必須

### 例

```
- yum: name=httpd state=latest
- yum: name=httpd state=removed
- yum: name=httpd enablerepo=testing state=installed
- yum: name=* state=latest
- yum: name=http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm state=present
- yum: name=/usr/local/src/nginx-release-centos-6-0.el6.ngx.noarch.rpm state=present
- yum: name="@Development tools" state=present
```



