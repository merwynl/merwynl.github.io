---
title: "TKinterとPythonによるフォルダ構造の自動化"
tags: [code, Auto, Automation, Py, python]
category: [code]
lang: ja
ref: posts
---

私は、さまざまなアプリケーションや分野に基づいてフォルダ構造を整理するのが好きです。プロジェクト構造がどのようなものかを明確に把握することで、ファイルやアセットが行方不明になることがなくなります。私はパスとディレクトリを少しいじっていて、これはPythonを使ってこれらのスキルのいくつかに少し取り組む良い機会だと思いました。このスクリプトのゴールは、必ずしも最適ではないが、素早くシンプルなものを書くことだった。

この短いスクリプトは、ユーザーが指定したディレクトリにあるフォルダの階層を生成することができる。プロジェクト構造を生成するディレクトリのクエリにtkinterを活用しており、より素早くアクセスするためにbatファイルから実行することができる。

```python
import os
import tkinter as tk
from tkinter import filedialog
 
# Initializes tKinter widget window
root = tk.Tk()
root.withdraw()
 
# Ask the user for a directory
file_path = filedialog.askdirectory()
 
# List of parent folders
folders = ["houdini", "renders", "maya", "meshes", "references", "textures", "unreal"]
 
# Path to parent folders
houdini_dir = os.path.join((file_path + "/" + folders[0]))
textures_dir = os.path.join((file_path + "/" + folders[5]))
renders_dir = os.path.join((file_path + "/" + folders[1]))
 
# Sub-directories
houdini_folders = ["geo", "hda", "scripts", "tex"]
texture_folders = ["designer", "painter", "output", "mixer", "psd"]
renders_folder = ["wips", "finals", "marmoset"]
 
def make_project_dir():
    # Topline folders with sub-directories
    houdini_dir = os.path.join((file_path + "/" + folders[0]))
    textures_dir = os.path.join((file_path + "/" + folders[5]))
    renders_dir = os.path.join((file_path + "/" + folders[1]))
 
    # Create primary folders
    for f in folders:
        folder_path = os.path.join((file_path + "/" + f))
        try:
            os.mkdir(folder_path)
            print("Creating " + f + " folders...")
        except FileExistsError:
            print("Folder already exists!")
 
    # Create houdini sub-directories
    for hou in houdini_folders:
        houdini_sub_dir = os.path.join((houdini_dir + "/" + hou))
        try:
            os.mkdir(houdini_sub_dir)
            print("Creating " + hou + " folders...")
        except FileExistsError:
            print("Folder already exists!")
 
    # Create Texture sub-directories
    for tex in texture_folders:
        textures_sub_dir = os.path.join((textures_dir + "/" + tex))
        try:
            os.mkdir(textures_sub_dir)
            print("Creating " + tex + " folders...")
        except FileExistsError:
            print("Folder already exists!")
 
    # Create Render sub-directories
    for out in render_folders:
        renders_sub_dir = os.path.join((renders_dir + "/" + out))
        try:
            os.mkdir(renders_sub_dir)
            print("Creating " + out + " folders...")
        except FileExistsError:
            print("Folder already exists!")
 
 
make_project_dir()
```

テンプレート・フォルダー構造を特注の場所に置くこともできたが、それでは面白くない。また、簡単に置き忘れてしまう可能性もある。また、何らかの理由でそのテンプレートの複製があった場合、どれが古いものなのかを見つけなければならない。過去の失敗の数々が呼び起こされる。

Let’s break it down a bit:

```python
root = tk.Tk()
root.withdraw()
```

メイン・ウィンドウを描画するtKinterを初期化しました。しかし、filedialogクラスをインスタンス化するので、そのウィジェットは使いたくない。つまり、ウィジェット・ウィンドウを隠す方法が必要です。そこでwithdraw()関数の登場です。その反対はdeiconify()で、以前に非表示にしたウィジェットを表示できます。

