---
title: SmartMatch マッチメイキング
author: KevinAsgari
description: マルチプレイヤー ゲームでプレイヤーをマッチングする Xbox Live SmartMatch マッチメイキング サービスについて説明します。
ms.assetid: ba0c1ecb-e928-4e86-9162-8cb456b697ff
ms.author: kevinasg
ms.date: 04/04/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: Xbox Live, Xbox, ゲーム, UWP, Windows 10, Xbox One, マルチプレイヤー, マッチメイキング, SmartMatch
ms.localizationpriority: low
ms.openlocfilehash: 5214b85ca7a0e4f8460044b34279895027d0b8d4
ms.sourcegitcommit: 01760b73fa8cdb423a9aa1f63e72e70647d8f6ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/24/2018
---
# <a name="smartmatch-matchmaking"></a>SmartMatch マッチメイキング

この記事は次のセクションで構成されています。
* SmartMatch の概要
* SmartMatch のランタイム操作
* タイトルの SmartMatch の構成
* SmartMatch 構成時のチーム ルールの定義
* ターゲット セッションの初期化と QoS

## <a name="introduction-to-smartmatch"></a>SmartMatch の概要

XSAPI は、[Multiplayer Manager API](../multiplayer-manager/multiplayer-manager-api-overview.md) によってラップされている、SmartMatch と呼ばれるマッチメイキング サービスを提供します。  API の高度な使用方法については「**MatchmakingService クラス**」で解説していますが、Multiplayer Manager を使用して実装できないマッチメイキングのシナリオがある場合は、担当 DAM を介してフィードバックをご提供ください。  どちらの API を使用するかにかかわらず、この記事の概念情報が適用されます。

