---
title: "Pyside 対 PySide2"
tags: [code, Auto, Automation, Py, python]
category: [code]
lang: ja
ref: posts
---

# 1. PySide vs PySide2

PySide

- Python 2.7-2.8をサポート
- Qt4までサポート

PySide2：

- Python 3.7-3.10をサポート
- Qt5に対応

PySide2 (Qt for Python) と PyQt5 の違い：

- ライセンスの違い
- Qt for PythonはQtのPythonバインディングを提供し、Qt5のAPIを利用可能にします。
- 開発者はPySide 2モジュールを使ってQtの潜在能力をフルに活用することができます。
- PySide2 は、QtCore や QtGui など、個々の Qt モジュールへのアクセスを提供します。

PySide 2(Qt for Python)：

- LGPL v3

PyQt5：

- GNU GPL v3 でリリースされています。

# 2. Python 用 Qt (PySide2) モジュール

Qt Core：

- コアメモリ機能とクラスを提供

Qt GUI：

- Qt GuiでQtCoreを拡張する
- インターフェースの作成

Qt Widget：

- アプリケーション、ラベル、プッシュボタンなどのウィジェットの作成

Qt QML：

- マークアップ言語
- メインデザインとロジックを分離

Qt Quick：

- QT クイックと Qt アプリケーションを組み込むためのクラスを提供します。

Qt Quick ウィジェット：

- Qt Quick アプリケーション用のウィジェットを作成

データの視覚化： チャート、ダイアグラム、アニメーション、これらの要素を UI に含めるための大量のクラス
Qt バーチャート
Qr データビジュアライゼーション

