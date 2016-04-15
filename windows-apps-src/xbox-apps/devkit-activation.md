---
title: Xbox One 開発者モードのアクティブ化
description: 開発者モードをアクティブ化して、リテール モードと開発者モードを切り替えることができるようにする方法を説明します。
area: Xbox
---

# Xbox One 開発者モードのアクティブ化

* [開発者モードの動作](#how-developer-mode-works)
* [製品版の Xbox One 本体で開発者モードをアクティブにする](#activate-developer-mode-on-your-retail-xbox-one-console)  
* [リテール モードと開発者モードを切り替える](#switch-between-retail-and-developer-mode)

## 開発者モードの動作
Xbox One には、*リテール* モード (1) と*開発者*モード (2) の 2 つのモードがあります。 リテール モードは、Xbox One 本体のユーザーが本体を使うときのモードです。ユーザーとしてゲームをプレイしたり、アプリを実行したりできます。 開発者モードでは、本体用のソフトウェアを開発することができますが、製品版のゲームをプレイしたり、製品版のアプリを実行したりすることはできません。
開発者モードは、製品版のすべての Xbox One 本体で有効にできます。 開発者モードを有効にした後は、リテール モード (2a) と開発者モード (2b) を相互に切り替えることができます。

> **重要 **&nbsp;&nbsp;Xbox One で開発者モードをアクティブ化すると、開発者プレビュー リリース向けの Xbox システムの更新をオプト インすることになります。これらのプレビュー リリースには、実験的な初期のプレリリース ソフトウェアが含まれています。 このため、一部の人気ゲームやアプリが想定どおりに動作しなかったり、クラッシュやデータの損失が発生したりする可能性があります。 開発者プレビューへの参加を終了する場合は、本体が出荷時の設定にリセットされるため、ゲーム、アプリ、コンテンツをすべて再インストールする必要があります。 

> **注**&nbsp;&nbsp;Xbox One Beta プログラムのような既存のプレビュー プログラムに参加している場合は、Xbox One で開発者モードをアクティブ化することはできません。 Xbox プレビュー ダッシュボード アプリを使うと、既存のプレビュー プログラムへの参加を終了できます。 

![Xbox One のモード](images/dev-mode-flow.png)

## 製品版の Xbox One 本体で開発者モードをアクティブにする

1.  Xbox One 本体を起動します。

2.  Xbox One ストアから、開発者モードのアクティブ化用アプリを検索してインストールします。  
    ![](images/activation-store-search.png)

3.  **[マイ コレクション]** の **[アプリ]** に移動します。

    ![開発者モードのアクティブ化用アプリ](images/activation-step-3.png)
4. 開発者モードのアクティブ化用アプリを開きます。    
    
    > **注**&nbsp;&nbsp;免責事項をよくお読みください。 Xbox を開発用にアクティブ化すると、初期のプレリリース ビルドを取得することになります。 ゲームやアプリを実行するには、リテール モードに切り替える必要があります。 サイドローディングしたアプリは、開発者モードでのみ動作します。

5.  開発者モードのアクティブ化用アプリに表示されたコードを書き留めます。  

    ![アクティブ化手順 5](images/activation-step-5.png)  
    
6.  [developer.microsoft.com/xboxactivate](https://developer.microsoft.com/xboxactivate) にアクセスします。
7.  デベロッパー センター アカウントを使ってデベロッパー センターにサインインします。  
8.  開発者モードのアクティブ化用アプリに表示されたアクティブ化コードを入力します。   
   
     > **注**&nbsp;&nbsp;アカウントに関連付けられているアクティブ化の数には制限があります。 開発者モードがアクティブになると、アカウントに関連付けられているアクティブ化の 1 つが使われたことを示す通知がデベロッパー センターに表示されます。 
    
    ![アクティブ化手順 8](images/activation-step-8.png)    
    
9.  **[Agree and activate]** (同意してアクティブ化) をクリックします。 ページの再読み込みが行われ、デバイスが表に追加されます。  
10. アクティブ化コードを入力すると、アクティブ化プロセスの進行状況が表示されます。  
11. アクティブ化が完了したら、必要なプレビュー ビルドに本体が更新されるまで待機する必要があります。 これには数時間かかることがあります。しばらくお待ちください。  

    ![アクティブ化手順 11](images/activation-step-11.png)    
    
12. アクティブ化の完了後、開発者モードのアクティブ化用アプリを開き、**[Switch and restart]** (切り替えて再起動) をクリックして、開発者モードに移行します。 これは通常の再起動よりも時間がかかります。  

    ![アクティブ化手順 12](images/activation-step-12.png)   
    

    
## リテール モードと開発者モードを切り替える
本体で開発者モードを有効にした後、リテール モードと開発者モードを切り替えるには、**Dev Home** を使います。 **Dev Home** の起動と使用について詳しくは、「[Xbox One ツールの概要](introduction-to-xbox-tools.md)」をご覧ください。

* リテール モードに切り替えるには、**Dev Home** を使って **[Leave developer mode]** (開発者モードの終了) をクリックします。 これにより、本体がリテール モードで再起動します。    

  ![アクティブ化手順 13](images/activation-step-13.png)  
  
* 開発者モードに切り替えるには、開発者モードのアクティブ化用アプリを使います。 アプリを開き、**[Switch and restart]** (切り替えて再起動) をクリックします。 これにより、本体が開発者モードで再起動します。  

  ![アクティブ化手順 14](images/activation-step-12.png)  

## 参照
- [Xbox One 開発者モードの非アクティブ化](devkit-deactivation.md)
- [Xbox One の UWP](index.md)


<!--HONumber=Mar16_HO5-->