SmartMatch マッチメイキングは、プレイヤーをユーザー情報および一緒にプレイしたいユーザーのマッチメイキング要求に基づいてグループ化します。 マッチメイキングはサーバー ベースであり、ユーザーはサービスに要求を送信し、後からマッチが見つかったときに通知を受けます。 Xbox One 用のタイトルをビルドするとき、「[SmartMatch マッチメイキングの使用](using-smartmatch-matchmaking.md)」に説明されているように、SmartMatch を使用できます。 または、「[独自のマッチメイキング サービスの使用](https://developer.microsoft.com/en-us/games/xbox/docs/xboxlive/xbox-live-partners/multiplayer-and-networking/using-your-own-matchmaking-service)」に説明されているように、独自のマッチメイキング サービスを使用できます。 このリンクにアクセスするには、Xbox Live 開発に対して有効にされている Microsoft デベロッパー センター アカウントが必要なことに注意してください。

### <a name="about-smartmatch"></a>SmartMatch について

マッチメイキング サービスは、MPSD を緊密に連携してマッチメイキングを簡素化します。 それにより、タイトルは、ユーザーがタイトル内でシングル プレイヤーでプレイしているときなど、バックグラウンドでマッチメイキングを容易に行うことができます。

マッチメイキングに参加したい個人またはグループは、マッチ チケット セッションを作成し、マッチメイキング サービスを要求してマッチを設定する他のプレイヤーを検索します。 これにより、一定期間マッチメイキング サービス内に常駐する一時的な "マッチ チケット" が作成されます。

マッチメイキング サービスは、構成、プレイヤーごとに格納される統計情報、マッチ要求時に指定される追加の情報に基づいて、一緒にプレイするセッションを選択します。 次に、サービスは、マッチしたすべてのプレイヤーを含むマッチ ターゲット セッションを作成し、ユーザーのタイトルにマッチを通知します。

ターゲット セッションの準備ができると、タイトルは QoS チェックを実行してグループが一緒にプレイできることを確認し、何も問題ない場合、プレイを開始します。 QoS プロセスおよびマッチメイキングされたゲーム プレイ中、タイトルは、MPSD 内でセッション状態を最新の状態に保ち、セッションの変更に関する通知を MPSD から受信します。 こうした変更には、ユーザーの入退出、セッション アービターの変更が含まれます。


### <a name="match-ticket-session"></a>マッチ チケット セッション

マッチ チケット セッションは、マッチを行うプレイヤーのクライアントを表します。 ゲームに基づいて、ロビーに一緒にいる見知らぬユーザーのグループに基づいて、または他のタイトル固有のプレイヤーのグループに基づいて作成されます。 チケット セッションは、追加のプレイヤーを探している既に進行中のゲーム セッションの場合もあります。


### <a name="match-ticket"></a>マッチ チケット

マッチメイキングにチケット セッションを送信するとマッチ チケットが作成され、マッチ チケットはマッチメイキングの試行を追跡します。 ゲーム マップ、プレイヤー レベルなどのチケット内の属性は、チケット セッション内のプレイヤーの属性と共に、マッチを判断するために使用されます。
#### <a name="hoppers"></a>ホッパー

ホッパーは、マッチ チケットが集められる論理的な場所です。 同じホッパーの内部にあるチケットのみがマッチング可能です。 タイトルには複数のホッパーを含めることができます。 たとえば、タイトルでは、プレイヤーのスキルがマッチングに最も重要な項目であるホッパーを作成できます。 同じダウンロード可能なコンテンツを購入している場合のみプレイヤーがマッチされる、別のホッパーを使用できます。


#### <a name="hopper-rules"></a>ホッパー ルール

ホッパー ルールは、グループ化するプレイヤーを決定するためにマッチメイキング サービスが使用する基準の定義を提供します。 以下の 2 種類のルールがあります。   必須ルール - マッチ チケットの互換性認定のために満たされる必要があります。
-   推奨ルール -- ルールに一致するマッチ チケットは、そうでないマッチ チケットよりも優先されます。

上記の各カテゴリー内に複数の種類のルールがあります。 詳細については、「**SmartMatch のランタイム操作**」のランタイム操作の構成情報を参照してください。


### <a name="match-target-session"></a>マッチ ターゲット セッション

マッチしたグループが見つかったら、サービスではマッチ ターゲット セッションが作成され、一緒にマッチされたチケット セッションのすべてのプレイヤー用の場所が予約されます。


## <a name="smartmatch-runtime-operations"></a>SmartMatch のランタイム操作



| 注意                                                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------------------|
| タイトルで SmartMatch マッチメイキングを使用する方法については、「[SmartMatch マッチメイキングの使用](using-smartmatch-matchmaking.md)」を参照してください。 |


### <a name="creating-a-match-ticket-session-and-a-match-ticket"></a>マッチ チケット セッションとマッチ チケットの作成

マッチメイキングの "スカウト" として指定されたクライアントは、マッチ チケット セッションを設定して、マッチメイキングに参加するプレイヤーのグループを表します。 このグループ内のすべてのプレイヤーが MultiplayerSession.Join メソッドを使用してセッションに参加します。 セッションにプレイヤーが設定されると、タイトルはセッションを MatchmakingService.CreateMatchTicketAsync メソッドを使用してマッチメイキング サービスに送信し、セッションを表すマッチ チケットが作成されます。

| 注意                                                                                                                                                        |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SmartMatch サービスは、CreateMatchTicketAsync 操作中にチケット セッションの /servers/matchmaking/properties/system/status フィールドを "Searching" に更新します。 |

マッチ チケット作成メソッドからの応答は CreateMatchTicketResponse オブジェクトです。 この応答には、マッチ チケット ID、チケットの削除によってマッチメイキングをキャンセルするために使用できる GUID が含まれます。 さらに、プレイヤーの期待の設定で使用される、ホッパーの平均待機時間が応答に含まれます。

| 注意                                                                                                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 保持する必要がある特定のゲーム統計情報データがない限り、CreateMatchTicketAsync を呼び出すときにタイトルで PreserveSessionMode.Never 値を使用することをお勧めします。 PreserveSessionMode.Never を使用すると、マッチメイキングが高速になり、ゲームの検索ではなくゲームのホスティングのためのユーザー インターフェイス オプションを用意する必要がなくなります。 |


### <a name="setting-matchmaking-attributes-on-the-session-and-players"></a>セッションおよびプレイヤーでのマッチメイキング属性の設定

チケット セッションを送信するときに、タイトルは、マッチメイキング サービスがセッションを他のセッションとグループ化するために使用するセッションおよびプレイヤーの属性を設定します。 属性は、チケット レベルまたはメンバーごとのレベルで指定できます。


### <a name="setting-matchmaking-attributes-at-the-match-ticket-level"></a>マッチ チケット レベルでのマッチメイキング属性の設定

タイトルは、MatchmakingService.CreateMatchTicketAsync メソッドの ticketAttributesJson パラメーターで、マッチ チケット レベルでの属性を送信します。 チケット レベルで指定された属性は、メンバーごとのレベルで指定された同じ属性をオーバーライドします。


#### <a name="setting-matchmaking-attributes-at-the-per-member-level"></a>メンバーごとのレベルでのマッチメイキング属性の設定

タイトルは、マッチ チケット セッション内の各メンバーでメンバーごとの属性を指定します。 これらは、MultiplayerSession.SetCurrentUserMemberCustomPropertyJson メソッドを呼び出し、プロパティ名 "matchAttrs" を使用して設定されます。 この呼び出しは、属性をチケット セッション内の各プレイヤーの /members/{index}/properties/custom/matchAttrs フィールドに配置します。

マッチメイキング プロセスは、メンバーごとの各属性を、ホッパーの XDP 構成 UI でその属性に対して指定した均一化メソッドに基づいて、単一のチケット レベルの属性に均一化します。


### <a name="making-the-match"></a>マッチの実行

設定されたチケット セッションとマッチ チケットを使用して、マッチメイキング サービスは、表されたチケット セッションを他のグループを表す他のチケット セッションとマッチさせ、マッチ ターゲット セッションを作成または識別します。 また、サービスは、ターゲット セッションでマッチされたプレイヤーの予約を作成し、チケット セッションをマッチ済みとしてマークします。 MPSD は、チケット セッションのこの変更をタイトルに通知します。

次に、タイトルは十分なプレイヤーが現れたことを確認するためにターゲット セッションを初期化し、サービスの品質 (QoS) チェックを実行してプレイヤーが互いに正しく接続できることを確認する必要があります。 初期化や QoS が失敗した場合、タイトルは、別のグループを見つけることができるよう、マッチメイキングに再送信するようにチケット セッションをマークします。 このプロセスの詳細については、「**ターゲット セッションの初期化と QoS**」を参照してください。

マッチ アクティビティ中、以下の変更がセッションの JSON オブジェクトに対して行われます。

-   /servers/matchmaking/properties/system/status フィールドが "found" に設定されます。
-   /servers/matchmaking/properties/system/targetSessionRef フィールドがターゲット セッションに設定されます。
-   各チケット セッションの /members/{index}/properties/custom/matchAttrs フィールドが /members/{index}/constants/custom/matchmakingResult/playerAttrs フィールドにコピーされます。
-   各プレイヤーについて、チケット属性がマッチ チケット内の ticketAttributes フィールドから /members/{index}/constants/custom/matchmakingResult/ticketAttrs フィールドにコピーされます。


### <a name="maintaining-the-match-ticket"></a>マッチ チケットの維持

マッチメイキング サービスは、マッチ チケットがセッションに対して作成されたときのチケット セッションのスナップショットを使用します。 したがって、プレイヤーがチケット セッションに参加した場合やマッチ チケット セッションを抜けた場合、タイトルはマッチメイキング サービスを使用してマッチ チケットを削除し作成しなおす必要があります。


### <a name="filling-spots-in-an-in-progress-game-session"></a>進行中のゲーム セッションでのプレイヤーの補充

タイトルは、既存のゲーム セッションをマッチ チケット セッションとして再利用して、既に進行中のゲームに参加するプレイヤーを見つけたり、ラウンドが完了して一部のプレイヤーが抜けた後でゲーム セッションのプレイヤーを補充したりすることができます。 このプロセスは "バックフィル" と呼ばれています。

バックフィルを実行する方法の 1 つは、preserveSession パラメーターを PreserveSessionMode.Always に設定して **MatchmakingService.CreateMatchTicketAsync メソッド**を呼び出し、進行中のセッションを "保持" するマッチ チケットを作成することです。 マッチメイキング サービスは、既存のセッションがマッチメイキング プロセス全体を通じて保持され、結果としてターゲット セッションになるようにします。

このパターンには潜在的な欠点があります。preserveSession が Always に設定された 2 つのセッションを結合することができないため、これらのセッションは互いにマッチできません。 これにより、バックフィル マッチメイキングが非常に低速になる可能性があります。 このシナリオを回避するために、タイトルでは、ゲーム状態の保持を必要とする場合のみ PreserveSessionMode.Always を使用するようにしてください。 それ以外の場合は、PreserveSessionMode.Never を設定し、マッチが見つかったときにプレイヤーを新しい targetSession に移行します。


### <a name="deleting-the-match-ticket"></a>マッチ チケットの削除

マッチ チケットを削除するには、タイトルで **MatchmakingService.DeleteMatchTicketAsync メソッド**を呼び出します。 チケットの削除時、マッチメイキング サービスは以下を行います。

1.  チケット セッションでユーザーのマッチメイキングを停止します。
2.  チケット セッションの /servers/matchmaking/properties/system/status フィールドを "canceled" に更新します。


### <a name="matchmaking-for-games-using-xbox-live-compute"></a>Xbox Live Compute を使用したゲームのマッチメイキング

次の例は、Live Compute サービスを使用した高レベルのマッチメイキングを示しています。 同様の方法を、サード パーティー リソースにホストされているゲームに適用できます。

1.  'スカウト' クライアントは、グループを表すためのチケット セッションを作成します。 このセッションには、候補となるデータセンターのリストが含まれます。このリストは、/constants/system/measurementServerAddresses のセッション構成内にあります。 このリストは、セッション テンプレート (データセンター リストが静的である場合) から取得されるか、Live Compute サービスから受信した後のセッションの作成時にクライアントから取得されます。 このセッションの targetSessionConstants/custom/gameServerPlatform オブジェクトには、gsiSetId、gameVariantId、および maxAllowedPlayers の値も含まれています。
2.  グループに属する他のすべてのクライアントがチケット セッションに参加します。
3.  グループのすべてのメンバーが、チケット セッションの /constants/system オブジェクトの measurementServerAddresses 値をダウンロードします。 次に、各メンバーは、プラットフォーム API を使用して各アドレスに ping を実行して、/members/{index}/properties/system/serverMeasurements で定義される、優先するデータ センターの順序付きリストをセッションにアップロードします。

| 注意                                                                                                                                                                                                                                                                                                                                                                       |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| タイトルは、セッションの measurementServerAddresses 値を **MultiplayerSession.SetMeasurementServerAddresses メソッド**および **MultiplayerSessionConstants.MeasurementServerAddressesJson プロパティ**を使用して設定および取得できます。 |

4.  'スカウト' クライアントは、チケット セッションへの参照を渡して **MatchmakingService.CreateMatchTicketAsync メソッド**を呼び出します。

| 注意                                                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| チケット セッション オブジェクトの定数が一致していない場合、CreateMatchTicket メソッドは失敗する場合があります。 これは、ホッパーに必須ルールを追加し、定数が一致しないプレイヤーのマッチを防止することで回避できます。 |

5.  **MatchTicketDetailsResponse.PreserveSession プロパティ**が Never に設定されている場合、マッチメイキング サービスは各メンバーからのサーバー測定値をチケットの内部表現にコピーしてから、収集した値をチケット用の単一のコレクションに均一化し、"特別な" チケット属性として格納します。
6.  **MatchTicketDetailsResponse.PreserveSession プロパティ**が Always に設定されている場合、サーバー測定値は使用されません。 代わりに、マッチメイキング サービスは、セッションの /properties/system/matchmaking/serverConnectionString 値を、サイズ 1 で遅延ゼロの serverMeasurements コレクションとしてチケットの内部表現にコピーします。
7.  マッチメイキング サービスでは、サーバー測定値コレクションを考慮に入れて、チケット セッションが他のグループを表すその他のチケット セッションとマッチングされます。 同じデータセンターの優先度が高いグループ間でのマッチングが試行されます。
8.  マッチしたグループが見つかったら、マッチメイキング サービスではターゲット セッションが作成または識別され、一緒にマッチされたチケット セッションのすべてのプレイヤーが追加されます。 サービスでは、マッチされたグループの最終的に均一化されたサーバー測定値が /properties/system/serverConnectionStringCandidates に書き込まれます。 次に、ターゲット セッションの新しいメンバーごとに、最初のサーバー測定値が /members/{index}/constants/system/matchmakingResult/serverMeasurements に書き込まれます。
9.  すべてのクライアントは、前述のように、ターゲット セッションで初期化を実行します。 ただし、クライアントは Live Compute に接続するため、接続確認のための QoS を互いに実行しません。
10. 一部またはすべてのクライアントが **GameServerPlatformService.AllocateClusterAsync メソッド**を呼び出します。 最初の呼び出しによって割り当てがトリガーされ、それ以外の呼び出しでは受信確認のみを受け取ります。 このメソッドによって、MPSD からターゲット セッションが取得され、負荷などの Live Compute 固有の情報のみならずターゲット セッション内のデータセンター優先順位に基づいて、データセンターが選択されます。
11. すべてのクライアントがプレイします。

## <a name="configuring-smartmatch-for-your-title"></a>タイトルの SmartMatch の構成


### <a name="configuration-of-smartmatch-matchmaking-runtime-operations"></a>SmartMatch マッチメイキング ランタイム操作の構成

SmartMatch マッチメイキングの構成はすべて、[Xbox デベロッパー ポータル (XDP)](https://xdp.xboxlive.com) を通じて行われます。 構成にはタイトルの [ServiceConfiguration] -&gt; [Multiplayer & Matchmaking] セクションを使用します。


#### <a name="matchmaking-session-template-configuration"></a>マッチメイキング セッション テンプレートの構成

「[SmartMatch マッチメイキング]()」で説明したように、マッチメイキングに関連するセッションには、マッチ チケット セッションとマッチ ターゲット セッションの 2 種類があります。 基本的には、チケット セッションはマッチメイキング サービスへの入力で、ターゲット セッションは出力です。 XDP でセッション テンプレートを構成するときは、セッションの種類ごとにテンプレートを作成する必要があります。

チケット セッションでは、専用テンプレートを使用できます。 または、ゲーム プレイへの使用を意図していないロビー セッションまたは他のセッション用にテンプレートを再利用できます。

| 重要                                                                                      |
|-------------------------------------------------------------------------------------------------------------|
| チケット セッションでは QoS チェックを有効にしてはなりません。また、"ゲームプレイ" 機能でマークしてはなりません。 |

ターゲット セッションでは、マッチメイキングされるゲーム プレイ向けのテンプレートを使用する必要があります。 ゲーム プレイの開始前にピア間の QoS チェックを有効にする設定が含まれている必要があり、"ゲームプレイ" 機能でマークされている必要があります。

XDP UI で、各セッションを 1 つ以上のホッパーにマップできます。各ホッパーには、そのホッパーでセッションがどのようにマッチされるかを決定するルールが含まれます。 詳細については、「マッチメイキングの基本的なホッパー構成」を参照してください。


#### <a name="basic-hopper-configuration-for-matchmaking"></a>マッチメイキングの基本的なホッパー構成

このセクションでは、基本的なホッパー フィールドを構成するのに使用するフィールドを定義します。 この構成の後、「ホッパー ルールの構成」に説明されているように、ホッパー ルールを構成する必要があります。

![](../../images/multiplayer/session_template_hopper_edit.png)


###### <a name="name"></a>Name

セッションをマッチメイキングへ送信するときに使用されるホッパーの名前。 この名前は、マッチ チケットの作成中に **CreateMatchTicketAsync** メソッドへのパラメーターとして渡される値と一致する必要があります。


###### <a name="minmax-group-size"></a>Min/Max Group Size

ホッパー内のセッションから作成されるプレイヤー グループの最小および最大サイズ。 マッチメイキング サービスは、マッチされるグループを、最大グループ サイズまで、可能な限り大きく作成しようとします。 ただし、マッチされるグループは、最小グループ サイズを満たすために十分なプレイヤーを集めることができる場合に作成します。


###### <a name="should-rule-expansion-cycles"></a>Should Rule Expansion Cycles

SHOULD ルールの場合、マッチメイキング サービスは、成功するマッチが見つからない場合、検索領域を増やし、指定されたマッチメイキング ルールを徐々に緩和しようとします。 このプロセスは、[Should Rule Expansion Cycles] フィールドを使用して指定される、複数のサイクルに対して実行されます。 最後の拡張サイクルで SHOULD ルールは削除されるため、チケットのマッチを妨げなくなります。 ただし、複数のチケットが使用可能な場合は、最適なマッチを判断するために引き続き使用されます。 Number と QoS 型のみが、削除される前に拡張されます。 このトピックの「ホッパー ルールの構成」も参照してください。

Should Rule Explansion Cycles 設定の値を増加させると、SHOULD ルール拡張のサイクル数が増えますが、マッチメイキングの時間も増加します。 既定値は 3 で、ほとんどの構成で一般的に十分です。

| 重要                                                                                                                                                                        |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 拡張サイクルは 5 秒の固定間隔で発生します。 最後の拡張サイクルで、すべての "推奨" ルールは、残りのマッチメイキングを試行するときに考慮されなくなります。 |

##### <a name="ranked-hopper"></a>ランク ホッパー
通常、SmartMatch はブロックされているプレイヤーがマッチングされることを防ぎます。 [Ranked Hopper] がチェックされている場合、プレイヤーがこのシステムを使用してよりスキルの高いプレイヤーを回避することを防ぐために、このロジックがバイパスされます。

#### <a name="configuration-of-hopper-rules"></a>ホッパー ルールの構成

このセクションでは、ホッパーのルールを構成するのに使用するフィールドを定義します。

###### <a name="common-rule-fields"></a>Common Rule Fields

このセクションで定義されているフィールドはすべてのホッパー ルールに共通です。

**ルール名**

構成目的でルールに表示されるフレンドリ名。

**ルールの種類**

ルールの種類。 オプションは [MUST] および [SHOULD] です。 マッチメイキングが成功するには、MUST ルールが満たされる必要があります。 成功したマッチを見つけるには、SHOULD ルールを緩和したり削除したりすることができます。 このプロセスの詳細については、「SHOULD ルール拡張の構成」を参照してください。


**データ型**

マッチメイキング ルールの属性のデータ型。 設定可能な値:   [Number]。 単純な 32 ビットの数値を指定します。
-   [String]。 最大 128 文字の Unicode 文字列を指定します。
-   [Collection]。 文字列の配列を指定します。 この値を使用して、ダウンロード コンテンツ (DLC)、チーム メンバーシップ、またはプレイヤーの役割設定を識別します。
-   [Quality of Service]。 マッチメイキングにレイテンシー QoS データを含めるためのカスタム データ型を指定します。 このようなルールは、マッチメイキング ホッパーあたり 1 つだけ使用してください。

| 注意 |
|----------|
| この制限がタイトルで問題となる場合は、デベロッパー アカウント マネージャーに問い合わせてください。 |

-   [Total Value]。 送信されたマッチメイキング値を合計するカスタム データ型を指定します。 この値を使用して、結果として得られる合計を特定の範囲内に収める、または正確な値にすることができます。
-   [Team]。 マッチメイキング要求に含まれるプレイヤーのチームのカスタム データ型を指定します。 この値を使用して、単一のマッチ チケット内のプレイヤーが複数のチームに分散されるのを回避できます。


###### <a name="data-type-specific-rule-fields"></a>データ型に固有のルール フィールド

このセクションでは、一部のデータ型に適用されるが、その他のデータ型には適用されないルールを定義するために使用するフィールドを定義します。 XDP UI は、どのデータ型が特定のルールに適用されるかを明確に示すことができます。

**Allow Wildcards**

マッチ チケットで属性を省略できるかどうかを示す値。 省略される場合、チケットは、この属性の値に関係なく、その他のチケットと互換性を持つようになります。


**Attribute Source**

データ型の値のソース。 使用できるソースは次のとおりです。
- [Title provided]。 データ値は、マッチ チケットで送信されます。
-   [User stat instance]。 データ値は、UserStatistics サービスから自動的に取得されます。


**属性名**

属性値のソースの名前。 マッチ チケット内のプロパティ名またはユーザー統計情報の名前のいずれかです。


**既定値**

マッチメイキング要求に対して値が指定されていない、または使用できない場合の、データ型の既定値。 [Allow Wildcards] フィールドが選択されていて、値が指定されていない場合、既定値は適用されません。


**Weight**

ルールの重要性。 Weight は、マッチメイキングおよびルール拡張中にどのルールを優先するかを示すために使用できます。 Weight の値は正数で、既定では 1 に設定されています。


**Flatten Method**

Number データ型のみ。 マッチを満たすために複数の値がどのように組み合わされるかを示す値。 単一のマッチ チケット内および複数のチケットにわたる異なるプレイヤーの複数の値に適用されます。 設定できる値は次のとおりです。
-  Min/Max。 異なるマッチ チケットからの複数の値の最小または最大値を使用します。
-   Average。 複数のマッチ チケットに含まれている複数の値の平均値を使用します。


**Max Diff**

Number データ型のみ。 ルールを満たすために 2 つの比較される値の間で許容される数値の最大差。 SHOULD ルールの場合、この値はルール拡張の開始点です。


**Set Operation**

Collection データ型のみ。 設定値のグループのマッチ時に実行する操作。 使用できるオプションは次のとおりです。
- [Intersection]。 2 つのコレクションを、それらの交差の量に基づいてマッチさせます。 この設定により、類似または同一のコレクション値になります。
-   [Difference]。 2 つのコレクションを、それらの差の量に基づいてマッチさせます。
-   [Role Preference]。 役割ベースのゲーム モードでプレイヤーの役割の設定に基づいてコレクションをマッチさせます。


**Target Intersection**

[Set Operation] 構成の一部。 マッチされる前の、2 つのコレクションの最小の交差または最大の差。


**Network Topology**

Quality of service データ型のみ。 QoS に使用されるネットワーク トポロジー。 可能な値は、[Peer to Peer]、[Peer to Host]、および [Client/Server] です。


**Maximum Latency/Scaling Maximum**  
Quality of service データ型のみ。 指定されたネットワーク トポロジー内でマッチメイキングを成功させるための最大遅延。 [Client-Server] の [Quality of service] SHOULD ルールを使用するとき、この値は (必須の遅延ではなく) スケーリング値として扱われます。


| 注意                                                                                                                                                           |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| さらに、ホッパーには既定の評判ルールも適用されます。 これらのルールは削除できません。マッチメイキング中に評判の処理を正しく行うために使用されます。 |


**Allow Waiting for Roles**

Collection Role Preferences データ型のみ。 すべての利用可能な役割を埋めるためにマッチ サービスがマッチメイキング チケットを保持するかどうかを指定します。


###### <a name="expansion-delta"></a>Expansion Delta

送信されたルールを各拡張生成のためにどのぐらい緩和するかを示す値。 拡張デルタは、Max Diff 値に加えて適用されます。 詳細については、「例 1 (ルール拡張)」を参照してください。

拡張デルタを使用して、複数の数値を異なる速度で拡張することもできます。 すべてのルールに適用されるため、拡張サイクル構成設定を通じてこれを行うことはできません。 代わりに、小数の拡張値 (0.4 など) を使用します。 拡張は、新しい整数に達したときにのみ発生します。これにより、同じ数の拡張サイクルに対しても、異なる拡張速度が可能になります。


###### <a name="qos-expansion-peer-to-peer-peer-to-host"></a>QoS 拡張 (ピア ツー ピア、ピア ツー ホスト)
ピア ゲーム用の Quality of Service 型の拡張の場合、拡張デルタを構成することはできません。 代わりに、以下の拡張方法のいずれかを使用する必要があります。

<table>

<tr>

<tr>
<td>
<b>1. MaxLatency が 256 未満。</b><p/><p/>

拡張は MaxLatency * 拡張サイクルで実行されます。<p/>
たとえば、初期値が 200 の場合、最初のサイクルで 200 が使用され、2 番目のサイクルでは 400 が使用されます。以降についても同様です。
</td>
</tr>

<tr>
<td>
<b>2. MaxLatency が 256 以上。</b><p/><p/>

拡張は、50 から MaxLatency-256 まで線形的に行われます。<p/>
たとえば、初期値が 556 の場合、値は、サイクルの数にわたって 50 から 300 まで線形的に拡張します。 つまり、6 つのサイクルが選ばれた場合、値は 50、100、150、200、250、および 300 になります。 5 つのサイクルが選ばれた場合、値は 50、112.5、175、237.5、および 300 になります。
</td>
</tr>

</tr>
</table>

##### <a name="qos-expansion-client-server"></a>QoS 拡張 (クライアント/サーバー)
専用サーバーを使用しているとき、拡張は相対的な優先度に基づきます。 早期の拡張サイクルでは、最も優先度の高いサーバーのみが考慮されます。 時間が経過すると、より優先度の低い他のサーバーが使用されます。 適切な拡張を保証するために、Scaling Maximum と呼ばれる、MaxLatency に似た値が必要です。 この Scaling Maximum は引き続き、最大の許容 ping 時間に設定する必要がありますが、この値は ping 時間の絶対要件を提供するのではなく、プレイヤーによって提供される異なったサーバー ping 時間の相対的スケールを与えます。 要求でリストから削除することにより、許容できない ping 時間のサーバーを意図的に除外できることに注意してください。

#### <a name="example-1-rule-expansion"></a>例 1 (ルール拡張)

マッチメイキングにはプレイヤー レベルが使用されます。プレイヤーは、レベルの近さに基づいて大まかにマッチされます。 レベル間の違いが最も少ないプレイヤーが優先されます。

-   プレイヤー レベルのルール
-   [Rule Type]: SHOULD
-   [Data Type]: Number
-   [Max Diff]: 1
-   [Expansion Delta]: 2
-   [Flatten Method]: Average

既定では、プレイヤー レベルの必要な差は 1 以下です。 この差の範囲内でマッチが見つかった場合、プレイヤーはマッチされます。 最初の一致が見つからない場合、プレイヤー レベル値は反復ごとに 2 拡張されます (既定では 3 反復)。 このシナリオの結果、レベル 20 のプレイヤーのマッチメイキング動作は次の表に示すようになります。

| 手順                    | マッチ候補のレベル値 | マッチを成功させるための効果的なレベルの差 |
|-----|
| 初期の送信値 | 19-21                                      | 1                                             |
| 拡張サイクル 1       | 17-23                                      | 3                                             |
| 拡張サイクル 2       | 15-25                                      | 5                                             |
| 拡張サイクル 3       | 13-27                                      | 7                                             |

拡張サイクルが続くにつれ、マッチを成功させるための効果的なレベルの差は、[Max Diff] 値を変更することなく増加します。 プレイヤー レベル値のみが緩和されます。


#### <a name="example-2-collection-rule"></a>例 2 (コレクション ルール)

ゲームは、プレイヤーに対して利用可能な 3 種類の DLC をリリースします。 このマッチメイキング ルールは、"DLC のみ" のゲーム プレイ マッチメイキングに適用されます。プレイヤーは、他のプレイヤーとマッチメイキングされるためには、少なくとも 1 つの DLC を所有している必要があります。

-   プレイヤー DLC ルール
-   [Rule Type]: MUST
-   [Data Type]: Collection
-   [Set Operation]: [Intersection]
-   [Target Intersection]: 1

プレイヤーは、自分の DLC を評価し、次の表に示す値をマッチ チケットで送信します。

| 注意                                                                                                                                   |
|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| 次の表で、コレクション値は DLC の所有を示しています。 DLC をプレイヤーが利用可能な場合は 1 に設定され、利用可能でない場合は 0 に設定されます。 |

| プレイヤー   | コレクション値 | プレイヤーとのマッチ | 注意           |
|----------|------------------|----------------------|----------------|
| プレイヤー 1 | { "1", "1", "1"} | 3                    | すべての DLC を所有  |
| プレイヤー 2 | { "0", "0", "0"} | なし                 | DLC を所有していない    |
| プレイヤー 3 | { "1", "0", "0"} | 1                    | 最初の DLC を所有 |

例において [Target Intersection] を 2 に設定した場合、交差は 1 のみであるため、プレイヤー 1 と 3 はマッチされません。

#### <a name="example-3-avoid-previous-players"></a>例 3 (以前のプレイヤーを避ける)
タイトルは、最近一緒にプレイしたプレイヤーとのゲームを避けることを優先します。
* [Rule Type]: MUST
* [Data Type]: Collection
* [Set Operation]: Difference
* [Target Intersection]: 0

## <a name="defining-team-rules-during-smartmatch-configuration"></a>SmartMatch 構成時のチーム ルールの定義

### <a name="configuring-team-rules"></a>チーム ルールの構成

チーム ルールを設定するには、まず XDP でチーム ルールを作成します。 ゲームがこのホッパーでマッチングされたチケットから作成するチーム サイズを入力します。 たとえば、4 対 4 を想定しているゲームでは、それぞれの最大サイズが 4 で、名前が異なる 2 つのエントリを作成する必要があります。 最小チーム サイズもあります。これは、チームのプレイヤー数が最大数より少なくてもゲームをプレイできるようにする場合に使用します。 それ以外の場合は、最大サイズと最小サイズを同じ値にします。


#### <a name="using-team-rules"></a>チーム ルールの使用

チーム ルールの構成後、ホッパー内のチケットは、分割なしで各グループをチームに組み込むことができない場合はマッチングされなくなります。 ルールによって、チーム割り当ての結果が members/constants/custom/matchmakingresult/initialTeam の下のターゲット セッションに書き込まれます。 これは推奨される割り当てにすぎません。タイトルは、プレイヤーを再編成することによりさらに良いゲームにできると判断することもできますが、その場合も、チケットが別々のチームに分割されないようにします。

進行中のゲームに対してチケットが作成される場合、チーム ルールは追加情報を必要とします。 たとえば、8 人のプレイヤーが 4 対 4 のゲーム内にいるときに、2 人のプレイヤーが離脱または接続解除したとします。 タイトルはそれらの空きを埋める必要がありますが、ゲームがプレイ中の間はチームを再編成できません。

進行中のゲームの補充を実行しようとしていることは、PreserveSession フィールドが "always" に設定されたチケットによって表されます。 このような場合、チームは既にプレイヤーに割り当てられているので、タイトルは現在のチーム割り当てを指定して、マッチで各チームの空き数がわかるようにする必要があります。 各プレイヤーがいるチームの名前を提供するために、各プレイヤーは自分のチーム名を members/me/properties/system/groups の下のゲーム セッションに書き込みます。 このフィールドは JArray です。

前述のプロパティがゲーム セッションに書き込まれると、1 人のプレイヤーが、さらにプレイヤーを探そうとして、そのセッションのチケットを作成します。 チケットが実行されると、マッチは参加するプレイヤーによる推奨チームを members/constants/custom/matchmakingresult/initialTeam に再び書き込みます。


###### <a name="preferring-even-teams"></a>同等サイズのチームを優先する

さらに、マッチはまず最もサイズの大きいチームによって作成されます。 このため、仮定の 4 対 4 ホッパーでは、4 プレイヤーのチケットが、4 プレイヤーのチケットがなくなるまで先にマッチングされます。 続いて 3 プレイヤーのチケットどうしがマッチングされ、その次は 2 プレイヤーのチケットのマッチングに進みます。 この方法では、同等サイズのチケットが存在し、他のルールで禁止されていなければ、通常は同等サイズのチケットどうしが対戦することになります。 チーム ルールの優先度は他のルールよりもかなり高いことに注意してください。 たとえば、ユーザーが限られており、高スキルでサイズが 4 のチケットが 1 つ (A)、低スキルでサイズが 4 のチケットが 1 つ (B)、および高スキルでサイズが 1 のチケットが 4 つ (C ～ F) からなると仮定します。 チーム ルールにより、マッチでは A と C、D、E、F ではなく、A と B のマッチングが優先されます。


###### <a name="should-variant"></a>推奨ルールとの違い

必須ルールは、すべての生成でチケットの分割を阻止し、同等サイズのチームを優先する分類を提供します。 推奨ルールは、最後の生成までは同じで、その後はチケットが分割される可能性がありますが、同等サイズのチームを優先する分類は引き続き有効です。

## <a name="target-session-initialization-and-qos"></a>ターゲット セッションの初期化と QoS

プレイヤーのグループは、「[SmartMatch マッチメイキング]()」に説明されているように、SmartMatch マッチメイキングによってターゲット セッションにマッチされます。 タイトルは、十分なプレイヤーが参加したこと、また、必要に応じて互いに正常に接続できることを確認するための手順を実行する必要があります。 このプロセスは、ターゲット セッションの初期化と呼ばれます。

ピア ツー ピア ネットワーク トポロジーを使用するゲームの場合、ターゲット セッションの初期化の重要な要素は QoS の測定と評価です。 関係する操作は、Xbox One 本体間 (または本体とサーバー間) の遅延と帯域幅の測定、およびノード間のネットワーク接続が良好であるかどうかを判断するための測定値の評価です。

次のフロー チャートは、ターゲット セッションの初期化と QoS 処理を実装する方法を示しています。

![](../../images/multiplayer/Multiplayer_2015_Matchmaking_QoS.png)

### <a name="managed-initialization"></a>初期化の管理

MPSD は、"初期化の管理" という機能をサポートします。この機能を通じて、セッションに関与するクライアント間でターゲット セッションの初期化プロセスを調整します。 MPSD は、セッションの初期化ステージおよび関連付けられたタイムアウトを自動的に追跡し、必要に応じてクライアント間の接続を評価します。 初期化の管理は、**MultiplayerManagedInitialization クラス**によって表されます。

| 注意                                                                                                                  |
|------------------------------------------------------------------------------------------------------------------------------------|
| タイトルで SmartMatch マッチメイキングを使用して MPSD の初期化の管理機能を活用することを強くお勧めします。 |


#### <a name="managed-initialization-episodes-and-stages"></a>初期化の管理のエピソードおよびステージ

ターゲット セッションでは、マッチメイキングが新しいプレイヤーをセッションに追加するたびに初期化の管理が行われます。 SmartMatch は、セッション メンバーをユーザー状態 Reserved として追加します。つまり、各メンバーはスロットを占有しますが、まだセッションには参加していません。 新しいプレイヤーの各グループは、新しい初期化エピソードをトリガーします。

初期化の完了時、各プレイヤーはプロセスに成功または失敗します。 初期化に成功したプレイヤーは、ターゲット セッションを使用してプレイできます。 失敗したプレイヤーは、マッチメイキングに再送信され、別のセッションにマッチされる必要があります。 セッションが *preserveSession* パラメーターを Always に設定してマッチメイキングに送信される場合、セッションの既存のメンバーで初期化されません。それらのメンバーは適切に設定されていると MPSD が想定するためです。

初期化の管理の各エピソードは以下のステージで構成されます。

-   参加 - セッション メンバーは自身をセッションに書き込んでユーザー状態を Reserved から Active に移行し、セキュア デバイス アドレスなどの基本データをアップロードします。
-   測定 - ピア ベースのトポロジーでは、セッション メンバーは互いに QoS を測定し、結果をセッションにアップロードします。
-   評価 - MPSD は、最後の 2 段階の結果を評価し、セッションやメンバーが正常に初期化されたかどうかを判断します。

タイトル コードは、セッション上で動作して、各ユーザー (およびその結果としてセッション) の参加および測定フェーズを進めます。 評価ステージが成功または失敗した後、プレイを開始する、またはマッチメイキングに戻ることができます。


### <a name="configuring-the-target-session-for-initialization"></a>初期化のためのターゲット セッションの構成

タイトルは、初期化されるターゲット セッションで定数を使用して、初期化の管理プロセスを構成できます。 これらの定数は、バージョン 107 (推奨されるテンプレート バージョン) のセッション テンプレートでは /constants/system の下で設定されます。 2 種類の構成設定を行うことができます。初期化の管理プロセスを全体として構成する設定と、QoS 要件を構成する設定です。 一般的なタイトル シナリオのセッション テンプレートの例については、「[MPSD セッション テンプレート](multiplayer-session-directory.md)」を参照してください。

| 注意                                                                                                                              |
|------------------------------------------------------------------------------------------------------------------------------------------------|
| QoS 要件がターゲット セッションの初期化構成で定義されていない場合、初期化中の測定ステージはスキップされます。 |


#### <a name="configuring-managed-initialization-as-a-whole"></a>全体としての初期化の管理の構成

以下は、初期化の管理を全体的に制御する場合に設定するフィールドです。 これらは /constants/system/memberInitialization オブジェクトの一部です。
- joinTimeout。 初期化エピソードの開始後に MPSD が各メンバーの参加を待機する時間を指定します。 既定値は 10 秒です。
-   measurementTimeout。 測定ステージの開始後に MPSD が各メンバーの QoS 測定結果のアップロードを待機する時間を指定します。 既定値は 30000 秒です。
-   membersNeededToStart。 最初の初期化エピソードが成功するために初期化で成功する必要があるメンバーの数を指定します。 既定値は 1 です。

| 注意                                              |
|----------------------------------------------------------------|
| このしきい値が満たされない場合は、すべてのメンバーが初期化に失敗します。 |


#### <a name="configuring-qos-requirements"></a>QoS 要件の構成

QoS は、タイトルがピア ツー ピアまたはピアー ツー ホスト トポロジーを使用する場合のみ、初期化中に必要です。 各トポロジーは、/constants/system/ の下にあるトポロジー固有の定数にマップされます。
###### <a name="configuring-qos-requirements-for-peer-to-peer-topology"></a>ピア ツー ピア トポロジーの QoS 要件の構成

| 注意                                                                                                                                                                                         |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ピアー ツー ピアー トポロジーでタイトルが QoS 要件設定を行うことはまれです。 これらの設定は、非常に制約が厳しく、厳格なネットワーク アドレス変換 (NAT) を使用するプレイヤーで問題が発生します。 |

ピア ツー ピア トポロジーの QOS 要件は、peerToPeerRequirements オブジェクトで設定されます。 すべてのクライアントが他のすべてのクライアントに接続できることが必要です。 このオブジェクトには、次の関連フィールドがあります。
-   latencyMaximum。 任意の 2 つのクライアント間の最大遅延時間を指定します。
-   bandwidthMinimum。 任意の 2 つのクライアント間の最小帯域幅を指定します。


###### <a name="configuring-qos-requirements-for-peer-to-host-topology"></a>ピア ツー ホスト トポロジーの QoS 要件の構成

ピア ツー ホスト トポロジーの QOS 要件は、peerToHostRequirements オブジェクトで設定されます。 すべてのクライアントが単一の共通ホストに接続できることが必要です。 このオブジェクトが構成され、初期化が成功した場合、MPSD は、可能性のあるホスト ("ホスト候補" と呼ばれます) であるクライアントの初期リストを作成します。 設定するフィールドは次のとおりです。
-   latencyMaximum。 各ピアとホストの間の最大遅延時間を指定します。
-   bandwidthDownMinimum。 各ピアとホストの間の最小ダウンストリーム帯域幅を指定します。
-   bandwidthUpMinimum。 各ピアとホストの間の最小アップストリーム帯域幅を指定します。
-   hostSelectionMetric。 ホストを選択するために使用するメトリックを指定します。

## <a name="see-also"></a>関連項目

[タイトルの SmartMatch の構成]()

[MPSD セッション テンプレート](multiplayer-session-directory.md)

[SmartMatch のランタイム操作]()