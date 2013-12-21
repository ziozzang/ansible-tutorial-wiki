# 結果を変数に保存して利用する

`register` を使って task の結果、出力を変数に登録し、後の task でその値を利用することができます

```
- name: test play
  hosts: all
  tasks:
      - shell: cat /etc/motd
        register: motd_contents
      - shell: echo "motd contains the word hi"
        when: motd_contents.stdout.find('hi') != -1
```

`cat /etc/motd` の結果が motd_contents に登録されます。上の例では /etc/motd に "hi" が含まれなかった場合にのみ2つ目の task が実行されます

task の出力をリストにして `with_items` で扱うことも可能です。行を単位にするなら stdout_lines が使えます。 stdout.split() で任意のデリミタでリストに分割することもできます

```
- name: registered variable usage as a with_items list
  hosts: all
  tasks:
      - name: retrieve the list of home directories
        command: ls /home
        register: home_dirs
      - name: add home dirs to the backup spooler
        file: path=/mnt/bkspool/{{ item }} src=/home/{{ item }} state=link
        with_items: home_dirs.stdout_lines
        # with_items: home_dirs.stdout.split()
```

`register` で登録されるデータは `debug` モジュールを使うことで確認できます。 `debug` モジュールの出力を有効にするには `-v` オプションをつけて実行する必要があります

```
      - debug: msg="{{ motd_contents }}"
```

これを実行すると次のように表示されます

```
TASK: [debug msg="{{motd_contents}}"] ***************************************** 
ok: [192.168.33.12] => {"msg": "{u'changed': True, u'end': u'2013-08-18 15:12:18.808685', u'stdout': u'Welcome to your Vagrant-built virtual machine.', u'cmd': u'cat /etc/motd ', u'start': u'2013-08-18 15:12:18.803476', u'delta': u'0:00:00.005209', u'stderr': u'', u'rc': 0, 'invocation': {'module_name': 'shell', 'module_args': 'cat /etc/motd'}, 'stdout_lines': [u'Welcome to your Vagrant-built virtual machine.']}"}
```

長いので整形してみます

```python
u'changed': True,
u'end': u'2013-08-18 15:12:18.808685',
u'stdout': u'Welcome to your Vagrant-built virtual machine.',
u'cmd': u'cat /etc/motd ',
u'start': u'2013-08-18 15:12:18.803476',
u'delta': u'0:00:00.005209',
u'stderr': u'',
u'rc': 0,
'invocation': {
  'module_name': 'shell',
  'module_args': 'cat /etc/motd'
},
'stdout_lines': [u'Welcome to your Vagrant-built virtual machine.']
```

skip した場合

```python
u'skipped': True,
u'stdout': u'skipped, since /etc/motd exists',
u'cmd': u'cat /etc/motd ',
u'rc': 0,
u'stderr': False,
u'changed': False,
'invocation': {
  'module_name': 'shell',
  'module_args': 'cat /etc/motd creates=/etc/motd'
},
'stdout_lines': [u'skipped, since /etc/motd exists']
```

もっと手軽に確認したい場合は `debug` モジュールなしに `-v` をつけて実行することでもだいたい確認することができます

```
TASK: [shell cat /etc/motd] *************************************************** 
changed: [192.168.33.12] => {"changed": true, "cmd": "cat /etc/motd ", "delta": "0:00:00.005462", "end": "2013-08-18 13:27:43.277139", "rc": 0, "start": "2013-08-18 13:27:43.271677", "stderr": "", "stdout": "Welcome to your Vagrant-built virtual machine."}
```

これも長いので整形してみましょう

```json
{
  "changed": true,
  "cmd": "cat /etc/motd ",
  "delta": "0:00:00.005462",
  "end": "2013-08-18 13:27:43.277139",
  "rc": 0,
  "start": "2013-08-18 13:27:43.271677",
  "stderr": "",
  "stdout": "Welcome to your Vagrant-built virtual machine."
}
```

skip した場合は次のような文字列が stdout に入っていました

```
skipped, since /etc/motd exists
```

そして、実は debug モジュールを使えば中身が見れるのでした