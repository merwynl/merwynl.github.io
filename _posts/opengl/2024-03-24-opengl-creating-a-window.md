---
title: "OpenGL #1: Creating a Window | OpenGL #1: 入門　ー"
tags: [glsl, code, opengl, 基本, 🔰初心者]
category: [shaders, gamedev, ゲーム開発]
toc: true
---

# About this series 
For some time now I have been intending to come to terms with understanding the ins and outs of OpenGL and GLSL and its many quirks and intricacies. This all began many moons ago when I was first fidling my way through shading languages & graphics API's but I could not or *had* not afforded the time or headspace to fully dive down the rabbit hole. The goal of this series is to serve as a place to document my journey as I stumble my way through learning its fundamentals and figure things out in creating OpenGL applications and graphics programming. 

I'll be primarily relying on the excellent [https://learnopengl.com](https://learnopengl.com) by Joey De Vries as the primary resource though there may be times where other resources are referenced. Those will be linked as I work my way through the many challenges and roadblocks that I'll inevitably come acrosss. Let's get started!

## Required Programs and files

- Some sort of IDE or code editor with Intellisense code completion and basic debugging. Some choices:
    - [JetBrains Rider](https://www.jetbrains.com/rider/)
    - [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/vs/older-downloads/)
- [CMake](https://cmake.org/download/)
- [GLFW 3.3 Source Package](https://github.com/glfw/glfw/tree/3.3-stable)
- [GLAD1](https://glad.dav1d.de/)

I'm sticking with Rider as my preferred IDE of choice as I find its minimalist interface and integration with off the shelf engines easier to work with. 


## Build GLFW


## Compile GLFW Libraries 


## Resource Preparation


## Creating an Empty Project/Solution


## Linking


## Generating GLAD file 


## Referencing GLAD


## Creating main function


## Initializing GLFW


## Creating a Window


## Initializing GLAD


## Creating frame buffer & glViewport


## Some basic error checks


## Running the application

---

# このシリーズについて 
ここしばらくの間、私はOpenGLとGLSLの内部と外部、そしてその多くの癖と複雑さを理解しようと思っていました。これは、私がシェーディング言語とグラフィックスAPIを初めていじくりまわしていた何ヶ月も前に始まったことなのですが、ウサギの穴に完全に飛び込む時間や余裕を持つことができなかったし、持ってもいなかったのです。このシリーズのゴールは、私がOpenGLアプリケーションとグラフィックス・プログラミングを作成する上で、その基礎を学び、物事を理解する中でつまずいた私の旅を記録する場所として機能することです。

主なリソースとして、Joey De Vriesによる素晴らしい[https://learnopengl.com](https://learnopengl.com)に主に頼るつもりですが、他のリソースが参照されることもあるかもしれません。しかし、他のリソースが参照されることもあるでしょう。それらのリソースは、私が必然的に出くわすであろう多くの課題や障害に対処する過程でリンクされるでしょう。始めよう！

## 必要なプログラムとファイル

- Intellisenseによるコード補完と基本的なデバッグが可能な、何らかのIDEまたはコードエディタ。いくつかの選択肢があります：
    - [JetBrains Rider](https://www.jetbrains.com/rider/)
    - [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/vs/older-downloads/)
- [CMake](https://cmake.org/download/)
- [GLFW 3.3 ソースパッケージ](https://github.com/glfw/glfw/tree/3.3-stable)
- [GLAD1](https://glad.dav1d.de/)

Riderのミニマルなインターフェースと既製のエンジンとの統合が作業しやすいので、私はRiderを好みのIDEとして選んでいる。

## GLFWをビルドする


## GLFWライブラリのコンパイル 


## リソースの準備


## 空のプロジェクト/ソリューションの作成


## リンク


## GLADファイルの生成 


## GLADの参照


## メイン関数の作成


## GLFWの初期化


## ウィンドウの作成


## GLADの初期化


## フレームバッファとglViewportの作成


## いくつかの基本的なエラーチェック


## アプリケーションの実行