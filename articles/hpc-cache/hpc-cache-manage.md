---
title: Azure HPC Cache を管理して更新する
description: Azure portal を使用して Azure HPC Cache を管理および更新する方法
author: ekpgh
ms.service: hpc-cache
ms.topic: conceptual
ms.date: 1/29/2020
ms.author: rohogue
ms.openlocfilehash: 57d6a2024cd6fd979426ca5de5e261f110f6156f
ms.sourcegitcommit: 849bb1729b89d075eed579aa36395bf4d29f3bd9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "81537952"
---
# <a name="manage-your-cache-from-the-azure-portal"></a>Azure portal からキャッシュを管理する

Azure portal のキャッシュの概要ページには、お使いのキャッシュに関して、プロジェクトの詳細、キャッシュの状態、基本的な統計が表示されます。 キャッシュの停止または開始、キャッシュの削除、長期ストレージへのデータのフラッシュ、ソフトウェア更新を行うためのコントロールも用意されています。

概要ページを開くには、Azure portal でお使いのキャッシュのリソースを選択します。 たとえば、 **[すべてのリソース]** ページを読み込んで、キャッシュ名をクリックします。

![Azure HPC Cache インスタンスの [概要] ページのスクリーンショット](media/hpc-cache-overview.png)

ページの上部のボタンは、キャッシュを管理する助けになります。

