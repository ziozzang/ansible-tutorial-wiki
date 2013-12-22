[戻る](ansible-note)

# エラーを無視する

通常、task でエラーが発生するとそのホストに対してはそれ以降の処理を行いませんが、エラーになっても処理を続けたい場合にはその task に

```
ignore_errors: yes
```

を設定することで実現できます。

[Ignoring Failed Commands](http://www.ansibleworks.com/docs/playbooks_error_handling.html#id4)