```python
file_path = filedialog.askdirectory()
```
次にしたいことは、階層を生成するルートの場所を問い合わせることだ。

```python
folders = ["houdini", "renders", "maya", "meshes", "references", "textures", "unreal"]
houdini_folders = ["geo", "hda", "scripts", "tex"]
texture_folders = ["designer", "painter", "output", "mixer", "psd"]
renders_folder = ["wips", "finals", "marmoset"]
```

次に、作成したいさまざまなフォルダーとサブ・ディレクトリーがある。サブディレクトリのコレクションごとに別々のリストを持つことは、その時点では最も理にかなっているように思えたが、新しいアイテムが必要になるたびにコードをさらに適応させる必要があるため、オプションを拡張するのが少し難しくなる。

これはまた、この上に派手なUIを投げれば、プリセットとしてこれらを使用し、さらにこれらのサブディレクトリの各リストを拡張する権限をユーザーに与えることができます。

```python
# Path to parent folders
houdini_dir = os.path.join((file_path + "/" + folders[0]))
textures_dir = os.path.join((file_path + "/" + folders[5]))
renders_dir = os.path.join((file_path + "/" + folders[1]))
```

サブ・ディレクトリーも同じ状況だ。これは2段階で行う。まず、サブディレクトリを含むであろう親フォルダそれぞれに変数とパスを設定する。次に、関連するフォルダーごとに一連のリストを作成する。これらのリストによって、第3レベルのディレクトリが決定される。

```python
# Sub-directories
houdini_folders = ["geo", "hda", "scripts", "tex"]
texture_folders = ["designer", "painter", "output", "mixer", "psd"]
render_folders = ["wips", "finals", "marmoset"]
```
インデックスの位置が変われば、サブディレクトリは間違った場所に置かれることになり、とても悲しいことになるからだ。また、前述したように、これらのディレクトリを拡張する可能性をさらに制限してしまう。

一連の固定リストではなく、インポートされた定数ファイルやJSON辞書を使って、これらのリストがすべて決定論的に生成されれば、より良いだろう。

```python
def make_project_dir():
 
    # Create primary folders
    for f in folders:
        folder_path = os.path.join((file_path + "/" + f))
        try:
            os.mkdir(folder_path)
            print("Creating " + f + " folders...")
        except FileExistsError:
            print("Folder already exists!")
```

次にメイン関数本体が来るが、これはほとんど同じコードで、異なるディレクトリごとに2つのレベルで繰り返される。クラス内にラップしてインスタンス化することで、繰り返しを減らすことができる。

アイディアは単純明快だ。リストの各項目について、サブ・ディレクトリのパスを設定し、そのリストの各項目について、tryとexceptでそれをラップして、フォルダがすでに存在するかどうかをキャッチする。すでに存在する場合は何もしない。

しかし、このスクリプトが考慮に入れていないことのひとつは、ユーザーがプロセスから離脱した場合だ。ディレクトリの入力を求められたときにキャンセルを押してしまうと、フォルダはドライブルートに作成されたままになってしまう。

理想的には、スクリプトが確認ボックスを表示するか、ユーザーがキャンセルを押したかどうかを検出する方法を見つけることだ。

```python
@echo off
python %~dp0\project_structure.py %*
pause
```

この最後のスニペットは、スクリプトを呼び出してプロセスを実行するために使われる。このbatファイルが動作するためには、ファイルはpythonファイルと同じ場所になければなりません。要するに、%~dp0はそのbatファイルのパスに検索を展開します。これはバッチファイルをよりポータブルでアクセスしやすくする本当に便利な方法です。

最後に、DirectFolderやListaryのようなクイックアクセスツールからこのバッチファイルを呼び出して、キーストロークにこのバッチファイルをバインドすることができる。結局のところ、これが私がこのスクリプトで実現したかったことであり、このスクリプトは、改善すべき点は多々あるものの、想定したとおりに仕上がっている。