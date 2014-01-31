[戻る](ansible-note)

# あるグループのメンバーだけに適用する

## テンプレートファイルの中

```
{% if 'webserver' in group_names %}
   # some part of a configuration file that only applies to webservers
{% endif %}
```

## role の when 句

```
when: ansible_hostname in some_group_name
```

ただし、 `ansible.cfg` で `error_on_undefined_vars` が `False` になっていない（デフォルト）場合、そのグループが未定義の場合にエラーとなります。
