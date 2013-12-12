# file モジュール (ファイル・ディレクトリ操作)

ファイル、シンボリックリンク、ディレクトリの所有者やモードの設定、削除削除を行うモジュールです。 他の多くのモジュールが同じオプションをサポートしています copy, template, assemble など

parameter | default | choices | comments
----------|---------|---------|----------
force | no | yes / no | yes にすると2つのケースでシンボリックリンクを強制的に作成します。1) リンク元ファイルが存在しない場合 2) リンク先にファイルが存在する場合(unlink 後にリンクを作成します)
group | | | グループ (chown で使うもの)
mode | | | モード (chmod で使うもの)
owner | | | ファイルの所有者 (chown で使うもの)
**path*** | | | ファイルやディレクトリのpath、`state=link` の場合は `src` に対するリンク先を指定します
recurse | no | yes / no | `state=directory` の場合に attribute 設定を再帰的に行うかどうか
selevel | s0 | | SELinux の設定（石川さんごめんなさい） level part of the SELinux file context. This is the MLS/MCS attribute, sometimes known as the `range`. `_default` feature works as for seuser
serole | | | role part of SELinux file context, `_default` feature works as for seuser
setype | | | type part of SELinux file context, `_default` feature works as for seuser
seuser | | | user part of SELinux file context. Will default to system policy, if applicable. If set to `_default`, it will use the `user` portion of the policy if available
src | | | シンボリックリンクのリンク元path
state | file | file / link / directory / hard / absent | `directory` の場合、`mkdir -p` のように途中の directory も作成します。`absent` の場合、directory は再帰的に削除され、ファイルやリンクは unlink されます
**太字*** は必須

### 例
```yml
- file: path=/etc/foo.conf owner=foo group=foo mode=0644
- file: src=/file/to/link/to dest=/path/to/symlink owner=foo group=foo state=link
```