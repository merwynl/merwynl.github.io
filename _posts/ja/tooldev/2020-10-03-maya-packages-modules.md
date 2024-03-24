---
title: "Maya でモジュールとパッケージ スクリプトをインポートする"
tags: [code, Auto, Automation, Py]
category: [code]
lang: ja
ref: posts
---

外部スクリプトをインポートして実行することは、スクリプトをポータブルにするための重要な要素です。スクリプトを別々のファイルに分割することは、大きなコードの塊や機能を小さく分割する便利な方法です。作成された別々の Python ファイルはそれぞれモジュールであり、パッケージはモジュール/パッケージの集まりです。

Pythonパッケージの考え方は次のようなものです：

```python
/bin
main.py
    /package
    __init__.py
    module_1.py
    module_2.py
```

Maya内でPythonスクリプトをインポートして実行する例を示します。例えば、my_module.py というモジュールがあり、そこには次のような関数がたくさんあるとします：

```python
import maya.cmds as cmds
 
# Function that does stuff
def MakeCube():
    cmds.polySphere()
    print('Sphere made!')
```

このモジュールは、現在maya\version\scripts\packageにあり、Maya 内からこのスクリプトをインポートして実行します。このスニペットでは、polySphere() 関数にアクセスできる Maya Commands モジュールをインポートしています。

このスクリプトが scripts フォルダの中にあり、1 つ下の階層になければ、次のようにできます：

```python
import my_module
reload(my_module)
my_module.MakeCube()
```

reload 関数を使用すると、インポートするものが常に同期されます。Maya Commandsをインポートしたときと同じように、独自のモジュールをインポートすることで、コードの入力量を減らすことができます：

```python
import my_module as md
reload(md)
md.MakeCube()
```

この例では、モジュールは scripts フォルダの下の独自のパッケージの中にあるので、 Maya はそのパスについて何も知りません。python sys モジュールを使用することで、Maya が現在認識しているパ スを知ることができます：

```python
 
for path in sys.path:
    print path
```

これを Maya のスクリプト エディタで実行すると、Maya が自動的に認 識するパスのリストが表示されます。これを拡張して、sys.path.append() 関数を使用してこのリ ストに追加するか、Maya.env ファイルの変数を使用してパスを追加します。絶対パスで .mod ファイルを作成し、そのファイルを maya.env フォルダに追加することもできます。これは、Maya がさまざまなプラグイン モジュールの配布を処理する方法の 1 つです。

要件によっては、これらのオプションのいずれかを実行可能なソリューションと して使用できます。ただし、スクリプトが比較的単純で、単一の python モジュールまたはパッケージで構成されている場合は、不必要な複雑化を避け、Maya が認識するパッケージまたはパスにスクリプトを保存して、そこからインポートする方がよいでしょう。

しかし、元の問題に戻ると、そのままインポートすることはできません。前述したように、Mayaはパッケージのパスを知りません。パッケージが他の場所にある場合は、sys.path.append() を使用することができます。しかし、この場合、パッケージは Maya がアクセスできるパスの中にあるので、 Python の from メソッドを使って読み込むことができます。次のようにします：

```python
from package import my_module as module
reload(module)
module.makeCube()
```

ここでは、パッケージからモジュールをインポートし、Maya インタプリタが最新のモジュールと同期していることを確認するためにモジュールをリロードしてから、関数を実行しています。

関数呼び出しがモジュール内にある場合は、スクリプトをインポートしてリロードすれば十分です。しかし、関数を呼び出すタイミングを制御したい場合や、複数の関数がある場合にどの関数を呼び出すかを決定したい場合があります。

また、モジュールにはいくつかのクラスがあり、単純にMainClassのクラスをインスタンス化したい場合もあるでしょう。

関数呼び出しの周りにいくつかの安全チェックを追加することもできます。

```python
from package import my_module as module
import maya.OpenMaya as om
 
 
# Attempts to reload the module & run a function
try:
    reload(module)
    om.MGlobal.displayInfo('Module Reloaded')
    module.makeCube()
except NameError:
    om.MGlobal.displayWarning('Incorrect module name!')
except ImportError:
    om.MGlobal.displayWarning('Failed to import module!')
```

または、モジュールのリロードが成功したかどうかをチェックする別の関数を書く：

```python
from package import my_module as module
import maya.OpenMaya as om
 
 
# Reload the module & run a function
def RunExternalFunction():
    if reload(module):
        om.MGlobal.displayInfo('Module Reloaded')
        module.makeCube()
    else:
        om.MGlobal.displayWarning('Failed to execute function')
 
RunExternalFunction()
```

ここでは、OpenMaya API を利用して、インポートが失敗した場合にステータスバーに情報を表示するようにしています。

これは単純なことなのでやりすぎですが、有用な情報を提供できればと思います。