* **[開始]** と [ **[停止]** ](#stop-the-cache) - キャッシュ操作を中断します
* [ **[フラッシュ]** ](#flush-cached-data) - 変更されたデータをストレージ ターゲットに書き込みます
* [ **[フラッシュ]** ](#upgrade-cache-software) - キャッシュ ソフトウェアを更新します
* **[最新の情報に更新]** - 概要ページを再読み込みします
* [ **[削除]** ](#delete-the-cache) - キャッシュを完全に破棄します

これらのオプションの詳細については、以下をご覧ください。

## <a name="stop-the-cache"></a>キャッシュを停止する

キャッシュを停止して、アクティブでない期間中のコストを削減することができます。 キャッシュが停止している間はアップタイムに対して課金されませんが、キャッシュの割り当て済みディスク ストレージに対しては課金されます。 (詳細については、[価格](https://aka.ms/hpc-cache-pricing)のページを参照してください。)

停止したキャッシュはクライアント要求に応答しません。 キャッシュを停止する前に、クライアントのマウントを解除する必要があります。

**[停止]** ボタンで、アクティブなキャッシュが中断されます。 **[停止]** ボタンは、キャッシュの状態が **[正常]** または **[低下]** の場合に使用できます。

![[停止] が強調表示された上部のボタンと、'続行しますか?' とたずねている停止アクションのポップアップ メッセージのスクリーンショット [はい] (既定) および [いいえ] ボタンで '続行しますか?' とたずねているポップアップ メッセージのスクリーンショット](media/stop-cache.png)

[はい] をクリックしてキャッシュの停止を確認すると、キャッシュの内容がストレージ ターゲットに自動的にフラッシュされます。 この処理には時間がかかることがありますが、データの一貫性が確保されます。 最後に、キャッシュの状態が **[Stopped]\(停止\)** に変わります。

停止しているキャッシュを再アクティブ化するには、 **[開始]** ボタンをクリックします。 確認は必要ありません。

![[開始] が強調表示されている上部のボタンのスクリーンショット](media/start-cache.png)

## <a name="flush-cached-data"></a>キャッシュ データをフラッシュする

概要ページの **[フラッシュ]** ボタンは、キャッシュに格納されている変更されたすべてのデータを、バックエンド ストレージ ターゲットに直ちに書き込むようにキャッシュに指示します。 キャッシュはデータをストレージ ターゲットに定期的に保存するため、バックエンド ストレージ システムが最新の状態であることを確認する場合を除き、これを手動で行う必要はありません。 たとえば、ストレージのスナップショットを取ったり、データ セットのサイズを調べたりする前に **[フラッシュ]** を使用することがあります。

> [!NOTE]
> フラッシュ プロセスの間、キャッシュはクライアント要求を処理できません。 キャッシュ アクセスは一時停止され、操作の完了後に再開されます。

![[フラッシュ] が強調表示された一番上のボタンと、フラッシュ アクションが記述され、 [はい] (既定) および [いいえ] ボタンで '続行しますか?' とたずねているポップアップ メッセージのスクリーンショット](media/hpc-cache-flush.png)

キャッシュのフラッシュ操作を開始すると、キャッシュはクライアント要求の受け付けを停止し、概要ページのキャッシュの状態は **[Flashing] (フラッシュ中)** に変わります。

キャッシュ内のデータは、適切なストレージ ターゲットに保存されます。 フラッシュする必要があるデータの量によっては、このプロセスに数分または 1 時間以上かかることがあります。

すべてのデータがストレージ ターゲットに保存された後、キャッシュは再度、クライアント要求の取得を自動的に開始します。 キャッシュの状態は **[正常]** に戻ります。

## <a name="upgrade-cache-software"></a>キャッシュ ソフトウェアをアップグレードする

新しいソフトウェア バージョンが利用可能な場合は、 **[アップグレード]** ボタンがアクティブになります。 また、ページの上部にソフトウェアの更新に関するメッセージも表示されます。

![[アップグレード] ボタンが有効になった状態の、ボタンの最上位行のスクリーンショット](media/hpc-cache-upgrade-button.png)

ソフトウェアのアップグレード中にクライアント アクセスは中断されませんが、キャッシュのパフォーマンスが低下します。 ピーク以外の使用時間帯や計画済みのメンテナンス期間にソフトウェアをアップグレードするよう計画してください。

ソフトウェアの更新は数時間かかることがあります。 スループットが高い構成のキャッシュは、ピーク スループット値が低いキャッシュよりもアップグレードするのに時間がかかります。

ソフトウェア アップグレードが入手可能になった場合、それを手動で適用するには 1 週間程度かかります。 終了日は、アップグレード メッセージに記載されています。 ユーザーがその期間中にアップグレードしないと、Azure が自動的に、更新プログラムをキャッシュに適用します。 自動アップグレードのタイミングは構成可能ではありません。 キャッシュ パフォーマンスへの影響が懸念される場合は、有効期限が切れる前に、ソフトウェアを自分でアップグレードする必要があります。

有効期限が切れ、お使いのキャッシュが停止している場合、次回の起動時にキャッシュによってソフトウェアが自動的にアップグレードされます。 (更新プログラムは直ちに開始されない場合もありますが、最初の 1 時間で開始されます)。

**[アップグレード]** ボタンをクリックしてソフトウェアの更新を開始します。 操作が完了するまで、キャッシュの状態は **[アップグレード中]** に変わります。

## <a name="delete-the-cache"></a>キャッシュの削除

**[削除]** ボタンでキャッシュが破棄されます。 キャッシュを削除すると、そのリソースすべてが破棄され、アカウントの料金が発生しなくなります。

キャッシュを削除しても、ストレージ ターゲットとして使用されたバックエンド ストレージ ボリュームは影響を受けません。 後で新しいキャッシュに追加することも、個別に使用を停止することもできます。

> [!NOTE]
> Azure HPC Cache は、キャッシュを削除する前に、変更されたデータをキャッシュからバックエンド ストレージ システムに自動的に書き込みません。
>
> キャッシュ内のすべてのデータが長期ストレージに書き込まれるようにするには、[キャッシュを停止](#stop-the-cache)してから、削除します。 [削除] ボタンをクリックする前に、ステータス **[Stopped]\(停止\)** が表示されていることを確認します。

## <a name="cache-metrics-and-monitoring"></a>キャッシュのメトリックと監視

概要ページには、キャッシュのスループット、1 秒あたりの操作数、待機時間など、いくつかの基本的なキャッシュ統計情報のグラフが表示されます。

![サンプル キャッシュについて前述の統計情報を示している、3 つの折れ線グラフのスクリーンショット](media/hpc-cache-overview-stats.png)

これらのグラフは、Azure の組み込みの監視および分析ツールの一部です。 その他のツールとアラートは、ポータルのサイドバーにある **[監視]** という見出しの下にあるページから利用できます。 詳細については、[Azure 監視のドキュメント](../azure-monitor/insights/monitor-azure-resource.md#monitoring-in-the-azure-portal)のポータルに関するセクションを参照してください。

## <a name="next-steps"></a>次のステップ

* [Azure のメトリックと統計ツール](../azure-monitor/index.yml)について確認する
* [Azure HPC Cache に関する支援](hpc-cache-support-ticket.md)を依頼する
