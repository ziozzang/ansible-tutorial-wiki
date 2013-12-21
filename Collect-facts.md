# サーバーの情報(fact)を集める

[サーバーの情報を利用する (GATHERING FACTS)](gathering-facts) で得られる情報は全サーバーから収集できると便利ですよね。ansible コマンドで簡単に収集することができます。

```
$ ansible -s -m setup -i hosts -t /tmp/facts all
```

このコマンドで /tmp/facts フォルダにホスト毎のファイルとして結果が出力されます。-s は sudo を使うというオプションで、これは無しでも実行できますが、root でないと取得できない情報もあるので指定します。

「[Ansible の fatcs (インベントリ情報) を MongoDB に突っ込む](http://blog.1q77.com/2013/10/ansible-fatcs/)」なんてこともできます。

