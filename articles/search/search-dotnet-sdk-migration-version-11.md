---
title: Upgrade auf .NET SDK-Version 11
titleSuffix: Azure Cognitive Search
description: Migrieren Sie Code von älteren Versionen zum Azure Cognitive Search .NET SDK-Version 11. Hier finden Sie Informationen zu Neuheiten und erfahren, welche Änderungen am Code erforderlich sind.
manager: nitinme
author: HeidiSteen
ms.author: heidist
ms.service: cognitive-search
ms.devlang: dotnet
ms.topic: conceptual
ms.date: 08/05/2020
ms.openlocfilehash: 03d40dcaeaefe01fecbc201cf28dc20c8634af9d
ms.sourcegitcommit: 4f1c7df04a03856a756856a75e033d90757bb635
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87926670"
---
# <a name="upgrade-to-azure-cognitive-search-net-sdk-version-11"></a>Upgrade auf Version 11 des Azure Cognitive Search .NET SDK

Wenn Sie die Version 10.0 oder eine frühere Version des [.NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/search) verwenden, unterstützt dieser Artikel Sie beim Upgrade auf Version 11.

Version 11 ist eine vollständig neu gestaltete Clientbibliothek, die vom Azure SDK-Entwicklungsteam freigegeben wurde (frühere Versionen wurden vom Azure Cognitive Search-Entwicklungsteam erstellt). Die Bibliothek wurde neu gestaltet, um eine größere Konsistenz mit anderen Azure-Clientbibliotheken zu erreichen. Dabei wurde eine Abhängigkeit von [Azure.Core](https://docs.microsoft.com/dotnet/api/azure.core) und [System.Text.Json](https://docs.microsoft.com/dotnet/api/system.text.json) berücksichtigt und bewährte Ansätze für gängige Aufgaben implementiert.

Zu den wichtigsten Unterschieden, die Ihnen in der neuen Version auffallen werden, gehören:

+ Ein Paket und eine Bibliothek im Gegensatz zu mehreren
+ Ein neuer Paketname: `Azure.Search.Documents` anstelle von `Microsoft.Azure.Search`
+ Drei Clients anstelle von zwei: `SearchClient`, `SearchIndexClient`, `SearchIndexerClient`
+ Benennungsunterschiede bei verschiedenen APIs und kleine strukturelle Unterschiede, die einige Aufgaben vereinfachen

## <a name="package-and-library-consolidation"></a>Paket- und Bibliothekskonsolidierung

Version 11 fasst mehrere Pakete und Bibliotheken in jeweils ein Paket bzw. eine Bibliothek zusammen. Nach der Migration müssen Sie weniger Bibliotheken verwalten.

+ [Azure.Search.Documents-Paket](https://www.nuget.org/packages/Azure.Search.Documents/)

+ [API-Referenz für die Clientbibliothek](https://docs.microsoft.com/dotnet/api/overview/azure/search.documents-readme?view=azure-dotnet)

## <a name="client-differences"></a>Clientunterschiede

In der folgenden Tabelle werden die Clientbibliotheken soweit möglich einer der beiden Versionen zugeordnet.

| Umfang von Vorgängen | Microsoft.Azure.Search&nbsp;(v10) | Azure.Search.Documents&nbsp;(v11) |
|---------------------|------------------------------|------------------------------|
| Client für Abfragen und zum Auffüllen eines Index | [SearchIndexClient](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.searchindexclient) | [SearchClient](https://docs.microsoft.com/dotnet/api/azure.search.documents.searchclient) |
| Client für Indizes, Analysetools, Synonymzuordnungen | [SearchServiceClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchserviceclient) | [SearchIndexClient](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.searchindexclient) |
| Client für Indexer, Datenquellen, Skillsets | [SearchServiceClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchserviceclient) | [SearchIndexerClient (**neu**)](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.searchindexerclient) |

> [!Important]
> `SearchIndexClient` ist in beiden Versionen vorhanden, unterstützt aber unterschiedliche Dinge. In Version 10 erstellt `SearchIndexClient` Indizes und andere Objekte. In Version 11 arbeitet `SearchIndexClient` mit vorhandenen Indizes. Achten Sie auf die Reihenfolge, in der die Clientverweise aktualisiert werden, damit keine Unklarheiten entstehen. Befolgen Sie die Reihenfolge in den [Schritten zum Aktualisieren](#UpgradeSteps), um Probleme beim Ersetzen von Zeichenfolgen zu vermeiden.

<a name="naming-differences"></a>

## <a name="naming-and-other-api-differences"></a>Benennung und andere API-Unterschiede

Abgesehen von den Clientunterschieden (die bereits erwähnt und daher hier weggelassen werden), wurden mehrere andere APIs umbenannt und in einigen Fällen überarbeitet. Die Unterschiede bei den Klassennamen sind unten zusammengefasst. Diese Liste ist nicht vollständig, aber darin werden API-Änderungen nach Aufgaben gruppiert, was für Revisionen bei bestimmten Codeblöcken hilfreich sein kann. Eine detaillierte Liste der API-Updates finden Sie im [Änderungsprotokoll](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/search/Azure.Search.Documents/CHANGELOG.md) für `Azure.Search.Documents` auf GitHub.

### <a name="authentication-and-encryption"></a>Authentifizierung und Verschlüsselung

| Version 10 | Entsprechung in Version 11 |
|------------|-----------------------|
| [SearchCredentials](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchcredentials) | [AzureKeyCredential](https://docs.microsoft.com/dotnet/api/azure.azurekeycredential) |
| `EncryptionKey` (war im [Vorschau-SDK](https://www.nuget.org/packages/Microsoft.Azure.Search/8.0.0-preview) als allgemein verfügbares Feature vorhanden) | [SearchResourceEncryptionKey](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchresourceencryptionkey) |

### <a name="indexes-analyzers-synonym-maps"></a>Indizes, Analysetools, Synonymzuordnungen

| Version 10 | Entsprechung in Version 11 |
|------------|-----------------------|
| [Index](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.index) | [SearchIndex](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchindex) |
| [Feld](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.field) | [SearchField](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchfield) |
| [DataType](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.datatype) | [SearchFieldDataType](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchfielddatatype) |
| [ItemError](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.itemerror) | [SearchIndexerError](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchindexererror) |
| [Analyzer](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.analyzer) | [LexicalAnalyzer](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.lexicalanalyze) (auch `AnalyzerName` in `LexicalAnalyzerName`) |
| [AnalyzeRequest](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.analyzerequest) | [AnalyzeTextOptions](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.analyzetextoptions) |
| [StandardAnalyzer](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.standardanalyzer) | [LuceneStandardAnalyzer](https://docs.microsoft.com//dotnet/api/azure.search.documents.indexes.models.lucenestandardanalyzer) |
| [StandardTokenizer](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.standardtokenizer) | [LuceneStandardTokenizer](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.lucenestandardtokenizer) (auch `StandardTokenizerV2` in `LuceneStandardTokenizerV2`) |
| [TokenInfo](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.tokeninfo) | [AnalyzedTokenInfo](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.analyzedtokeninfo) |
| [Tokenizer](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.tokenizer) | [LexicalTokenizer](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.lexicaltokenizer) (auch `TokenizerName` in `LexicalTokenizerName`) |
| [SynonymMap.Format](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.synonymmap.format) | Keine. Verweise auf `Format` entfernen. |

Felddefinitionen sind optimiert: [SearchableField](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchablefield), [SimpleField](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.simplefield), [ComplexField](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.complexfield) sind neue APIs zur Erstellung von Felddefinitionen.

### <a name="indexers-datasources-skillsets"></a>Indexer, Datenquellen, Skillsets

| Version 10 | Entsprechung in Version 11 |
|------------|-----------------------|
| [Indexer](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer) | [SearchIndexer](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchindexer) |
| [DataSource](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.datasource) | [SearchIndexerDataSourceConnection](https://docs.microsoft.com//dotnet/api/azure.search.documents.indexes.models.searchindexerdatasourceconnection) |
| [Skill](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.skill) | [SearchIndexerSkill](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchindexerskill) |
| [Qualifikationsgruppe](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.skillset) | [SearchIndexerSkillset](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchindexerskillse) |
| [DataSourceType](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.datasourcetype) | [SearchIndexerDataSourceType](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.models.searchindexerdatasourcetype) |

### <a name="data-import"></a>Datenimport

| Version 10 | Entsprechung in Version 11 |
|------------|-----------------------|
| [IndexAction](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexaction) | [IndexDocumentsAction](https://docs.microsoft.com/dotnet/api/azure.search.documents.models.indexdocumentsaction) |
| [IndexBatch](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexbatch) | [IndexDocumentsBatch](https://docs.microsoft.com/dotnet/api/azure.search.documents.models.indexdocumentsbatch) |

### <a name="query-definitions-and-results"></a>Abfragedefinitionen und -ergebnisse

| Version 10 | Entsprechung in Version 11 |
|------------|-----------------------|
| [DocumentSearchResult](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.documentsearchresult-1) | [SearchResult](https://docs.microsoft.com/dotnet/api/azure.search.documents.models.searchresult-1) oder [SearchResults](https://docs.microsoft.com/dotnet/api/azure.search.documents.models.searchresults-1), abhängig davon, ob das Ergebnis ein einziges Dokument oder mehrere Dokumente ist. |
| [DocumentSuggestResult](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.documentsuggestresult-1) | [SuggestResults](https://docs.microsoft.com/dotnet/api/azure.search.documents.models.suggestresults-1) |
| [SearchParameters](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters) |  [SearchOptions](https://docs.microsoft.com/dotnet/api/azure.search.documents.searchoptions)  |

<a name="WhatsNew"></a>

## <a name="whats-in-version-11"></a>Neuerungen in Version 11

Jede Version einer Azure Cognitive Search-Clientbibliothek ist auf eine entsprechende Version der REST-API ausgelegt. Die REST-API gilt als Basis für den Dienst, wobei einzelne SDKs eine Version der REST-API umschließen. Für .NET-Entwickler kann es hilfreich sein, die [REST-API-Dokumentation](https://docs.microsoft.com/rest/api/searchservice/) durchzusehen, wenn Sie mehr Hintergrundinformationen zu bestimmten Objekten oder Vorgängen benötigen.

Version 11 ist auf den [2020-06-30-Suchdienst](https://github.com/Azure/azure-rest-api-specs/blob/master/specification/search/data-plane/Azure.Search/preview/2020-06-30/searchservice.json) ausgelegt. Da es sich bei Version 11 auch um eine von Grund auf neu erstellte Clientbibliothek handelt, konzentriert sich der größte Teil der Entwicklungsarbeit auf die Äquivalenz mit Version 10, wobei die Unterstützung einiger REST-API-Features noch aussteht.

Version 11 bietet vollständige Unterstützung für die folgenden Objekte und Vorgänge:

+ Indexerstellung und -verwaltung
+ Erstellung und Verwaltung von Synonymzuordnungen
+ Jegliche Abfragetypen und Syntax (ausgenommen räumliche Filter)
+ Indexerobjekte und -vorgänge zur Indizierung von Azure-Datenquellen, einschließlich Datenquellen und Skillsets

### <a name="pending-features"></a>Ausstehende Features

Die folgenden Features der Version 10 sind noch nicht in Version 11 verfügbar. Wenn Sie diese Features verwenden, warten Sie mit der Migration, bis diese unterstützt werden.

+ Räumliche Typen
+ [FieldBuilder](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.fieldbuilder) (obwohl Sie [diese Umgehung](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/search/Azure.Search.Documents/tests/Samples/FieldBuilder/FieldBuilder.cs) verwenden können).
+ [Wissensspeicher](knowledge-store-concept-intro.md)

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a>Schritte zum Upgrade

Mit den folgenden Schritten können Sie eine Codemigration beginnen, indem Sie die ersten erforderlichen Aufgaben durchgehen, insbesondere im Hinblick auf die Clientverweise.

1. Installieren Sie das [Azure.Search.Documents-Paket](https://www.nuget.org/packages/Azure.Search.Documents/), indem Sie mit der rechten Maustaste auf Ihre Projektreferenzen klicken und in Visual Studio „NuGet-Pakete verwalten...“ auswählen.

1. Ersetzen Sie die using-Anweisungen für Microsoft.Azure.Search durch die folgenden:

   ```csharp
   using Azure;
   using Azure.Search.Documents;
   using Azure.Search.Documents.Indexes;
   using Azure.Search.Documents.Indexes.Models;
   using Azure.Search.Documents.Models;
   ```

1. Ersetzen Sie [SearchCredentials](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchcredentials) durch [AzureKeyCredential](https://docs.microsoft.com/dotnet/api/azure.azurekeycredential).

1. Aktualisieren Sie Clientverweise für indexerbezogene Objekte. Wenn Sie Indexer, Datenquellen oder Skillsets verwenden, ändern Sie die Clientverweise in [SearchIndexerClient](https://docs.microsoft.com/dotnet/api/azure.search.documents.indexes.searchindexerclient). Dieser Client ist in Version 11 neu und hat keine Vorgängerversion.

1. Aktualisieren Sie Clientverweise für Abfragen und Datenimport. Instanzen von [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) müssen in [SearchClient](https://docs.microsoft.com/dotnet/api/azure.search.documents.searchclient) geändert werden. Stellen Sie sicher, dass Sie alle Instanzen abfangen, bevor Sie mit dem nächsten Schritt fortfahren, um Namensverwechslungen zu vermeiden.

1. Aktualisieren Sie Clientverweise für Index-, Indexer-, Synonymzuordnungs- und Analysetoolobjekte. Instanzen von [SearchServiceClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchserviceclient) müssen in [SearchIndexClient](https://docs.microsoft.com/dotnet/api/azure.search.documents.searchindexclient) geändert werden. 

1. Aktualisieren Sie die Klassen, Methoden und Eigenschaften so weit wie möglich, um die APIs der neuen Bibliothek zu verwenden. Sie können mit dem Abschnitt [Benennungsunterschiede](#naming-differences) beginnen oder auch das [Änderungsprotokoll](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/search/Azure.Search.Documents/CHANGELOG.md) einsehen.

   Wenn Sie Schwierigkeiten haben, entsprechende APIs zu finden, schlagen wir vor, ein Problem unter [https://github.com/MicrosoftDocs/azure-docs/issues](https://github.com/MicrosoftDocs/azure-docs/issues) zu melden, damit wir die Dokumentation verbessern oder das Problem untersuchen können.

1. Generieren Sie die Projektmappe neu. Wenn Sie alle Buildfehler bzw. Warnungen behoben haben, können Sie weitere Änderungen an Ihrer Anwendung vornehmen, um die [neue Funktionalität](#WhatsNew) zu nutzen.

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-11"></a>Breaking Changes in Version 11

Angesichts der tiefgreifenden Änderungen an Bibliotheken und APIs ist ein Upgrade auf Version 11 nicht trivial und stellt einen Breaking Change in der Hinsicht dar, dass Ihr Code nicht mehr abwärtskompatibel mit Version 10 und früheren Versionen ist. Eine ausführliche Übersicht über die Unterschiede finden Sie in dem [Änderungsprotokoll](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/search/Azure.Search.Documents/CHANGELOG.md) für `Azure.Search.Documents`.

In Bezug auf die Dienstversionen bringt der Wechsel von 10 auf 11 die folgenden Behavior Changes mit sich: 

+ Der [BM25-Ähnlichkeitsalgorithmus für die Rangfolge](index-ranking-similarity.md) ersetzt den bisherigen Rangfolgealgorithmus durch neuere Technologie. Neue Dienste verwenden diesen Algorithmus automatisch. Für vorhandene Dienste müssen Sie Parameter festlegen, um den neuen Algorithmus zu verwenden.

+ Die Behandlung von Nullwerten in [sortierten Ergebnissen](search-query-odata-orderby.md) hat sich in dieser Version geändert, Nullwerte werden bei `asc`-Sortierung zuerst und bei `desc`-Sortierung zuletzt angezeigt. Wenn Sie die Handhabung von Nullwerten in Code geschrieben haben, sollten Sie diesen überprüfen und möglicherweise entfernen, wenn er nicht mehr erforderlich ist.

## <a name="next-steps"></a>Nächste Schritte

+ [Azure.Search.Documents-Paket](https://www.nuget.org/packages/Azure.Search.Documents/)
+ [Beispiele bei GitHub](https://github.com/azure/azure-sdk-for-net/tree/Azure.Search.Documents_11.0.0/sdk/search/Azure.Search.Documents/samples)
+ [Azure.Search.Document-API-Referenz](https://docs.microsoft.com/dotnet/api/overview/azure/search.documents-readme?view=azure-dotnet)