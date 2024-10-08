# amkb
Avatar modification knowledge base

## はぁ？
UnityやBlenderでそう思ったこと、一度はありますよね。
あるいは、「アレってどうやるんだっけ？」

このプロジェクトは私のそんな悩みを未来の私が解決するついでに消えないよう永続化しておくレポジトリです。多分。

## ライセンス
CC0

## Unity
### 衣装のきせかえをしたいのにうまくいかない

チェックリスト
1. 非MA: パラメーター名が間違っている
2. MA: MA Merge Animatorと同じGameObjectか上にMA Parametersがない
3. MA: MA Merge Animatorがその上のGameObjectを操作しているのにパスモードが相対的のまま
4. MA: MA Merge Animatorのルートがおかしい (★明示的に指定していない場合は問題ない)
5. AnimationでレイヤーのWeightが0になっている
6. stateのmotionに何も割り当てられていない
7. ゲームオブジェクトの名前を変えた
8. ゲームオブジェクトの階層を変えた
9. アニメーションクリップの長さが有限→デフォルトで設定されている2番目のキーフレームを<kbd>Delete</kbd>で消すこと

★未確認情報: LilycalInventoryでGameObjectの同時切り替えを指定しても連動しない

### コンポーネントの値をコピペしたい

1. 右上の︙からCopy Component
2. コンポーネントがないなら1と同じコンポーネントをAdd Component
3. 追加したコンポーネントの︙からPaste Component Values

### 非対応衣装を着せるとき

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

### liltoonDPSの入れ方

1. https://twitter.com/lil_xyzw/status/1489593222988845059 を見る
2. Dropboxからunitypackageをダウンロードする
3. プロジェクトに最新版のlilToonを入れる[^1]
4. unitypackageをインポートする

[^1]: lilToonは破壊的変更が今の所無いのでそれで良い

### ごろ寝システムのインストーラーがLinuxだと動かない

おそらく既知のバグ。ソース上でディレクトリ同士を分ける文字列が`\`としてハードコーディングされているので、`/`に書き換える必要がある。

### アバターにlilToonが同梱されているのが気に食わない

インポートした当時のパスから変更していないのであれば、シームレスにVPM管理に移行することができる。

### PhysBoneのコライダーが動作しない

1. PhysBone colliderをAdd Componentしたか確認する
2. PhysBone側でColliderという名前のプロパティに値を設定しているかどうか確認する

### Meshのポリゴン数を数えたい

フレアさんが作っているMeshPolyCounterを入れる

1. https://github.com/whiteflare/vpm-repos
2. `jp.whiteflare.avatartools`をインストール
3. Tools > whiteflare > Mesh Poly Counter
4. ルートのゲームオブジェクトをVRC Avatar Descriptorがついてるオブジェクトにする
5. 各メッシュのポリゴン数が表示される

★ヒント: Play modeでも動作するので、AAOやMAが走った後の結果を調べるのにも使える。

### ポリゴン数を減らしたい

Blenderなどで湯通しする方法もあるが、ここでは非破壊でポリゴン数を減らす(デシメートする)ことができるlilNDMFMeshSimplifierを使う方法を紹介する。

1. Gitをインストール。詳細は割愛するのでGoogle検索を使って各自調べること。
2. lilNDMFMeshSimplifierの前提のNon-Destructive Modular Frameworkが入ってなければVCCなどで入れる。これも詳細は割愛。
3. Unityのプロジェクトを開く
4. プロジェクトウィンドウ上部のツールバーで、Window > Package Manager
5. 左上の \[+▼\] を押す
6. Add package from git URLを押す
7. `https://github.com/lilxyzw/lilNDMFMeshSimplifier.git` と入力
8. 右の \[Add\] を押す
9. インポートが走るのでしばらく待つ
10. デシメートする(ポリゴン数を減らす)メッシュに"NDMF Mesh Simplifier"というコンポーネントをAdd Component
11. 品質はメッシュのポリゴン数を何倍にするか。0から1なのでお好みでどうぞ
12. Play modeに入ってプレビュー。

### どのテクスチャがTexture Memoryをどれだけ消費しているか調べたい
1. https://github.com/Thryrallo/VRC-Avatar-Performance-Tools をインストール。
2. プロジェクトウィンドウ上部のツールバーで、GameObject > Thry > Avatar > VRAM
3. どのテクスチャがどれだけTexture Memoryを消費しているか出る

