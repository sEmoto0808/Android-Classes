# ライフサイクル
# 画面遷移
Fragment <-> Fragment
```
// Activityから
supportFragmentManager
    .beginTransaction()
    .add(Fragmentのid,
         Fragmentのinstance,
         String型のTag)
    .commit()
```

AACのNavigationを使った場合
```
findNavController().navigate(Navigationグラフに定義したアクションのId)
```
[詳しくはNavigationのファイルに記載](/Navigation.md)

# 開発してて調べたこと
- Fragmentが破棄された時に表示状態などのデータを保持する
- Fragmentが保持したデータはonActivityCreated()内で復元される
