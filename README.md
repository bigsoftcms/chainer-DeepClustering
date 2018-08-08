[Deep Clustering for Unsupervised Learning of Visual Features](https://arxiv.org/pdf/1807.05520.pdf)
===

## どんなもの？
画像分類タスクにおいてConv構造を利用した新しい教師なし学習手法の提案．

## 先行研究と比べてどこがすごいの？
これまでも教師学習としては画像などの入力そのものに対してクラスタリングを行いクラスタリングを行っていたために，より有効な画像記述子を獲得できていなかったが，画像認識の分野で有効とされているConv構造のあとでクラスタリングにより，その恩恵を受けられるようになる.

## 技術や手法の"キモ"はどこにあるの？
Fig 1.のアーキテクチャが示すとおり，Conv構造の出力をクラスタリングし，その結果を元に擬似ラベルを付与，その結果で分類を行いその誤差を逆伝搬することで重みの更新を行う．Conv出力をPCAで256まで圧縮してK-meansでクラスタリング，そのラベルの推論，これを交互に繰り返していく．

![](https://i.imgur.com/wGctLOT.png)


また，クラスタリング手法に関して空のクラスタが内容にする，一つのクラスタに全ての入力が集中するのを防ぐために以下を行っている．

- 空のクラスタが存在した場合に空でないクラスタをランダムに選択し，そのセントロイドをわずかに移動させ，その他のデータをリアサインする．
- 分類の際にクラスタに割り当てられたデータ数の逆数を入力にかけることにより，ハッシュタグのようなメタデータの影響を抑え一つのクラスタに全てのデータが割り当てられるのを防いでいる．


## どうやって有効だと検証した？

Table 1.が示すのはAlexNetのConv部分を固定してfcを学習した結果の比較であり，多くの層の特徴量において既存の教師なし学習の成果を上回った．さらに，Plaseに置けるImageNetの教師あり学習で得られた特徴量の有効性はConv3,Conv4において提案手法が上回る結果となっているのがわかる．これから，目的のタスクがImageNetのドメインから離れていればもはやラベルはそれほど重要でないとわかる．

![](https://i.imgur.com/EaLFoDX.png)

また，Table 2.はディテクションとセグメンテーションに関して，finetuningではなく転移学習が適用されやすい実際のアプリケーションにとっていい結果である．

![](https://i.imgur.com/CzcFwRz.png)


## 議論はあるか？

AlexNetとImageNetによる検証を主として行ったが，これまでに成果が出ている他のデータセットモデル，また，画像検索のタスクにおいても期待すべき成果が出ている．

## 次に読むべき論文はあるか？

いっぱいあるよー

## memo

###### tags:`paper-servey` `unsupervised`
