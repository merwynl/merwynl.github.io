---
title: "Gaeaへ入門"
tags: [proceduralism, houdini, gamedev, ゲーム開発, basics, 基本, 🔰初心者]
category: [gamedev]
lang: ja
ref: posts
---

# ガイア入門

ノードベースの地形システム。バグが多く、安定性に問題があります。

## 1. UI

ユーザーリサーチが製品や機能の開発に大きく役立つと思われる機会があれば、Docsデータベースに提案書を書くことから始めてください。

**ツールボックス**

- すべての地形ノードを含む
- 標準とエキスパートの2つのモードがあり、ノードのカテゴリーを隠したり見せたりできます。
- 右上のスライダーでよく使うノードに切り替えられます。
- 位置は右、下、フルに変更できます。
- ノードはTabキーを使ってグラフからアクセスすることもできます。

**グラフ**

- メイン作業エリア
- いくつかの異なるノードスタイルがあり、環境設定で変更できます。
- 複数のグラフを作成し、色分けすることができます。
- Mark for Export（エクスポート用マーク）」は、ノードをエクスポート用にマークします。

**プロパティ**

- 各ノードのプロパティを調整

**コントロール・キー**

- U - グラフビューでマスクビューモードを切り替える
- F6 - グラフ・ビューで2Dビューを切り替える
- Alt + 左マウス - 回転
- 中マウス - パン
- マウスホイール - ズーム
- F4 - ノードの自動レイアウト
- Ctrl + R - 現在のノードプロパティをリセット
- F8 - 2つ以上のノードを混ぜ合わせます。Combineノードをレイアウトするのと同じです。
- ビューポートの回転はワールドの中心に固定されます。

## 2. ノード

**山**

- 基本的な山を作ります。
- Edge - 山を押し下げ、円形のクレーターを作ります。
- Seed - 山のバリエーション
- Shape Style - クラシックな山と砂丘スタイルの山を切り替えます。

**ボロノイ**

- プロシージャルノイズの作成
- デュアルボロノイを有効にする
- 高いスケール値を使用する場合、ある閾値を超えないようにクランプすることができます。
- ワープ（Warp）ノイズをワープさせることができます。高いワープ周波数でマグマの流れを作成するのに便利です。

**ボロノイ**

- 標準的なボロノイとは全く異なる。
- ジャイアンツ・コーズウェイのようなゴツゴツした岩を作るのに使える。

**スロープノイズ**

- 斜面上のノイズ
- Stratified - テラスのようなゴツゴツした地形を作るのに便利。

**プレート**

- 方向性のある強いプロファイル

**ドロー**

- カスタム形状を描画可能

**Igneous**

- ソフトな峡谷とアンダーレイを多用した大きな山。
- クランプと併用することで、ノイズの影響を抑えることができる。

**ヒール**

- ノイズ除去に似た働きをする。
- 高周波ノイズの多くを和らげますが、高いピークは維持します。
- ブルーノードはすべてをぼかします。
