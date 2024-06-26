---
title: "テクスチャとPBRに関するメモ"
tags: [pbr, shading, materials, textures, rendering, basics, 基本, 🔰初心者]
category: [gamedev]
lang: ja
ref: posts
---

### Channel Packing Textures

- TextureName_ALB.tga
  - Albedo map
- TextureName_NORM.tga
  - Normal map
- TextureName_ORM.tga
  - O = Occlusion
  - R = Roughness
  - M =Metallic

### Acronyms

PBR = Physically Based Rendering
- Rendering & Lighting Concepts

PBS = Physically Based Shading
- Shading Concepts

### PBR Theory

Both PBR & PBS refers to representing assets in a physically accurate context
### チャンネルパッキングテクスチャ

- テクスチャ名_ALB.tga
  - アルベドマップ
- テクスチャ名_NORM.tga
  - 法線マップ
- テクスチャ名_ORM.tga
  - O = オクルージョン
  - R =ラフネス
  - M =メタリック

### 頭字語

PBR = 物理ベースレンダリング
- レンダリングとライティングのコンセプト

PBS = 物理ベースシェーディング
- シェーディングの概念

### PBR理論

PBRとPBSはどちらも物理的に正確なコンテキストでアセットを表現することを指す

- 正確なアルベドカラーと反射率の値を使用することを保証します。
- あらゆる種類の照明条件において物理的に正確に見える
- マテリアル定義との一貫性を確保

PBRを理解するための3つの異なるテント

### エネルギー会話

- 反射光の総量は、入射/入射光より多くなることはありません。
- 拡散/粗い表面は、非常に薄暗く広いハイライトを反射する。
- より滑らかで光沢のある表面は、よりタイトで明るいハイライトを反射する。
- 物体は自ら光を生成できない

### BRDF (双方向反射率分布関数)

- 表面の反射特性を表す数学的な関数。
- 多くの異なるBRDFが存在する
  - ディズニーのBRDF（GGX BRDFの改良版）
  - GGX
  - クック-トーランス
  - オーレン-ナイヤー
  - ランバート
  - ブリン-フォン
  - フォン（ブリン-フォンと混同しないように）
  - ウォード
  - UE4はGGXを使用

### 導電性材料と誘電性材料
- 誘電体
- 絶縁体
  - 反射よりも吸収が大きい
- 電気を吸収する
  - 例：プラスチック、ゴム、氷、ガラス、錆びた金属など
- 一般的に金属以外のもの
- 導電性
- 電気を通す
  - 一般的にすべての金属を含む
  - 錆びた金属は含まない

これらの素材を扱うための2つの異なるワークフロー：
- 光沢/スペック
- 金属性/粗さ
Unrealでは、Metalness/Roughnessを使用します。

### 金属性／粗さ
- 一般的にGloss Specよりも費用対効果が高く、アーティストが理解しやすい。
- チャンネルパッキングが可能
- アルベドにはライティング情報/AOを含めない。
- メタルネス/ラフネスワークフローでは、技術的にはメタリックチャンネルにカラーを注入できますが、メタルネスを白黒に保ち、アルベドチャンネルにカラーを注入する方がシンプルで正確です。
- AOは、特定の葉のためにアルベドに含まれることがありますが、マイクロ/マクロディテールにのみ使用されるべきです。
- メタルネス
  - 黒 / 0.0 = 非金属
- 白 / 1.0 = フルメタル
  - 値は1を超えることはできません。
  - 錆や汚れのような過渡的な素材には、グレーの値を使用できる場合があります。
  - 黒と白のコントラストがはっきりしないのは、過渡的なマテリアルでレンダリングの問題を引き起こす可能性があるため、お勧めできません。
  - 基本的には、黒と白のマスクでメタルネス・マップを作成する場合、黒から白への遷移部分やその逆は、グレーのフェザーで構成される必要があります。

### グロス／スペック
- Gloss/Specを使用してメタリックなものを作成する場合は、スペキュラチャンネルの色を使用する必要があります。
- 真っ黒なスペキュラマップは存在しません。
- スペキュラ値に対して、すべてのものは最小のグレー値を持ちます。
- Gloss/SpecはMetalness/Roughnessと逆の動作をします。
- 光沢
  - 黒/0.1 = 光沢が少ない / 非金属
  - 白/1.0 = 光沢のあるプラスチック/金属
- 完全な光沢では、素材はよりタイトで明るいハイライトを持つ。
  - 逆の場合、ハイライトと反射はより広く、より拡散する。
- スペキュラー
  - 黒 / 0.0 = 反射が少ない
  - 白 / 1.0 = 反射率が高い
- 鏡のような表面を得るには、グロスとスペックの両方を1にする必要があります。
- アルベドはグロス／スペックに寄与しない。
- カラーメタルは、スペキュラチャンネル内で色相を調整する必要があります。