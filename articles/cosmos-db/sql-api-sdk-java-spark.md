---
title: 'Azure Cosmos DB-Connector für Apache Spark für die SQL-API: Versionshinweise und Ressourcen'
description: Hier finden Sie umfassende Informationen zum Azure Cosmos DB-Connector für Apache Spark für die SQL-API – einschließlich Veröffentlichungsterminen, Deaktivierungsterminen und Änderungen an den einzelnen Versionen des Azure Cosmos DB SQL Async Java SDK.
author: anfeldma-ms
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.devlang: java
ms.topic: reference
ms.date: 08/05/2020
ms.author: anfeldma
ms.custom: devx-track-java
ms.openlocfilehash: 72b3b190492be5cec9986729875c5b09e2559ae5
ms.sourcegitcommit: 7fe8df79526a0067be4651ce6fa96fa9d4f21355
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87854119"
---
# <a name="azure-cosmos-db-apache-spark-connector-for-core-sql-api-release-notes-and-resources"></a>Azure Cosmos DB-Connector für Apache Spark für die Core-API (SQL): Versionshinweise und Ressourcen
> [!div class="op_single_selector"]
> * [.NET SDK v3](sql-api-sdk-dotnet-standard.md)
> * [.NET SDK v2](sql-api-sdk-dotnet.md)
> * [.NET Core SDK v2](sql-api-sdk-dotnet-core.md)
> * [.NET Change Feed SDK v2](sql-api-sdk-dotnet-changefeed.md)
> * [Node.js](sql-api-sdk-node.md)
> * [Java SDK v4](sql-api-sdk-java-v4.md)
> * [Asynchrones Java SDK v2](sql-api-sdk-async-java.md)
> * [Sync Java SDK v2](sql-api-sdk-java.md)
> * [Spring Data](sql-api-sdk-java-spring.md)
> * [Spark-Connector](sql-api-sdk-java-spark.md)
> * [Python](sql-api-sdk-python.md)
> * [REST](/rest/api/cosmos-db/)
> * [REST-Ressourcenanbieter](/rest/api/cosmos-db-resource-provider/)
> * [SQL](sql-api-query-reference.md)
> * [Bulk Executor – .NET v2](sql-api-sdk-bulk-executor-dot-net.md)
> * [Bulk Executor – Java](sql-api-sdk-bulk-executor-java.md)

