---
title: 'Azure Cosmos DB: SQL Async Java-API, SDK und Ressourcen'
description: Wichtige Informationen zur SQL Async Java-API und zum SDK, einschließlich Veröffentlichungsterminen, Deaktivierungsterminen und Änderungen an den einzelnen Versionen des Azure Cosmos DB SQL Async Java SDK.
author: anfeldma-ms
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.devlang: java
ms.topic: reference
ms.date: 08/05/2020
ms.author: anfeldma
ms.custom: devx-track-java
ms.openlocfilehash: 3f7b6c46a69acf8eea546469cf7919e86703f17c
ms.sourcegitcommit: 7fe8df79526a0067be4651ce6fa96fa9d4f21355
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87852683"
---
# <a name="azure-cosmos-db-async-java-sdk-for-sql-api-release-notes-and-resources"></a>Azure Cosmos DB Async Java SDK für die SQL-API: Versionshinweise und Ressourcen
> [!div class="op_single_selector"]
> * [.NET SDK v3](sql-api-sdk-dotnet-standard.md)
> * [.NET SDK v2](sql-api-sdk-dotnet.md)
> * [.NET Core SDK v2](sql-api-sdk-dotnet-core.md)
> * [.NET Change Feed SDK v2](sql-api-sdk-dotnet-changefeed.md)
> * [Node.js](sql-api-sdk-node.md)
> * [Java SDK v4](sql-api-sdk-java-v4.md)
> * [Async Java SDK v2](sql-api-sdk-async-java.md)
> * [Sync Java SDK v2](sql-api-sdk-java.md)
> * [Spring Data](sql-api-sdk-java-spring.md)
> * [Spark-Connector](sql-api-sdk-java-spark.md)
> * [Python](sql-api-sdk-python.md)
> * [REST](/rest/api
> * [REST-Ressourcenanbieter](/azure/azure-resource-manager/management/azure-services-resource-providers)
> * [SQL](sql-api-query-reference.md)
> * [Bulk Executor – .NET v2](sql-api-sdk-bulk-executor-dot-net.md)
> * [Bulk Executor – Java](sql-api-sdk-bulk-executor-java.md)

Das Async Java SDK für die SQL-API unterscheidet sich vom Java SDK für die SQL-API dahingehend, dass es asynchrone Vorgänge mit Unterstützung der [Netty-Bibliothek](https://netty.io/) bereitstellt. Das bereits vorhandene [Java SDK für die SQL-API](sql-api-sdk-java.md) unterstützt asynchrone Vorgänge nicht. 

> [!IMPORTANT]  
> Dies ist *nicht* das neueste Java SDK für Azure Cosmos DB! Erwägen Sie die Verwendung des [Azure Cosmos DB Java SDK v4](sql-api-sdk-java-v4.md) für Ihr Projekt. Befolgen Sie für ein Upgrade die Anweisungen in den Anleitungen [Migrieren zum Azure Cosmos DB Java SDK v4](migrate-java-v4-sdk.md) und [Gegenüberstellung von Reactor und RxJava](https://github.com/Azure-Samples/azure-cosmos-java-sql-api-samples/blob/master/reactor-rxjava-guide.md). 
>

| |  |
|---|---|
| **SDK-Download** | [Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-cosmosdb) |
|**API-Dokumentation** |[Java-API-Referenzdokumentation](https://docs.microsoft.com/java/api/com.microsoft.azure.cosmosdb.rx.asyncdocumentclient?view=azure-java-stable) | 
|**Am SDK mitwirken** | [GitHub](https://github.com/Azure/azure-cosmosdb-java) | 
|**Erste Schritte** | [Erste Schritte mit dem Async Java SDK](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started) | 
|**Codebeispiel** | [GitHub](https://github.com/Azure/azure-cosmosdb-java#usage-code-sample)| 
| **Leistungstipps**| [GitHub-Infodatei](https://github.com/Azure/azure-cosmosdb-java#guide-for-prod)| 
| **Unterstützte Mindestlaufzeit**|[JDK 8](/java/azure/jdk/?view=azure-java-stable) | 

[!INCLUDE [Release notes](~/azure-cosmosdb-java-v2/changelog/README.md)]
## <a name="faq"></a>Häufig gestellte Fragen
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Weitere Informationen
Weitere Informationen zu Cosmos DB finden Sie auf der Seite zum Dienst [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

