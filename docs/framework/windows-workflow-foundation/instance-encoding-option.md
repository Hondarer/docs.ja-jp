---
title: インスタンス エンコーディング オプション
ms.date: 03/30/2017
ms.assetid: 89e4b029-4f68-438c-8117-9b21fe094ef4
ms.openlocfilehash: c4de7c45d899f45a7b5b71d563257d9accb8fdbb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61928716"
---
# <a name="instance-encoding-option"></a>インスタンス エンコーディング オプション
**インスタンス エンコーディング オプション**SQL Workflow Instance Store のプロパティでは、SQL 永続化プロバイダーが保存する前に、GZip アルゴリズムを使用して、ワークフロー インスタンス状態情報を圧縮するかどうかを指定できます、。永続性データベースに情報。 このプロパティに使用できる値は次のとおりです。GZip と None です。 既定値は None です。 これらのオプションを次の一覧で説明します。  
  
1. **GZip**します。 永続化プロバイダーは、永続性データベースに状態情報を永続化する前に、GZip アルゴリズムを使用して状態情報をエンコードします。  
  
2. **None**します。 永続化プロバイダーは、永続性データベースに情報を保存する前は、状態情報をエンコードしません。  
  
 GZip を使用してワークフロー インスタンスの状態情報をエンコードすると、SQL データベースのメモリ消費量が減ります。また、ワークフロー サービス ホストが実行されているコンピューターとは異なるコンピューターがネットワーク上にあり、そこにデータベースが配置されている場合、ネットワークの消費量も減ります。 一般的なガイダンスを設定するのには、**インスタンス エンコーディング オプション**プロパティを**None**ワークフロー インスタンスの状態が小さい場合。
