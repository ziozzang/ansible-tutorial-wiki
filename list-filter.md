[戻る](ansible-note)

# リスト型変数に対するフィルター

これが使えるのは 1.4 以降

### list1 内の重複を除く
```
{{ list1 |unique }}
```

### list1 と list2 の和
```
{{ list1 | union(list2) }}
```

### list1 と list2 の両方に存在するもの
```
{{ list1 |intersect(list2)}}
```

### list1 にあるけど list2 に無いもの
```
{{ list1 |difference(list2)}}
```

### list1 と list2 のどちらかにしか無いもの
```
{{ list1 |symmetric_difference(list2)}}
```

