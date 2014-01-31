[戻る](ansible-note)

# あるグループのメンバーだけに適用する

## テンプレートファイルの中

```
{% if 'webserver' in group_names %}
   # 所属しているグループ名のリストに 'webserver' が含まれている場合の処理
{% endif %}
```

```
{% if ansible_hostname in some_group_name %}
  # some_group_name に当該ホストが属している場合の処理
{% endif %}
```

## role の when 句

```
when: 'webserver' in group_names
```

```
when: ansible_hostname in some_group_name
```

後者の場合、 `ansible.cfg` で `error_on_undefined_vars` が `False` になっていない（デフォルト）場合、そのグループが未定義の場合にエラーとなります。
