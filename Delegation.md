# 委譲 (task を別のホストで実行する)

例えば deploy の前にロードバランサーから外し、終わったらまた戻すという処理を行う場合 `delegate_to` を使ってその task をロードバランサーで実行させることができます。 Ansible には BIG-IP や NetScaler のモジュールがあります。

```
- hosts: webservers
  serial: 5
  tasks:
  - name: take out of load balancer pool
    command: /usr/bin/take_out_of_pool {{ inventory_hostname }}
    delegate_to: 127.0.0.1
  - name: actual steps would go here
    yum: name=acme-web-stack state=latest
  - name: add back to load balancer pool
    command: /usr/bin/add_back_to_pool {{ inventory_hostname }}
    delegate_to: 127.0.0.1
```

この例ではロードバランサーの処理を 127.0.0.1 で実行します。これは Ansible の実行ホストです。この場合 `local_action` を使って次のように書くこともできます。

```
# ...
  tasks:
  - name: take out of load balancer pool
    local_action: command /usr/bin/take_out_of_pool {{ inventory_hostname }}
# ...
  - name: add back to load balancer pool
    local_action: command /usr/bin/add_back_to_pool {{ inventory_hostname }}
```

`local_action` を使うことで file モジュールではできないディレクトリごとファイルをコピーする処理を次のように書くこともできます。

```
# ...
  tasks:
  - name: recursively copy files from management server to target
    local_action: command rsync -a /path/to/files {{ inventory_hostname }}:/path/to/target/
```
