---
title: Berechtigungen in Azure Sentinel | Microsoft-Dokumentation
description: In diesem Artikel wird beschrieben, wie Azure Sentinel rollenbasierte Zugriffssteuerung zum Zuweisen von Berechtigungen für Benutzer verwendet und die zulässigen Aktionen für jede Rolle identifiziert.
services: sentinel
cloud: na
documentationcenter: na
author: yelevin
manager: rkarlin
ms.assetid: ''
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/28/2020
ms.author: yelevin
ms.openlocfilehash: 7dded3b938444198e72d6eb87476f571dd3f4d78
ms.sourcegitcommit: 2ff0d073607bc746ffc638a84bb026d1705e543e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87836767"
---
# <a name="permissions-in-azure-sentinel"></a>Berechtigungen in Azure Sentinel

Azure Sentinel verwendet die  [rollenbasierte Zugriffssteuerung in Azure](../role-based-access-control/role-assignments-portal.md) (Azure Role-Based Access Control, Azure RBAC). Dabei werden [integrierte Rollen](../role-based-access-control/built-in-roles.md) bereitgestellt, die Benutzern, Gruppen und Diensten in Azure zugewiesen werden können.

Verwenden Sie RBAC, um Rollen innerhalb Ihres Security Operations-Teams zu erstellen und zuzuweisen, um angemessenen Zugriff auf Azure Sentinel zu ermöglichen. Mithilfe der verschiedenen Rollen können Sie präzise steuern, was Benutzer von Azure Sentinel anzeigen und welche Aktionen sie ausführen können. Azure-Rollen können direkt im Azure Sentinel-Arbeitsbereich zugewiesen werden (siehe Hinweis unten) oder in einem Abonnement oder einer Ressourcengruppe, zu dem bzw. der der Arbeitsbereich gehört, der von Azure Sentinel geerbt wird.

## <a name="roles-for-working-in-azure-sentinel"></a>Rollen für das Arbeiten in Azure Sentinel

### <a name="azure-sentinel-specific-roles"></a>Azure Sentinel-spezifische Rollen

Es gibt drei dedizierte integrierte Azure Sentinel-Rollen.

**Alle in Azure Sentinel integrierten Rollen gewähren Lesezugriff auf die Daten in Ihrem Azure Sentinel-Arbeitsbereich.**

