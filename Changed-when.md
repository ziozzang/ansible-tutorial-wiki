[戻る](ansible-note)

# 結果を changed とする条件を指定する

`shell`, `command` モジュールはコマンドが成功すれば常に changed として扱われます。しかし、実際には何も変更されていない場合、これはあまりうれしいことではありません。そこで使えるのが 1.3 で追加された `changed_when` です。

```
tasks:
  # exit code が 2 でなければ changed
  - shell: /usr/bin/billybass --mode="take me to the river"
    register: bass_result
    changed_when: "bass_result.rc != 2"

  # このタスクは change になりません
  - shell: wall 'beep'
    changed_when: False
```

[Overriding The Changed Result](http://www.ansibleworks.com/docs/playbooks_error_handling.html#id6)


Subversion で管理してる設定ファイルがあった場合に、 `svn update` で更新するわけですがこれが常に `changed` となるのは好ましくありません。
そこで `changed_when` の出番です。

```
- name: svn update
  command: svn update chdir=/some/where
  register: svn
  changed_when: "'Updated to' in svn.stdout"
```
