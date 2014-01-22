[戻る](ansible-note)

# lineinfile モジュール (ファイルの行を編集)

デフォルトの config ファイルなどを置換で変換する用途に使うと便利です。 `insertafter`, `insertbefore` を使うことでコメントアウトされてるかもしれないファイルをうまく扱うことができるます。

しかし、同じファイルに対して `backup=yes` な `lineinfile` タスクを複数定義してもバックアップファイルの `timestamp` は分の精度であるためか、最後の変更のバックアップしか残らない

parameter | default | choices | comments
----------|---------|---------|---------
backrefs | no | yes / no | `state=present` とともに使います。 セットされている場合 `backreferences` (ポジションと名前付きの両方) を使うことができます。このフラグはモジュールの動作を変えます。`insertbefore` と `insertafter` は無視されます。正規表現がどこにもマッチしない場合、ファイルは更新されません。複数行にマッチした場合、最後にマッチした行が置換されます
backup | no | yes / no | タイムスタンプを含むファイル名でバックアップファイルを作成します
create | no | yes / no | `state=present` とともに使います。`yes` の場合、ファイルが存在しない場合に作成します。デフォルトではファイルが存在しない場合はエラーとなります
**dest*** | | | 編集するファイルのパス
insertafter | | EOF / *regex* | `state=present` とともに使います。 `regexp` にマッチすればその行を置換するが、マッチしなかった場合にこの値にマッチした行の次の行として `line` を挿入します。 `EOF` という値は特別で、ファイル末尾に挿入されます。`backrefs` を有効にするとこのオプションは無視されます
insertbefore | | BOF / *regex* | `insertafter` とほぼ同じ動作ですが、次の行ではなく前の行として挿入されます
line | | | `state=present` では必須。ファイルに挿入、置換する行。`backrefs=yes` の場合、正規表現の `backreference` が使える。\1, \2 や \g&lt;name&gt;
regexp | | | 対象の行を探す正規表現を指定します。`state=present` では行を置換します。複数行にマッチする場合最後にマッチした行が置換されます。`state=absent` の場合はマッチした行が削除されます。Python の正規表現を確認してください http://docs.python.org/2/library/re.html
state | present | present / absent | `absent` の場合は `regexp` にマッチする行を削除します。`present` の場合は他のオプションによってさまざまな動作をします
validate | None | | ファイルを入れ替える前に任意のコマンドを実行してファイルの syntax チェックなどを行います (1.4 で追加されました)
その他 | | | file モジュールで指定可能なものすべてが使えます

単にとある1行を追加したいだけの場合はこれだけでOK
```yml
- lineinfile: dest=/etc/snmp/snmpd.conf line='dontLogTCPWrappersConnects yes'
```

## 例

```yml
- lineinfile: dest=/etc/selinux/config regexp=^SELINUX= line=SELINUX=disabled

- lineinfile: dest=/etc/sudoers state=absent regexp="^%wheel"

- lineinfile: dest=/etc/hosts regexp='^127\.0\.0\.1' line='127.0.0.1 localhost' owner=root group=root mode=0644

- lineinfile: dest=/etc/httpd/conf/httpd.conf regexp="^Listen " insertafter="^#Listen " line="Listen 8080"

- lineinfile: dest=/etc/services regexp="^# port for http" insertbefore="^www.*80/tcp" line="# port for http by default"

- lineinfile: dest=/etc/sudoers state=present regexp='^%wheel' line='%wheel ALL=(ALL) NOPASSWD: ALL'

# オリジナルのドキュメントにはこう書いてあるんだけど間違ってる？
- lineinfile: dest=/opt/jboss-as/bin/standalone.conf regexp='^(.*)Xms(\d+)m(.*)$' line='\1Xms${xms}m\3' backrefs=yes

# これが正解？
- lineinfile: dest=/opt/jboss-as/bin/standalone.conf regexp='^(.*)Xms(?P<xms>\d+)m(.*)$' line='\1Xms\g<xms>m\3' backrefs=yes

# Validate a the sudoers file before saving
- lineinfile: dest=/etc/sudoers state=present regexp='^%ADMIN ALL\=' line='%ADMIN ALL=(ALL) NOPASSWD:ALL' validate='visudo -cf %s'
```
