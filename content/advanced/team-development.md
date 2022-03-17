---
title: "Git と チーム開発"
date: 2022-03-16T07:53:56+09:00
weight: 1
---

基礎編をマスターすることができたのであれば、Git 管理をしながら開発することに自信を持つことができていると思います。  
しかし、チーム開発で Git を扱うにはまだ不十分です。  
例えば、次のような状態になったとき、あなたはどうしますか？

### あらまし
仮にチーム内で開発者とテスターが分かれていた場合でのお話です。
開発者AはテスターBにソースを渡すため、リモートリポジトリに変更を加えたソースを push しました。

ところが、テスターBが pull をしてテストをしたところバグが見つかりました。
そこで、テスターBは開発者Aにバグがあることを伝え、修正を依頼しました。

一見問題はなさそうですが、もし別の開発者Cがいた場合はどうでしょう？
開発者Cももちろんリモートリポジトリから最新のソースを取得して開発をおこないます。

リモートリポジトリから取得したソースにバグがあった場合、開発者Cにも影響を与えてしまいます。

このようなときに **ブランチ** は活躍します。  
ブランチの運用方法は様々ですが、今回はデフォルトの main ブランチの他に開発用のブランチ（ develop ブランチ）を作成する運用をすることで今回の問題は解消されます。

ここからはブランチについて学んでいきましょう。