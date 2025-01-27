---
title: Codieren einer Client-App
titleSuffix: Azure Digital Twins
description: Tutorial zum Schreiben des Minimalcodes für eine Client-App mit dem .NET (C#) SDK.
author: cschormann
ms.author: cschorm
ms.date: 05/05/2020
ms.topic: tutorial
ms.service: digital-twins
ms.openlocfilehash: d063418bb8e78bf306dda8fc558bb0e3005dbd0a
ms.sourcegitcommit: 02ca0f340a44b7e18acca1351c8e81f3cca4a370
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88584895"
---
# <a name="coding-with-the-azure-digital-twins-apis"></a>Codieren mit den Azure Digital Twins-APIs

Entwickler, die mit Azure Digital Twins arbeiten, schreiben in der Regel eine Clientanwendung, um mit ihrer Azure Digital Twins-Dienstinstanz zu interagieren. Dieses Tutorial für Entwickler bietet eine Einführung in die Programmierung für den Azure Digital Twins-Dienst unter Verwendung der [Azure IoT Digital Twin-Clientbibliothek für .NET (C#)](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/digitaltwins/Azure.DigitalTwins.Core). Sie werden Schritt für Schritt und von Grund auf durch die Entwicklung einer Client-App für die C#-Konsole geleitet.

## <a name="prerequisites"></a>Voraussetzungen

Dieses Tutorial verwendet die Befehlszeile für Setup und Projektarbeit. Deshalb können Sie einen beliebigen Code-Editor verwenden, um die Übungen zu durchlaufen.

Zum Einstieg benötigen Sie Folgendes:
* Einen beliebigen Code-Editor
* **.NET Core 3.1** auf Ihrem Entwicklungscomputer. Sie können diese Version des .NET Core SDK für verschiedene Plattformen unter [Download .NET Core 3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1) herunterladen.

[!INCLUDE [Azure Digital Twins tutorials: instance prereq](../../includes/digital-twins-tutorial-prereq-instance.md)]

## <a name="set-up-project"></a>Einrichten des Projekts

Sobald Ihre Azure Digital Twins-Instanz bereit ist, können Sie mit der Einrichtung des Client-App-Projekts beginnen. 

Öffnen Sie eine Eingabeaufforderung oder ein anderes Konsolenfenster auf Ihrem Rechner, und erstellen Sie ein leeres Projektverzeichnis, in dem Sie Ihre Arbeit während dieses Tutorials speichern möchten. Geben Sie dem Verzeichnis einen beliebigen Namen (z. B. *DigitalTwinsCodeTutorial*).

Navigieren Sie zum neuen Verzeichnis.

Öffnen Sie das Projektverzeichnis, und erstellen Sie ein leeres .NET-Konsolen-App-Projekt. Führen Sie im Befehlsfenster den folgenden Befehl aus, um ein C#-Minimalprojekt für die Konsole zu erstellen:

```cmd/sh
dotnet new console
```

Auf diese Weise werden verschiedene Dateien in Ihrem Verzeichnis erstellt, darunter eine Datei mit dem Namen *Program.cs*, in der Sie den Großteil Ihres Codes schreiben werden.

Als Nächstes fügen Sie zwei erforderliche Abhängigkeiten für die Arbeit mit Azure Digital Twins hinzu:

```cmd/sh
dotnet add package Azure.DigitalTwins.Core --version 1.0.0-preview.3
dotnet add package Azure.identity --version 1.1.1
```

Die erste Abhängigkeit ist die [Azure IoT Digital Twin-Clientbibliothek für .NET](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/digitaltwins/Azure.DigitalTwins.Core). Die zweite Abhängigkeit stellt Tools bereit, die die Authentifizierung bei Azure unterstützen.

Lassen Sie das Befehlsfenster geöffnet, da Sie es während des gesamten Tutorials weiter verwenden werden.

## <a name="get-started-with-project-code"></a>Erste Schritte mit dem Projektcode

In diesem Abschnitt beginnen Sie damit, den Code für Ihr neues App-Projekt zur Arbeit mit Azure Digital Twins zu schreiben. Folgende Aufgaben werden behandelt:
* Authentifizierung beim Dienst
* Hochladen eines Modells
* Abfangen von Fehlern
* Erstellen von digitalen Zwillingen
* Erstellen von Beziehungen
* Abfragen von digitalen Zwillingen

Es ist auch ein Abschnitt vorhanden, der den vollständigen Code am Ende des Tutorials zeigt. Sie können diesen als Referenz zur Überprüfung Ihres Programms verwenden.

Öffnen Sie zunächst die Datei *Program.cs* in einem beliebigen Code-Editor. Es wird eine Minimalcodevorlage angezeigt, die in etwa so aussieht:

```csharp
using System;

namespace DigitalTwinsCodeTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

Fügen Sie zunächst oberhalb des Codes einige `using`-Zeilen ein, um erforderliche Abhängigkeiten hineinzuziehen.

```csharp
using Azure.DigitalTwins.Core;
using Azure.Identity;
```

Anschließend fügen Sie Code in diese Datei ein, um etwas Funktionalität hinzuzufügen. 

### <a name="authenticate-against-the-service"></a>Authentifizierung beim Dienst

Als Erstes muss sich Ihre App beim Azure Digital Twins-Dienst authentifizieren. Anschließend können Sie eine Dienstclientklasse für den Zugriff auf die SDK-Funktionen erstellen.

Für die Authentifizierung benötigen Sie die folgenden Informationen:
* Die *Verzeichnis-ID (Mandanten-ID)* für Ihr Abonnement
* Die *Anwendungs-ID (Client-ID)* , die beim Einrichten der Azure Digital Twins-Instanz erstellt wurde
* Den *Hostnamen* Ihrer Azure Digital Twins-Instanz

>[!TIP]
> Wenn Sie die *Verzeichnis-ID (Mandanten-ID)* nicht kennen, können Sie sie über diesen Befehl in [Azure Cloud Shell](https://shell.azure.com) abrufen:
> 
> ```azurecli-interactive
> az account show --query tenantId
> ```

Fügen Sie in *Program.cs* den folgenden Code unterhalb der Ausgabezeile „Hello, World!“ in der `Main`-Methode ein. Legen Sie den Wert von `adtInstanceUrl` auf den *hostName*-Wert Ihrer Azure Digital Twins-Instanz, `clientId` auf Ihre *Anwendungs-ID* und `tenantId` auf Ihre *Verzeichnis-ID* fest.

```csharp
string clientId = "<your-application-ID>";
string tenantId = "<your-directory-ID>";
string adtInstanceUrl = "https://<your-Azure-Digital-Twins-instance-hostName>";
var credentials = new InteractiveBrowserCredential(tenantId, clientId);
DigitalTwinsClient client = new DigitalTwinsClient(new Uri(adtInstanceUrl), credentials);
Console.WriteLine($"Service client created – ready to go");
```

Speichern Sie die Datei . 

Beachten Sie, dass in diesem Beispiel interaktive Browseranmeldeinformationen verwendet werden:
```csharp
var credentials = new InteractiveBrowserCredential(tenantId, clientId);
```

Diese Art von Anmeldeinformationen führen dazu, dass ein Browserfenster geöffnet wird, in dem Sie zur Eingabe Ihrer Azure-Anmeldeinformationen aufgefordert werden. 

>[!NOTE]
> Informationen zu weiteren Arten von Anmeldeinformationen finden Sie in der Dokumentation [Microsoft Identity Plattform: Authentifizierungsbibliotheken](../active-directory/develop/reference-v2-libraries.md).

Führen Sie in Ihrem Befehlsfenster den Code mit diesem Befehl aus: 

```cmd/sh
dotnet run
```

Auf diese Weise werden die Abhängigkeiten bei der ersten Ausführung wiederhergestellt, und anschließend wird das Programm ausgeführt. 
* Falls keine Fehler auftreten, gibt das Programm die folgende Meldung aus: *Service client created - ready to go*.
* Weil in diesem Projekt noch keine Fehlerbehandlung stattfindet, löst der Code bei Problemen eine Ausnahme aus.

### <a name="upload-a-model"></a>Hochladen eines Modells

Azure Digital Twins umfasst kein intrinsisches Domänenvokabular. Die Elementtypen in Ihrer Umgebung, die Sie in Azure Digital Twins darstellen können, werden von Ihnen mithilfe von **Modellen** definiert. [Modelle](concepts-models.md) ähneln Klassen in objektorientierten Programmiersprachen. Sie stellen benutzerdefinierte Vorlagen für [digitale Zwillinge](concepts-twins-graph.md) bereit, die später eingesetzt und instanziiert werden. Sie werden in einer JSON-ähnlichen Sprache namens **Digital Twins Definition Language (DTDL)** geschrieben.

Beim Erstellen einer Azure Digital Twins-Lösung wird im ersten Schritt mindestens ein Modell in einer DTDL-Datei definiert.

Erstellen Sie in dem Verzeichnis, in dem Sie Ihr Projekt erstellt haben, eine neue *JSON*-Datei mit dem Namen *SampleModel.json*. Fügen Sie den folgenden Dateitext ein: 

```json
{
  "@id": "dtmi:com:contoso:SampleModel;1",
  "@type": "Interface",
  "displayName": "SampleModel",
  "contents": [
    {
      "@type": "Relationship",
      "name": "contains"
    },
    {
      "@type": "Property",
      "name": "data",
      "schema": "string"
    }
  ],
  "@context": "dtmi:dtdl:context;2"
}
```

> [!TIP]
> Wenn Sie für dieses Tutorial Visual Studio verwenden, können Sie die neu erstellte JSON-Datei auswählen und im Eigenschaften-Inspektor die Eigenschaft *In Ausgabeverzeichnis kopieren* auf *Kopieren, falls aktueller* oder *Immer kopieren* festlegen. So kann Visual Studio die JSON-Datei mit dem Standardpfad finden, wenn Sie das Programm im weiteren Verlauf des Tutorials mit **F5** ausführen.

> [!TIP] 
> Es gibt ein sprachunabhängiges [DTDL-Überprüfungsbeispiel](https://docs.microsoft.com/samples/azure-samples/dtdl-validator/dtdl-validator), mit dem Sie Modelldokumente überprüfen können, um sicherzustellen, dass die DTDL gültig ist. Es basiert auf der DTDL-Parserbibliothek. Weitere Informationen dazu finden Sie unter [ *Clientseitige DTDL-Parserbibliothek*](how-to-parse-models.md).

Als Nächstes fügen Sie *Program.cs* weiteren Code hinzu, um das soeben erstellte Modell in Ihre Azure Digital Twins-Instanz hochzuladen.

Im ersten Schritt fügen Sie am Dateianfang die folgenden `using`-Anweisungen hinzu:

```csharp
using System.Threading.Tasks;
using System.IO;
using System.Collections.Generic;
using Azure;
```

Als Nächstes bereiten Sie die Verwendung der asynchronen Methoden im Dienst-SDK für C# vor, indem Sie die `Main`-Methodensignatur so ändern, dass eine asynchrone Ausführung zulässig ist. 

```csharp
static async Task Main(string[] args)
```

> [!NOTE]
> Die Verwendung von `async` ist nicht unbedingt erforderlich, weil das SDK auch synchrone Versionen aller Aufrufe bereitstellt. In diesem Tutorial wird die Verwendung von `async` geübt.

Als Nächstes folgt ein Codeabschnitt, der mit dem Azure Digital Twins-Dienst interagiert. Dieser Code lädt die erstellte DTDL-Datei von Ihrem Datenträger in Ihre Azure Digital Twins-Dienstinstanz hoch. 

Fügen Sie den folgenden Code unterhalb des Autorisierungscodes ein, den Sie zuvor erstellt haben.

```csharp
Console.WriteLine();
Console.WriteLine($"Upload a model");
var typeList = new List<string>();
string dtdl = File.ReadAllText("SampleModel.json");
typeList.Add(dtdl);
// Upload the model to the service
await client.CreateModelsAsync(typeList);
```

Führen Sie in Ihrem Befehlsfenster das Programm mit diesem Befehl aus: 

```cmd/sh
dotnet run
```
„Modell hochladen“ wird in der Ausgabe gedruckt, aber es gibt noch keine Ausgabe, mit der angegeben wird, ob Modelle erfolgreich hochgeladen wurden.

Um eine Meldung auszugeben, ob Modelle tatsächlich erfolgreich hochgeladen wurden, fügen Sie nach dem vorherigen Abschnitt den folgenden Code hinzu:

```csharp
// Read a list of models back from the service
AsyncPageable<ModelData> modelDataList = client.GetModelsAsync();
await foreach (ModelData md in modelDataList)
{
    Console.WriteLine($"Type name: {md.DisplayName}: {md.Id}");
}
```

Bedenken Sie vor Ausführung des Programms zum Testen dieses neuen Codes, dass Sie Ihr Modell bei der letzten Programmausführung bereits hochgeladen haben. Azure Digital Twins lässt nicht zu, dass Sie dasselbe Modell zweimal hochladen. Rechnen Sie deshalb damit, dass beim erneuten Ausführen des Programms eine Ausnahme angezeigt wird.

Führen Sie jetzt in Ihrem Befehlsfenster das Programm mit diesem Befehl erneut aus:

```cmd/sh
dotnet run
```

Das Programm sollte eine Ausnahme ausgeben. Wenn Sie versuchen, ein Modell hochzuladen, das bereits hochgeladen wurde, gibt der Dienst über die REST-API einen Fehler vom Typ „Ungültige Anforderung“ aus. Als Ergebnis löst das Azure Digital Twins-Client SDK für jeden Rückgabecode des Diensts, der nicht „Erfolgreich“ lautet, eine Ausnahme aus. 

Im nächsten Abschnitt wenden wir uns Ausnahmen wie diesen zu, und es wird erläutert, wie Sie sie in Ihrem Code behandeln.

### <a name="catch-errors"></a>Abfangen von Fehlern

Um zu verhindern, dass das Programm abstürzt, können Sie Ausnahmecode um den Code zum Hochladen eines Modells einfügen. Umschließen Sie den vorhandenen Clientaufruf `client.CreateModelsAsync` wie folgt mit einem try/catch-Handler:

```csharp
try {
    await client.CreateModelsAsync(typeList);
} catch (RequestFailedException rex) {
    Console.WriteLine($"Load model: {rex.Status}:{rex.Message}");
}
```

Wenn Sie das Programm jetzt mit `dotnet run` in Ihrem Befehlsfenster ausführen, wird ein Fehlercode zurückgegeben. Die Ausgabe sieht in etwa wie folgt aus:

```cmd/sh
Hello World!
Service client created - ready to go

Upload a model
Load model: 409:Service request failed.
Status: 409 (Conflict)

Content:
{"error":{"code":"DocumentAlreadyExists","message":"A document with same identifier already exists.","details":[]}}

Headers:
api-supported-versions: REDACTED
Date: Tue, 05 May 2020 01:57:51 GMT
Content-Length: 115
Content-Type: application/json; charset=utf-8

Type name: : dtmi:com:contoso:SampleModel;1
```

Von diesem Punkt an werden in diesem Tutorial alle Aufrufe von Dienstmethoden in try/catch-Handler eingeschlossen.

### <a name="create-digital-twins"></a>Erstellen digitaler Zwillinge

Nun, da Sie ein Modell in Azure Digital Twins hochgeladen haben, können Sie diese Modelldefinition zum Erstellen **digitaler Zwillinge** verwenden. [Digitale Zwillinge](concepts-twins-graph.md) sind Instanzen eines Modells und repräsentieren die Entitäten in Ihrer Geschäftsumgebung – beispielsweise Sensoren in einer Farm, Räume in einem Gebäude oder die Beleuchtung in einem Fahrzeug. Im vorliegenden Abschnitt werden basierend auf dem zuvor hochgeladenen Modell einige digitale Zwillinge erstellt.

Fügen Sie oben eine neue `using`-Anweisung hinzu, da Sie das integrierte .NET-JSON-Serialisierungsmodul in `System.Text.Json` benötigen:

```csharp
using System.Text.Json;
using Azure.DigitalTwins.Core.Serialization;
```

Fügen Sie anschließend am Ende der `Main`-Methode den folgenden Code hinzu, um basierend auf diesem Modell drei digitale Zwillinge zu erstellen und zu initialisieren.

```csharp
// Initialize twin data
BasicDigitalTwin twinData = new BasicDigitalTwin();
twinData.Metadata.ModelId = "dtmi:com:contoso:SampleModel;1";
twinData.CustomProperties.Add("data", $"Hello World!");

string prefix="sampleTwin-";
for(int i=0; i<3; i++) {
    try {
        twinData.Id = $"{prefix}{i}";
        await client.CreateDigitalTwinAsync($"{prefix}{i}", JsonSerializer.Serialize(twinData));
        Console.WriteLine($"Created twin: {prefix}{i}");
    } catch(RequestFailedException rex) {
        Console.WriteLine($"Create twin error: {rex.Status}:{rex.Message}");  
    }
}
```

Führen Sie in Ihrem Befehlsfenster das Programm mit `dotnet run` aus. Wiederholen Sie anschließend diesen Vorgang, um das Programm erneut auszuführen. 

Beachten Sie, dass beim zweiten Erstellen der digitalen Zwillinge kein Fehler ausgegeben wird, obwohl die Zwillinge bereits nach der ersten Ausführung vorhanden sind. Im Gegensatz zur Modellerstellung erfolgt die Erstellung der Zwillinge auf REST-Ebene über einen *PUT*-Aufruf mit *upsert*-Semantik. Wenn also ein Zwilling bereits vorhanden ist, wird bei einem erneuten Erstellungsversuch der vorhandene Zwilling einfach ersetzt. Kein Fehler erforderlich.

### <a name="create-relationships"></a>Erstellen von Beziehungen

Im nächsten Schritt können Sie **Beziehungen** zwischen den erstellten Zwillingen erstellen, um sie in einem **Zwillingsgraphen** zu verbinden. [Zwillingsgraphen](concepts-twins-graph.md) werden verwendet, um Ihre gesamte Umgebung darzustellen.

Um Beziehungen erstellen zu können, fügen Sie eine `using`-Anweisung für den Beziehungsbasistyp im SDK hinzu. Wenn bereits eine hinzugefügt ist, überspringen Sie diesen Schritt.
```csharp
using Azure.DigitalTwins.Core.Serialization;
```

Als Nächstes fügen Sie eine neue statische Methode zur `Program`-Klasse hinzu, unterhalb der `Main`-Methode:
```csharp
public async static Task CreateRelationship(DigitalTwinsClient client, string srcId, string targetId)
{
    var relationship = new BasicRelationship
    {
        TargetId = targetId,
        Name = "contains"
    };

    try
    {
        string relId = $"{srcId}-contains->{targetId}";
        await client.CreateRelationshipAsync(srcId, relId, JsonSerializer.Serialize(relationship));
        Console.WriteLine("Created relationship successfully");
    }
    catch (RequestFailedException rex) {
        Console.WriteLine($"Create relationship error: {rex.Status}:{rex.Message}");
    }
}
```

Dann fügen Sie den folgenden Code am Ende der `Main`-Methode zum Aufrufen des `CreateRelationship`-Codes hinzu:
```csharp
// Connect the twins with relationships
await CreateRelationship(client, "sampleTwin-0", "sampleTwin-1");
await CreateRelationship(client, "sampleTwin-0", "sampleTwin-2");
```

Führen Sie in Ihrem Befehlsfenster das Programm mit `dotnet run` aus.

Beachten Sie, dass Azure Digital Twins das Erstellen einer Beziehung nicht zulässt, wenn bereits eine Beziehung mit derselben ID vorhanden ist. Wenn Sie das Programm also mehrfach ausführen, werden beim Erstellen von Beziehungen Ausnahmen angezeigt. Mit diesem Code werden die Ausnahmen abgefangen und ignoriert. 

### <a name="list-relationships"></a>Auflisten von Beziehungen

Der nächste Codeabschnitt, den Sie hinzufügen, ermöglicht die Anzeige einer Liste der Beziehungen, die Sie erstellt haben.

Fügen Sie der `Program`-Klasse die folgende neue Methode hinzu:

```csharp
public async static Task ListRelationships(DigitalTwinsClient client, string srcId)
{
    try {
        AsyncPageable<string> results = client.GetRelationshipsAsync(srcId);
        Console.WriteLine($"Twin {srcId} is connected to:");
        await foreach (string rel in results)
        {
            var brel = JsonSerializer.Deserialize<BasicRelationship>(rel);
            Console.WriteLine($" -{brel.Name}->{brel.TargetId}");
        }
    } catch (RequestFailedException rex) {
        Console.WriteLine($"Relationship retrieval error: {rex.Status}:{rex.Message}");   
    }
}
```

Anschließend fügen Sie den folgenden Code am Ende der `Main`-Methode zum Aufrufen des `ListRelationships`-Codes hinzu:

```csharp
//List the relationships
await ListRelationships(client, "sampleTwin-0");
```

Führen Sie in Ihrem Befehlsfenster das Programm mit `dotnet run` aus. Es sollte eine Liste aller Beziehungen angezeigt werden, die Sie erstellt haben.

### <a name="query-digital-twins"></a>Abfragen von digitalen Zwillingen

Eine Hauptfunktion von Azure Digital Twins ist das einfache [Abfragen](concepts-query-language.md) des Zwillingsgraphen und das effiziente Beantworten von Fragen zur Umgebung.

Mit dem letzten Codeabschnitt, den wir im Rahmen dieses Tutorials hinzufügen, wird eine Abfrage der Azure Digital Twins-Instanz ausgeführt. Die in diesem Beispiel verwendete Abfrage gibt alle digitalen Zwillinge in der Instanz zurück.

Fügen Sie am Ende der `Main`-Methode den folgenden Code hinzu:

```csharp
// Run a query    
AsyncPageable<string> result = client.QueryAsync("Select * From DigitalTwins");
await foreach (string twin in result)
{
    object jsonObj = JsonSerializer.Deserialize<object>(twin);
    string prettyTwin = JsonSerializer.Serialize(jsonObj, new JsonSerializerOptions { WriteIndented = true });
    Console.WriteLine(prettyTwin);
    Console.WriteLine("---------------");
}
```

Führen Sie in Ihrem Befehlsfenster das Programm mit `dotnet run` aus. In der Ausgabe sollten alle digitalen Zwillinge in dieser Instanz angezeigt werden.

## <a name="complete-code-example"></a>Vollständiges Codebeispiel

An dieser Stelle des Tutorials verfügen Sie über eine vollständige Client-App, die in der Lage ist, grundlegende Aktionen in Azure Digital Twins auszuführen. Zu Ihrer Referenz wird nachfolgend der vollständige Code des Programms in *Program.cs* aufgeführt:

```csharp
using System;
using Azure.DigitalTwins.Core;
using Azure.Identity;
using System.Threading.Tasks;
using System.IO;
using System.Collections.Generic;
using Azure;
using Azure.DigitalTwins.Core.Models;
using Azure.DigitalTwins.Core.Serialization;
using System.Text.Json;

namespace minimal
{
    class Program
    {
        static async Task Main(string[] args)
        {
            Console.WriteLine("Hello World!");
            
            string clientId = "<your-application-ID>";
            string tenantId = "<your-directory-ID>";
            string adtInstanceUrl = "https://<your-Azure-Digital-Twins-instance-hostName>";
            var credentials = new InteractiveBrowserCredential(tenantId, clientId);
            DigitalTwinsClient client = new DigitalTwinsClient(new Uri(adtInstanceUrl), credentials);
            Console.WriteLine($"Service client created – ready to go");

            Console.WriteLine();
            Console.WriteLine($"Upload a model");
            var typeList = new List<string>();
            string dtdl = File.ReadAllText("SampleModel.json");
            typeList.Add(dtdl);

            // Upload the model to the service
            try {
                await client.CreateModelsAsync(typeList);
            } catch (RequestFailedException rex) {
                Console.WriteLine($"Load model: {rex.Status}:{rex.Message}");
            }
            // Read a list of models back from the service
            AsyncPageable<ModelData> modelDataList = client.GetModelsAsync();
            await foreach (ModelData md in modelDataList)
            {
                Console.WriteLine($"Type name: {md.DisplayName}: {md.Id}");
            }

            // Initialize twin data
            BasicDigitalTwin twinData = new BasicDigitalTwin();
            twinData.Metadata.ModelId = "dtmi:com:contoso:SampleModel;1";
            twinData.CustomProperties.Add("data", $"Hello World!");
    
            string prefix="sampleTwin-";
            for(int i=0; i<3; i++) {
                try {
                    twinData.Id = $"{prefix}{i}";
                    await client.CreateDigitalTwinAsync($"{prefix}{i}", JsonSerializer.Serialize(twinData));
                    Console.WriteLine($"Created twin: {prefix}{i}");
                } catch(RequestFailedException rex) {
                    Console.WriteLine($"Create twin error: {rex.Status}:{rex.Message}");  
                }
            }

            // Connect the twins with relationships
            await CreateRelationship(client, "sampleTwin-0", "sampleTwin-1");
            await CreateRelationship(client, "sampleTwin-0", "sampleTwin-2");

            //List the relationships
            await ListRelationships(client, "sampleTwin-0");

            // Run a query    
            AsyncPageable<string> result = client.QueryAsync("Select * From DigitalTwins");
            await foreach (string twin in result)
            {
                object jsonObj = JsonSerializer.Deserialize<object>(twin);
                string prettyTwin = JsonSerializer.Serialize(jsonObj, new JsonSerializerOptions { WriteIndented = true });
                Console.WriteLine(prettyTwin);
                Console.WriteLine("---------------");
            }
        }

        public async static Task CreateRelationship(DigitalTwinsClient client, string srcId, string targetId)
        {
            var relationship = new BasicRelationship
            {
                TargetId = targetId,
                Name = "contains"
            };
        
            try
            {
                string relId = $"{srcId}-contains->{targetId}";
                await client.CreateRelationshipAsync(srcId, relId, JsonSerializer.Serialize(relationship));
                Console.WriteLine("Created relationship successfully");
            }
            catch (RequestFailedException rex) {
                Console.WriteLine($"Create relationship error: {rex.Status}:{rex.Message}");
            }
        }
        
        public async static Task ListRelationships(DigitalTwinsClient client, string srcId)
        {
            try {
                AsyncPageable<string> results = client.GetRelationshipsAsync(srcId);
                Console.WriteLine($"Twin {srcId} is connected to:");
                await foreach (string rel in results)
                {
                    var brel = JsonSerializer.Deserialize<BasicRelationship>(rel);
                    Console.WriteLine($" -{brel.Name}->{brel.TargetId}");
                }
            } catch (RequestFailedException rex) {
                Console.WriteLine($"Relationship retrieval error: {rex.Status}:{rex.Message}");   
            }
        }

    }
}
```
## <a name="clean-up-resources"></a>Bereinigen von Ressourcen
 
Die in diesem Tutorial verwendete Instanz kann im nächsten Tutorial wiederverwendet werden: [ *Erkunden von Azure Digital Twins mit einer Beispielclient-App*](tutorial-command-line-app.md). Wenn Sie auch das nächste Tutorial bearbeiten möchten, können Sie die hier eingerichtete Azure Digital Twins-Instanz beibehalten.
 
Wenn Sie die in diesem Tutorial erstellten Ressourcen nicht mehr benötigen, folgen Sie den Schritten unten, um sie zu löschen.

Bei Verwendung von [Azure Cloud Shell](https://shell.azure.com) können Sie alle Azure-Ressourcen in einer Ressourcengruppe mit dem Befehl [az group delete](https://docs.microsoft.com/cli/azure/group?view=azure-cli-latest#az-group-delete) löschen. Dadurch werden die Ressourcengruppe und die Azure Digital Twins-Instanz entfernt.

> [!IMPORTANT]
> Das Löschen einer Ressourcengruppe kann nicht rückgängig gemacht werden. Die Ressourcengruppe und alle darin enthaltenen Ressourcen werden unwiderruflich gelöscht. Achten Sie daher darauf, dass Sie nicht versehentlich die falsche Ressourcengruppe oder die falschen Ressourcen löschen. 

Öffnen Sie eine Azure Cloud Shell-Instanz, und führen Sie den folgenden Befehl aus, um die Ressourcengruppe und alle darin enthaltenen Elemente zu löschen.

```azurecli-interactive
az group delete --name <your-resource-group>
```

Löschen Sie als Nächstes mit dem folgenden Befehl die Azure Active Directory-App-Registrierung, die Sie für Ihre Client-App erstellt haben:

```azurecli
az ad app delete --id <your-application-ID>
```

Löschen Sie abschließend den Projektordner, den Sie auf Ihrem lokalen Computer erstellt haben.

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie eine Clientanwendung für die .NET-Konsole von Grund auf neu erstellt. Sie haben Code für die Client-App erstellt, um grundlegende Aufgaben für eine Azure Digital Twins-Instanz auszuführen.

Fahren Sie mit dem nächsten Tutorial fort, um zu untersuchen, welche Möglichkeiten eine solche Beispiel-Client-App bietet: 

> [!div class="nextstepaction"]
> [*Tutorial: Erkunden von Azure Digital Twins mit einer Beispielclient-App*](tutorial-command-line-app.md)

Sie können den Code aus diesem Tutorial auch ergänzen, indem Sie mithilfe der Gewusst-wie-Artikel weitere Verwaltungsvorgänge kennenlernen oder anhand der Konzeptdokumentation mehr über die Elemente erfahren, mit denen Sie im Tutorial gearbeitet haben.
* [ *Verwalten von Azure Digital Twins-Modellen*](how-to-manage-model.md)
* [ *Grundlegendes zu Zwillingsmodellen in Azure Digital Twins*](concepts-models.md)
