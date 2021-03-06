---
description: 予約されたキーワード (MDX 構文)
title: 予約済みキーワード (MDX 構文) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 630f004a230d473ef5aab6ea230dc2d3903ce0e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341348"
---
# <a name="reserved-keywords-mdx-syntax"></a>予約されたキーワード (MDX 構文)


  Analysis Services は、特定のキーワードを予約して排他的に使用します。 予約済みキーワードの一覧については、「 [MDX の予約語](../mdx/mdx-reserved-words.md)」を参照してください。  
  
 予約済みキーワードは次のガイドラインに従います。  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] によって定義される場所を除いて、多次元式 (MDX) ステートメントに予約されたキーワードを含めることはできません。  
  
-   データベース内のオブジェクトに、予約済みのキーワードに一致する名前を指定することはできません。 このような名前が存在する場合は、区切られた識別子を使用してオブジェクトを参照する必要があります。 この方法を使用すれば予約語と同じ名前のオブジェクトも使用できますが、オブジェクトの名前にはキーワードを使用しないことをお勧めします。  
  
-   予約されたキーワードを使用しない名前付け規則を使用してください。 オブジェクト名が予約済みキーワードのように見える場合は、子音または母音を削除できます。  
  
## <a name="see-also"></a>参照  
 [MDX 構文の要素 &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
