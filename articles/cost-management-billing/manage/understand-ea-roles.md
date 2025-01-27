---
title: Informationen zu den Administratorrollen für Enterprise in Azure
description: Erfahren Sie etwas über Enterprise-Administratorrollen in Azure. Sie können fünf verschiedene administrative Rollen zuweisen.
author: bandersmsft
ms.reviewer: adwise
ms.service: cost-management-billing
ms.topic: conceptual
ms.date: 08/14/2020
ms.author: banders
ms.openlocfilehash: b712a212a12cadb10473b9e4751239a48bf5cdc7
ms.sourcegitcommit: c293217e2d829b752771dab52b96529a5442a190
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88245977"
---
# <a name="managing-azure-enterprise-roles"></a>Verwalten von Azure Enterprise-Rollen

Azure-Kunden mit einem Enterprise Agreement (EA) können zur Verwaltung ihrer Organisation und ihrer Ausgaben fünf verschiedene Administratorrollen zuweisen:

- Unternehmensadministrator
- Unternehmensadministrator (nur Leseberechtigung)<sup>1</sup>
- Abteilungsadministrator
- Abteilungsadministrator (nur Leseberechtigung)
- Kontobesitzer<sup>2</sup>

<sup>1</sup> Der Rechnungsempfänger des Konzernvertrags hat diese Rolle.

<sup>2</sup> Der Rechnungsempfänger kann nicht im Azure EA-Portal hinzugefügt oder geändert werden. Er wird der EA-Registrierung basierend auf dem Benutzer hinzugefügt, der auf der Vereinbarungsebene als Rechnungsempfänger eingerichtet ist. Zum Ändern des Rechnungsempfängers muss über einen Partner/Software Advisor eine Anfrage an das regionale Betriebszentrum (Regional Operations Center, ROC) gerichtet werden.

Der erste Registrierungsadministrator, der während der Registrierungsbereitstellung eingerichtet wird, bestimmt den Authentifizierungstyp des Rechnungsempfängerkontos. Wenn der Rechnungsempfänger dem EA Portal als Administrator mit Leseberechtigung hinzugefügt wird, wird für ihn die Microsoft-Kontoauthentifizierung festgelegt. 

Wenn der ursprüngliche Authentifizierungstyp auf „Gemischt“ festgelegt wird, wird das EA als Microsoft-Konto hinzugefügt, und der Rechnungsempfänger besitzt EA-Administratorberechtigungen vom Typ „Schreibgeschützt“. Wenn der EA-Administrator die Microsoft-Kontoautorisierung für einen vorhandenen Rechnungsempfänger nicht genehmigt, kann der EA-Administrator den betreffenden Benutzer löschen und den Kunden bitten, den Benutzer als Administrator mit Leseberechtigung für ein Geschäfts-, Schul-oder Unikonto hinzuzufügen, das nur auf Registrierungsebene im EA Portal festgelegt ist.

Diese Rollen sind spezifisch für die Verwaltung von Azure Enterprise Agreements und ergänzend zu den integrierten Rollen in Azure zum Steuern des Zugriffs auf Ressourcen. Weitere Informationen finden Sie unter [Integrierte Azure-Rollen](../../role-based-access-control/built-in-roles.md).

Die folgenden Abschnitte beschreiben die Einschränkungen und Funktionen der einzelnen Rollen.

## <a name="user-limit-for-admin-roles"></a>Benutzerlimit für Administratorrollen

|Role| Benutzerlimit|
|---|---|
|Unternehmensadministrator|Unbegrenzt|
|Unternehmensadministrator (nur Leseberechtigung)|Unbegrenzt|
|Abteilungsadministrator|Unbegrenzt|
|Abteilungsadministrator (nur Leseberechtigung)|Unbegrenzt|
|Kontobesitzer|Einer pro Konto<sup>3</sup>|

<sup>3</sup> Für jedes Konto ist ein individuelles Microsoft-Konto oder Geschäfts-, Schul- oder Unikonto erforderlich.

## <a name="organization-structure-and-permissions-by-role"></a>Organisationsstruktur und Berechtigungen nach Rolle

