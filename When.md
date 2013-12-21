# 条件付き実行

`task` に `when` で条件を指定し、それを満たす場合にのみ実行させることができます。
次の例では Debian でのみコマンドを実行します。この変数 `ansible_os_family` は [GATHERING FACTS](gathering-facts) で得られるものです。

```
tasks:
  - name: "shutdown Debian flavored systems"
    command: /sbin/shutdown -t now
    when: ansible_os_family == "Debian"
```

```
tasks:
  - shell: echo "only on Red Hat 6, derivatives, and later"
    when: ansible_os_family == "RedHat" and ansible_lsb.major_release|int >= 6
```

`ansible-playbook` 実行時に `-e nmae=value` で指定した変数によって動作を変えることができます。

```
# is_hogehoge 変数に何か指定してある場合
  - command: hogehoge
    when: is_hogehoge is defined

# branch を指定して deploy
  - command: deploy-command {{branch}}
```

また、[ある task の結果を変数に入れて](register)おき、その値を使って条件を指定することができます。

```
tasks:
  - command: /bin/false
    register: result
    ignore_errors: True
  - command: /bin/something
    when: result|failed
  - command: /bin/something_else
    when: result|success
```

1番目の task は `/bin/false` なのでかならず失敗しますが、 `ignore_errors` によってエラーでも続行されます。 `register` で result という変数に task の結果が保存されます([結果を変数に保存して利用する](register) を参照)。以降の task で `when` を使ってその結果を条件として利用することができます。2番目の task は1番目が失敗した場合にのみ実行されます。3番目は1番目の task が成功した場合にのみ実行されます。 `register: 任意の名前` で結果を保存します。
([Conditional Execution](http://www.ansibleworks.com/docs/playbooks2.html#conditional-execution)) 

次の例は `/some/directory` が作成された場合にのみ、次の `commmand a` が実行されます。 `/some/directory` が既に存在していた場合は `changed` とならないので `command a` は実行されません。

```
  - file: state=directory path=/some/directory
    register: create_dir

  - command: command a
    when: create_dir.changed
```
