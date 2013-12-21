# エラーとする条件を指定する

デフォルトではコマンド実行時には exit code が 0 であれば成功(changed)として扱われます。でも、コマンドが常に 0 で終了してしまうけど xxx が出力されてたらエラーとして扱いたいなんていう場合があるかと思います。そんな時に使えるのが `failed_when` です。 (1.4 で追加されました)

次の例では標準エラー出力に FAILED という文字列が含まれる場合にエラーとします。

```
- name: this command prints FAILED when it fails
  command: /usr/bin/example-command -x -y -z
  register: command_result
  failed_when: "'FAILED' in command_result.stderr"
```

`failed_when` に対応していない古いバージョンでは次のように書く必要があります。

```
# 0 で終了していなくてもエラーとせず、出力を変数に登録
- name: this command prints FAILED when it fails
  command: /usr/bin/example-command -x -y -z
  register: command_result
  ignore_errors: True

# 前のコマンドの出力に FAILED が見つかったらエラーで終了させる
- name: fail the play if the previous command did not succeed
  fail: msg="the command failed"
  when: "'FAILED' in command_result.stderr"
```

[Controlling What Defines Failure](http://www.ansibleworks.com/docs/playbooks_error_handling.html#id5)
