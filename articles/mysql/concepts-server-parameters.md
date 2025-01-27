---
title: Serverparameter – Azure Database for MySQL
description: Dieses Thema bietet Richtlinien für die Konfiguration von Serverparametern in Azure Database for MySQL.
author: ajlam
ms.author: andrela
ms.service: mysql
ms.topic: conceptual
ms.date: 6/25/2020
ms.openlocfilehash: de1345fca418118e88929870cd2f4007dd36b3a4
ms.sourcegitcommit: 2ff0d073607bc746ffc638a84bb026d1705e543e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87835985"
---
# <a name="server-parameters-in-azure-database-for-mysql"></a>Serverparameter in Azure Database for MySQL

Dieser Artikel enthält Überlegungen und Richtlinien zur Konfiguration von Serverparametern in Azure Database for MySQL.

## <a name="what-are-server-parameters"></a>Was sind Serverparameter? 

Das MySQL-Modul bietet viele verschiedene Servervariablen/-parameter, die zur Konfiguration und Optimierung des Modulverhaltens verwendet werden können. Einige der Parameter können dynamisch während der Laufzeit festgelegt werden, während andere „statisch“ sind und ihre Anwendung einen Neustart des Servers erfordert.

Azure Database for MySQL bietet die Möglichkeit, den Wert verschiedener MySQL-Serverparameter unter Verwendung von [Azure-Portal](./howto-server-parameters.md), [Azure-Befehlszeilenschnittstelle](./howto-configure-server-parameters-using-cli.md) und [PowerShell](./howto-configure-server-parameters-using-powershell.md) zu ändern, um den Anforderungen Ihrer Workload zu entsprechen.

## <a name="configurable-server-parameters"></a>Konfigurierbare Serverparameter

Die Liste der unterstützten Serverparameter wächst ständig. Sie können die vollständige Liste im Azure-Portal auf der Registerkarte „Serverparameter“ anzeigen und die Werte der Serverparameter dort konfigurieren.

In den folgenden Abschnitten erfahren Sie mehr über die Grenzen der verschiedenen häufig aktualisierten Serverparameter. Die Grenzwerte werden durch den Tarif und die Anzahl der virtuellen Kerne des Servers bestimmt.

### <a name="thread-pools"></a>Threadpools

MySQL weist traditionell einen Thread für jede Clientverbindung zu. Wenn die Zahl der gleichzeitigen Benutzer wächst, sinkt die Leistung entsprechend. Viele aktive Threads können die Leistung aufgrund von erhöhtem Kontextwechsel, Threadkonflikten und ungeeignetem Speicherort für CPU-Caches erheblich beeinträchtigen.

Threadpools sind ein serverseitiges Feature und unterscheiden sich vom Verbindungspooling. Sie maximieren die Leistung durch die Einführung eines dynamischen Pools von Arbeitsthreads, mit dem die Anzahl der aktiven Threads, die auf dem Server ausgeführt werden, begrenzt und die Threadänderung minimiert werden kann. Auf diese Weise wird sichergestellt, dass dem Server bei einer Häufung der Verbindungen nicht die Ressourcen ausgehen oder er mit einem Fehler durch ungenügenden Arbeitsspeicher abstürzt. Threadpools sind am effizientesten für kurze Abfragen und CPU-intensive Workloads, z. B. OLTP-Workloads.

