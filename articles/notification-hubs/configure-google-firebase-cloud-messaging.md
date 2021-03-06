---
title: Azure Notification Hubs で Google Firebase Cloud Messaging を構成する | Microsoft Docs
description: Google Firebase Cloud Messaging の設定で Azure 通知ハブを構成する方法について説明します。
services: notification-hubs
author: sethmanheim
manager: femila
editor: jwargo
ms.service: notification-hubs
ms.workload: mobile
ms.topic: article
ms.date: 03/25/2019
ms.author: sethm
ms.reviewer: jowargo
ms.lastreviewed: 03/25/2019
ms.openlocfilehash: 1adbce654bc5c057270df9a874911731a0135034
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "80127465"
---
# <a name="configure-google-firebase-settings-for-a-notification-hub-in-the-azure-portal"></a>Azure portal で通知ハブ用に Google Firebase の設定を構成する

この記事では、Azure portal を使用して Azure 通知ハブ用に Google Firebase Cloud Messaging (FCM) の設定を構成する方法について説明します。  

## <a name="prerequisites"></a>前提条件
通知ハブを作成していない場合は、ここで作成します。 詳細については、「[Azure portal 内で Azure 通知ハブを作成する](create-notification-hub-portal.md)」を参照してください。 

## <a name="configure-google-firebase-cloud-messaging-fcm"></a>Google Firebase Cloud Messaging (FCM) の構成

次の手順は、通知ハブ用に Google Firebase Cloud Messaging (FCM) の設定を構成する手順を示しています。 

1. Azure portal の **[通知ハブ]** ページで、左側のメニューの **[Google (GCM/FCM)]** を選択します。 
2. 前に保存した FCM プロジェクトの **API キー**を貼り付けます。 
3. **[保存]** を選択します。 

   ![Google FCM 用に Notification Hubs を構成する方法を示したスクリーンショット](./media/notification-hubs-android-push-notification-google-fcm-get-started/fcm-server-key.png)

## <a name="next-steps"></a>次のステップ
Azure Notification Hubs と Google Firebase Cloud Messaging を使用して、Android デバイスにプッシュ通知を送信する詳細な手順については、[Notification Hubs と Google FCM を使用した Android デバイスへのプッシュ通知の送信](notification-hubs-android-push-notification-google-fcm-get-started.md)に関するページをご覧ください。