|Aufgaben| Unternehmensadministrator|Unternehmensadministrator (nur Leseberechtigung)|Abteilungsadministrator|Abteilungsadministrator (nur Leseberechtigung)|Kontobesitzer| Partner|
|---|---|---|---|---|---|---|
|Anzeigen von Unternehmensadministratoren|✔|✔|✘|✘|✘|✔|
|Hinzufügen und Entfernen von Unternehmensadministratoren|✔|✘|✘|✘|✘|✘|
|Anzeigen von Benachrichtigungskontakten<sup>4</sup> |✔|✔|✘|✘|✘|✔|
|Hinzufügen und Entfernen von Benachrichtigungskontakten<sup>4</sup> |✔|✘|✘|✘|✘|✘|
|Erstellen und Verwalten von Abteilungen |✔|✘|✘|✘|✘|✘|
|Anzeigen von Abteilungsadministratoren|✔|✔|✔|✔|✘|✔|
|Hinzufügen und Entfernen von Abteilungsadministratoren|✔|✘|✔|✘|✘|✘|
|Anzeigen von Konten in der Registrierung |✔|✔|✔<sup>5</sup>|✔<sup>5</sup>|✘|✔|
|Hinzufügen von zur Registrierung und Ändern des Kontobesitzers|✔|✘|✔<sup>5</sup>|✘|✘|✘|
|Erstellen und Verwalten von Abonnements und Abonnementberechtigungen|✘|✘|✘|✘|✔|✘|

- <sup>4</sup> Benachrichtigungskontakte erhalten E-Mail-Benachrichtigungen zum Azure Enterprise Agreement.
- <sup>5</sup> Die Aufgabe ist auf Konten in Ihrer Abteilung beschränkt.

## <a name="add-a-new-enterprise-administrator"></a>Hinzufügen eines neuen Unternehmensadministrators

