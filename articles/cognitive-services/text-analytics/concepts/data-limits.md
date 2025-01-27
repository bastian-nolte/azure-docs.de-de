---
title: Datengrenzwerte für die Textanalyse-API
titleSuffix: Azure Cognitive Services
description: Datenbeschränkungen für die Textanalyse-API von Azure Cognitive Services.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: text-analytics
ms.topic: overview
ms.date: 04/27/2020
ms.author: aahi
ms.reviewer: chtufts
ms.openlocfilehash: 0dc79132ae75be511b53bf272e578ff0ce7a7775
ms.sourcegitcommit: 25bb515efe62bfb8a8377293b56c3163f46122bf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87986813"
---
# <a name="data-and-rate-limits-for-the-text-analytics-api"></a>Datengrenzwerte und Ratenbegrenzungen für die Textanalyse-API
<a name="data-limits"></a>

In diesem Artikel finden Sie die Grenzwerte für die Datengröße und -rate, die beim Senden von Daten an die Textanalyse-API gelten. 

## <a name="data-limits"></a>Datengrenzwerte

> [!NOTE]
> * Wenn Sie größere Dokumente analysieren müssen, als der Grenzwert zulässt, können Sie den Text in kleinere Textabschnitte aufteilen, bevor Sie ihn an die API senden. 
> * Ein Dokument ist eine einzelne aus Textzeichen bestehende Zeichenfolge.  

| Begrenzung | Wert |
|------------------------|---------------|
| Maximale Größe eines einzelnen Dokuments | 5\.120 Zeichen (gemessen von [StringInfo.LengthInTextElements](https://docs.microsoft.com/dotnet/api/system.globalization.stringinfo.lengthintextelements)). |
| Maximale Größe der gesamte Anforderung | 1 MB |

Die maximale Anzahl von Dokumenten, die Sie in einer einzelnen Anforderung senden können, hängt von der API-Version und -Funktion ab, die Sie verwenden.

#### <a name="version-3"></a>[Version 3](#tab/version-3)

Die folgenden Grenzwerte haben sich in Version 3 der API geändert. Wenn Sie die folgenden Grenzwerte überschreiten, wird der HTTP-Fehlercode 400 generiert.


| Funktion | Max. Anzahl von Dokumenten pro Anforderung | 
|----------|-----------|
| Spracherkennung | 1000 |
| Standpunktanalyse | 10 |
| Schlüsselwortextraktion | 10 |
| Erkennung benannter Entitäten | 5 |
| Entitätsverknüpfung | 5 |

#### <a name="version-2"></a>[Version 2](#tab/version-2)

| Funktion | Max. Anzahl von Dokumenten pro Anforderung | 
|----------|-----------|
| Spracherkennung | 1000 |
| Standpunktanalyse | 1000 |
| Schlüsselwortextraktion | 1000 |
| Erkennung benannter Entitäten | 1000 |
| Entitätsverknüpfung | 1000 |

---

## <a name="rate-limits"></a>Ratenbegrenzungen

Die Ratenbegrenzung variiert je nach [Tarif](https://azure.microsoft.com/pricing/details/cognitive-services/text-analytics/). Diese Begrenzungen sind bei beiden Versionen der API identisch.

| Tarif          | Anforderungen pro Sekunde | Anforderungen pro Minute |
|---------------|---------------------|---------------------|
| S/Mehrere Dienste | 1000                | 1000                |
| S0/F0         | 100                 | 300                 |
| S1            | 200                 | 300                 |
| S2            | 300                 | 300                 |
| S3            | 500                 | 500                 |
| S4            | 1000                | 1000                |

Die Anforderungen werden für jede Textanalysefunktion separat gemessen. So können Sie beispielsweise die maximale Anzahl von Anforderungen für Ihren Tarif gleichzeitig an alle Funktionen senden.  


## <a name="see-also"></a>Weitere Informationen

* [Worum handelt es sich bei der Textanalyse-API?](../overview.md)
* [Preisübersicht](https://azure.microsoft.com/pricing/details/cognitive-services/text-analytics/)
