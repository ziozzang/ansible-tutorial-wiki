# fetch モジュール (ファイルを収集する)

[copy モジュール](module-copy)と似た動作をしますが、これは push ではなく pull となります。コピー元が存在しない場合をエラーとするには `fail_on_missing` を `yes` にする必要があります。 管理対象サーバーからファイルを収集したい場合に利用します

parameter | default | choices | comments
----------|---------|---------|---------
**dest*** | | | ファイルの保存先を指定します。対象ホストが `host.example.com` で `dest` が `/backup` で、`src` が `/etc/profile` の場合、`/backup/host.example.com/etc/profile` に保存されます
fail_on_missing | no | yes / no | コピー元ファイルが存在しかなった場合を失敗として扱います (1.1 で追加されました)
flat | | | `hostname/path/to/file` というデフォルトの保存先の上書きを許可します。`dest` が '/' で終わる場合は `basename` をファイル名としてそのディレクトリに保存します (1.2 で追加されました)
src | | | fetch するファイルの対象ホスト上の path を指定します。ディレクトリには対応していません。再帰的なコピーは今後のリリースで対応予定です
validate_md5 | yes | yes / no | fetch 後に md5sum を比較します (1.4 で追加されました)

**太字*** は必須


## 例

```yml
# Store file into /tmp/fetched/host.example.com/tmp/somefile
- fetch: src=/tmp/somefile dest=/tmp/fetched

# Specifying a path directly
- fetch: src=/tmp/somefile dest=/tmp/prefix-{{ ansible_hostname }} flat=yes

# Specifying a destination path
- fetch: src=/tmp/uniquefile dest=/tmp/special/ flat=yes

# Storing in a path relative to the playbook
- fetch: src=/tmp/uniquefile dest=special/prefix-{{ ansible_hostname }} flat=yes
```
