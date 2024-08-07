# アッシュちゃん
## スパッツが破れている
仕様。どうしても嫌ならPSDレイヤーを非表示にすること。

## スパッツとレギンスで表記ゆれしている
仕様。

## 素体(スパッツなし)
~~仕様。~~ 2024年7月14日のアップデートで統一されたので存在しなくなった[^10]。

[^10]: https://x.com/Mito_Arisaka/status/1812313017201377576

### 対処
<details>
  <summary>旧情報のため折りたたみ</summary>

  ここではスパッツの破れを維持しながら下腹部から足先まで全てのメッシュを持つ素体 (以下「全身素体」とする) に寄せる方法を紹介する。
  どうしても全身素体に寄せたいんだ！！！じゃないと死ぬ！！！って変人以外はこの対処を見なかったことにするべきである。そうでもないと面倒すぎて死ぬ。
  
  大まかな方針としては、スパッツのメッシュをそこに対応するボーンを中心として外側に拡張する方針である。
  
  1. Blenderを開く。
  2. 「レギンス」という名前のメッシュを探してクリック。
  3. 編集モードへ移行。
  4. レギンスのテクスチャでT字に縫い目が入っている辺を探し、水平方向に走っている縫い目から上の面を全て選択。
  5. 4で選択した面に加えて、股間部のメッシュ、Vラインのメッシュ[^2]と、「足の付け根」[^3]のループから上のメッシュを全て選択する。
  6. <kbd>S</kbd>を押してスケールモードへ移行。
  7. <kbd>Shift + Z</kbd>を押してZ平面に沿うスケールモードに変更。
  8. 適当にドラッグしてクリック。
  9. スケール倍率を微調整するためのウィンドウが左下に出てくるので、それをクリック。倍率を覚えておく。ここでは、X軸方向の倍率を𝑋、Y軸方向への倍率を𝑌としておく[^5]。
  10. 選択を反転。
  11. 「足の付け根」ループから下かつ、縫い目から片側にある面だけを全て選択。
  12. <kbd>S</kbd>を押す。
  13. <kbd>Y</kbd>を押す[^1]。
  14. 適当にドラッグしてクリック。
  15. スケール倍率を微調整するためのウィンドウが左下に出てくるので、それをクリック。Y軸方向への倍率を𝑌に設定する。
  16. メッシュ > スナップ > 「カーソル → 選択物」[^4]をしてスケールの原点をボーンの中心あたりにする。
  17. <kbd>S</kbd>を押す。
  18. <kbd>X</kbd>を押す。
  19. 適当にドラッグしてクリック。
  20. スケール倍率を微調整するためのウィンドウが左下に出てくるので、それをクリック。X軸方向への倍率を𝑋にする。
  21. もう片足も同様にやる。
  22. 多分股間部分が貫通するのでうまいことメッシュを移動させるなりスケールするなりでうまいことごまかす。
  23. オブジェクトモードへ移行。
  24. 「下着」という名前のメッシュを探してクリック。
  25. 編集モードへ移行。
  26. <kbd>S</kbd>からの<kbd>Shift + Z</kbd>。
  27. X軸方向の倍率を𝑋、Y軸方向への倍率を𝑌と設定する[^6]。
  
  [^1]: <kbd>Shift + Z</kbd>を押してZ平面に沿ったスケールモードでX軸を変更してしまうと、縫い目が潰されるような変形になってしまい良くない。
  [^2]: 見えにくいがそこにメッシュがある
  [^3]: お好みで調整せよ。ただし、左右で同じ高さのループであることが望ましい。
  [^4]: こうしないとレギンスが素体に合わない
  [^5]: お好み。筆者はどちらも1.05とした。
  [^6]: そうしないと下着がレギンスにめり込む。

</details>

## スパッツの破れが実際の肌テクスチャを参照しないのが嫌だ

### 対処
大まかな方針として、半透明マテリアルを使うことで解決する。ただし、実際に素体を絞っている場合はうまいことやる必要がある。
ここでは、簡単のために素体を絞っていないケースを考える。

まず、アルファマスクを作る:

1. PSDを開く。
2. 新しいレイヤーグループを作る[^7]。
3. 作ったレイヤーグループの下に両足のスパッツのレイヤーグループを入れる。
4. その上に除算レイヤーを作る。
5. スパッツのベージュ色をスポイトし、除算レイヤーを塗りつぶす。
6. 除算レイヤーの上に、減算レイヤーを作る。
7. スパッツの描画されている色[^8]をスポイトし、その色で減算レイヤーを塗りつぶす。
8. 両足の「質感」「影」レイヤーをそれぞれオフにする[^9]。
9. 作ったレイヤーグループ以外のレイヤーグループを全て不可視にする。
10. PNGで保存。

アルファマスクを作ったらやることはいつものアレである。

1. Unityのプロジェクトに入れる
2. lilToonの描画モードを半透明にする。
3. アルファマスクを指定する。
4. Invertを有効にする！！！！！！！！！！！
5. (任意) メインテクスチャに対して焼き込む。

課題: 当然半透明シェーダーなので意図せず透けることがある。今後の展望としては[lilToon_MsdfMask](https://kb10uy.org/posts/liltoon-msdfmask-instruction/) を活用した抜きにすることも考えられるが、確立には至っていない。

[^7]: この後で作る調整用のレイヤーが不必要なレイヤーにまでかかることを防ぐため
[^8]: おそらくかなり暗い水色になっているのではないだろうか？
[^9]: 多分やらなくても見た目的には大した違いが生まれないだろうが、「質感」レイヤーのノイズテクスチャが量子化の面では不利になりそうなのであえて切ることとした。

## 靴のロゴが反転している

~~多分誰も気づいていない~~ [報告](https://x.com/kisaragi_marine/status/1782986873641857051) はした。

### 対処

1. Blenderを開く。
2. 靴のメッシュを選択。
3. 右足のシュータンにあるロゴが書かれている面とその側面を選択。
4. UV Editingタブへ行く。
5. さっき選んだ面が選択されていることを確認。
6. UV画面で選択されているUVを右クリック。
7. 「ミラーX」をクリック。

