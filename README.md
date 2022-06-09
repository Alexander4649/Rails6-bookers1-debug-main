エラー内容と変更箇所

起動〜Top表示まで
* topのViewまでのroutesがない為、Top.Viewに遷移しない 
=>rotes.rbにroot to"homes#top"を追記

* homes_controllerがControllerと記載されているのでアクションが成立しない
=>homes.controller.rbにHomesを追記

* top.viewの文字サイズが違う => application.cssにて記述

* link_toの記述が違う為、リンクが機能してない =>a要素ref属性に変更

* startボタンのオンマウスオーバーが機能してない =>cssにて記述

Bookindex〜form_with.htmlまで
* Topのstartボタンから遷移できない
=> _from.htmlにて モデル名とバリデーションエラーメッセージ設定にて「books」と定義されており、エラーとなる。=> formのViewにて@bookに変更

* formの中、Newbook(新規投稿フォーム)にて見本と見た目(段落)が合っていない
=> <br>追加にて対応-title,body,submit各種

* 投稿ができない①-dbカラムにtitleカラムが追加andマイグレートされていない
=>カラムADDしてmigrate対応(今回はADDにて追加指示)=> rails g migration ADDTitleToBooks title:string =>rails db:migrate

* 投稿ができない②ーbook.controllerにてさdef index部分の記述の順番が逆である。
=>コントローラは上から制御していく為。

* linktoの記述が間違っている
=>classは使わずにリンク先をrails routesで確認してpathを追記。showページ・editページに関しては(book.id)を追記。destroyはbook_path(book.id)に変更

update・destroy機能が使えない問題
* updateが機能しない
=> <form>が邪魔をしている=>formを外すのみ

バリデーション付近
* バリデーションが機能しない=>
=>create失敗時に@boosに対するアクション定義がない為、@books = Book.allをelseの後に追記
=>pluralize(book.errors.count, "error")よくわからない記述を変更=>@book.errors.count,また、<h2>要素を削除

* editフォームにてバリデーションが機能していない
=> <form>が邪魔をしている=>formを外すのみ

フラッシュメッセージ
* フラッシュメッセージが機能していない
=>books_controllerにてflash:noticeとメッセージを記述

* フラッシュメッセージの色が緑じゃない
=> appleication.htmlのflash:notice部分を<div class>で囲い、cssにてcolor設定