Unternehmensadministratoren haben die meisten Berechtigungen bei der Verwaltung einer Azure EA-Registrierung. Der erste Azure EA-Administrator wurde erstellt, als die EA-Vereinbarung eingerichtet wurde. Sie können jedoch jederzeit neue Administratoren hinzufügen oder entfernen. Neue Administratoren werden nur von vorhandenen Administratoren hinzugefügt. Weitere Informationen zum Hinzufügen zusätzlicher Unternehmensadministratoren finden Sie unter [Erstellen eines weiteren Unternehmensadministrators](ea-portal-get-started.md#create-another-enterprise-administrator). Weitere Informationen zu Rollen und Aufgaben für ein Abrechnungsprofil finden Sie unter [Rollen und Aufgaben für ein Abrechnungsprofil](understand-mca-roles.md#billing-profile-roles-and-tasks).

## <a name="update-account-owner-state-from-pending-to-active"></a>Aktualisieren des Kontobesitzerstatus von „Ausstehend“ in „Aktiv“

Wenn neue Kontobesitzer (Account Owners, AO) erstmals zu einer Azure EA-Registrierung hinzugefügt werden, wird ihr Status als _Ausstehend_ angezeigt. Wenn ein neuer Kontobesitzer die Begrüßungs-E-Mail für die Aktivierung erhält, kann er sich anmelden, um sein Konto zu aktivieren. Nach Aktivierung des Kontos wird der Kontostatus von _Ausstehend_ in _Aktiv_ geändert. Der Kontobesitzer muss die Warnmeldung lesen und die Option **Weiter** auswählen. Neue Benutzer werden möglicherweise aufgefordert, ihren Vor- und Nachnamen einzugeben, um ein Commerce-Konto zu erstellen. In dem Fall müssen die erforderlichen Informationen hinzugefügt werden, damit der Vorgang fortgesetzt und das Konto aktiviert werden kann.

## <a name="add-a-department-admin"></a>Hinzufügen eines Abteilungsadministrators

Nachdem ein Azure EA-Administrator eine Abteilung erstellt hat, kann der Azure-Unternehmensadministrator Abteilungsadministratoren hinzufügen und diese einer Abteilung zuordnen. Ein Abteilungsadministrator kann neue Konten erstellen. Neue Konten sind erforderlich, damit Azure EA-Abonnements erstellt werden können.

Weitere Informationen zum Hinzufügen eines Abteilungsadministrators finden Sie unter [Erstellen eines Azure EA-Abteilungsadministrators](ea-portal-get-started.md#add-a-department-administrator).

## <a name="usage-and-costs-access-by-role"></a>Zugriff auf Nutzung und Kosten nach Rolle

|Aufgaben| Unternehmensadministrator|Unternehmensadministrator (nur Leseberechtigung)|Abteilungsadministrator|Abteilungsadministrator (nur Leseberechtigung) |Kontobesitzer| Partner|
|---|---|---|---|---|---|---|
|Anzeigen des Guthabens einschließlich Azure-Vorauszahlung|✔|✔|✘|✘|✘|✔|
|Anzeigen von Ausgabenkontingenten der Abteilungen|✔|✔|✘|✘|✘|✔|
|Festlegen von Ausgabenkontingenten der Abteilungen|✔|✘|✘|✘|✘|✘|
|Anzeigen der EA-Preisliste der Organisation|✔|✔|✘|✘|✘|✔|
|Anzeigen von Nutzungs- und Kostendetails|✔|✔|✔<sup>6</sup>|✔<sup>6</sup>|✔<sup>7</sup>|✔|
|Verwalten von Ressourcen im Azure-Portal|✘|✘|✘|✘|✔|✘|

- <sup>6</sup> Erfordert die Aktivierung der Richtlinie **DA-Ansichtsgebühren** im Enterprise Portal durch den Unternehmensadministrator. Der Abteilungsadministrator kann dann Kostendetails für die Abteilung einsehen.
- <sup>7</sup> Erfordert die Aktivierung der Richtlinie **AO-Ansichtsgebühren** im Enterprise Portal durch den Unternehmensadministrator. Der Kontobesitzer kann dann Kostendetails für das Konto einsehen.

## <a name="see-pricing-for-different-user-roles"></a>Anzeige von Preisen für verschiedene Benutzerrollen

Möglicherweise werden Ihnen im Azure-Portal abhängig von Ihrer administrativen Rolle und der Festlegung der Richtlinien zum Anzeigen von Gebühren durch den Unternehmensadministrator unterschiedliche Gebühren angezeigt. Die beiden folgenden Richtlinien im Enterprise-Portal haben Auswirkungen auf die im Azure-Portal angezeigten Preise:

- DA view charges (Gebühren anzeigen für Abteilungsadministratoren)
- AO view charges (Gebühren anzeigen für Kontobesitzer)

Informationen zum Festlegen dieser Richtlinien finden Sie unter [Verwalten des Zugriffs auf Abrechnungsinformationen für Azure](manage-billing-access.md).

Die folgende Tabelle zeigt die Beziehungen zwischen den Enterprise Agreement-Administratorrollen, den Richtlinien zum Anzeigen von Gebühren, der Azure-Rolle im Azure-Portal und den im Azure-Portal angezeigten Preisen. Dem Unternehmensadministrator werden Nutzungsdetails immer basierend auf den EA-Preisen der Organisation angezeigt. Dem Abteilungsadministrator und dem Kontobesitzer werden jedoch – entsprechend der Richtlinie zum Anzeigen von Gebühren und ihrer Azure-Rolle – unterschiedliche Preise angezeigt. Die in der folgenden Tabelle aufgeführte Rolle des Abteilungsadministrators bezieht sich sowohl auf die Rolle „Abteilungsadministrator“ als auch die auf die Rolle „Abteilungsadministrator (nur Leseberechtigung)“.

|Enterprise Agreement-Administratorrolle|Richtlinie zum Anzeigen von Gebühren für die Rolle|Azure-Rolle|Preisansicht|
|---|---|---|---|
|Kontobesitzer ODER Abteilungsadministrator|✔ Aktiviert|Besitzer|EA-Preise der Organisation|
|Kontobesitzer ODER Abteilungsadministrator|✘ Deaktiviert|Besitzer|Einzelhandelspreise|
|Kontobesitzer ODER Abteilungsadministrator|✔ Aktiviert |none|Keine Preise|
|Kontobesitzer ODER Abteilungsadministrator|✘ Deaktiviert |none|Keine Preise|
|Keine|Nicht verfügbar |Besitzer|Einzelhandelspreise|

Sie legen die Enterprise-Administratorrolle und die Richtlinien zum Anzeigen von Gebühren im Enterprise-Portal fest. Die Azure-Rolle kann im Azure-Portal aktualisiert werden. Weitere Informationen finden Sie unter [Verwalten des Zugriffs mithilfe von RBAC und des Azure-Portals](../../role-based-access-control/role-assignments-portal.md).



## <a name="next-steps"></a>Nächste Schritte

- [Verwalten des Zugriffs auf Abrechnungsinformationen für Azure](manage-billing-access.md)
- [Verwalten des Zugriffs mithilfe der RBAC und des Azure-Portals](../../role-based-access-control/role-assignments-portal.md)
- [Integrierte Azure-Rollen](../../role-based-access-control/built-in-roles.md)
