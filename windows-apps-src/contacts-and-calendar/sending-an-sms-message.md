---
description: このトピックでは、SMS の作成ダイアログを起動して、ユーザーが SMS メッセージを送信できるようにする方法について説明します。 ダイアログを表示する前に、SMS の各フィールドにデータを設定することができます。 メッセージは、ユーザーが送信ボタンをタップするまで送信されません。
title: SMS メッセージの送信
ms.assetid: 4D7B509B-1CF0-4852-9691-E96D8352A4D6
keywords: 連絡先, SMS, 送信
ms.date: 02/08/2017
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: ea262e026f31e1d690673f9b1d88e882d88ee4aa
ms.sourcegitcommit: b52ddecccb9e68dbb71695af3078005a2eb78af1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74255003"
---
# <a name="send-an-sms-message"></a>SMS メッセージの送信

このトピックでは、SMS の作成ダイアログを起動して、ユーザーが SMS メッセージを送信できるようにする方法について説明します。 ダイアログを表示する前に、SMS の各フィールドにデータを設定することができます。 メッセージは、ユーザーが送信ボタンをタップするまで送信されません。

このコードを呼び出すには、パッケージマニフェストで chat、 **smssend**、および**チャット** **システム**の機能を宣言します。 これらの[機能は制限](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations#special-and-restricted-capabilities)されていますが、アプリで使用することができます。 アプリをストアに発行する場合にのみ、承認が必要です。 「[アカウントの種類、場所、料金](https://docs.microsoft.com/windows/uwp/publish/account-types-locations-and-fees)」を参照してください。

## <a name="launch-the-compose-sms-dialog"></a>SMS の作成ダイアログの起動

新しい [**ChatMessage**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.chat.chatmessage) オブジェクトを作成し、メールの作成ダイアログに事前に入力するデータを設定します。 ダイアログを表示するには、[**ShowComposeSmsMessageAsync**](https://docs.microsoft.com/uwp/api/windows.applicationmodel.chat.chatmessagemanager.showcomposesmsmessageasync) を呼び出します。

```cs
private async void ComposeSms(Windows.ApplicationModel.Contacts.Contact recipient,
    string messageBody,
    StorageFile attachmentFile,
    string mimeType)
{
    var chatMessage = new Windows.ApplicationModel.Chat.ChatMessage();
    chatMessage.Body = messageBody;

    if (attachmentFile != null)
    {
        var stream = Windows.Storage.Streams.RandomAccessStreamReference.CreateFromFile(attachmentFile);

        var attachment = new Windows.ApplicationModel.Chat.ChatMessageAttachment(
            mimeType,
            stream);

        chatMessage.Attachments.Add(attachment);
    }

    var phone = recipient.Phones.FirstOrDefault<Windows.ApplicationModel.Contacts.ContactPhone>();
    if (phone != null)
    {
        chatMessage.Recipients.Add(phone.Number);
    }
    await Windows.ApplicationModel.Chat.ChatMessageManager.ShowComposeSmsMessageAsync(chatMessage);
}
```

次のコードを使用して、アプリを実行しているデバイスが SMS メッセージを送信できるかどうかを判断できます。

```csharp
if (Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.ApplicationModel.Chat"))
{
   // Call code here.
}
```

## <a name="summary-and-next-steps"></a>要約と次のステップ

このトピックでは、SMS の作成ダイアログの起動方法を示しました。 SMS メッセージの受信者として使う連絡先を選ぶ方法については、「[連絡先の選択](selecting-contacts.md)」をご覧ください。 バックグラウンド タスクを使用して SMS メッセージを送受信する方法の例については、GitHub から [ユニバーサル Windows アプリのサンプル](https://github.com/Microsoft/Windows-universal-samples) をダウンロードしてください。

## <a name="related-topics"></a>関連トピック

* [連絡先の選択](selecting-contacts.md)