- [Azure Sentinel-Leser](../role-based-access-control/built-in-roles.md#azure-sentinel-reader) können Daten, Incidents, Arbeitsmappen und andere Azure Sentinel-Ressourcen anzeigen.

- [Azure Sentinel-Antwortberechtigte](../role-based-access-control/built-in-roles.md#azure-sentinel-responder) können zusätzlich zu den oben genannten Aktionen auch Incidents verwalten (zuweisen, verwerfen usw.).

- [Azure Sentinel-Mitwirkende](../role-based-access-control/built-in-roles.md#azure-sentinel-contributor) können zusätzlich zu den oben aufgeführten Aktionen Arbeitsmappen, Analyseregeln und andere Azure Sentinel-Ressourcen erstellen und bearbeiten.

> [!NOTE]
>
> - Um optimale Ergebnisse zu erzielen, sollten diese Rollen für die **Ressourcengruppe** zugewiesen werden, die den Azure Sentinel-Arbeitsbereich enthält. Auf diese Weise gelten die Rollen für alle Ressourcen, die zur Unterstützung von Azure Sentinel bereitgestellt werden, da diese Ressourcen auch in derselben Ressourcengruppe platziert werden sollten.
>
> - Eine andere Möglichkeit besteht darin, die Rollen direkt für den Azure Sentinel-**Arbeitsbereich** selbst zuzuweisen. Wenn Sie so vorgehen, müssen Sie die gleichen Rollen auch für die SecurityInsights-**Lösungsressource** in diesem Arbeitsbereich zuweisen. Sie müssen sie möglicherweise auch anderen Ressourcen zuweisen, und Sie müssen die Rollenzuweisungen für Ressourcen kontinuierlich verwalten.

### <a name="additional-roles-and-permissions"></a>Weitere Rollen und Berechtigungen

Benutzern mit besonderen Arbeitsanforderungen müssen möglicherweise zusätzliche Rollen oder spezifische Berechtigungen zugewiesen werden, um ihre Aufgaben erfüllen zu können.

- Arbeiten mit Playbooks zur Automatisierung von Reaktionen auf Bedrohungen

    Azure Sentinel verwendet **Playbooks** für automatische Reaktionen auf Bedrohungen. Playbooks nutzen **Azure Logic Apps** und sind eine separate Azure-Ressource. Sie können bestimmten Mitgliedern Ihres Security Operations-Teams die Option zuweisen, Logic Apps für SOAR-Vorgänge (Sicherheitsorchestrierung, Automatisierung und Reaktion) zu verwenden. Sie können die Rolle [Logik-App-Mitwirkender](../role-based-access-control/built-in-roles.md#logic-app-contributor) oder die Rolle [Logik-App-Operator](../role-based-access-control/built-in-roles.md#logic-app-operator) verwenden, um eine explizite Berechtigung für die Verwendung von Playbooks zu erteilen.

- Verbinden von Datenquellen mit Azure Sentinel

    Damit ein Benutzer **Data Connectors**hinzufügen kann, müssen Sie dem Benutzer Schreibberechtigungen im Azure Sentinel-Arbeitsbereich zuweisen. Beachten Sie außerdem die erforderlichen zusätzlichen Berechtigungen für jeden Connector, die auf der Seite zum jeweiligen Connector aufgeführt werden.

Eine Gegenüberstellung finden Sie in der [Tabelle unten](#roles-and-allowed-actions).

### <a name="other-roles-you-might-see-assigned"></a>Weitere Rollen, die möglicherweise zugewiesen sind

Bei der Zuweisung von Azure Sentinel-spezifischen Azure-Rollen können Sie auf andere Azure- und Log Analytics-Rollen stoßen, die Benutzern für andere Zwecke zugewiesen worden sein können. Sie sollten sich bewusst sein, dass diese Rollen eine breitere Palette von Berechtigungen festlegen, die auch den Zugriff auf Ihren Azure Sentinel-Arbeitsbereich und andere Ressourcen umfasst:

- **Azure-Rollen:** [Besitzer](../role-based-access-control/built-in-roles.md#owner), [Mitwirkender](../role-based-access-control/built-in-roles.md#contributor) und [Leser](../role-based-access-control/built-in-roles.md#reader). Azure-Rollen gewähren Zugriff auf alle Ihre Azure-Ressourcen, einschließlich Log Analytics-Arbeitsbereiche und Azure Sentinel-Ressourcen.

- **Log Analytics-Rollen:** [Log Analytics-Mitwirkender](../role-based-access-control/built-in-roles.md#log-analytics-contributor) und [Log Analytics-Leser](../role-based-access-control/built-in-roles.md#log-analytics-reader). Log Analytics-Rollen gewähren Zugriff auf Ihre Log Analytics-Arbeitsbereiche. 

Beispielsweise kann ein Benutzer, dem die Rolle **Azure Sentinel-Leser**, aber nicht die Rolle **Azure Sentinel-Mitwirkender** zugewiesen wurde, immer noch Ressourcen in Azure Sentinel bearbeiten, wenn ihm die Rolle **Mitwirkender** auf Azure-Ebene zugewiesen wurde. Wenn Sie daher einem Benutzer Berechtigungen nur in Azure Sentinel gewähren möchten, sollten Sie die vorherigen Berechtigungen dieses Benutzers sorgfältig entfernen und sicherstellen, dass Sie keinen erforderlichen Zugriff auf eine andere Ressource aufheben.

## <a name="roles-and-allowed-actions"></a>Rollen und zulässige Aktionen

In der folgenden Tabelle sind die Rollen und zulässigen Aktionen in Azure Sentinel zusammengefasst. 

| Role | Playbooks erstellen und ausführen| Erstellen und Bearbeiten von Arbeitsmappen, Analyseregeln und anderen Azure Sentinel-Ressourcen | Incidents verwalten (verwerfen, zuweisen usw.) | Anzeigen von Daten, Incidents, Arbeitsmappen und anderen Azure Sentinel-Ressourcen |
|---|---|---|---|---|
| Azure Sentinel-Leser | -- | -- | -- | &#10003; |
| Azure Sentinel-Antwortender | -- | -- | &#10003; | &#10003; |
| Azure Sentinel-Mitwirkender | -- | &#10003; | &#10003; | &#10003; |
| Azure Sentinel-Mitwirkender und Mitwirkender für Logik-Apps | &#10003; | &#10003; | &#10003; | &#10003; |

## <a name="custom-roles-and-advanced-rbac"></a>Benutzerdefinierte Rollen und erweitertes RBAC

- Zusätzlich zu integrierten Azure-Rollen oder anstelle von diesen können Sie benutzerdefinierte Azure-Rollen für Azure Sentinel erstellen. Benutzerdefinierte Azure-Rollen für Azure Sentinel werden genauso erstellt, wie Sie andere [benutzerdefinierte Azure-RBAC](../role-based-access-control/custom-roles-rest.md#create-a-custom-role)-Rollen basierend auf [bestimmten Berechtigungen für Azure Sentinel](../role-based-access-control/resource-provider-operations.md#microsoftsecurityinsights) und für [Azure Log Analytics-Ressourcen](../role-based-access-control/resource-provider-operations.md#microsoftoperationalinsights) erstellen.

- Sie können die erweiterte rollenbasierte Zugriffssteuerung von Log Analytics für die Daten in Ihrem Azure Sentinel-Arbeitsbereich verwenden. Dies umfasst sowohl auf dem Datentyp basierendes RBAC als auch die ressourcenzentriertes RBAC. Weitere Informationen zu den Log Analytics-Rollen finden Sie unter  [Verwalten von Protokolldaten und Arbeitsbereichen in Azure Monitor](../azure-monitor/platform/manage-access.md#manage-access-using-workspace-permissions).

## <a name="next-steps"></a>Nächste Schritte

In diesem Dokument haben Sie erfahren, wie Sie mit Rollen für Azure Sentinel-Benutzer arbeiten und was die einzelnen Rollen den Benutzern ermöglichen.

* [Azure Sentinel-Blog](https://aka.ms/azuresentinelblog). Hier finden Sie Blogbeiträge zur Sicherheit und Compliance von Azure.