Weitere Informationen zu Threadpools finden Sie unter [Einführung in Threadpools in Azure Database for MySQL](https://techcommunity.microsoft.com/t5/azure-database-for-mysql/introducing-thread-pools-in-azure-database-for-mysql-service/ba-p/1504173)

> [!NOTE]
> Die Threadpoolfunktion wird für MySQL 5.6 nicht unterstützt. 

### <a name="configuring-the-thread-pool"></a>Konfigurieren des Threadpools
Aktualisieren Sie zum Aktivieren des Threadpools den Serverparameter `thread_handling` auf „pool-of-threads“. Standardmäßig ist dieser Parameter auf `one-thread-per-connection` festgelegt, was bedeutet, dass MySQL für jede neue Verbindung einen neuen Thread erzeugt. Beachten Sie, dass es sich hierbei um einen statischen Parameter handelt, der zur Anwendung einen Serverneustart erfordert.

Sie können auch die maximale und minimale Anzahl von Threads im Pool konfigurieren, indem Sie die folgenden Serverparameter festlegen: 
- `thread_pool_max_threads`: Dieser Wert stellt sicher, dass es nicht mehr als diese Anzahl von Threads im Pool gibt.
- `thread_pool_min_threads`: Dieser Wert legt die Anzahl der Threads fest, die auch nach dem Schließen von Verbindungen reserviert werden.

Um Leistungsprobleme bei kurzen Abfragen im Threadpool zu verbessern, können Sie mit Azure Database for MySQL eine Batchausführung aktivieren, bei der die Threads, anstatt unmittelbar nach der Ausführung einer Abfrage wieder in den Threadpool zurückzukehren, für kurze Zeit aktiv bleiben, um über diese Verbindung auf die nächste Abfrage zu warten. Der Thread führt dann die Abfrage schnell aus und wartet nach Abschluss auf die nächste Abfrage, bis der Gesamtzeitverbrauch dieses Prozesses einen Schwellenwert überschreitet. Das Verhalten der Batchausführung wird anhand der folgenden Serverparameter bestimmt:  

-  `thread_pool_batch_wait_timeout`: Dieser Wert gibt die Zeit an, die ein Thread auf die Verarbeitung einer anderen Abfrage wartet.
- `thread_pool_batch_max_time`: Dieser Wert bestimmt die maximale Zeit, die ein Thread den Zyklus der Abfrageausführung und des Wartens auf die nächste Abfrage wiederholt.

> [!IMPORTANT]
> Testen Sie den Threadpool, bevor Sie ihn in der Produktionsumgebung aktivieren. 

### <a name="innodb_buffer_pool_size"></a>innodb_buffer_pool_size

Weitere Informationen zu diesem Parameter finden Sie in der [MySQL-Dokumentation](https://dev.mysql.com/doc/refman/5.7/en/innodb-parameters.html#sysvar_innodb_buffer_pool_size).

#### <a name="servers-supporting-up-to-4-tb-storage"></a>Server, die bis zu 4 TB Speicher unterstützen

|**Tarif**|**vCore(s)**|**Standardwert (Bytes)**|**Mindestwert (Bytes)**|**Höchstwert (Bytes)**|
|---|---|---|---|---|
|Basic|1|872415232|134217728|872415232|
|Basic|2|2684354560|134217728|2684354560|
|Universell|2|3758096384|134217728|3758096384|
|Universell|4|8053063680|134217728|8053063680|
|Universell|8|16106127360|134217728|16106127360|
|Universell|16|32749125632|134217728|32749125632|
|Universell|32|66035122176|134217728|66035122176|
|Universell|64|132070244352|134217728|132070244352|
|Arbeitsspeicheroptimiert|2|7516192768|134217728|7516192768|
|Arbeitsspeicheroptimiert|4|16106127360|134217728|16106127360|
|Arbeitsspeicheroptimiert|8|32212254720|134217728|32212254720|
|Arbeitsspeicheroptimiert|16|65498251264|134217728|65498251264|
|Arbeitsspeicheroptimiert|32|132070244352|134217728|132070244352|

#### <a name="servers-support-up-to-16-tb-storage"></a>Server, die bis zu 16 TB Speicher unterstützen

|**Tarif**|**vCore(s)**|**Standardwert (Bytes)**|**Mindestwert (Bytes)**|**Höchstwert (Bytes)**|
|---|---|---|---|---|
|Basic|1|872415232|134217728|872415232|
|Basic|2|2684354560|134217728|2684354560|
|Universell|2|7516192768|134217728|7516192768|
|Universell|4|16106127360|134217728|16106127360|
|Universell|8|32212254720|134217728|32212254720|
|Universell|16|65498251264|134217728|65498251264|
|Universell|32|132070244352|134217728|132070244352|
|Universell|64|264140488704|134217728|264140488704|
|Arbeitsspeicheroptimiert|2|15032385536|134217728|15032385536|
|Arbeitsspeicheroptimiert|4|32212254720|134217728|32212254720|
|Arbeitsspeicheroptimiert|8|64424509440|134217728|64424509440|
|Arbeitsspeicheroptimiert|16|130996502528|134217728|130996502528|
|Arbeitsspeicheroptimiert|32|264140488704|134217728|264140488704|

### <a name="innodb_file_per_table"></a>innodb_file_per_table

> [!NOTE]
> `innodb_file_per_table` kann nur in den Tarifen „Universell“ und „Arbeitsspeicheroptimiert“ aktualisiert werden.

MySQL speichert die InnoDB-Tabelle in verschiedenen Tabellenbereichen, basierend auf der Konfiguration, die Sie während der Tabellenerstellung angegeben haben. Der [Systemtabellenbereich](https://dev.mysql.com/doc/refman/5.7/en/innodb-system-tablespace.html) ist der Speicherbereich für das InnoDB-Datenwörterbuch. Ein [file-per-table-Tabellenbereich](https://dev.mysql.com/doc/refman/5.7/en/innodb-file-per-table-tablespaces.html) enthält die Daten und Indizes für eine einzelne InnoDB-Tabelle und wird im Dateisystem in einer eigenen Datendatei gespeichert. Dieses Verhalten wird vom `innodb_file_per_table`-Serverparameter gesteuert. Durch Festlegen von `innodb_file_per_table` auf `OFF` werden Tabellen von InnoDB im Systemtabellenbereich erstellt. Andernfalls werden die Tabellen im Tabellen-Tabellenbereich erstellt.

Azure Database for MySQL unterstützt bis zu **1 TB** in einer einzelnen Datendatei. Wenn die Datenbankgröße 1 TB überschreitet, sollten Sie die Tabelle in [innodb_file_per_table](https://dev.mysql.com/doc/refman/5.7/en/innodb-parameters.html#sysvar_innodb_file_per_table) erstellen. Wenn eine einzelne Tabelle größer als ein Terabyte ist, sollten Sie die Partitionstabelle verwenden.

### <a name="join_buffer_size"></a>join_buffer_size

Weitere Informationen zu diesem Parameter finden Sie in der [MySQL-Dokumentation](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html#sysvar_join_buffer_size).

|**Tarif**|**vCore(s)**|**Standardwert (Bytes)**|**Mindestwert (Bytes)**|**Höchstwert (Bytes)**|
|---|---|---|---|---|
|Basic|1|Nicht konfigurierbar im Basic-Tarif|–|–|
|Basic|2|Nicht konfigurierbar im Basic-Tarif|–|–|
|Universell|2|262144|128|268435455|
|Universell|4|262144|128|536870912|
|Universell|8|262144|128|1073741824|
|Universell|16|262144|128|2147483648|
|Universell|32|262144|128|4294967295|
|Universell|64|262144|128|4294967295|
|Arbeitsspeicheroptimiert|2|262144|128|536870912|
|Arbeitsspeicheroptimiert|4|262144|128|1073741824|
|Arbeitsspeicheroptimiert|8|262144|128|2147483648|
|Arbeitsspeicheroptimiert|16|262144|128|4294967295|
|Arbeitsspeicheroptimiert|32|262144|128|4294967295|

### <a name="max_connections"></a>max_connections

|**Tarif**|**vCore(s)**|**Standardwert**|**Mindestwert**|**Höchstwert**|
|---|---|---|---|---|
|Basic|1|50|10|50|
|Basic|2|100|10|100|
|Universell|2|300|10|600|
|Universell|4|625|10|1250|
|Universell|8|1250|10|2500|
|Universell|16|2500|10|5.000|
|Universell|32|5\.000|10|10000|
|Universell|64|10000|10|20000|
|Arbeitsspeicheroptimiert|2|625|10|1250|
|Arbeitsspeicheroptimiert|4|1250|10|2500|
|Arbeitsspeicheroptimiert|8|2500|10|5.000|
|Arbeitsspeicheroptimiert|16|5.000|10|10000|
|Arbeitsspeicheroptimiert|32|10000|10|20000|

Wenn Verbindungen den Grenzwert übersteigen, erhalten Sie möglicherweise den folgenden Fehler:
> FEHLER 1040 (08004): Zu viele Verbindungen

> [!IMPORTANT]
> Für eine optimale Erfahrung empfehlen wir, dass Sie einen Verbindungsspooler wie ProxySQL verwenden, um Verbindungen effizient zu verwalten.

Das Erstellen neuer Clientverbindungen mit MySQL nimmt Zeit in Anspruch, und nach der Herstellung belegen diese Verbindungen Datenbankressourcen, auch wenn Sie sich im Leerlauf befinden. Die meisten Anwendungen fordern viele kurzlebige Verbindungen an, was diese Situation erschwert. Das Ergebnis sind weniger Ressourcen, die für ihre tatsächliche Workload verfügbar sind, was zu verringerter Leistung führt. Ein Verbindungspooler, der Verbindungen im Leerlauf reduziert und vorhandene Verbindungen wiederverwendet, hilft dabei, dies zu vermeiden. Weitere Informationen zum Einrichten von ProxySQL finden Sie in unserem [Blogbeitrag](https://techcommunity.microsoft.com/t5/azure-database-for-mysql/load-balance-read-replicas-using-proxysql-in-azure-database-for/ba-p/880042).

>[!Note]
>ProxySQL ist ein Open Source-Communitytool. Es wird von Microsoft bestmöglich unterstützt. Wenden Sie sich an den [ProxySQL-Produktsupport](https://proxysql.com/services/support/), wenn Sie Produktionssupport mit autoritativen Hinweisen benötigen.

### <a name="max_heap_table_size"></a>max_heap_table_size

Weitere Informationen zu diesem Parameter finden Sie in der [MySQL-Dokumentation](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html#sysvar_max_heap_table_size).

|**Tarif**|**vCore(s)**|**Standardwert (Bytes)**|**Mindestwert (Bytes)**|**Höchstwert (Bytes)**|
|---|---|---|---|---|
|Basic|1|Nicht konfigurierbar im Basic-Tarif|–|–|
|Basic|2|Nicht konfigurierbar im Basic-Tarif|–|–|
|Universell|2|16777216|16384|268435455|
|Universell|4|16777216|16384|536870912|
|Universell|8|16777216|16384|1073741824|
|Universell|16|16777216|16384|2147483648|
|Universell|32|16777216|16384|4294967295|
|Universell|64|16777216|16384|4294967295|
|Arbeitsspeicheroptimiert|2|16777216|16384|536870912|
|Arbeitsspeicheroptimiert|4|16777216|16384|1073741824|
|Arbeitsspeicheroptimiert|8|16777216|16384|2147483648|
|Arbeitsspeicheroptimiert|16|16777216|16384|4294967295|
|Arbeitsspeicheroptimiert|32|16777216|16384|4294967295|

### <a name="query_cache_size"></a>query_cache_size

Der Abfragecache ist standardmäßig deaktiviert. Um den Abfragecache zu aktivieren, konfigurieren Sie den Parameter `query_cache_type`. 

Weitere Informationen zu diesem Parameter finden Sie in der [MySQL-Dokumentation](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html#sysvar_query_cache_size).

> [!NOTE]
> Der Abfragecache ist seit MySQL 5.7.20 veraltet und wurde in MySQL 8.0 entfernt.

|**Tarif**|**vCore(s)**|**Standardwert (Bytes)**|**Mindestwert (Bytes)**|**Höchstwert **|
|---|---|---|---|---|
|Basic|1|Nicht konfigurierbar im Basic-Tarif|–|–|
|Basic|2|Nicht konfigurierbar im Basic-Tarif|–|–|
|Universell|2|0|0|16777216|
|Universell|4|0|0|33554432|
|Universell|8|0|0|67108864|
|Universell|16|0|0|134217728|
|Universell|32|0|0|134217728|
|Universell|64|0|0|134217728|
|Arbeitsspeicheroptimiert|2|0|0|33554432|
|Arbeitsspeicheroptimiert|4|0|0|67108864|
|Arbeitsspeicheroptimiert|8|0|0|134217728|
|Arbeitsspeicheroptimiert|16|0|0|134217728|
|Arbeitsspeicheroptimiert|32|0|0|134217728|

### <a name="lower_case_table_names"></a>lower_case_table_names

„lower_case_table_name“ ist standardmäßig auf „1“ festgelegt, und Sie können diesen Parameter in MySQL 5.6 und MySQL 5.7 aktualisieren.

Weitere Informationen zu diesem Parameter finden Sie in der [MySQL-Dokumentation](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html#sysvar_lower_case_table_names).

> [!NOTE]
> In MySQL 8.0 ist „lower_case_table_name“ standardmäßig auf „1“ festgelegt, und Sie können dies nicht ändern.

### <a name="innodb_strict_mode"></a>innodb_strict_mode

Wenn ein Fehler wie „Zeile zu groß (> 8126)“ angezeigt wird, sollten Sie den Parameter **innodb_strict_mode** deaktivieren. Der Serverparameter **innodb_strict_mode** darf nicht global auf der Serverebene geändert werden, da die Daten bei Überschreitung einer Zeilendatengröße von 8.000 ohne Fehlermeldung gekürzt werden, was zu Datenverlusten führen kann. Es wird empfohlen, das Schema so zu ändern, dass es der Seitengrößenbeschränkung entspricht. 

Dieser Parameter kann mithilfe von `init_connect` auf Sitzungsebene festgelegt werden. Informationen zum Festlegen von **innodb_strict_mode** auf Sitzungsebene finden Sie [Nicht aufgeführte Einstellungsparameter](https://docs.microsoft.com/azure/mysql/howto-server-parameters#setting-parameters-not-listed).

### <a name="sort_buffer_size"></a>sort_buffer_size

Weitere Informationen zu diesem Parameter finden Sie in der [MySQL-Dokumentation](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html#sysvar_sort_buffer_size).

|**Tarif**|**vCore(s)**|**Standardwert (Bytes)**|**Mindestwert (Bytes)**|**Höchstwert (Bytes)**|
|---|---|---|---|---|
|Basic|1|Nicht konfigurierbar im Basic-Tarif|–|–|
|Basic|2|Nicht konfigurierbar im Basic-Tarif|–|–|
|Universell|2|524288|32768|4194304|
|Universell|4|524288|32768|8388608|
|Universell|8|524288|32768|16777216|
|Universell|16|524288|32768|33554432|
|Universell|32|524288|32768|33554432|
|Universell|64|524288|32768|33554432|
|Arbeitsspeicheroptimiert|2|524288|32768|8388608|
|Arbeitsspeicheroptimiert|4|524288|32768|16777216|
|Arbeitsspeicheroptimiert|8|524288|32768|33554432|
|Arbeitsspeicheroptimiert|16|524288|32768|33554432|
|Arbeitsspeicheroptimiert|32|524288|32768|33554432|

### <a name="tmp_table_size"></a>tmp_table_size

Weitere Informationen zu diesem Parameter finden Sie in der [MySQL-Dokumentation](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html#sysvar_tmp_table_size).

|**Tarif**|**vCore(s)**|**Standardwert (Bytes)**|**Mindestwert (Bytes)**|**Höchstwert (Bytes)**|
|---|---|---|---|---|
|Basic|1|Nicht konfigurierbar im Basic-Tarif|–|–|
|Basic|2|Nicht konfigurierbar im Basic-Tarif|–|–|
|Universell|2|16777216|1024|67108864|
|Universell|4|16777216|1024|134217728|
|Universell|8|16777216|1024|268435456|
|Universell|16|16777216|1024|536870912|
|Universell|32|16777216|1024|1073741824|
|Universell|64|16777216|1024|1073741824|
|Arbeitsspeicheroptimiert|2|16777216|1024|134217728|
|Arbeitsspeicheroptimiert|4|16777216|1024|268435456|
|Arbeitsspeicheroptimiert|8|16777216|1024|536870912|
|Arbeitsspeicheroptimiert|16|16777216|1024|1073741824|
|Arbeitsspeicheroptimiert|32|16777216|1024|1073741824|

### <a name="time_zone"></a>time_zone

Bei der ersten Bereitstellung enthält ein Azure for MySQL-Server Systemtabellen für Zeitzoneninformationen, aber diese Tabellen sind nicht gefüllt. Die Zeitzonentabellen können durch Aufrufen der gespeicherten Prozedur `mysql.az_load_timezone` über ein Tool wie die MySQL-Befehlszeile oder MySQL Workbench aufgefüllt werden. Informationen zum Aufrufen der gespeicherten Prozedur und zum Festlegen der globalen Zeitzonen oder Zeitzonen auf Sitzungsebene finden Sie in den Artikeln für das [Azure-Portal](howto-server-parameters.md#working-with-the-time-zone-parameter) und die [Azure CLI](howto-configure-server-parameters-using-cli.md#working-with-the-time-zone-parameter).

## <a name="non-configurable-server-parameters"></a>Nicht konfigurierbare Serverparameter

Die folgenden Serverparameter können im Dienst nicht konfiguriert werden:

|**Parameter**|**Fester Wert**|
| :------------------------ | :-------- |
|innodb_file_per_table (im Tarif „Basic“)|OFF|
|innodb_flush_log_at_trx_commit|1|
|sync_binlog|1|
|innodb_log_file_size|256 MB|
|innodb_log_files_in_group|2|

Andere Variablen, die hier nicht aufgeführt sind, werden auf die MySQL-Standardwerte festgelegt. Die Standardwerte finden Sie in den MySQL-Dokumentationen für die Versionen [8.0](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html), [5.7](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html) und [5.6](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html). 

## <a name="next-steps"></a>Nächste Schritte

- Informationen zum [Konfigurieren von Serverparametern mithilfe des Azure-Portals](./howto-server-parameters.md)
- Informationen zum [Konfigurieren von Serverparametern mithilfe der Azure CLI](./howto-configure-server-parameters-using-cli.md)
- Informationen zum [Konfigurieren von Serverparametern mithilfe von PowerShell](./howto-configure-server-parameters-using-powershell.md)
