[戻る](ansible-note)

# パス(path)への便利フィルター

### basename （パスからファイル名部分を取り出す）
```
{{ path | basename }}
```

### dirname （パスからディレクトリ部分を取り出す）
```
{{ path | dirname }}
```

### Base64 encode/decode （パス関係ない...）
```
{{ encoded | b64decode }}
{{ decoded | b64encode }}
```

### md5sum （これもパス関係ない...）
```
{{ filename | md5 }}
```
