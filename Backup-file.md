[戻る](ansible-note)

# Backup File

`copy`, `template`, `lineinfile` などに `backup` オプションがある。これは更新対象のファイル(path)に日時(%Y-%m-%d@%H:%M~)サフィックスをつけてバックアップとして保存します。変更の必要がない場合はバックアップファイルも作成されません。

当該部分のコードは `ansible/module_common.py` にある

```python
    def backup_local(self, fn):
        '''make a date-marked backup of the specified file, return True or False on success or failure'''
        # backups named basename-YYYY-MM-DD@HH:MM~
        ext = time.strftime("%Y-%m-%d@%H:%M~", time.localtime(time.time()))
        backupdest = '%s.%s' % (fn, ext)

        try:
            shutil.copy2(fn, backupdest)
        except shutil.Error, e:
            self.fail_json(msg='Could not make backup of %s to %s: %s' % (fn, backupdest, e))
        return backupdest
```

分の精度の日時だけでのバックアップファイル名を生成するため、一度の playbook 適用内で同一ファイルを複数回更新する処理を行なっても最後の変更分しか残らないので注意が必要。たまたまtaskの間に分が変われば複数ファイルが残ります。 ファイルのコピーには `shutil.copy2` が使われているのでメタデータもすべてコピーされます。
