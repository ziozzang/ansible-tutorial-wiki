# 特定のグループに入っている場合にのみ実行する

通常、この目的では playbook の `hosts` でグループを指定しますが、レイヤーの違う複数のグループに所属している場合に困ります。
グループAのサーバーでかつグループBにも入っているサーバーに対してのみ実行したい場合とか、とある role で環境(本番・テスト)によって別の処理をさせたい場合など。

```
- hosts: group-a
  tasks:
    - name: ...
      action: ...
      when: ansible_hostname in group['group-b']
```
