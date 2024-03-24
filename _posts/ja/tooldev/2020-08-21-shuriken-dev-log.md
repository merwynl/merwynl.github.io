---
title: "Shuriken Toolkit Dev Log 0.0.1"
tags: [code, Auto, Automation, Py, Tkinter]
category: [code]
lang: ja
ref: posts
---

しばらくの間、私は個人的なワークフローをスピードアップする方法を探していた。ホットキーやショートカットは素晴らしいが、特定のツールが手の届くところにあれば、クリックだけで済ませたいと思うこともあるだろう。それに、素早くホットキーで操作できるツールは限られている。異なるDCC間を行き来することは、多くの異なるホットキーを呼び出さなければならないことも意味する。それは悪いことではないが、使い始めたばかりの人は、何十種類ものホットキーを覚えなければならないことに少し圧倒されるかもしれない。

私がMayaのShelvesシステムを気に入っている大きな理由の1つは、カスタマイズがとても簡単で、頭の中でコンテキストの切り替えを繰り返すことなく、よく使うツールの束に素早くアクセスできることです。しかし、シェルフが占めるUIの面積が大きいため、制限されることもあります。

数ヶ月前にShurikenというカスタムツールセット（名前は今のところプレースホルダ）を作り始めたが、まだ開発の初期段階なので話すのをためらっていた。このツールの着想は、[froTools][frotools]やMJPolyToolsのような本当に素晴らしいツールを使っていることから得たものだ。

このツールは、MayaのPython APIをより使いこなすための手段として開発してきましたが、いつかもっと広い文脈で使えるようなものを作る機会にもなりました。

このツールセットの目的は、私が日常的に使う最も一般的なツールのいくつかと、より速い反復のためのカスタムツールのいくつかに、素早く簡単にアクセスすることです。

最初にMaya Commandsを使ったのは、その利点について聞いたことがあり、少し試してみたかったからです。ツールの動作が少し遅くなり始めたら、Maya Commandsに戻すかもしれませんが、今のところ、私はこれを学習実験として扱っています。

このページには、MayaのPython APIといくつかのスピード・ベンチマークについてかなり詳しく説明されている。Shurikenツールキットのスピードテストは、もっと機能が追加されるまではあまり意味がない。今のところ、スピードの差は顕著ではない。

次に決めたのは、UIをどのようにフロントロードするかということだった。ドッキングできるようにしたいとは思っていた。もし私が本当に嫌いなものがたくさんあるとすれば、それはフローティングウィンドウが多すぎることだ。また、今後さらにツールや機能を追加することになった場合、ある程度スケーラブルでなければなりません。

PySideはいい選択肢だと思った。PySideは広く使われていて、Mayaのネイティブ・サポートがあり、QtDesignerからカスタムUIファイルを作成できる。しかし、ウィジェットやスタイルシートを使って派手なUIを構築することはおろか、Qtを使って書いた経験もまだあまりなかった。仕事でQtのコンセプトには触れてきたけど、Shurikenにはちょっとやり過ぎで不必要な気がしたんだ。

workspaceControlというコマンドに出会った。これはMaya 2017で導入されたもので、uiScriptフラグを通してUIファイルを呼び出すことで、MayaでカスタムQtウィジェットをドッキングする方法を提供する。しかし、デザイナーの UI ファイルを使用する必要はありません。そのドキュメントによると、UI を別の関数の下に置き、その関数を呼び出すことができます。

以下はその一例である。:
```python
import pymel.core as pm
 
if pm.workspaceControl("Window", exists =True):
    pm.deleteUI("Window")
 
def UI(*args):
    # Main Column layout
    pm.columnLayout(adj = True, w=250, h=805)   
 
    # Primitive Layout
    primitives_layout = pm.columnLayout(adj =True)
 
    # Buttons for creating primitives
    create_sphere_button = pm.button( label= "Sphere")
    create_cube_button = pm.button( label= "CubeCube ")
     
    pm.setParent(primitives_layout)
 
pm.workspaceControl("Window", retain=False, floating=True, uiScript="UI()")
```


別のファイルを管理する必要がなければ、別のファイルを管理する必要はないと思ったので、別のUIファイルは使っていない。しかし、もしこのツールが大きくなって、もっと別のモジュールに分けなければならなくなったら、その時はこのアイデアを見直すかもしれない。上記のソリューションは、私の現在のニーズに合っている。

他にも素晴らしい例がいくつかある。

[Kaine van Germet][Kaine van Germet]は、ドッキング可能なウィンドウを作成するために、標準的なQtレイアウトでWorkspace Controlsを使用する方法について、より詳しく説明しています。私はMayaレイアウトを使うことにしました。

このツールがリリースするほど便利になったと判断したら、この開発ログを扱うのにもっと伝統的なソフトウェア開発アプローチを使うことを検討するつもりだ。今のところは、この形式でアップデートをリリースし続けるかもしれない。


[frotools]: https://www.froyok.fr/assets/frotools/
[here]: https://python.hotexamples.com/examples/maya.cmds/-/workspaceControl/python-workspacecontrol-function-examples.html
[Kaine van Germet]: https://kainev.com/qt-for-maya-dockable-windows/