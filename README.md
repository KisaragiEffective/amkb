# amkb
Avatar modification knowledge base

## コンポーネントの値をコピペしたい

1. 右上の︙からCopy Component
2. コンポーネントがないなら1と同じコンポーネントをAdd Component
3. 追加したコンポーネントの︙からPaste Component Values

## FBXのメッシュを分割するとき
★ここではすでに存在する辺の上で分割することを想定する

1. Blenderを手に入れる
2. BlenderでFBXをインポート
3. 分割する元のメッシュを選択
4. 編集モードに入る
5. 選択モードを面にする
6. 分割されて新しいメッシュとなる面をすべて選択
7. <kbd>P</kbd>キーを押して「選択」をクリック

※注: 切断面と接する面がある場合、新しい面が作成されるわけではないので注意

## 非対応衣装を着せるとき

1. プロジェクトに[Modular Avatar](https://modular-avatar.nadena.dev/ja)を入れる
2. 衣装をダウンロードする
3. 衣装のunitypackageをインポート
4. Hierarchyで衣装のprefabをアバターの直下にドラッグアンドドロップ
5. 衣装のprefabを右クリックしてMAのSetup outfit
6. (MAがいい感じにならなかったら手動でボーンの名前とか調整する)
7. ボーンを適当に拡大縮小・移動する。\[注: [キセテネ for MA](https://booth.pm/ja/items/5057270)を使っても良いかもしれないが未検証\] \
   実機で動かしても良いが、簡単な確認ならUnityのCameraで四方から見たり[Av3Emu](https://github.com/lyuma/Av3Emulator)を使うほうが経験上速くサイクルを回せる。
9. 貫通するならモデルの貫通防止シェイプキーをいじる \
   特に膝や肘などは貫通しやすいため注意
10. それでも貫通するなら[AAO: Avatar Optimizer](https://vpm.anatawa12.com/avatar-optimizer/ja/)の[Remove Mesh in Box](https://vpm.anatawa12.com/avatar-optimizer/ja/docs/reference/remove-mesh-in-box/)でごまかす

## liltoonDPSの入れ方

1. https://twitter.com/lil_xyzw/status/1489593222988845059 を見る
2. Dropboxからunitypackageをダウンロードする
3. プロジェクトに最新版のlilToonを入れる[^1]
4. unitypackageをインポートする

[^1]: lilToonは破壊的変更が今の所無いのでそれで良い

## ごろ寝システムのインストーラーがLinuxだと動かない

おそらく既知のバグ。ソース上でディレクトリ同士を分ける文字列が`\`としてハードコーディングされているので、`/`に書き換える必要がある。

## アバターにlilToonが同梱されているのが気に食わない

インポートした当時のパスから変更していないのであれば、シームレスにVPM管理に移行することができる。

## PhysBoneのコライダーが動作しない

1. PhysBone colliderをAdd Componentしたか確認する
2. PhysBone側でColliderという名前のプロパティに値を設定しているかどうか確認する
