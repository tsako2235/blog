---
title: "20190109_Hyper V+Linux[Ubunts]開発環境の構築"
date: 2019-01-09T16:43:53+09:00
draft: false
---

# Hyper V+Linux[Ubunts]開発環境の構築

## 目的

現在（2019-01-09）開発環境について以下構成のローカル環境で行っているが、  
正直なところ雑多なツールとコードが繁茂しつつある

* Windows 10 Pro + VSCode + GitHub

跡から取捨選択する際、まっさらな環境と不要になった際、即捨てられる環境が欲しいとこ  
ということで、せっかくWin 10 Pro なのでHyperV使えるじゃん、ならHyperV+Ubuntsでいいよね  
ということで早速導入してみる

実はParallels入れてあるMacはあるんだけど、いかんせんMacBookProでな、重いんだ…

## 事前準備

### Ubuntsイメージを入手

適当なUbuntsイメージを…LTS、うーんバージョンは固定にしたいような気もするが  
まぁ、Linuxはまぁいいでしょう、そこまで気にしなくてということでUbuntu 18.04.1 LTS版をダウンロード

### ダウンロードURL
https://www.ubuntu.com/download/desktop

### Hyper-Vの準備

一応systeminfoで確認  

    PS C:\WINDOWS\system32> systeminfo
    .
    .
    Hyper-V の要件:         VM モニター モード拡張機能: はい
                            ファームウェアで仮想化が有効になっています: はい
                            第 2 レベルのアドレス変換: はい
                            データ実行防止が使用できます: はい

OK、次アプリケーションを適宜有効化  
「dism /online /Enable-Feature /FeatureName:XX」（XXは機能名）  

    PS C:\WINDOWS\system32> dism /online /Get-Features

    展開イメージのサービスと管理ツール
    バージョン: 10.0.17134.1

    イメージのバージョン: 10.0.17134.472

    パッケージの機能の一覧 : Microsoft-Windows-Foundation-Package~31bf3856ad364e35~amd64~~10.0.17134.1

    .
    .

    機能名 : Microsoft-Hyper-V-All
    状態 : 有効

    機能名 : Microsoft-Hyper-V
    状態 : 有効

    機能名 : Microsoft-Hyper-V-Tools-All
    状態 : 有効

    機能名 : Microsoft-Hyper-V-Management-PowerShell
    状態 : 有効

    機能名 : Microsoft-Hyper-V-Hypervisor
    状態 : 有効

    機能名 : Microsoft-Hyper-V-Services
    状態 : 有効

    機能名 : Microsoft-Hyper-V-Management-Clients
    状態 : 有効

    .
    .

    操作は正常に完了しました。
    PS C:\WINDOWS\system32>

## Hyper-Vの構築

### 仮想マシンの新規作成

管理ツールからHyper-Vマネージャを起動して、  
左パネルのアイコン右クリック > 新規  

...IISチックなGUIだこと

メモリの割当まで進んだ、うーん、Ubuntuの推奨スペックは以下

>2 GHz以上のデュアルコアプロセッサ  
>2 GBのシステムメモリ  
>25 GBのハードドライブ空き容量  
>インストーラメディア用のDVDドライブまたはUSBポート  
>インターネットアクセスは便利です

で、とりあえず今欲しい環境は以下2点

* VSCode を動作させるGUI環境
* Node.js及びReactの実行環境

4Gありゃええじゃろ…うん
ネットワークは規定のスイッチで

ハード32Gでいいでしょ
インストールオプションで先ほど準備したUbuntuのイメージを  
セットして、要約を確認して、OK

## Ubuntuセットアップ

### の前に

Ubuntuインストール後、起動しないそうなので  
セキュアブートを無効に、またローカルからファイルコピペしたいので  
ゲストサービスのチェックを有効に  

### インストール

GUIに従って適当に実施でいい

### 起動後の初期設定

うーん、サーフェスちゃんだと重い、CUIモードをデフォルトにしておこう
折角だけどVSCodeでの開発はあきらめてvimでええかもしれん

## 結論

ガチャガチャやってみたけど、結局のところこのマシンでの  
運用はコア１割り振りしかできないなどの理由により、  
難しいという結論にたっしてしまいました  

WLS (Windows Subsystem for Linux)で何とかやりくりするしかなさそう  
あとはやっぱり色々整理しつつやるしかないすね…