### VRChatでアバターをアップロードしたはずなのにdescriptionだけ更新されてる！
2022.3.6よりも未来のエディターを使ってるとゲーム内で無視される。必ず[指定された](https://creators.vrchat.com/sdk/upgrade/current-unity-version/)バージョンを使うこと。

### AAO Remove Mesh in BoxのEdit This Boxを押してもBoxが出ない！
チェックリスト:
1. ギズモを切ってない？ ([AAO#923](https://github.com/anatawa12/AvatarOptimizer/issues/923#issuecomment-1987869463)) \
    切っている場合はScene viewの右上のプルダウンを調整すること。

### デフォルトのスクショの解像度が荒すぎる！
<https://github.com/Reiya1013/UnityScreenshot/> を入れようね

### 複製したプロジェクトでアップロードすると上書きされる！
1. `VRChat Avatar Descriptor`という名前のコンポーネントがついているゲームオブジェクトをヒエラルキーから探す。
2. インスペクターから`Pipeline Manager`という名前のコンポーネントを探す。
3. \[Detach (Optional)\]を押す[^2]。
4. アップロードする際に、新しく名前、サムネ、説明文、[Content Gating](https://hello.vrchat.com/blog/content-gating)の設定をする。

### インポートしたFBXにAnimatorがない！
1. FBXをAssetsから探す。
2. InspectorのImport Settingsを見る。
3. \[Rig\] タブを見る。
4. Animation Typeが「Humanoid」になっているかどうか見る。
5. \[Apply\] を押す。

もしボーンの動き方がおかしければ、ホーンを調整する:

1. Avatar Definitionの下にある\[Configure\]を押す。
2. `UnityEngine.Avatar`のInspectorに遷移するので、\[Configure Avatar\]を押す。
3. ボーンを調整する。
4. 反映する。

[^2]: `avtr_`から始まるBlueprint IDが消える。VRChatではBlueprint IDが変わると別のアバターとして扱われる。

## Blender
### FBXのメッシュを分割するとき
★ここではすでに存在する辺の上で分割することを想定する

2. FBXをインポート
3. 分割する元のメッシュを選択
4. 編集モードに入る
5. 選択モードを面にする
6. 分割されて新しいメッシュとなる面をすべて選択
7. <kbd>P</kbd>キーを押して「選択」をクリック

※注: 切断面と接する面がある場合、新しい面が作成されるわけではないので注意

※注2: [MeshSplitter](https://booth.pm/ja/items/1633965)を使う方法もあるが、マテリアルごとの分割あるいはQuadをPlaneとしてみなしたときに交差するポリゴンを境界として新しいポリゴンを作成せずに分割するため、きれいに分割できないことが多い


### FBXのエクスポートの呪文

1. 出力オブジェクト: 「アーマチュア」と「メッシュ」に \
   理由: カメラとライトがエクスポートされるため、ゴミになる
3. スケールを適用: 「すべて FBX」
4. 前方: 「Z が前方」
5. トランスフォームを適用にチェックをつける
6. リーフボーン追加のチェックを外す

### 補助ボーンの入れ方

#### 手続き: アーマチュア変形の再計算
1. メッシュを選択する
2. アーマチュアを選択する
3. <kbd>Ctrl</kbd>+<kbd>P</kbd>を押す
4. With Automatic Weights、あるいはそれが多言語化されたボタンを押す

#### 本編
2. モデルをインポート
3. 補助ボーンを適用する対象のメッシュに対して**アーマチュア変形の再計算**を行う
7. ポーズモードに切り替える
8. 関節が破綻するポーズにする
9. 編集モードに切り替える
10. <kbd>Shift</kbd>+<kbd>A</kbd>を押す
11. ボーンが新しく生える
12. <kbd>G</kbd>で移動、<kbd>S</kbd>で大きさの変更、<kbd>R</kbd>で回転ができるので「それっぽい位置」に移動させる
13. ポーズモードに切り替える
14. 破綻がないか確認
15. 満足が行くまで**アーマチュア変形の再計算**をしたり、11や12に戻ったりして繰り返す

#### Q. メッシュが歪んで関節が破綻するのが気に食わない
A. 関節が膨らんでほしい方向に向かって補助ボーンを入れてね。例えば外側に膨らんでほしいならメッシュの外側に入れた補助ボーンがはみ出るように。

### UVガイドを出力したい
ウィンドウ上のツールバー > UV Editing > UV > UV配置をエクスポート。以下、おすすめの設定。

* フォーマット: PNG
* 解像度: 4096×4096
   * 使ってるメインテクスチャの解像度に合わせたほうが良い
* フィルの不透明度: 0.0
   * 下地の色がわからなくなる

設定し終わったら保存する場所を選択して保存。

### メッシュのマージ
1. オブジェクトモードにする
2. シーンコレクションを選択
3. マージしたいメッシュを<kbd>Ctrl</kbd>押しながら全部選択
4. <kbd>Ctrl</kbd> + <kbd>J</kbd>
