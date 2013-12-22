# pause モジュール (一時停止)

ポーズモジュールは task の実行後一定時間待つ必要がある場合などに使います。サーバー起動時の初期化に時間がかかるため、起動完了まで待つ場合など。 `minutes`, `seconds` で時間を指定した場合、指定時間経過で自動的に次の task へ進みます。そうでない場合は入力をずっと待ちます。時間を指定した場合もしなかった場合も待っている間に Ctrl-C を入力すると即座に次に進むか、中断してそれ以降の task の実行も行わないかの選択プロンプトが表示されます。

```
TASK: [pause test] ************************************************************ 
[servername]
Press enter to continue: ^C
Action? (a)bort/(c)ontinue:
```

parameter | default | choices | comments
----------|---------|---------|----------
minutes | | | 指定の分待ちます。経過後自動で先に進みます
prompt | | | 指定の文字列を表示して待ちます
seconds | | | 指定の秒待ちます。経過後自動で先に進みます

### 例

```
# アプリケーションのキャッシュ生成のため5分待つ
- pause: minutes=5

# アプリケーションが正しく更新されたことを確認するまで待つ。(何かを入力するまで待つ)
- pause:

# 更新後の確認事項のリマインダーとして役に立つ
- pause: prompt="Make sure org.foo.FooOverload exception is not present"
```