Beschleunigen Sie Big Data-Analysen mit dem Azure Cosmos DB-Connector für Apache Spark für Core (SQL). Der Spark-Connector ermöglicht die Ausführung von [Spark](https://spark.apache.org/)-Aufträgen für Daten, die in Azure Cosmos DB gespeichert sind. Batch- und Streamverarbeitung werden unterstützt.

Sie können den Connector mit [Azure Databricks](https://azure.microsoft.com/services/databricks) oder [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) verwenden, die beide verwaltete Spark-Cluster in Azure bieten. Die folgende Tabelle zeigt die unterstützten Spark-Versionen.

| Komponente | Version |
|---------|-------|
| Apache Spark | 2.4.x, 2.3.x, 2.2.x und 2.1.x |
| Scala | 2.11 |
| Azure Databricks Runtime-Version | 3\.4 und höher |

> [!WARNING]
> Dieser Connector unterstützt die Haupt-(SQL)-API von Azure Cosmos DB.
> Verwenden Sie für die Cosmos DB für MongoDB-API den [MongoDB-Spark-Connector](https://docs.mongodb.com/spark-connector/master/).
> Verwenden Sie für die Cosmos DB-Cassandra-API den [Cassandra-Spark-Connector](https://github.com/datastax/spark-cassandra-connector).
>

## <a name="helpful-content"></a>Hilfreiche Inhalte

| Inhalt | Link |
|---|---|
| **SDK-Download** | [Download von Apache Spark](https://aka.ms/CosmosDB_OLTP_Spark_2.4_LKG) |
|**API-Dokumentation** | [Spark Connector-Referenz]() |
|**Am SDK mitwirken** | [Azure Cosmos DB-Connector für Apache Spark auf GitHub](https://github.com/Azure/azure-cosmosdb-spark) | 
|**Erste Schritte** | [Beschleunigen von Big Data-Analysen mit dem Apache Spark-Connector für Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/spark-connector#bk_working_with_connector) <br> [Verwenden von strukturiertem Apache Spark-Streaming mit Apache Kafka und Azure Cosmos DB](https://docs.microsoft.com/azure/hdinsight/apache-kafka-spark-structured-streaming-cosmosdb?toc=/azure/cosmos-db/toc.json&bc=/azure/cosmos-db/breadcrumb/toc.json) | 

## <a name="release-history"></a>Releaseverlauf

### <a name="311"></a>3.1.1
#### <a name="new-features"></a>Neue Funktionen
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen
* Grenzfall im Zusammenhang mit dem Streamingprüfpunkt korrigiert, bei dem die ID das Zeichen „|“ enthält und die Konfiguration „ChangeFeedMaxPagesPerBatch" angewendet wurde

### <a name="310"></a>3.1.0
#### <a name="new-features"></a>Neue Funktionen
* Unterstützung für Massenaktualisierungen bei Verwendung geschachtelter Partitionsschlüssel hinzugefügt
* Unterstützung von Dezimal- und Gleitkommadatentypen bei Schreibvorgängen in Cosmos DB hinzugefügt
* Unterstützung von Zeitstempeltypen mit Long-Wert (Unix-Epoche) hinzugefügt
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen

### <a name="308"></a>3.0.8
#### <a name="new-features"></a>Neue Funktionen
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen
* Typumwandlungsausnahme bei Verwendung der Konfiguration „WriteThroughputBudget“ korrigiert

### <a name="307"></a>3.0.7
#### <a name="new-features"></a>Neue Funktionen
* Fehlerinformationen für Massenfehler zu Ausnahme und Protokoll hinzugefügt
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen

### <a name="306"></a>3.0.6
#### <a name="new-features"></a>Neue Funktionen
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen
* Probleme im Zusammenhang mit dem Streamingprüfpunkt behoben

### <a name="305"></a>3.0.5
#### <a name="new-features"></a>Neue Funktionen
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen
* Problem behoben, sodass die Protokollstufe einer Meldung nicht mehr unbeabsichtigt auf der Stufe „FEHLER“ verbleibt, um unnötige Informationen zu verringern

### <a name="304"></a>3.0.4
#### <a name="new-features"></a>Neue Funktionen
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen
* Fehler im strukturierten Streaming bei Partitionsteilungen behoben. Dadurch werden möglicherweise einige Änderungsfeed-Datensätze übersehen oder bei Prüfpunkt-Schreibvorgängen keine Ausnahmen angezeigt.

### <a name="303"></a>3.0.3
#### <a name="new-features"></a>Neue Funktionen
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen
* Fehler behoben, der dazu führte, dass ein benutzerdefiniertes, für „readStream“ angegebenes Schema ignoriert wird

### <a name="302"></a>3.0.2
#### <a name="new-features"></a>Neue Funktionen
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen
* Regression korrigiert (JAR-Datei ohne Shading enthält alle Abhängigkeiten mit Shading), durch die sich die Buildzeit um 50 Prozent erhöhte

### <a name="301"></a>3.0.1
#### <a name="new-features"></a>Neue Funktionen
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen
* Abhängigkeitsproblem korrigiert, das dazu führte, dass der direkte Transport über TCP nicht erfolgreich war und der Fehler „RequestTimeoutException“ auftrat

### <a name="300"></a>3.0.0
#### <a name="new-features"></a>Neue Funktionen
* Weniger Metadatenaufrufe dank verbesserter Verbindungsverwaltung und verbessertem Verbindungspooling
#### <a name="key-bug-fixes"></a>Wichtige Fehlerbehebungen

## <a name="faq"></a>Häufig gestellte Fragen
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Cosmos DB finden Sie auf der Seite zum Dienst [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

Weitere Informationen zu Apache Spark finden Sie auf der [Homepage](https://spark.apache.org/).