---
title: Azure AD-Rollenbeschreibungen und -Berechtigungen – Azure Active Directory | Microsoft-Dokumentation
description: Eine Administratorrolle kann zum Hinzufügen von Benutzern, zum Zuweisen von Administratorrollen, zum Zurücksetzen von Benutzerkennwörtern sowie zum Verwalten von Benutzerlizenzen oder Domänen verwendet werden.
services: active-directory
author: curtand
manager: daveba
search.appverid: MET150
ms.service: active-directory
ms.workload: identity
ms.subservice: users-groups-roles
ms.topic: reference
ms.date: 06/15/2020
ms.author: curtand
ms.reviewer: vincesm
ms.custom: it-pro, fasttrack-edit
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09050bc6895076994baf1c98c65aa87672a5652e
ms.sourcegitcommit: d8b8768d62672e9c287a04f2578383d0eb857950
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/11/2020
ms.locfileid: "88066065"
---
# <a name="administrator-role-permissions-in-azure-active-directory"></a>Berechtigungen der Administratorrolle in Azure Active Directory

Mithilfe von Azure Active Directory (Azure AD) können Sie Administratoren mit eingeschränkten Rechten bestimmen, um Identitätsaufgaben in Rollen mit weniger Rechten zu verwalten. Administratoren können für Zwecke wie das Hinzufügen oder Ändern von Benutzern, das Zuweisen von Administratorrollen, das Zurücksetzen von Benutzerkennwörtern, das Verwalten von Benutzerlizenzen oder das Verwalten von Domänennamen festgelegt werden. Die [Standardberechtigungen für Benutzer](../fundamentals/users-default-permissions.md) können nur in den Benutzereinstellungen in Azure AD geändert werden.

## <a name="limit-use-of-global-administrator"></a>Einschränken der Verwendung der Rolle „Globaler Administrator“

Benutzer, denen die Rolle „Globaler Administrator“ zugewiesen ist, können alle administrativen Einstellungen in Ihrer Azure AD-Organisation lesen und ändern. Standardmäßig wird der Person, die sich für ein Azure-Abonnement registriert, die Rolle „Globaler Administrator“ für die Azure AD-Organisation zugewiesen. Nur globale Administratoren und Administratoren für privilegierte Rollen können Administratorrollen delegieren. Um das Risiko für Ihr Unternehmen zu verringern, wird empfohlen, diese Rolle möglichst wenigen Personen in Ihrer Organisation zuzuweisen.

Als bewährte Methode wird empfohlen, diese Rolle weniger als fünf Personen in Ihrer Organisation zuzuweisen. Im Folgenden finden Sie einige Möglichkeiten zum Verringern der Verwendung der Rolle „Globaler Administrator“, die Sie nutzen können, wenn diese Rolle in Ihrer Organisation mehr als fünf Adminisratoren zugewiesen ist.

### <a name="find-the-role-you-need"></a>Suchen nach der erforderlichen Rolle

Es kann frustrierend sein, eine umfangreiche Rollenliste nach der benötigten Rolle zu durchsuchen. Azure AD kann daher anhand von Rollenkategorien eine Teilmenge der Rollen anzeigen. Sehen Sie sich unseren neuen Filter **Typ** für [Rollen und Administratoren](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RolesAndAdministrators) in Azure AD an, mit dem Sie nur die Rollen im ausgewählten Typ anzeigen können.

### <a name="a-role-exists-now-that-didnt-exist-when-you-assigned-the-global-administrator-role"></a>Jetzt ist eine Rolle vorhanden, die noch nicht verfügbar war, als Sie die Rolle „Globaler Administrator“ zugewiesen haben

Es ist möglich, dass Azure AD Rollen hinzugefügt wurden, die differenziertere Berechtigungen bieten, die nicht zur Verfügung standen, als Sie einige Benutzer auf die Rolle „Globaler Administrator“ heraufgestuft haben. Im Laufe der Zeit stellen wir zusätzliche Rollen bereit, die das Ausführen von Aufgaben ermöglichen, die zuvor nur von einem globalen Administrator ausgeführt werden konnten. Diese werden nachstehend im Abschnitt [Verfügbare Rollen](#available-roles) aufgeführt.

## <a name="assign-or-remove-administrator-roles"></a>Zuweisen oder Entfernen von Administratorrollen

Anweisungen zum Zuweisen von Administratorrollen zu einem Benutzer in Azure Active Directory finden Sie unter [Anzeigen und Zuweisen von Administratorrollen in Azure Active Directory](directory-manage-roles-portal.md).

> [!Note]
> Wenn Sie über eine Azure AD P2 Premium-Lizenz verfügen und bereits PIM-Benutzer (Privileged Identity Management) sind, werden alle Rollenverwaltungsaufgaben in Privileged Identity Management und nicht in Azure AD ausgeführt.
>
> ![In PIM verwaltete Azure AD-Rollen für Benutzer, die PIM bereits nutzen und über eine P2 Premium-Lizenz verfügen](./media/directory-manage-roles-portal/pim-manages-roles-for-p2.png)

## <a name="available-roles"></a>Verfügbare Rollen

Die folgenden Administratorrollen sind verfügbar:

### <a name="application-administrator"></a>[Anwendungsadministrator](#application-administrator-permissions)

Benutzer mit dieser Rolle können alle Aspekte von Unternehmensanwendungen, Anwendungsregistrierungen und Anwendungsproxyeinstellungen erstellen und verwalten. Beachten Sie, dass Benutzer, denen diese Rolle zugewiesen wurde, bei der Erstellung neuer Anwendungsregistrierungen oder Unternehmensanwendungen nicht als Besitzer hinzugefügt werden.

Anwendungsadministratoren können Anmeldeinformationen von Anwendungen verwalten, die es ihnen ermöglichen, die Identität der Anwendung zu wechseln. So können Benutzer, die dieser Rolle zugewiesen sind, nur Anmeldeinformationen von Anwendungen verwalten, die entweder keinen Azure AD-Rollen oder nur folgenden Administratorrollen zugeordnet sind:

* Anwendungsadministrator
* Anwendungsentwickler
* Cloudanwendungsadministrator
* Rolle „Verzeichnis lesen“

Wenn eine Anwendung einer anderen Rolle zugeordnet ist, die oben nicht aufgeführt ist, kann der Anwendungsadministrator die Anmeldeinformationen dieser Anwendung nicht verwalten.

Diese Rolle ermöglicht auch die _Zustimmung_ zu delegierten Berechtigungen und Anwendungsberechtigungen mit Ausnahme von Berechtigungen für Microsoft Graph-API.

> [!IMPORTANT]
> Aufgrund dieser Ausnahme können Sie zwar Berechtigungen für _andere_ Apps (z. B. nicht von Microsoft stammenden Apps oder Apps, die Sie registriert haben) zustimmen, jedoch nicht Berechtigungen für Azure AD selbst. Sie können diese Berechtigungen weiterhin als Teil der App-Registrierung _anfordern_, aber für das _Erteilen_ (d. h. die Zustimmung) dieser Berechtigungen ist ein Azure AD-Administrator erforderlich. Dies bedeutet, dass ein böswilliger Benutzer seine Berechtigungen nicht problemlos erhöhen kann, z. B. könnte er versuchen, eine App zu erstellen, die in das gesamte Verzeichnis schreiben kann, und sich durch die Berechtigungen dieser App selbst zu einem globalen Administrator zu machen.

### <a name="application-developer"></a>[Anwendungsentwickler](#application-developer-permissions)

Benutzer mit dieser Rolle können Anwendungsregistrierungen erstellen, wenn die Einstellung „Benutzer können Anwendungen registrieren“ auf „Nein“ festgelegt ist. Diese Rolle ermöglicht auch die Berechtigung, im eigenen Namen zuzustimmen, wenn die Einstellung „Benutzer können Apps zustimmen, die in ihrem Namen auf Unternehmensdaten zugreifen“ auf „Nein“ festgelegt ist. Benutzer, denen diese Rolle zugewiesen wurde, werden bei der Erstellung neuer Anwendungsregistrierungen oder Unternehmensanwendungen als Besitzer hinzugefügt.

### <a name="authentication-administrator"></a>[Authentifizierungsadministrator](#authentication-administrator-permissions)

Benutzer mit dieser Rolle können Anmeldeinformationen ohne Kennwort für einige Benutzer festlegen oder zurücksetzen und Kennwörter für alle Benutzer aktualisieren. Authentifizierungsadministratoren können Benutzer, die keine Administratoren sind, oder die Rollen zugewiesen sind, auffordern, ihre vorhandenen Anmeldeinformationen ohne Kennwort (z. B. MFA oder FIDO) erneut zu registrieren, und können auch **Speichern der MFA auf dem Gerät** widerrufen. Dann werden Benutzer bei der nächsten Anmeldung zur Eingabe ihrer MFA-Anmeldeinformationen aufgefordert. Diese Aktionen gelten nur für Benutzer, die nicht Administratoren sind oder denen eine oder mehrere der folgenden Rollen zugewiesen sind:

* Authentifizierungsadministrator
* Rolle „Verzeichnis lesen“
* Gasteinladender
* Nachrichtencenter-Leser
* Meldet Reader

Die Rolle [Privilegierter Authentifizierungsadministrator](#privileged-authentication-administrator) verfügt über die Berechtigung zum Erzwingen der erneuten Registrierung und der Multi-Factor Authentication für alle Benutzer.

> [!IMPORTANT]
> Benutzer mit dieser Rolle können Anmeldeinformationen für Benutzer ändern, die Zugriff auf vertrauliche oder private Informationen bzw. kritische Konfigurationen innerhalb und außerhalb von Azure Active Directory haben. Das bedeutet, dass Benutzer, die Anmeldeinformationen ändern können, ggf. auch die Identität und die Berechtigungen des betreffenden Benutzers annehmen können. Beispiel:
>
>- Besitzer von Anwendungsregistrierungen und Unternehmensanwendungen, die Anmeldeinformationen von Apps verwalten können, die sie besitzen. Diese Apps können über höhere Berechtigungen in Azure AD und in anderen Diensten verfügen, die Authentifizierungsadministratoren nicht gewährt werden. So kann ein Authentifizierungsadministrator die Identität eines Anwendungsbesitzers annehmen und dann die Identität einer privilegierten Anwendung durch Aktualisieren der Anmeldeinformationen für die Anwendung annehmen.
>- Besitzer von Azure-Abonnements, die ggf. auf vertrauliche oder private Informationen bzw. kritische Konfigurationen in Azure zugreifen können.
>- Besitzer von Sicherheitsgruppen und Office 365-Gruppen, die die Gruppenmitgliedschaft verwalten können. Diese Gruppen können Zugriff auf vertrauliche oder private Informationen bzw. kritische Konfigurationen in Azure AD und in anderen Diensten gewähren.
>- Administratoren in anderen Diensten außerhalb von Azure AD wie Exchange Online, Office Security and Compliance Center und Personalwesen.
>- Nichtadministratoren wie Führungskräfte, Rechtsberater und Mitarbeiter der Personalabteilung mit Zugriff auf vertrauliche oder private Informationen.

### <a name="azure-devops-administrator"></a>[Azure DevOps-Administrator](#azure-devops-administrator-permissions)

Benutzer mit dieser Rolle können die Azure DevOps-Richtlinie verwalten, um die Erstellung einer neuen Azure DevOps-Organisation auf eine Gruppe von konfigurierbaren Benutzern oder Gruppen zu beschränken. Benutzer mit dieser Rolle können diese Richtlinie über jede Azure DevOps-Organisation verwalten, die von der Azure AD-Organisation des Unternehmens unterstützt wird.

Alle Azure DevOps-Richtlinien des Unternehmens können von Benutzern mit dieser Rolle verwaltet werden.

### <a name="azure-information-protection-administrator"></a>[Azure Information Protection-Administrator](#azure-information-protection-administrator-permissions)

Benutzer mit dieser Rolle besitzen alle Berechtigungen für den Azure Information Protection-Dienst. Sie können Bezeichnungen für die Azure Information Protection-Richtlinie konfigurieren, Schutzvorlagen verwalten und den Schutz aktivieren. Diese Rolle gewährt keine Berechtigungen für Identity Protection Center, Privileged Identity Management, Monitor Office 365 Service Health oder Office 365 Security & Compliance Center.

### <a name="b2c-ief-keyset-administrator"></a>[B2C-IEF-Schlüsselsatzadministrator](#b2c-ief-keyset-administrator-permissions)

Benutzer können die Richtlinienschlüssel und -geheimnisse für Tokenverschlüsselung, Tokensignaturen und Verschlüsselung/Entschlüsselung von Ansprüchen erstellen und verwalten. Durch das Hinzufügen neuer Schlüssel zu vorhandenen Schlüsselcontainern kann dieser Administrator mit eingeschränkten Rechten, nach Bedarf Rollover für Geheimnisse ausführen, ohne dass dies Auswirkungen auf vorhandene Anwendungen hat. Diese Benutzer können den vollständigen Inhalt dieser Geheimnisse und deren Ablaufdaten anzeigen – auch nach deren Erstellung.

> [!IMPORTANT]
> Dies ist eine sensible Rolle. Die Administratorrolle für Schlüsselsätze muss sorgfältig überwacht und mit Bedacht für Präproduktion und Produktion zugewiesen werden.

### <a name="b2c-ief-policy-administrator"></a>[B2C-IEF-Richtlinienadministrator](#b2c-ief-policy-administrator-permissions)

Benutzer mit dieser Rolle können alle benutzerdefinierten Richtlinien in Azure AD B2C erstellen, lesen, aktualisieren und löschen und haben daher vollständige Kontrolle über das Identity Experience Framework in der zugehörigen Azure AD B2C-Organisation. Durch das Bearbeiten von Richtlinien können diese Benutzer einen direkten Verbund mit externen Identitätsanbietern einrichten, das Verzeichnisschema und alle benutzerseitigen Inhalte (HTML, CSS, JavaScript) sowie die Anforderungen für das Abschließen einer Authentifizierung ändern, neue Benutzer erstellen, Benutzerdaten an externe Systeme senden (einschließlich einer vollständigen Migration) und alle Benutzerinformationen bearbeiten (einschließlich vertraulicher Felder wie Kennwörter und Telefonnummern). Andererseits kann diese Rolle keine Verschlüsselungsschlüssel ändern oder Geheimnisse für den Verbund in der Organisation bearbeiten.

> [!IMPORTANT]
> Der B2-IEF-Richtlinienadministrator ist eine streng vertrauliche Rolle, die nur sehr wenigen Benutzern für Organisationen in der Produktion zugewiesen werden sollte. Aktivitäten dieser Benutzer sollten streng überwacht werden. Dies gilt vor allem für Organisationen in der Produktion.

### <a name="billing-administrator"></a>[Rechnungsadministrator](#billing-administrator-permissions)

Tätigt Käufe, verwaltet Abonnements und Supporttickets und überwacht die Dienstintegrität.

### <a name="cloud-application-administrator"></a>[Cloudanwendungsadministrator](#cloud-application-administrator-permissions)

Benutzer mit dieser Rolle haben die gleichen Berechtigungen wie die Rolle des Anwendungsadministrators, mit Ausnahme der Möglichkeit, den Anwendungsproxy zu verwalten. Diese Rolle ermöglicht die Erstellung und Verwaltung aller Aspekte von Unternehmensanwendungen und Anwendungsregistrierungen. Diese Rolle ermöglicht auch die Zustimmung zu delegierten Berechtigungen und Anwendungsberechtigungen mit Ausnahme von Berechtigungen für Microsoft Graph-API. Benutzer, denen diese Rolle zugewiesen wurde, werden bei der Erstellung neuer Anwendungsregistrierungen oder Unternehmensanwendungen nicht als Besitzer hinzugefügt.

Cloudanwendungsadministratoren können Anmeldeinformationen von Anwendungen verwalten, die es ihnen ermöglichen, die Identität der Anwendung zu wechseln. So können Benutzer, die dieser Rolle zugewiesen sind, nur Anmeldeinformationen von Anwendungen verwalten, die entweder keinen Azure AD-Rollen oder nur folgenden Administratorrollen zugeordnet sind:

* Anwendungsentwickler
* Cloudanwendungsadministrator
* Rolle „Verzeichnis lesen“

Wenn eine Anwendung einer anderen Rolle zugeordnet ist, die oben nicht aufgeführt ist, kann der Cloudanwendungsadministrator die Anmeldeinformationen dieser Anwendung nicht verwalten.

### <a name="cloud-device-administrator"></a>[Cloudgeräteadministrator](#cloud-device-administrator-permissions)

Benutzer mit dieser Rolle können Geräte in Azure AD aktivieren, deaktivieren und löschen sowie Windows 10-BitLocker-Schlüssel (falls vorhanden) im Azure-Portal lesen. Die Rolle gewährt keine Berechtigungen für die Verwaltung anderer Eigenschaften auf dem Gerät.

### <a name="compliance-administrator"></a>[Complianceadministrator](#compliance-administrator-permissions)

Benutzer mit dieser Rolle verfügen über Berechtigungen zum Verwalten von Compliancefeatures im Microsoft 365 Compliance Center, Microsoft 365 Admin Center, Azure, und Office 365 Security & Compliance Center. Zugewiesene Personen können auch alle Features im Exchange Admin Center sowie im Teams und Skype for Business Admin Center verwalten und Supporttickets für Azure und Microsoft 365 erstellen. Weitere Informationen finden Sie unter [Informationen zu Administratorrollen von Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

Geben Sie in | Möglich
----- | ----------
[Microsoft 365 Compliance Center](https://protection.office.com) | Schützen und Verwalten Ihrer Organisationsdaten für Microsoft 365-Dienste<br>Verwalten von Konformitätwarnungen
[Compliance Manager](https://docs.microsoft.com/office365/securitycompliance/meet-data-protection-and-regulatory-reqs-using-microsoft-cloud) | Nachverfolgen, Zuweisen und Überprüfen der Einhaltung gesetzlicher Vorschriften durch Ihre Organisation
[Office 365 Security & Compliance Center](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d) | Verwalten der Datengovernance<br>Durchführen von Untersuchung zu rechtlichen Aspekten und von Daten<br>Verwalten von DRS-Anforderungen<br><br>Diese Rolle verfügt über die gleichen Berechtigungen wie die Rollengruppe [Complianceadministrator](https://docs.microsoft.com/microsoft-365/security/office-365-security/permissions-in-the-security-and-compliance-center#permissions-needed-to-use-features-in-the-security--compliance-center) der rollenbasierten Zugriffssteuerung im Office 365 Security & Compliance Center.
[Intune](https://docs.microsoft.com/intune/role-based-access-control) | Anzeigen aller Intune-Überwachungsdaten
[Cloud App Security](https://docs.microsoft.com/cloud-app-security/manage-admins) | Verfügt über schreibgeschützten Zugriff und kann Warnungen verwalten<br>Kann Dateirichtlinien erstellen und ändern und Dateigovernanceaktionen zulassen<br>Kann alle unter „Datenverwaltung“ integrierten Berichte anzeigen

### <a name="compliance-data-administrator"></a>[Compliancedatenadministrator](#compliance-data-administrator-permissions)

Benutzer mit dieser Rolle verfügen über Berechtigungen zum Nachverfolgen von Daten im Microsoft 365 Compliance Center, Microsoft 365 Admin Center und in Azure. Die Benutzer können auch Compliancedaten im Exchange Admin Center, in Compliance-Manager sowie im Teams und Skype for Business Admin Center nachverfolgen und Supporttickets für Azure und Microsoft 365 erstellen.

Geben Sie in | Möglich
----- | ----------
[Microsoft 365 Compliance Center](https://protection.office.com) | Überwachen von compliancerelevanten Richtlinien in Microsoft 365-Diensten<br>Verwalten von Konformitätwarnungen
[Compliance Manager](https://docs.microsoft.com/office365/securitycompliance/meet-data-protection-and-regulatory-reqs-using-microsoft-cloud) | Nachverfolgen, Zuweisen und Überprüfen der Einhaltung gesetzlicher Vorschriften durch Ihre Organisation
[Office 365 Security & Compliance Center](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d) | Verwalten der Datengovernance<br>Durchführen von Untersuchung zu rechtlichen Aspekten und von Daten<br>Verwalten von DRS-Anforderungen<br><br>Diese Rolle verfügt über die gleichen Berechtigungen wie die Rollengruppe [Compliancedatenadministrator](https://docs.microsoft.com/microsoft-365/security/office-365-security/permissions-in-the-security-and-compliance-center#permissions-needed-to-use-features-in-the-security--compliance-center) der rollenbasierten Zugriffssteuerung im Office 365 Security & Compliance Center.
[Intune](https://docs.microsoft.com/intune/role-based-access-control) | Anzeigen aller Intune-Überwachungsdaten
[Cloud App Security](https://docs.microsoft.com/cloud-app-security/manage-admins) | Verfügt über schreibgeschützten Zugriff und kann Warnungen verwalten<br>Kann Dateirichtlinien erstellen und ändern und Dateigovernanceaktionen zulassen<br>Kann alle unter „Datenverwaltung“ integrierten Berichte anzeigen

### <a name="conditional-access-administrator"></a>[Administrator für bedingten Zugriff](#conditional-access-administrator-permissions)

Benutzer mit dieser Rolle können Azure Active Directory-Einstellungen für den bedingten Zugriff verwalten.
> [!NOTE]
> Um die Exchange ActiveSync-Richtlinie für bedingten Zugriff in Azure bereitzustellen, muss der Benutzer auch ein globaler Administrator sein.

### <a name="customer-lockbox-access-approver"></a>[Genehmiger für Kunden-Lockboxzugriff](#customer-lockbox-access-approver-permissions)

Verwaltet [Kunden-Lockbox-Anforderungen](https://docs.microsoft.com/office365/admin/manage/customer-lockbox-requests) in Ihrer Organisation. Sie erhalten E-Mail-Benachrichtigungen für Kunden-Lockbox-Anforderungen und können Anforderungen über das Microsoft 365 Admin Center genehmigen und ablehnen. Außerdem können sie das Feature Kunden-Lockbox aktivieren und deaktivieren. Nur globale Administratoren können die Kennwörter von Personen, die dieser Rolle zugewiesen sind, zurücksetzen.

### <a name="desktop-analytics-administrator"></a>[Desktop Analytics-Administrator](#desktop-analytics-administrator-permissions)


Benutzer in dieser Rolle können Desktop Analytics und die Dienste für Office-Anpassung und -Richtlinien verwalten. Bei Desktop Analytics umfasst dies die Möglichkeit, den Assetbestand anzuzeigen, Bereitstellungspläne zu erstellen sowie die Bereitstellung und den Integritätsstatus zu anzuzeigen. Beim Dienst für Office-Anpassung und -Richtlinien ermöglicht diese Rolle den Benutzern die Verwaltung von Office-Richtlinien.

### <a name="device-administrators"></a>[Geräteadministratoren](#device-administrators-permissions)

Diese Rolle kann nur als zusätzlicher lokaler Administrator in den [Geräteeinstellungen](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/DevicesMenuBlade/DeviceSettings/menuId/) zugewiesen werden. Benutzer mit dieser Rolle werden auf allen Windows 10-Geräten, die in Azure Active Directory eingebunden sind, als Administratoren für den lokalen Computer festgelegt. Sie haben nicht die Möglichkeit zum Verwalten von Geräteobjekten in Azure Active Directory.

### <a name="directory-readers"></a>[Verzeichnisleseberechtigte](#directory-readers-permissions)

Benutzer in dieser Rolle können grundlegende Verzeichnisinformationen lesen. Diese Rolle sollte für folgende Zwecke verwendet werden:

* Gewähren von Lesezugriff für eine bestimmte Gruppe von Gastbenutzern statt für alle Gastbenutzer.
* Gewähren von Zugriff auf das Azure-Portal für eine bestimmten Gruppe von Benutzern ohne Administratorberechtigung, wenn „Zugriff auf Azure AD-Portal auf Administratoren beschränken“ auf „Ja“ festgelegt ist.
* Gewähren von Zugriff auf das Verzeichnis für Dienstprinzipale, wenn „Directory.Read.All“ keine Option darstellt.

### <a name="directory-synchronization-accounts"></a>[Verzeichnissynchronisierungskonten](#directory-synchronization-accounts-permissions)

Darf nicht verwendet werden. Diese Rolle wird automatisch dem Azure AD Connect-Dienst zugewiesen und ist weder für eine andere Verwendung vorgesehen, noch wird eine andere Verwendung unterstützt.

### <a name="directory-writers"></a>[Verzeichnisschreibberechtigte](#directory-writers-permissions)
Benutzer mit dieser Rolle können grundlegende Informationen von Benutzern, Gruppen und Dienstprinzipalen lesen und aktualisieren. Weisen Sie diese Rolle nur Anwendungen zu, die das [Zustimmungsframework](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app) nicht unterstützen. Diese Rolle sollte keinem Benutzer zugewiesen werden.

### <a name="dynamics-365-administrator--crm-administrator"></a>[Dynamics 365-Administrator/CRM-Administrator](#crm-service-administrator-permissions)

Benutzer mit dieser Rolle besitzen globale Berechtigungen innerhalb von Microsoft Dynamics 365 Online, wenn der Dienst verfügbar ist, und können Supporttickets verwalten und die Dienstintegrität überwachen. Weitere Informationen finden Sie unter [Verwenden der Dienstadministratorrolle zum Verwalten Ihrer Azure AD-Organisation](https://docs.microsoft.com/dynamics365/customer-engagement/admin/use-service-admin-role-manage-tenant).

> [!NOTE]
> In Microsoft Graph-API und Azure AD PowerShell wird diese Rolle als „Dynamics 365-Dienstadministrator“ bezeichnet. Im [Azure-Portal](https://portal.azure.com) lautet sie „Dynamics 365-Administrator“.

### <a name="exchange-administrator"></a>[Exchange-Administrator](#exchange-service-administrator-permissions)

Benutzer mit dieser Rolle besitzen globale Berechtigungen in Microsoft Exchange Online, wenn der Dienst verfügbar ist. Außerdem haben sie die Möglichkeit, alle Office 365-Gruppen zu erstellen und zu verwalten, Supporttickets zu verwalten und die Dienstintegrität zu überwachen. Weitere Informationen finden Sie unter [Informationen zu Administratorrollen von Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

> [!NOTE]
> In Microsoft Graph-API und Azure AD PowerShell wird diese Rolle als „Exchange-Dienstadministrator“ bezeichnet. Im [Azure-Portal](https://portal.azure.com) lautet sie „Exchange-Administrator“. Im [Exchange Admin Center](https://go.microsoft.com/fwlink/p/?LinkID=529144) lautet sie „Exchange Online-Administrator“.


### <a name="external-id-user-flow-administrator"></a>[Administrator für Benutzerflows mit externer ID](#external-id-user-flow-administrator-permissions)

Benutzer mit dieser Rolle können Benutzerflows (auch als „integrierte“ Richtlinien bezeichnet) im Azure-Portal erstellen und verwalten. Sie können HTML-/CSS-/JavaScript-Inhalte anpassen, MFA-Anforderungen ändern, Ansprüche im Token auswählen, API-Connectors verwalten und Sitzungseinstellungen für alle Benutzerflows in der Azure AD-Organisation konfigurieren. Auf der anderen Seite bietet diese Rolle nicht die Möglichkeit, Benutzerdaten zu überprüfen oder Änderungen an Attributen vorzunehmen, die im Organisationsschema enthalten sind. Änderungen an Richtlinien des Identity Experience Framework (auch „benutzerdefinierte Richtlinien“ genannt) gehören ebenfalls nicht zum Berechtigungsumfang dieser Rolle.

### <a name="external-id-user-flow-attribute-administrator"></a>[Administrator für Benutzerflowattribute mit externer ID](#external-id-user-flow-attribute-administrator-permissions)

Benutzer mit dieser Rolle können benutzerdefinierte Attribute, die für alle Benutzerflows in der Azure AD-Organisation verfügbar sind, hinzufügen und löschen. Daher können Benutzer mit dieser Rolle dem Benutzerschema neue Elemente hinzufügen und diese ändern und haben damit Einfluss auf das Verhalten aller Benutzerflows. Indirekt kann dies auch ändern, welche Daten von Benutzern abgefragt und letztendlich als Ansprüche an Anwendungen gesendet werden. Diese Rolle kann keine Benutzerflows bearbeiten.

### <a name="external-identity-provider-administrator"></a>[Externer Identitätsanbieteradministrator](#external-identity-provider-administrator-permissions)

Dieser Administrator verwaltet den Verbund zwischen Azure AD-Organisationen und externen Identitätsanbietern. Benutzer mit dieser Rolle können neue Identitätsanbieter hinzufügen und alle verfügbaren Einstellungen (z.B. Authentifizierungspfad, Dienst-ID, zugewiesene Schlüsselcontainer) konfigurieren. Diese Benutzer können festlegen, dass die Azure AD-Organisation Authentifizierungen von externen Identitätsanbietern vertraut. Die resultierenden Auswirkungen auf die Benutzerumgebung hängt vom Typ der Organisation ab:

* Azure AD-Organisationen für Mitarbeiter und Partner: Das Hinzufügen eines Verbunds (z. B. mit Gmail) hat sofortige Auswirkungen auf Einladungen für Gäste, die noch nicht eingelöst wurden. Weitere Informationen finden Sie unter [Hinzufügen von Google als Identitätsanbieter für B2B-Gastbenutzer](https://docs.microsoft.com/azure/active-directory/b2b/google-federation).
* Azure Active Directory B2C-Organisationen: Das Hinzufügen eines Verbunds (z. B. bei Facebook oder einer anderen Azure AD-Organisation) wirkt sich nicht sofort auf die Endbenutzerflows aus, sondern erst, wenn der Identitätsanbieter in einem Benutzerflow als Option hinzugefügt wird (auch bezeichnet als „integrierte Richtlinie“). Ein Beispiel finden Sie unter [Konfigurieren eines Microsoft-Kontos als Identitätsanbieter](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app). Um Benutzerflows zu ändern, ist die Rolle „B2C-Benutzerflowadministrator“ mit eingeschränkten Rechen erforderlich.

### <a name="global-administrator--company-administrator"></a>[Globaler Administrator/Unternehmensadministrator](#company-administrator-permissions)

Benutzer mit dieser Rolle besitzen Zugriff auf alle administrativen Features in Azure Active Directory sowie Dienste, die Azure Active Directory-Identitäten nutzen, z.B. Microsoft 365 Security Center, Microsoft 365 Compliance Center, Exchange Online, SharePoint Online oder Skype for Business Online. Zudem können globale Administratoren ihre [Zugriffsrechte erhöhen](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin), um alle Azure-Abonnements und Verwaltungsgruppen zu verwalten. Dadurch erhalten sie mithilfe des entsprechenden Azure AD-Mandanten Vollzugriff auf alle Azure-Ressourcen. Die Person, die die Anmeldung für die Azure AD-Organisation vornimmt, wird ein globaler Administrator. In Ihrem Unternehmen können mehrere globale Administratoren vorhanden sein. Globale Administratoren können das Kennwort für alle Benutzer und alle anderen Administratoren zurücksetzen.

> [!NOTE]
> In Microsoft Graph-API und Azure AD PowerShell wird diese Rolle als „Unternehmensadministrator“ bezeichnet. Im [Azure-Portal](https://portal.azure.com)ist dies der „globale Administrator“.
>
>

### <a name="global-reader"></a>[Globaler Leser](#global-reader-permissions)

Benutzer in dieser Rolle können in Microsoft 365-Diensten Einstellungen und administrative Informationen lesen, aber keine Verwaltungsaktionen ausführen. Die Rolle „Globaler Leser“ ist das Gegenstück zu „Globaler Administrator“, hat jedoch eine Nur-Lese-Berechtigung. Weisen Sie die Rolle „Globaler Leser“ anstelle der Rolle „Globaler Administrator“ für Planungen, Audits oder Untersuchungen zu. Kombinieren Sie die Rolle „Globaler Leser“ mit anderen eingeschränkten Administratorrollen (z.B. Exchange-Administrator), um bei der Arbeit leichter auf die Rolle „Globaler Administrator“ verzichten zu können. Die Rolle „Globaler Leser“ funktioniert mit Microsoft 365 Admin Center, Exchange Admin Center, SharePoint Admin Center, Teams Admin Center, Security Center, Compliance Center, Azure AD Admin Center und Device Management Admin Center.

> [!NOTE]
> Die Rolle „Globaler Leser“ weist zurzeit einige Einschränkungen auf.
>
>- [OneDrive Admin Center:](https://admin.onedrive.com/) OneDrive Admin Center unterstützt die Rolle „Globaler Leser“ nicht.
>- [M365 Admin Center](https://admin.microsoft.com/Adminportal/Home#/homepage): Die Rolle „Globaler Leser“ kann keine Kunden-Lockbox-Anforderungen lesen. Im linken Bereich von M365 Admin Center wird keine Registerkarte **Kunden-Lockbox-Anforderungen** unter **Support** angezeigt.
>- [Office Security & Compliance Center](https://sip.protection.office.com/homepage): Die Rolle „Globaler Leser“ kann weder SCC-Überwachungsprotokolle lesen, die Inhaltssuche durchführen noch die Sicherheitsbewertung anzeigen.
>- [Teams Admin Center](https://admin.teams.microsoft.com): Die Rolle „Globaler Leser“ kann den **Teams-Lebenszyklus**, **Analysen und Berichte**, die **IP-Telefon-Geräteverwaltung** und den **App-Katalog** nicht lesen.
>- [Privileged Access Management (PAM)](https://docs.microsoft.com/office365/securitycompliance/privileged-access-management-overview) unterstützt die Rolle „Globaler Leser“ nicht.
>- [Azure Information Protection:](https://docs.microsoft.com/azure/information-protection/what-is-information-protection) Die Rolle „Globaler Leser“ wird nur für die [zentrale Berichterstellung](https://docs.microsoft.com/azure/information-protection/reports-aip) unterstützt, wenn sich Ihre Azure AD-Organisation nicht auf der [Plattform für einheitliche Bezeichnungen](https://docs.microsoft.com/azure/information-protection/faqs#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform) befindet.
>
> Diese Features befinden sich zurzeit in der Entwicklung.
>

### <a name="groups-administrator"></a>[Gruppenadministrator](#groups-administrator-permissions)

Benutzer mit dieser Rolle können Gruppen und die zugehörigen Einstellungen wie Benennungs- und Ablaufrichtlinien erstellen und verwalten. Es ist wichtig zu verstehen, dass der Benutzer durch die Zuweisung dieser Rolle alle Gruppen in der Organisation nicht nur in Outlook, sondern in verschiedenen Workloads wie Teams, SharePoint und Yammer verwalten kann. Außerdem kann der Benutzer die verschiedenen Gruppeneinstellungen in verschiedenen Verwaltungsportalen wie Microsoft Admin Center und Azure-Portal sowie den workloadspezifischen Portalen wie Teams Admin Center und SharePoint Admin Center verwalten.

### <a name="guest-inviter"></a>[Gasteinladender](#guest-inviter-permissions)

Wenn die Benutzereinstellung **Mitglieder können einladen** auf „Nein“ festgelegt ist, können Benutzer in dieser Rolle Azure Active Directory B2B-Gastbenutzereinladungen verwalten. Weitere Informationen zur B2B-Zusammenarbeit finden Sie unter [Was ist die Azure AD B2B-Zusammenarbeit?](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b). Es sind keine anderen Berechtigungen eingeschlossen.

### <a name="helpdesk-administrator"></a>[Helpdeskadministrator](#helpdesk-administrator-permissions)

Benutzer mit dieser Rolle können Kennwörter ändern, Aktualisierungstoken für ungültig erklären, Dienstanforderungen verwalten und die Dienstintegrität überwachen. Wenn ein Aktualisierungstoken für ungültig erklärt wird, muss sich der Benutzer erneut anmelden. Helpdeskadministratoren können Kennwörter zurücksetzen und Aktualisierungstoken anderer Benutzer annullieren, die keine Administratoren sind oder denen nur die folgenden Rollen zugewiesen wurden:

* Rolle „Verzeichnis lesen“
* Gasteinladender
* Helpdeskadministrator
* Nachrichtencenter-Leser
* Kennwortadministrator
* Meldet Reader

> [!IMPORTANT]
> Benutzer mit dieser Rolle können Kennwörter für Benutzer ändern, die Zugriff auf vertrauliche oder private Informationen bzw. kritische Konfigurationen innerhalb und außerhalb von Azure Active Directory haben. Benutzer, die Kennwörter ändern können, können ggf. auch die Identität und die Berechtigungen des betreffenden Benutzers annehmen. Beispiel:
>
>- Besitzer von Anwendungsregistrierungen und Unternehmensanwendungen, die Anmeldeinformationen von Apps verwalten können, die sie besitzen. Diese Apps können über höhere Berechtigungen in Azure AD und in anderen Diensten verfügen, die Helpdeskadministratoren nicht gewährt werden. So kann ein Helpdeskadministrator die Identität eines Anwendungsbesitzers annehmen und dann die Identität einer privilegierten Anwendung durch Aktualisieren der Anmeldeinformationen für die Anwendung annehmen.
>- Besitzer von Azure-Abonnements, die möglicherweise auf vertrauliche oder private Informationen oder kritische Konfigurationen in Azure zugreifen können.
>- Besitzer von Sicherheitsgruppen und Office 365-Gruppen, die die Gruppenmitgliedschaft verwalten können. Diese Gruppen können Zugriff auf vertrauliche oder private Informationen bzw. kritische Konfigurationen in Azure AD und in anderen Diensten gewähren.
>- Administratoren in anderen Diensten außerhalb von Azure AD wie Exchange Online, Office Security and Compliance Center und Personalwesen.
>- Nichtadministratoren wie Führungskräfte, Rechtsberater und Mitarbeiter der Personalabteilung mit Zugriff auf vertrauliche oder private Informationen.

Das Delegieren von administrativen Berechtigungen für Teilmengen von Benutzern und das Anwenden von Richtlinien auf eine Benutzerteilmenge kann über [Verwaltungseinheiten (jetzt in der öffentlichen Vorschau verfügbar)](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-administrative-units) erfolgen.

Im [Azure-Portal](https://portal.azure.com/) hieß diese Rolle früher „Kennwortadministrator“. Der Name „Helpdeskadministrator“ in Azure AD entspricht jetzt dem Namen in Azure AD PowerShell und Microsoft Graph-API.

### <a name="hybrid-identity-administrator"></a>[Hybrididentitätsadministrator](#hybrid-identity-administrator-permissions)

Benutzer mit dieser Rolle können Dienste und Einstellungen im Zusammenhang mit der Aktivierung der Hybrididentität in Azure AD aktivieren, konfigurieren und verwalten. Diese Rolle bietet die Möglichkeit, Azure AD für eine der drei unterstützten Authentifizierungsmethoden Kennworthashsynchronisierung, Pass-Through-Authentifizierung oder Verbund (AD FS oder Drittanbieterverbund) zu konfigurieren und eine zugehörige lokale Infrastruktur für die Aktivierung bereitzustellen. Die lokale Infrastruktur umfasst die Bereitstellung und PTA-Agents. Diese Rolle gewährt die Fähigkeit, S-SSO (Seamless Single Sign-On, nahtloses einmaliges Anmelden) zu aktivieren, um eine nahtlose Authentifizierung auf Geräten ohne Windows 10 bzw. Computern ohne Windows Server 2016 zu ermöglichen. Außerdem gewährt diese Rolle zu Überwachungs- und Troubleshootingszwecken die Fähigkeit, Anmeldeprotokolle einzusehen und auf Daten zur Integrität und Analysen zuzugreifen. 

### <a name="insights-administrator"></a>[Insights Administrator](#insights-administrator-permissions)
Benutzer mit dieser Rolle können auf alle administrativen Funktionen in der [M365-Insights-Anwendung](https://go.microsoft.com/fwlink/?linkid=2129521) zugreifen. Diese Rolle kann Verzeichnisinformationen lesen, die Dienstintegrität überwachen, Supporttickets einordnen und auf die Einstellungsaspekte für Insights-Administratoren zuzugreifen.

### <a name="insights-business-leader"></a>[Insights Business Leader](#insights-business-leader-permissions)
Benutzer mit dieser Rolle können über die [M365-Insights-Anwendung](https://go.microsoft.com/fwlink/?linkid=2129521) auf eine Gruppe von Dashboards und Erkenntnisse zugreifen. Dies umfasst Vollzugriff auf alle Dashboards und die dargestellten Funktionen für Erkenntnisse sowie das Durchsuchen von Daten. Benutzer mit dieser Rolle haben keinen Zugriff auf die Einstellungen für die Produktkonfiguration, für die die Rolle „Insights Administrator“ zuständig ist.

### <a name="intune-administrator"></a>[Intune-Administrator](#intune-service-administrator-permissions)

Benutzer mit dieser Rolle besitzen globale Berechtigungen in Microsoft Intune Online, wenn der Dienst verfügbar ist. Darüber hinaus beinhaltet diese Rolle die Möglichkeit, Benutzer und Geräte zum Zuordnen von Richtlinien zu verwalten sowie Gruppen zu erstellen und zu verwalten. Weitere Informationen finden Sie unter [Rollenbasierte Zugriffssteuerung mit Microsoft Intune](https://docs.microsoft.com/intune/role-based-access-control).

Mit dieser Rolle können alle Sicherheitsgruppen erstellt und verwaltet werden. Der Intune-Administrator besitzt jedoch keine Administratorrechte für Office-Gruppen. Der Administrator kann also keine Besitzer oder Mitgliedschaften aller Office-Gruppen in der Organisation aktualisieren. Im Rahmen seiner Endbenutzerberechtigungen kann er allerdings die von ihm erstellte Office-Gruppe verwalten. Daher zählt jede von ihm erstellte Office-Gruppe (nicht Sicherheitsgruppe) zu seinem Kontingent von 250 Stück.

> [!NOTE]
> In Azure AD PowerShell und der Microsoft Graph-API wird diese Rolle als „Intune-Dienstadministrator“ bezeichnet. Im [Azure-Portal](https://portal.azure.com) lautet sie „Intune-Administrator“.

### <a name="kaizala-administrator"></a>[Kaizala-Administrator](#kaizala-administrator-permissions)

Benutzer mit dieser Rolle besitzen globale Berechtigungen zum Verwalten von Einstellungen in Microsoft Kaizala, wenn der Dienst verfügbar ist, und können Supporttickets verwalten und die Dienstintegrität überwachen. Darüber hinaus können diese Benutzer auf Berichte zur Einführung und Nutzung von Kaizala durch Mitglieder der Organisation sowie auf Geschäftsberichte zugreifen, die mithilfe von Kaizala-Aktionen generiert wurden.

### <a name="license-administrator"></a>[Lizenzadministrator](#license-administrator-permissions)

Benutzer mit dieser Rolle können Lizenzzuweisungen für Benutzer und Gruppen (unter Verwendung der gruppenbasierten Lizenzierung) hinzufügen, entfernen und aktualisieren sowie den Verwendungsstandort für Benutzer verwalten. Mit dieser Rolle ist es nicht möglich, Abonnements zu erwerben oder zu verwalten, Gruppen zu erstellen oder zu verwalten oder Benutzer zu erstellen oder zu verwalten (mit Ausnahme des Verwendungsstandorts). Diese Rolle kann keine Supporttickets anzeigen, erstellen oder verwalten.

### <a name="message-center-privacy-reader"></a>[Nachrichtencenter-Datenschutzleseberechtigter](#message-center-privacy-reader-permissions)

Benutzer mit dieser Rolle können alle Benachrichtigungen im Nachrichtencenter überwachen, einschließlich Nachrichten zum Datenschutz. Nachrichtencenter-Datenschutzleseberechtigte erhalten E-Mail-Benachrichtigungen, einschließlich Nachrichten zum Datenschutz, und können Benachrichtigungen mithilfe der Einstellungen im Nachrichtencenter abbestellen. Nur der globale Administrator und Nachrichtencenter-Datenschutzleseberechtigte können Nachrichten zum Datenschutz lesen. Darüber hinaus umfasst diese Rolle die Berechtigung zum Anzeigen von Gruppen, Domänen und Abonnements. Diese Rolle umfasst keine Berechtigung zum Anzeigen, Erstellen oder Verwalten von Service Requests.

### <a name="message-center-reader"></a>[Nachrichtencenter-Leseberechtigter](#message-center-reader-permissions)

Benutzer mit dieser Rolle können Benachrichtigungen und empfohlene Integritätsupdates für ihre Organisation und die konfigurierten Dienste wie Exchange, Intune und Microsoft Teams im [Office 365-Nachrichtencenter](https://support.office.com/article/Message-center-in-Office-365-38FB3333-BFCC-4340-A37B-DEDA509C2093) überwachen. Nachrichtencenter-Leser erhalten eine wöchentliche E-Mail-Übersicht der Beiträge und Updates und können Beiträge in Office 365 teilen. In Azure AD haben Benutzer mit dieser Rolle nur schreibgeschützten Zugriff auf Azure AD-Dienste wie Benutzer und Gruppen. Diese Rolle kann keine Supporttickets anzeigen, erstellen oder verwalten.

### <a name="modern-commerce-user"></a>[Modern Commerce User](#modern-commerce-user-permissions)

Darf nicht verwendet werden. Diese Rolle wird automatisch von Commerce zugewiesen und ist weder für eine andere Verwendung vorgesehen, noch wird eine andere Verwendung unterstützt. Die Details hierzu finden Sie unten.

Mit der Rolle „Modern Commerce User“ sind bestimmte Benutzer berechtigt, auf Microsoft 365 Admin Center zuzugreifen und die Navigationseinträge links für **Home**, **Abrechnung** und **Support** anzuzeigen. Der in diesen Bereichen verfügbare Inhalt wird von [commercespezifischen Rollen gesteuert](https://docs.microsoft.com/azure/cost-management-billing/manage/understand-mca-roles), die Benutzern zugewiesen werden, um Produkte zu verwalten, die sie für sich selbst oder für Ihre Organisation gekauft haben. Dies kann Aufgaben wie das Bezahlen von Rechnungen oder den Zugriff auf Abrechnungskonten und Abrechnungsprofile umfassen. 

Benutzer mit der Rolle „Modern Commerce User“ verfügen in der Regel über administrative Berechtigungen in anderen Microsoft-Einkaufssystemen, jedoch nicht über die Rollen „Unternehmensadministrator“ oder „Abrechnungsadministrator“, die für den Zugriff auf Admin Center verwendet werden. 

**Wann wird die Rolle „Modern Commerce User“ zugewiesen?**

* **Self-Service-Käufe in Microsoft 365 Admin Center**: Self-Service-Käufe bieten Benutzern die Möglichkeit, neue Produkte zu testen, indem sie sich diese Produkte selbst kaufen oder sich dafür registrieren. Diese Produkte werden in Admin Center verwaltet. Benutzern, die einen Self-Service-Kauf tätigen, werden eine Rolle im Commercesystem und die Rolle „Modern Commerce User“ zugewiesen, damit sie ihre Käufe in Admin Center verwalten können. Administratoren können über [PowerShell](https://docs.microsoft.com/microsoft-365/commerce/subscriptions/allowselfservicepurchase-powershell?view=o365-worldwide) Self-Service-Käufe (für Power BI, Power Apps, Power Automate) blockieren. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zu Self-Service-Einkäufen](https://docs.microsoft.com/microsoft-365/commerce/subscriptions/self-service-purchase-faq?view=o365-worldwide).  
* **Käufe über den kommerziellen Microsoft Marketplace:** Wenn ein Benutzer ein Produkt oder einen Dienst von Microsoft AppSource oder im Azure Marketplace kauft, wird ähnlich wie beim Self-Service-Kauf die Rolle „Modern Commerce User“ zugewiesen, wenn er nicht über die Rollen „Globaler Administrator“ oder „Abrechnungsadministrator“ verfügt. In einigen Fällen werden Benutzer möglicherweise daran gehindert, diese Käufe durchzuführen. Weitere Informationen finden Sie unter [Kommerzieller Microsoft Marketplace](https://docs.microsoft.com/azure/marketplace/marketplace-faq-publisher-guide#what-could-block-a-customer-from-completing-a-purchase).
* **Vorschläge von Microsoft**: Ein Vorschlag ist ein formales Angebot von Microsoft für Ihre Organisation, Microsoft-Produkte und -Dienste zu erwerben. Wenn die Person, die den Vorschlag annimmt, nicht in Azure AD über eine globale Administrator- oder Abrechnungsadministratorrolle verfügt, wird ihr eine commercespezifische Rolle zugewiesen, um den Vorschlag abzuschließen, sowie die Rolle „Modern Commerce User“ für den Zugriff auf Admin Center. Wenn diese Person auf Admin Center zugreifen, kann sie nur Funktionen verwenden, die von ihrer commercespezifischen Rolle autorisiert werden.
* **Commercespezifische Rollen**: Einigen Benutzern werden commercespezifische Rollen zugewiesen. Wenn ein Benutzer kein globaler Administrator oder Abrechnungsadministrator ist, erhält er die Rolle „Modern Commerce User“, damit er auf Admin Center zugreifen kann.  

Wenn die Zuweisung der Rolle „Modern Commerce User“ für einen Benutzer aufgehoben wird, verliert er den Zugriff auf Microsoft 365 Admin Center. Wenn er Produkte entweder für sich selbst oder für Ihre Organisation verwaltet hat, kann er die Verwaltung nicht fortsetzen. Dies kann das Zuweisen von Lizenzen, das Ändern von Zahlungsmethoden, das Bezahlen von Rechnungen oder andere Aufgaben zum Verwalten von Abonnements umfassen.

### <a name="network-administrator"></a>[Netzwerkadministrator](#network-administrator-permissions)

Benutzer mit dieser Rolle können Empfehlungen zur Netzwerkumkreisarchitektur von Microsoft überprüfen, die auf Netzwerktelemetriedaten von ihren Benutzerstandorten basieren. Die Netzwerkleistung für Office 365 basiert auf einer sorgfältigen Netzwerkumkreisarchitektur für Unternehmenskunden, die im Allgemeinen für den Benutzerstandort spezifisch ist. Diese Rolle ermöglicht das Bearbeiten von ermittelten Benutzerstandorten und das Konfigurieren von Netzwerkparametern für diese Standorte, um verbesserte Telemetriemessungen und Entwurfsempfehlungen zu ermöglichen.
### <a name="office-apps-administrator"></a>[Office-Apps-Administrator](#office-apps-administrator-permissions)

Benutzer mit dieser Rolle können die Cloudeinstellungen von Office 365-Apps verwalten. Dazu gehören die Verwaltung von Cloudrichtlinien, die Self-Service-Downloadverwaltung und die Möglichkeit, Office-Apps-bezogene Berichte anzuzeigen. Diese Rolle ermöglicht es außerdem, Supporttickets zu verwalten und die Dienstintegrität im Haupt-Admin Center zu überwachen. Benutzer, denen diese Rolle zugewiesen ist, können außerdem Mitteilungen zu neuen Features in Office-Apps verwalten. 

### <a name="partner-tier1-support"></a>[Partnersupport der Ebene 1](#partner-tier1-support-permissions)

Darf nicht verwendet werden. Diese Rolle wurde als veraltet markiert und wird aus Azure AD entfernt. Diese Rolle ist für einige wenige Wiederverkaufspartner von Microsoft und nicht zur allgemeinen Verwendung vorgesehen.

### <a name="partner-tier2-support"></a>[Partnersupport der Ebene 2](#partner-tier2-support-permissions)

Darf nicht verwendet werden. Diese Rolle wurde als veraltet markiert und wird aus Azure AD entfernt. Diese Rolle ist für einige wenige Wiederverkaufspartner von Microsoft und nicht zur allgemeinen Verwendung vorgesehen.

### <a name="password-administrator"></a>[Kennwortadministrator](#password-administrator-permissions)

Benutzer mit dieser Rolle haben eingeschränkte Möglichkeiten zum Verwalten von Kennwörtern. Mit dieser Rolle werden keine Berechtigungen zum Verwalten von Dienstanforderungen oder zum Überwachen der Dienstintegrität gewährt. Kennwortadministratoren können Kennwörter anderer Benutzer zurücksetzen, die nicht als Administratoren fungieren oder Mitglieder der folgenden Rollen sind:

* Rolle „Verzeichnis lesen“
* Gasteinladender
* Kennwortadministrator

### <a name="power-bi-administrator"></a>[Power BI-Administrator](#power-bi-service-administrator-permissions)

Benutzer mit dieser Rolle besitzen globale Berechtigungen innerhalb von Microsoft Power BI, wenn der Dienst verfügbar ist, und können Supporttickets verwalten und die Dienstintegrität überwachen. Weitere Informationen finden Sie unter [Grundlegendes zur Power BI-Administratorrolle](https://docs.microsoft.com/power-bi/service-admin-role).

> [!NOTE]
> In Microsoft Graph-API und Azure AD PowerShell wird diese Rolle als „Power BI-Dienstadministrator“ bezeichnet. Im [Azure-Portal](https://portal.azure.com) lautet sie „Power BI-Administrator“.

### <a name="power-platform-administrator"></a>[Power Platform-Administrator](#power-platform-administrator-permissions)

Benutzer in dieser Rolle können alle Aspekte von Umgebungen, PowerApps, Flows und Richtlinien zur Verhinderung von Datenverlust erstellen und verwalten. Darüber hinaus verfügen Benutzer mit dieser Rolle über die Möglichkeit, Supporttickets zu verwalten und die Dienstintegrität zu überwachen.

### <a name="printer-administrator"></a>[Druckeradministrator](#printer-administrator-permissions)

Benutzer mit dieser Rolle können Drucker registrieren und alle Aspekte sämtlicher Druckerkonfigurationen in der Microsoft-Lösung für universelles Drucken verwalten, einschließlich der Connectoreinstellungen für universelles Drucken. Sie können in alle delegierten Druckberechtigungsanforderungen einwilligen. Druckeradministratoren haben außerdem Zugriff auf Druckberichte.

### <a name="printer-technician"></a>[Druckertechniker](#printer-technician-permissions)

Benutzer mit dieser Rolle können Drucker registrieren und den Druckerstatus in der Microsoft-Lösung für universelles Drucken verwalten. Sie können außerdem alle Connectorinformationen lesen. Zu den Hauptaufgaben, die ein Druckertechniker nicht ausführen kann, gehören das Festlegen von Benutzerberechtigungen für Drucker sowie das Freigeben von Druckern.

### <a name="privileged-authentication-administrator"></a>[Privilegierter Authentifizierungsadministrator](#privileged-authentication-administrator-permissions)

Benutzer mit dieser Rolle können Anmeldeinformationen ohne Kennwort für alle Benutzer (einschließlich globaler Administratoren) festlegen oder zurücksetzen und Kennwörter für alle Benutzer aktualisieren. Privilegierte Authentifizierungsadministratoren können eine erneute Registrierung von Benutzern anhand von vorhandenen Anmeldeinformationen ohne Kennwort (z. B. MFA oder FIDO) erzwingen und die Einstellung „Speichern der MFA auf dem Gerät“ widerrufen, sodass alle Benutzer beim nächsten Anmeldevorgang zur mehrstufigen Authentifizierung aufgefordert werden. Die Rolle [Authentifizierungsadministrator](#authentication-administrator) kann die erneute Registrierung und MFA nur für Nicht-Administratoren und Benutzer erzwingen, die den folgenden Azure AD-Rollen zugewiesen sind:

* Authentifizierungsadministrator
* Rolle „Verzeichnis lesen“
* Gasteinladender
* Nachrichtencenter-Leser
* Meldet Reader

### <a name="privileged-role-administrator"></a>[Administrator für privilegierte Rollen](#privileged-role-administrator-permissions)

Benutzer mit dieser Rolle können Rollenzuweisungen in Azure Active Directory und Azure AD Privileged Identity Management verwalten. Sie können Gruppen erstellen und verwalten, die Azure AD-Rollen zugewiesen werden können. Überdies ermöglicht diese Rolle Verwaltung aller Aspekte von Privileged Identity Management und administrativer Einheiten.

> [!IMPORTANT]
> Diese Rolle ermöglicht die Verwaltung von Zuweisungen für alle Azure AD-Rollen, einschließlich der globalen Administratorrolle. Diese Rolle umfasst keine anderen privilegierten Funktionen in Azure AD wie das Erstellen oder Aktualisieren von Benutzern. Benutzer, die dieser Rolle zugewiesen sind, können sich selbst oder anderen jedoch zusätzliche Berechtigungen gewähren, indem sie zusätzliche Rollen zuweisen.

### <a name="reports-reader"></a>[Berichtleseberechtigter](#reports-reader-permissions)

Benutzer mit dieser Rolle können Nutzungsberichtsdaten und das Berichtsdashboard im Microsoft 365 Admin Center sowie das Einführungskontextpaket in Power BI anzeigen. Darüber hinaus stellt die Rolle Zugriff auf Anmeldeberichte und -aktivitäten in Azure AD und von der Microsoft Graph-Berichterstellungs-API zurückgegebene Daten zur Verfügung. Ein Benutzer, dem die Rolle „Meldet Reader“ zugewiesen ist, kann nur auf relevante Nutzungs- und Anpassungsmetriken zugreifen. Sie verfügen nicht über Administratorrechte, um Einstellungen zu konfigurieren oder auf produktspezifische Verwaltungskonsolen wie das Exchange Admin Center zuzugreifen. Diese Rolle kann keine Supporttickets anzeigen, erstellen oder verwalten.

### <a name="search-administrator"></a>[Suchadministrator](#search-administrator-permissions)

Benutzer mit dieser Rolle haben Vollzugriff auf alle Microsoft Search-Verwaltungsfunktionen im Microsoft 365 Admin Center. Darüber hinaus können diese Benutzer das Nachrichtencenter anzeigen, die Dienstintegrität überwachen und Service Requests erstellen.

### <a name="search-editor"></a>[Such-Editor](#search-editor-permissions)

Benutzer mit dieser Rolle können Inhalte für Microsoft Search im Microsoft 365 Admin Center erstellen, verwalten und löschen. Hierzu gehören Inhalte wie Lesezeichen, Fragen und Antworten sowie Standorte.

### <a name="security-administrator"></a>[Sicherheitsadministrator](#security-administrator-permissions)

Benutzer mit dieser Rolle haben Berechtigungen zur Verwaltung sicherheitsrelevanter Funktionen in Microsoft 365 Security Center, Azure Active Directory Identity Protection, für Azure Active Directory-Authentifizierung, Azure Information Protection und Office 365 Security & Compliance Center. Weitere Informationen zu Office 365-Berechtigungen finden Sie unter [Berechtigungen im Office 365 Security & Compliance Center](https://support.office.com/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

Geben Sie in | Möglich
--- | ---
[Microsoft 365 Security Center](https://protection.office.com) | Überwachen von sicherheitsrelevanten Richtlinien in Microsoft 365-Diensten<br>Verwalten von Sicherheitsbedrohungen und Warnungen<br>Berichte anzeigen
Identity Protection Center | Alle Berechtigungen der Rolle „Sicherheitsleseberechtigter“<br>Darüber hinaus die Möglichkeit, alle Vorgänge im Identity Protection Center außer des Zurücksetzens von Kennwörtern auszuführen
[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) | Alle Berechtigungen der Rolle „Sicherheitsleseberechtigter“<br>**Kann keine** Azure AD-Rollenzuweisungen oder -Einstellungen verwalten
[Office 365 Security & Compliance Center](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d) | Verwalten von Sicherheitsrichtlinien<br>Anzeigen, Untersuchen und Reagieren auf Sicherheitsbedrohungen<br>Berichte anzeigen
Azure Advanced Threat Protection | Überwachen und Reagieren auf verdächtige Sicherheitsaktivitäten
Windows Defender ATP und EDR | Zuweisen von Rollen<br>Verwalten von Computergruppen<br>Konfigurieren der Endpunkt-Bedrohungserkennung und der automatisierten Korrektur<br>Anzeigen, Untersuchen und Reagieren auf Warnungen
[Intune](https://docs.microsoft.com/intune/role-based-access-control) | Anzeigen von Benutzern, Geräten, Registrierung, Konfiguration und Anwendungsinformationen<br>Kann keine Änderungen an Intune vornehmen
[Cloud App Security](https://docs.microsoft.com/cloud-app-security/manage-admins) | Hinzufügen von Administratoren, Richtlinien und Einstellungen, Hochladen von Protokollen und Ausführen von Governanceaktionen
[Azure Security Center](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles) | Kann Sicherheitsrichtlinien und -zustände anzeigen, Sicherheitsrichtlinien bearbeiten sowie Warnungen und Empfehlungen anzeigen und verwerfen.
[Office 365-Dienstintegrität](https://docs.microsoft.com/office365/enterprise/view-service-health) | Anzeigen der Integrität von Office 365-Diensten
[Smart Lockout](../authentication/howto-password-smart-lockout.md) | Hiermit werden der Schwellenwert und die Dauer für Sperren definiert, wenn fehlerhafte Anmeldeereignisse auftreten.
[Kennwortschutz](../authentication/concept-password-ban-bad.md) | Konfigurieren Sie die benutzerdefinierte Liste der gesperrten Kennwörter oder lokalen Kennwortschutz.

### <a name="security-operator"></a>[Sicherheitsoperator](#security-operator-permissions)

Benutzer mit dieser Rolle können Warnungen verwalten und besitzen globalen schreibgeschützten Zugriff auf sicherheitsbezogene Features. Dies schließt sämtliche Informationen in Microsoft 365 Security Center, Azure Active Directory, Identity Protection, Privileged Identity Management und Office 365 Security & Compliance Center ein. Weitere Informationen zu Office 365-Berechtigungen finden Sie unter [Berechtigungen im Office 365 Security & Compliance Center](https://docs.microsoft.com/office365/securitycompliance/permissions-in-the-security-and-compliance-center).

Geben Sie in | Möglich
--- | ---
[Microsoft 365 Security Center](https://protection.office.com) | Alle Berechtigungen der Rolle „Sicherheitsleseberechtigter“<br>Anzeigen und Untersuchen von sowie Reagieren auf Warnungen zu Sicherheitsbedrohungen
Identity Protection Center | Alle Berechtigungen der Rolle „Sicherheitsleseberechtigter“<br>Darüber hinaus die Möglichkeit, alle Vorgänge im Identity Protection Center außer des Zurücksetzens von Kennwörtern auszuführen
[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) | Alle Berechtigungen der Rolle „Sicherheitsleseberechtigter“
[Office 365 Security & Compliance Center](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d) | Alle Berechtigungen der Rolle „Sicherheitsleseberechtigter“<br>Anzeigen und Untersuchen von sowie Reagieren auf Sicherheitswarnungen
Windows Defender ATP und EDR | Alle Berechtigungen der Rolle „Sicherheitsleseberechtigter“<br>Anzeigen und Untersuchen von sowie Reagieren auf Sicherheitswarnungen
[Intune](https://docs.microsoft.com/intune/role-based-access-control) | Alle Berechtigungen der Rolle „Sicherheitsleseberechtigter“
[Cloud App Security](https://docs.microsoft.com/cloud-app-security/manage-admins) | Alle Berechtigungen der Rolle „Sicherheitsleseberechtigter“
[Office 365-Dienstintegrität](https://docs.microsoft.com/office365/enterprise/view-service-health) | Anzeigen der Integrität von Office 365-Diensten

### <a name="security-reader"></a>[Sicherheitsleseberechtigter](#security-reader-permissions)

Benutzer mit dieser Rolle besitzen globalen schreibgeschützten Zugriff auf sicherheitsbezogene Features, einschließlich alle Informationen in Microsoft 365 Security Center, Azure Active Directory, Identity Protection, und Privileged Identity Management, sowie die Möglichkeit zum Lesen von Azure Active Directory-Anmeldeberichten und Überwachungsprotokollen und für das Office 365 Security & Compliance Center. Weitere Informationen zu Office 365-Berechtigungen finden Sie unter [Berechtigungen im Office 365 Security & Compliance Center](https://support.office.com/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

Geben Sie in | Möglich
--- | ---
[Microsoft 365 Security Center](https://protection.office.com) | Anzeigen von sicherheitsrelevanten Richtlinien in Microsoft 365-Diensten<br>Anzeigen von Sicherheitsbedrohungen und Warnungen<br>Berichte anzeigen
Identity Protection Center | Lesen von allen Sicherheitsberichten und Einstellungsinformationen für die Sicherheitsfunktionen<br><ul><li>Antispam<li>Verschlüsselung<li>Verhindern von Datenverlusten<li>Antischadsoftware<li>Erweiterter Schutz vor Bedrohungen<li>Antiphishing<li>Nachrichtenflussregeln
[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) | Verfügt über schreibgeschützten Zugriff auf alle eingeblendeten Informationen in Azure AD Privileged Identity Management: Richtlinien und Berichte für Azure AD-Rollenzuweisungen und Sicherheitsüberprüfungen.<br>Kann sich **nicht** für Azure AD Privileged Identity Management registrieren oder Änderungen daran vornehmen. Im Privileged Identity Management-Portal oder über PowerShell können Personen mit dieser Rolle zusätzliche Rollen (z. B. „Globaler Administrator“ oder „Administrator für privilegierte Rollen“) aktivieren, wenn der Benutzer dafür geeignet ist.
[Office 365 Security & Compliance Center](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d) | Anzeigen von Sicherheitsrichtlinien<br>Anzeigen und Untersuchen von Sicherheitsbedrohungen<br>Berichte anzeigen
Windows Defender ATP und EDR | Anzeigen und Untersuchen von Warnungen. Wenn Sie in Windows Defender ATP die rollenbasierte Zugriffssteuerung aktivieren, verlieren Benutzer mit reinen Leseberechtigungen (wie die Rolle „Azure AD-Sicherheitsleseberechtigter“) den Zugriff, bis ihnen eine Windows Defender ATP-Rolle zugewiesen wird.
[Intune](https://docs.microsoft.com/intune/role-based-access-control) | Anzeigen von Benutzern, Geräten, Registrierung, Konfiguration und Anwendungsinformationen Kann keine Änderungen an Intune vornehmen
[Cloud App Security](https://docs.microsoft.com/cloud-app-security/manage-admins) | Verfügt über schreibgeschützten Zugriff und kann Warnungen verwalten
[Azure Security Center](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles) | Kann Empfehlungen und Warnungen sowie Sicherheitsrichtlinien und -zustände anzeigen, aber keine Änderungen vornehmen.
[Office 365-Dienstintegrität](https://docs.microsoft.com/office365/enterprise/view-service-health) | Anzeigen der Integrität von Office 365-Diensten

### <a name="service-support-administrator"></a>[Dienstsupportadministrator](#service-support-administrator-permissions)

Benutzer mit dieser Rolle können bei Microsoft Supportanfragen für Azure- und Office 365-Dienste öffnen sowie das Dienstdashboard und das Nachrichtencenter im [Azure-Portal](https://portal.azure.com) und im [Microsoft 365 Admin Center](https://admin.microsoft.com) anzeigen. Weitere Informationen finden Sie unter [Informationen zu Administratorrollen](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

> [!NOTE]
> Bisher wurde diese Rolle im [Azure-Portal](https://portal.azure.com) und [Microsoft 365 Admin Center](https://admin.microsoft.com) als „Dienstadministrator“ bezeichnet. Wir haben diese Rolle umbenannt in „Dienstsupportadministrator“, um sie der bereits in der Microsoft Graph-API, der Azure AD Graph-API und in Azure AD PowerShell vorhandenen Bezeichnung anzupassen.

### <a name="sharepoint-administrator"></a>[SharePoint-Administrator](#sharepoint-service-administrator-permissions)

Benutzer mit dieser Rolle besitzen globale Berechtigungen innerhalb von Microsoft SharePoint Online, wenn der Dienst verfügbar ist, und können alle Office 365-Gruppen erstellen und verwalten, Supporttickets verwalten und die Dienstintegrität überwachen. Weitere Informationen finden Sie unter [Informationen zu Administratorrollen](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

> [!NOTE]
> In Microsoft Graph-API und Azure AD PowerShell wird diese Rolle als „SharePoint-Dienstadministrator“ bezeichnet. Im [Azure-Portal](https://portal.azure.com) lautet sie „SharePoint-Administrator“.

> [!NOTE]
> Diese Rolle gewährt auch der Microsoft Graph-API bereichsbezogene Berechtigungen für Microsoft Intune, um die Verwaltung und Konfiguration von Richtlinien für SharePoint- und OneDrive-Ressourcen zu ermöglichen.

### <a name="skype-for-business--lync-administrator"></a>[Skype for Business-Administrator/Lync-Dienstadministrator](#lync-service-administrator-permissions)

Benutzer mit dieser Rolle besitzen globale Berechtigungen in Microsoft Skype for Business, wenn der Dienst vorhanden ist, sowie die Berechtigung zur Verwaltung von Skype-spezifischen Benutzerattributen in Azure Active Directory. Darüber hinaus bietet diese Rolle die Möglichkeit, Supporttickets zu verwalten und die Dienstintegrität zu überwachen, sowie auf Teams und Skype for Business Admin Center zuzugreifen. Das Konto muss auch für Teams lizenziert sein, andernfalls kann es keine PowerShell-Cmdlets von Teams ausführen. Weitere Informationen dazu finden Sie unter [Skype for Business Online-Administrator](https://support.office.com/article/about-the-skype-for-business-admin-role-aeb35bda-93fc-49b1-ac2c-c74fbeb737b5) und Informationen zur Teams-Lizenzierung unter [Add-On-Lizenzierung für Skype for Business und Microsoft Teams](https://docs.microsoft.com/skypeforbusiness/skype-for-business-and-microsoft-teams-add-on-licensing/skype-for-business-and-microsoft-teams-add-on-licensing).

> [!NOTE]
> In Microsoft Graph-API und Azure AD PowerShell wird diese Rolle als „Lync-Dienstadministrator“ bezeichnet. Im [Azure-Portal](https://portal.azure.com/) lautet sie „Skype for Business-Administrator“.

### <a name="teams-communications-administrator"></a>[Teams-Kommunikationsadministrator](#teams-communications-administrator-permissions)

Benutzer mit dieser Rolle können Aspekte der Microsoft Teams-Workload im Zusammenhang mit Sprache und Telefonie verwalten. Dazu gehören die Verwaltungstools für die Telefonnummernzuweisung, Sprach- und Besprechungsrichtlinien und der uneingeschränkte Zugriff auf das Toolset zur Anrufanalyse.

### <a name="teams-communications-support-engineer"></a>[Supporttechniker für die Teams-Kommunikation](#teams-communications-support-engineer-permissions)

Benutzer in dieser Rolle können Kommunikationsprobleme innerhalb von Microsoft Teams und Skype for Business mithilfe der Problembehandlungstools für Benutzeranrufe im Admin Center für Microsoft Teams und Skype for Business behandeln. Benutzer in dieser Rolle können vollständige Anrufdatensatzinformationen für alle Teilnehmer anzeigen. Diese Rolle kann keine Supporttickets anzeigen, erstellen oder verwalten.

### <a name="teams-communications-support-specialist"></a>[Supportfachmann für die Teams-Kommunikation](#teams-communications-support-specialist-permissions)

Benutzer in dieser Rolle können Kommunikationsprobleme innerhalb von Microsoft Teams und Skype for Business mithilfe der Problembehandlungstools für Benutzeranrufe im Admin Center für Microsoft Teams und Skype for Business behandeln. Benutzer in dieser Rolle können Benutzerdetails im Anruf nur für den bestimmten Benutzer anzeigen, nach dem sie gesucht haben. Diese Rolle kann keine Supporttickets anzeigen, erstellen oder verwalten.

### <a name="teams-service-administrator"></a>[Teams-Dienstadministrator](#teams-service-administrator-permissions)

Benutzer mit dieser Rolle können alle Aspekte der Microsoft Teams-Workload über das Admin Center von Microsoft Teams und Skype for Business und die entsprechenden PowerShell-Module verwalten. Dazu zählen unter anderem alle Verwaltungstools im Zusammenhang mit Telefonie, Messaging, Besprechungen und den Teams selbst. Außerdem bietet diese Rolle die Möglichkeit, alle Office 365-Gruppen zu erstellen und zu verwalten, Supporttickets zu verwalten und die Dienstintegrität zu überwachen.

### <a name="user-administrator"></a>[Benutzeradministrator](#user-administrator-permissions)

Benutzer mit dieser Rolle können Benutzer erstellen und alle Aspekte von Benutzern verwalten (mit einigen Einschränkungen, siehe Tabelle). Außerdem können sie Richtlinien für den Kennwortablauf aktualisieren. Außerdem können Benutzer mit dieser Rolle Gruppen erstellen und verwalten. Zudem haben sie die Möglichkeit, Benutzeransichten und Supporttickets zu verwalten sowie die Dienstintegrität zu überwachen. Benutzeradministratoren haben keine Berechtigungen zum Verwalten bestimmter Benutzereigenschaften für Benutzer in den meisten Administratorrollen. Benutzer mit dieser Rolle verfügen nicht über Berechtigungen zum Verwalten von MFA. Die Rollen, die von dieser Einschränkung ausgenommen sind, sind in der folgenden Tabelle aufgeführt.

| **Berechtigung** | **Möglich** |
| --- | --- |
|Allgemeine Berechtigungen|<p>Erstellen von Benutzern und Gruppen</p><p>Erstellen und Verwalten von Benutzeransichten</p><p>Verwalten von Office-Supporttickets<p>Aktualisieren von Richtlinien für den Kennwortablauf|
| <p>Für alle Benutzer einschließlich aller Administratoren</p>|<p>Verwalten von Lizenzen</p><p>Verwalten aller Benutzereigenschaften mit Ausnahme des Benutzerprinzipalnamens</p>
| Nur für Benutzer, die keine Administratoren sind und keine der folgenden eingeschränkten Administratorrollen haben:<ul><li>Rolle „Verzeichnis lesen“<li>Gruppenadministrator<li>Gasteinladender<li>Helpdeskadministrator<li>Nachrichtencenter-Leser<li>Kennwortadministrator<li>Meldet Reader<li>Benutzeradministrator|<p>Löschen und Wiederherstellen</p><p>Deaktivieren und Aktivieren</p><p>Annullieren von Aktualisierungstoken</p><p>Verwalten aller Benutzereigenschaften einschließlich des Benutzerprinzipalnamens</p><p>Kennwort zurücksetzen</p><p>Aktualisieren von Geräteschlüsseln (FIDO)</p>|

> [!IMPORTANT]
> Benutzer mit dieser Rolle können Kennwörter für Benutzer ändern, die Zugriff auf vertrauliche oder private Informationen bzw. kritische Konfigurationen innerhalb und außerhalb von Azure Active Directory haben. Benutzer, die Kennwörter ändern können, können ggf. auch die Identität und die Berechtigungen des betreffenden Benutzers annehmen. Beispiel:
>
>- Besitzer von Anwendungsregistrierungen und Unternehmensanwendungen, die Anmeldeinformationen von Apps verwalten können, die sie besitzen. Diese Apps können über höhere Berechtigungen in Azure AD und in anderen Diensten verfügen, die Benutzeradministratoren nicht gewährt werden. So kann ein Benutzeradministrator die Identität eines Anwendungsbesitzers annehmen und dann die Identität einer privilegierten Anwendung durch Aktualisieren der Anmeldeinformationen für die Anwendung annehmen.
>- Besitzer von Azure-Abonnements, die ggf. auf vertrauliche oder private Informationen bzw. kritische Konfigurationen in Azure zugreifen können.
>- Besitzer von Sicherheitsgruppen und Office 365-Gruppen, die die Gruppenmitgliedschaft verwalten können. Diese Gruppen können Zugriff auf vertrauliche oder private Informationen bzw. kritische Konfigurationen in Azure AD und in anderen Diensten gewähren.
>- Administratoren in anderen Diensten außerhalb von Azure AD wie Exchange Online, Office Security and Compliance Center und Personalwesen.
>- Nichtadministratoren wie Führungskräfte, Rechtsberater und Mitarbeiter der Personalabteilung mit Zugriff auf vertrauliche oder private Informationen.

## <a name="role-permissions"></a>Rollenberechtigungen

In den folgenden Tabellen werden die spezifischen Berechtigungen der einzelnen Rollen in Azure Active Directory beschrieben. Einige Rollen können zusätzliche Berechtigungen in Microsoft-Diensten außerhalb von Azure Active Directory aufweisen.

### <a name="application-administrator-permissions"></a>Berechtigungen von Anwendungsadministratoren

Kann alle Aspekte von App-Registrierungen und Enterprise-Apps erstellen und verwalten.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/Application/appProxyAuthentication/update | Aktualisieren der App-Proxy-Authentifizierungseigenschaften für Dienstprinzipale in Azure Active Directory |
| microsoft.directory/Application/appProxyUrlSettings/update | Aktualisieren der internen und externen URLs von Anwendungsproxys in Azure Active Directory |
| microsoft.directory/applications/applicationProxy/read | Lesen aller App-Proxy-Eigenschaften |
| microsoft.directory/applications/applicationProxy/update | Aktualisieren aller App-Proxy-Eigenschaften |
| microsoft.directory/applications/audience/update | Aktualisieren der applications.audience-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/authentication/update | Aktualisieren der applications.authentication-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/basic/update | Aktualisieren der Basiseigenschaften für Anwendungen in Azure Active Directory |
| microsoft.directory/applications/create | Erstellen von Anwendungen in Azure Active Directory |
| microsoft.directory/applications/credentials/update | Aktualisieren der applications.credentials-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/delete | Löschen von Anwendungen in Azure Active Directory |
| microsoft.directory/applications/owners/update | Aktualisieren der applications.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/permissions/update | Aktualisieren der applications.permissions-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/policies/update | Aktualisieren der applications.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/appRoleAssignments/create | Erstellen von appRoleAssignments in Azure Active Directory |
| microsoft.directory/appRoleAssignments/read | Lesen von appRoleAssignments in Azure Active Directory |
| microsoft.directory/appRoleAssignments/update | Aktualisieren von appRoleAssignments in Azure Active Directory |
| microsoft.directory/appRoleAssignments/delete | Löschen von appRoleAssignments in Azure Active Directory |
| microsoft.directory/auditLogs/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Überwachungsprotokolle (auditLogs) in Azure Active Directory |
| microsoft.directory/connectorGroups/allProperties/read | Lesen der Eigenschaften von Anwendungsproxy-Connectorgruppen in Azure Active Directory |
| microsoft.directory/connectorGroups/allProperties/update | Aktualisieren aller Eigenschaften von Anwendungsproxy-Connectorgruppen in Azure Active Directory |
| microsoft.directory/connectorGroups/create | Erstellen von Anwendungsproxy-Connectorgruppen in Azure Active Directory |
| microsoft.directory/connectorGroups/delete | Löschen von Anwendungsproxy-Connectorgruppen in Azure Active Directory |
| microsoft.directory/connectors/allProperties/read | Lesen aller Eigenschaften von Anwendungsproxyconnectors in Azure Active Directory |
| microsoft.directory/connectors/create | Erstellen von Anwendungsproxyconnectors in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/basic/read | Lesen der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/basic/update | Aktualisieren der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/create | Erstellen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/delete | Löschen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/owners/read | Lesen der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/owners/update | Aktualisieren der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/policyAppliedTo/read | Lesen der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignedTo/update | Aktualisieren der servicePrincipals.appRoleAssignedTo-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignments/update | Aktualisieren der servicePrincipals.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/audience/update | Aktualisieren der servicePrincipals.audience-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/authentication/update | Aktualisieren der servicePrincipals.authentication-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/basic/update | Aktualisieren der Basiseigenschaften für servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/create | Erstellen von servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/credentials/update | Aktualisieren der servicePrincipals.credentials-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/delete | Löschen von servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/owners/update | Aktualisieren der servicePrincipals.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/permissions/update | Aktualisieren der servicePrincipals.permissions-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/policies/update | Aktualisieren der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="application-developer-permissions"></a>Berechtigungen von Anwendungsentwicklern

Erstellen von Anwendungsregistrierungen unabhängig von der Einstellung „Benutzer können Anwendungen registrieren“.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/applications/createAsOwner | Erstellen von Anwendungen in Azure Active Directory Der Ersteller wird als erster Besitzer hinzugefügt, und das erstellte Objekt wird auf das Kontingent von 250 erstellten Objekten angerechnet, das für den Ersteller gilt. |
| microsoft.directory/appRoleAssignments/createAsOwner | Erstellen von appRoleAssignments in Azure Active Directory Der Ersteller wird als erster Besitzer hinzugefügt, und das erstellte Objekt wird auf das Kontingent von 250 erstellten Objekten angerechnet, das für den Ersteller gilt. |
| microsoft.directory/oAuth2PermissionGrants/createAsOwner | Erstellen von oAuth2PermissionGrants in Azure Active Directory Der Ersteller wird als erster Besitzer hinzugefügt, und das erstellte Objekt wird auf das Kontingent von 250 erstellten Objekten angerechnet, das für den Ersteller gilt. |
| microsoft.directory/servicePrincipals/createAsOwner | Erstellen von servicePrincipals in Azure Active Directory Der Ersteller wird als erster Besitzer hinzugefügt, und das erstellte Objekt wird auf das Kontingent von 250 erstellten Objekten angerechnet, das für den Ersteller gilt. |

### <a name="authentication-administrator-permissions"></a>Berechtigungen von Authentifizierungsadministratoren

Ist berechtigt, Informationen zur Authentifizierungsmethode für alle Benutzer ohne Administratorrechte anzuzeigen, festzulegen und zurückzusetzen.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/users/invalidateAllRefreshTokens | Kennzeichnen sämtlicher Aktualisierungstoken für Benutzer in Azure Active Directory als ungültig. |
| microsoft.directory/users/strongAuthentication/update | Aktualisieren der Eigenschaften der strengen Authentifizierung (z. B. MFA-Anmeldeinformationen). |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.directory/users/password/update | Aktualisieren von Kennwörtern für alle Benutzer in der Office 365-Organisation. Weitere Informationen finden Sie in der Onlinedokumentation. |

### <a name="azure-devops-administrator-permissions"></a>Berechtigungen von Azure DevOps-Administratoren

Kann Richtlinien und Einstellungen für die Azure DevOps-Organisation verwalten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der [Rollenbeschreibung](#azure-devops-administrator) weiter oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.devOps/allEntities/allTasks | Lesen und Konfigurieren von Azure DevOps |

### <a name="azure-information-protection-administrator-permissions"></a>Berechtigungen von Azure Information Protection-Administratoren

Verwalten sämtlicher Aspekte des Azure Information Protection-Diensts.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der [Rollenbeschreibung](#) weiter oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.informationProtection/allEntities/allTasks | Verwalten sämtlicher Aspekte von Azure Information Protection |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="b2c-ief-keyset-administrator-permissions"></a>Berechtigungen von B2C-IEF-Schlüsselsatzadministratoren

Verwalten von Geheimnissen für Verbund und Verschlüsselung im Identity Experience Framework

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.aad.b2c/trustFramework/keySets/allTasks | Lesen und Konfigurieren von Schlüsselsätzen in Azure Active Directory B2C |

### <a name="b2c-ief-policy-administrator-permissions"></a>Berechtigungen von B2C-IEF-Richtlinienadministratoren

Erstellen und Verwalten von Vertrauensframework-Richtlinien im Identity Experience Framework

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.aad.b2c/trustFramework/policies/allTasks | Lesen und Konfigurieren benutzerdefinierter Richtlinien in Azure Active Directory B2C |

### <a name="billing-administrator-permissions"></a>Berechtigungen von Abrechnungsadministratoren

Ausführen von allgemeinen Abrechnungsaufgaben wie der Aktualisierung der Zahlungsinformationen.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/organization/basic/update | Aktualisieren der Basiseigenschaften für die Organisation in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.commerce.billing/allEntities/allTasks | Verwalten sämtlicher Aspekte der Abrechnung. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="cloud-application-administrator-permissions"></a>Berechtigungen von Cloudanwendungsadministratoren

Erstellen und Verwalten sämtlicher Aspekte von App-Registrierungen und Enterprise-Apps außer App-Proxy.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/applications/audience/update | Aktualisieren der applications.audience-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/authentication/update | Aktualisieren der applications.authentication-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/basic/update | Aktualisieren der Basiseigenschaften für Anwendungen in Azure Active Directory |
| microsoft.directory/applications/create | Erstellen von Anwendungen in Azure Active Directory |
| microsoft.directory/applications/credentials/update | Aktualisieren der applications.credentials-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/delete | Löschen von Anwendungen in Azure Active Directory |
| microsoft.directory/applications/owners/update | Aktualisieren der applications.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/permissions/update | Aktualisieren der applications.permissions-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/policies/update | Aktualisieren der applications.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/appRoleAssignments/create | Erstellen von appRoleAssignments in Azure Active Directory |
| microsoft.directory/appRoleAssignments/update | Aktualisieren von appRoleAssignments in Azure Active Directory |
| microsoft.directory/appRoleAssignments/delete | Löschen von appRoleAssignments in Azure Active Directory |
| microsoft.directory/auditLogs/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Überwachungsprotokolle (auditLogs) in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/create | Erstellen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/basic/read | Lesen der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/basic/update | Aktualisieren der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/delete | Löschen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/owners/read | Lesen der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/owners/update | Aktualisieren der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/applicationConfiguration/policyAppliedTo/read | Lesen der policies.applicationConfiguration-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignedTo/update | Aktualisieren der servicePrincipals.appRoleAssignedTo-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignments/update | Aktualisieren der servicePrincipals.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/audience/update | Aktualisieren der servicePrincipals.audience-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/authentication/update | Aktualisieren der servicePrincipals.authentication-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/basic/update | Aktualisieren der Basiseigenschaften für servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/create | Erstellen von servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/credentials/update | Aktualisieren der servicePrincipals.credentials-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/delete | Löschen von servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/owners/update | Aktualisieren der servicePrincipals.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/permissions/update | Aktualisieren der servicePrincipals.permissions-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/policies/update | Aktualisieren der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="cloud-device-administrator-permissions"></a>Berechtigungen von Cloudgeräteadministratoren

Vollzugriff zum Verwalten von Geräten in Azure AD.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/auditLogs/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Überwachungsprotokolle (auditLogs) in Azure Active Directory |
| microsoft.directory/devices/bitLockerRecoveryKeys/read | Lesen der devices.bitLockerRecoveryKeys-Eigenschaft in Azure Active Directory |
| microsoft.directory/devices/delete | Löschen von Geräten in Azure Active Directory |
| microsoft.directory/devices/disable | Deaktivieren von Geräten in Azure Active Directory |
| microsoft.directory/devices/enable | Aktivieren von Geräten in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |

### <a name="company-administrator-permissions"></a>Berechtigungen von Unternehmensadministratoren

Verwalten sämtlicher Aspekte von Azure AD und Microsoft-Diensten, die Azure AD-Identitäten verwenden. Diese Rolle wird auch als „Globaler Administrator“ bezeichnet. 

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.aad.cloudAppSecurity/allEntities/allTasks | Erstellen und Löschen aller Ressourcen sowie Lesen und Aktualisieren von Standardeigenschaften in microsoft.aad.cloudAppSecurity |
| microsoft.directory/administrativeUnits/allProperties/allTasks | Erstellen und Löschen von administrativeUnits und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/applications/allProperties/allTasks | Erstellen und Löschen von Anwendungen und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/appRoleAssignments/allProperties/allTasks | Erstellen und Löschen von appRoleAssignments und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/auditLogs/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Überwachungsprotokolle (auditLogs) in Azure Active Directory |
| microsoft.directory/contacts/allProperties/allTasks | Erstellen und Löschen von Kontakten und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/contracts/allProperties/allTasks | Erstellen und Löschen von Verträgen und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/devices/allProperties/allTasks | Erstellen und Löschen von Geräten und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/directoryRoles/allProperties/allTasks | Erstellen und Löschen von directoryRoles und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/directoryRoleTemplates/allProperties/allTasks | Erstellen und Löschen von directoryRoleTemplates und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/domains/allProperties/allTasks | Erstellen und Löschen von Domänen und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/groups/allProperties/allTasks | Erstellen und Löschen von Gruppen und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/groupsAssignableToRoles/allProperties/update | Aktualisieren von Gruppen, bei denen die isAssignableToRole-Eigenschaft in Azure Active Directory auf TRUE festgelegt ist |
| microsoft.directory/groupsAssignableToRoles/create | Erstellen von Gruppen, bei denen die isAssignableToRole-Eigenschaft in Azure Active Directory auf TRUE festgelegt ist |
| microsoft.directory/groupsAssignableToRoles/delete | Löschen von Gruppen, bei denen die isAssignableToRole-Eigenschaft in Azure Active Directory auf TRUE festgelegt ist |
| microsoft.directory/groupSettings/allProperties/allTasks | Erstellen und Löschen von groupSettings und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/groupSettingTemplates/allProperties/allTasks | Erstellen und Löschen von groupSettingTemplates und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/loginTenantBranding/allProperties/allTasks | Erstellen und Löschen von loginTenantBranding und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/oAuth2PermissionGrants/allProperties/allTasks | Erstellen und Löschen von oAuth2PermissionGrants und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/organization/allProperties/allTasks | Erstellen und Löschen der Organisationen und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/policies/allProperties/allTasks | Erstellen und Löschen von Richtlinien und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/roleAssignments/allProperties/allTasks | Erstellen und Löschen von roleAssignments und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/roleDefinitions/allProperties/allTasks | Erstellen und Löschen von roleDefinitions und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/scopedRoleMemberships/allProperties/allTasks | Erstellen und Löschen von scopedRoleMemberships und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/serviceAction/activateService | Ausführen der Dienstaktion Activateservice in Azure Active Directory |
| microsoft.directory/serviceAction/disableDirectoryFeature | Ausführen der Dienstaktion DisableDirectoryFeature in Azure Active Directory |
| microsoft.directory/serviceAction/enableDirectoryFeature | Ausführen der Dienstaktion Enabledirectoryfeature in Azure Active Directory |
| microsoft.directory/serviceAction/getAvailableExtentionProperties | Ausführen der Dienstaktion Getavailableextentionproperties in Azure Active Directory |
| microsoft.directory/servicePrincipals/allProperties/allTasks | Erstellen und Löschen von servicePrincipals und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |
| microsoft.directory/subscribedSkus/allProperties/allTasks | Erstellen und Löschen von subscribedSkus und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directory/users/allProperties/allTasks | Erstellen und Löschen von Benutzern und Lesen und Aktualisieren aller Eigenschaften in Azure Active Directory |
| microsoft.directorySync/allEntities/allTasks | Ausführen sämtlicher Aktionen in Azure AD Connect. |
| microsoft.aad.identityProtection/allEntities/allTasks | Erstellen und Löschen aller Ressourcen und Lesen und Aktualisieren von Standardeigenschaften in microsoft.identityProtection |
| microsoft.aad.privilegedIdentityManagement/allEntities/read | Lesen aller Ressourcen in microsoft.aad.privilegedIdentityManagement |
| microsoft.azure.advancedThreatProtection/allEntities/read | Lesen aller Ressourcen in microsoft.azure.advancedThreatProtection |
| microsoft.azure.informationProtection/allEntities/allTasks | Verwalten sämtlicher Aspekte von Azure Information Protection |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.commerce.billing/allEntities/allTasks | Verwalten sämtlicher Aspekte der Abrechnung. |
| microsoft.intune/allEntities/allTasks | Verwalten sämtlicher Aspekte von Intune. |
| microsoft.office365.complianceManager/allEntities/allTasks | Verwalten sämtlicher Aspekte von Office 365 Compliance-Manager |
| microsoft.office365.desktopAnalytics/allEntities/allTasks | Verwalten aller Aspekte von Desktop Analytics. |
| microsoft.office365.exchange/allEntities/allTasks | Verwalten sämtlicher Aspekte von Exchange Online. |
| microsoft.office365.lockbox/allEntities/allTasks | Verwalten sämtlicher Aspekte der Office 365 Kunden-Lockbox |
| microsoft.office365.messageCenter/messages/read | Lesen von Nachrichten in microsoft.office365.messageCenter |
| microsoft.office365.messageCenter/securityMessages/read | Lesen von securityMessages in microsoft.office365.messageCenter |
| microsoft.office365.protectionCenter/allEntities/allTasks | Verwalten sämtlicher Aspekte von Office 365 Protection Center |
| microsoft.office365.securityComplianceCenter/allEntities/allTasks | Erstellen und Löschen aller Ressourcen sowie Lesen und Aktualisieren von Standardeigenschaften in microsoft.office365.securityComplianceCenter |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.sharepoint/allEntities/allTasks | Erstellen und Löschen aller Ressourcen und Lesen und Aktualisieren von Standardeigenschaften in microsoft.office365.sharepoint |
| microsoft.office365.skypeForBusiness/allEntities/allTasks | Verwalten sämtlicher Aspekte von Skype for Business Online |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.usageReports/allEntities/read | Lesen von Office 365-Nutzungsberichten. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.powerApps.dynamics365/allEntities/allTasks | Verwalten sämtlicher Aspekte von Dynamics 365. |
| microsoft.powerApps.powerBI/allEntities/allTasks | Verwalten sämtlicher Aspekte von Power BI. |
| microsoft.windows.defenderAdvancedThreatProtection/allEntities/read | Lesen aller Ressourcen in microsoft.windows.defenderAdvancedThreatProtection |

### <a name="compliance-administrator-permissions"></a>Berechtigungen von Complianceadministratoren

Lesen und Verwalten der Konformitätskonfiguration und der zugehörigen Berichte in Azure AD und Office 365.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.complianceManager/allEntities/allTasks | Verwalten sämtlicher Aspekte von Office 365 Compliance-Manager |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="compliance-data-administrator-permissions"></a>Berechtigungen von Compliancedatenadministratoren

Erstellt und verwaltet Complianceinhalte.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory.cloudAppSecurity/allEntities/allTasks | Lesen und Konfigurieren von Microsoft Cloud App Security-Daten. |
| microsoft.azure.informationProtection/allEntities/allTasks | Verwalten sämtlicher Aspekte von Azure Information Protection |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.complianceManager/allEntities/allTasks | Verwalten sämtlicher Aspekte von Office 365 Compliance-Manager |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="conditional-access-administrator-permissions"></a>Berechtigungen von Administratoren für bedingten Zugriff

Verwalten von Funktionen zum bedingten Zugriff.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/policies/conditionalAccess/basic/read | Lesen der policies.conditionalAccess-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/conditionalAccess/basic/update | Aktualisieren der policies.conditionalAccess-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/conditionalAccess/create | Erstellen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/conditionalAccess/delete | Löschen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/conditionalAccess/owners/read | Lesen der policies.conditionalAccess-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/conditionalAccess/owners/update | Aktualisieren der policies.conditionalAccess-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/conditionalAccess/policiesAppliedTo/read | Lesen der policies.conditionalAccess-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/conditionalAccess/tenantDefault/update | Aktualisieren der policies.conditionalAccess-Eigenschaft in Azure Active Directory |

### <a name="crm-service-administrator-permissions"></a>Berechtigungen von CRM-Dienstadministratoren

Verwalten sämtlicher Aspekte des Produkts Dynamics 365.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.powerApps.dynamics365/allEntities/allTasks | Verwalten sämtlicher Aspekte von Dynamics 365. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="customer-lockbox-access-approver-permissions"></a>Berechtigungen von genehmigenden Personen für den Kunden-Lockbox-Zugriff

Kann Microsoft-Supportanfragen zum Zugriff auf Benutzerorganisationsdaten genehmigen.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.lockbox/allEntities/allTasks | Verwalten sämtlicher Aspekte der Office 365 Kunden-Lockbox |

### <a name="desktop-analytics-administrator-permissions"></a>Berechtigungen von Desktop Analytics-Administratoren

Kann Desktop Analytics und die Dienste für Office-Anpassung und -Richtlinien verwalten. Bei Desktop Analytics umfasst dies die Möglichkeit, den Assetbestand anzuzeigen, Bereitstellungspläne zu erstellen sowie die Bereitstellung und den Integritätsstatus zu anzuzeigen. Beim Dienst für Office-Anpassung und -Richtlinien ermöglicht diese Rolle den Benutzern die Verwaltung von Office-Richtlinien.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.desktopAnalytics/allEntities/allTasks | Verwalten aller Aspekte von Desktop Analytics. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="device-administrators-permissions"></a>Berechtigungen von Geräteadministratoren

Benutzer, die dieser Rolle zugewiesen wurden, werden der lokalen Administratorgruppe auf in Azure AD eingebundenen Geräten hinzugefügt.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/groupSettings/basic/read | Lesen der Basiseigenschaften für groupSettings in Azure Active Directory |
| microsoft.directory/groupSettingTemplates/basic/read | Lesen der Basiseigenschaften für groupSettingTemplates in Azure Active Directory |

### <a name="directory-readers-permissions"></a>Berechtigungen von Verzeichnisleseberechtigten
Lesen von grundlegenden Verzeichnisinformationen. Die Rolle gewährt Zugriff auf Anwendungen und ist nicht für Benutzer vorgesehen.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/administrativeUnits/basic/read | Lesen der Basiseigenschaften für administrativeUnits in Azure Active Directory |
| microsoft.directory/administrativeUnits/members/read | Lesen der administrativeUnits.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/basic/read | Lesen der Basiseigenschaften für Anwendungen in Azure Active Directory |
| microsoft.directory/applications/owners/read | Lesen der applications.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/policies/read | Lesen der applications.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/contacts/basic/read | Lesen der Basiseigenschaften für Kontakte in Azure Active Directory |
| microsoft.directory/contacts/memberOf/read | Lesen der contacts.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/contracts/basic/read | Lesen der Basiseigenschaften für Verträge in Azure Active Directory |
| microsoft.directory/devices/basic/read | Lesen der Basiseigenschaften für Geräte in Azure Active Directory |
| microsoft.directory/devices/memberOf/read | Lesen der devices.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/devices/registeredOwners/read | Lesen der devices.registeredOwners-Eigenschaft in Azure Active Directory |
| microsoft.directory/devices/registeredUsers/read | Lesen der devices.registeredUsers-Eigenschaft in Azure Active Directory |
| microsoft.directory/directoryRoles/basic/read | Lesen der Basiseigenschaften für directoryRoles in Azure Active Directory |
| microsoft.directory/directoryRoles/eligibleMembers/read | Lesen der directoryRoles.eligibleMembers-Eigenschaft in Azure Active Directory |
| microsoft.directory/directoryRoles/members/read | Lesen der directoryRoles.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/domains/basic/read | Lesen der Basiseigenschaften für Domänen in Azure Active Directory |
| microsoft.directory/groups/appRoleAssignments/read | Lesen der groups.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/basic/read | Lesen der Basiseigenschaften für Gruppen in Azure Active Directory |
| microsoft.directory/groups/memberOf/read | Lesen der groups.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/members/read | Lesen der groups.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/owners/read | Lesen der groups.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/settings/read | Lesen der groups.settings-Eigenschaft in Azure Active Directory |
| microsoft.directory/groupSettings/basic/read | Lesen der Basiseigenschaften für groupSettings in Azure Active Directory |
| microsoft.directory/groupSettingTemplates/basic/read | Lesen der Basiseigenschaften für groupSettingTemplates in Azure Active Directory |
| microsoft.directory/oAuth2PermissionGrants/basic/read | Lesen der Basiseigenschaften für oAuth2PermissionGrants in Azure Active Directory |
| microsoft.directory/organization/basic/read | Lesen der Basiseigenschaften für die Organisation in Azure Active Directory |
| microsoft.directory/organization/trustedCAsForPasswordlessAuth/read | Lesen der organizations.trustedCAsForPasswordlessAuth-Eigenschaft in Azure Active Directory |
| microsoft.directory/roleAssignments/basic/read | Lesen der Basiseigenschaften für roleAssignments in Azure Active Directory |
| microsoft.directory/roleDefinitions/basic/read | Lesen der Basiseigenschaften für roleDefinitions in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignedTo/read | Lesen der servicePrincipals.appRoleAssignedTo-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignments/read | Lesen der servicePrincipals.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/basic/read | Lesen der Basiseigenschaften für servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/memberOf/read | Lesen der servicePrincipals.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/oAuth2PermissionGrants/basic/read | Lesen der servicePrincipals.oAuth2PermissionGrants-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/ownedObjects/read | Lesen der servicePrincipals.ownedObjects-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/owners/read | Lesen der servicePrincipals.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/policies/read | Lesen der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/subscribedSkus/basic/read | Lesen der Basiseigenschaften für subscribedSkus in Azure Active Directory |
| microsoft.directory/users/appRoleAssignments/read | Lesen der users.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/basic/read | Lesen der Basiseigenschaften für Benutzer in Azure Active Directory |
| microsoft.directory/users/directReports/read | Lesen der users.directReports-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/manager/read | Lesen der users.manager-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/memberOf/read | Lesen der users.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/oAuth2PermissionGrants/basic/read | Lesen der users.oAuth2PermissionGrants-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/ownedDevices/read | Lesen der users.ownedDevices-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/ownedObjects/read | Lesen der users.ownedObjects-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/registeredDevices/read | Lesen der users.registeredDevices-Eigenschaft in Azure Active Directory |

### <a name="directory-synchronization-accounts-permissions"></a>Berechtigungen von Verzeichnissynchronisierungskonten

Nur vom Azure AD Connect-Dienst verwendet.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/organization/dirSync/update | Aktualisieren der organization.dirSync-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/create | Erstellen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/delete | Löschen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/basic/read | Lesen der Basiseigenschaften für Richtlinien in Azure Active Directory |
| microsoft.directory/policies/basic/update | Aktualisieren der Basiseigenschaften für Richtlinien in Azure Active Directory |
| microsoft.directory/policies/owners/read | Lesen der policies.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/owners/update | Aktualisieren der policies.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/policiesAppliedTo/read | Lesen der policies.policiesAppliedTo-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/tenantDefault/update | Aktualisieren der policies.tenantDefault-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignedTo/read | Lesen der servicePrincipals.appRoleAssignedTo-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignedTo/update | Aktualisieren der servicePrincipals.appRoleAssignedTo-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignments/read | Lesen der servicePrincipals.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignments/update | Aktualisieren der servicePrincipals.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/audience/update | Aktualisieren der servicePrincipals.audience-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/authentication/update | Aktualisieren der servicePrincipals.authentication-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/basic/read | Lesen der Basiseigenschaften für servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/basic/update | Aktualisieren der Basiseigenschaften für servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/create | Erstellen von servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/credentials/update | Aktualisieren der servicePrincipals.credentials-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/memberOf/read | Lesen der servicePrincipals.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/oAuth2PermissionGrants/basic/read | Lesen der servicePrincipals.oAuth2PermissionGrants-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/owners/read | Lesen der servicePrincipals.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/owners/update | Aktualisieren der servicePrincipals.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/ownedObjects/read | Lesen der servicePrincipals.ownedObjects-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/permissions/update | Aktualisieren der servicePrincipals.permissions-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/policies/read | Lesen der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/policies/update | Aktualisieren der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directorySync/allEntities/allTasks | Ausführen sämtlicher Aktionen in Azure AD Connect. |

### <a name="directory-writers-permissions"></a>Berechtigungen von Verzeichnisschreibberechtigten

Lesen und Schreiben von grundlegenden Verzeichnisinformationen. Die Rolle gewährt Zugriff auf Anwendungen und ist nicht für Benutzer vorgesehen.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/groups/appRoleAssignments/update | Aktualisieren der groups.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/assignLicense | Verwalten von Lizenzen für Gruppen in Azure Active Directory |
| microsoft.directory/groups/basic/update | Aktualisieren der Basiseigenschaften für Gruppen in Azure Active Directory  |
| microsoft.directory/groups/classification/update | Aktualisieren der classification-Eigenschaft der Gruppe in Azure Active Directory |
| microsoft.directory/groups/create | Erstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/groupType/update | Aktualisieren der groupType-Eigenschaft einer Gruppe in Azure Active Directory |
| microsoft.directory/groups/members/update | Aktualisieren der groups.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/owners/update | Aktualisieren der groups.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/reprocessLicenseAssignment | Erneutes Verarbeiten der Lizenzzuweisungen für eine Gruppe in Azure Active Directory |
| microsoft.directory/groups/securityEnabled/update | Aktualisieren der securityEnabled-Eigenschaft einer Gruppe in Azure Active Directory |
| microsoft.directory/groups/settings/update | Aktualisieren der groups.settings-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/visibility/update | Aktualisieren der visibility-Eigenschaft der Gruppe |
| microsoft.directory/groupSettings/basic/update | Aktualisieren der Basiseigenschaften für groupSettings in Azure Active Directory |
| microsoft.directory/groupSettings/create | Erstellen von groupSettings in Azure Active Directory |
| microsoft.directory/groupSettings/delete | Löschen von groupSettings in Azure Active Directory |
| microsoft.directory/oAuth2PermissionGrants/basic/update | Aktualisieren der Basiseigenschaften von oAuth2PermissionGrants in Azure Active Directory |
| microsoft.directory/oAuth2PermissionGrants/create | Erstellen von oAuth2PermissionGrants in Azure Active Directory |
| microsoft.directory/servicePrincipals/synchronizationCredentials/manage | Verwalten von Geheimnissen und Anmeldeinformationen für die Anwendungsbereitstellung |
| microsoft.directory/servicePrincipals/synchronizationJobs/manage | Starten, Neustarten und Anhalten von Synchronisierungsaufträgen für die Anwendungsbereitstellung |
| microsoft.directory/servicePrincipals/synchronizationSchema/manage | Erstellen und Verwalten von Synchronisierungsaufträgen und -schemas für die Anwendungsbereitstellung |
| microsoft.directory/users/appRoleAssignments/update | Aktualisieren der users.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/assignLicense | Verwalten der Lizenzen für Benutzer in Azure Active Directory |
| microsoft.directory/users/basic/update | Aktualisieren der Basiseigenschaften für Benutzer in Azure Active Directory |
| microsoft.directory/users/disable | Deaktivieren eines Benutzerkontos in Azure Active Directory |
| microsoft.directory/users/enable | Aktivieren eines Benutzerkontos in Azure Active Directory |
| microsoft.directory/users/invalidateAllRefreshTokens | Annullieren aller Benutzeraktualisierungstoken in Azure Active Directory, sodass sich die Benutzer bei ihrer nächsten Anmeldung erneut authentifizieren müssen |
| microsoft.directory/users/manager/update | Aktualisieren der users.manager-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/reprocessLicenseAssignment | Erneutes Verarbeiten der Lizenzzuweisungen für einen Benutzer in Azure Active Directory |
| microsoft.directory/users/userPrincipalName/update | Aktualisieren der users.userPrincipalName-Eigenschaft in Azure Active Directory |


### <a name="exchange-service-administrator-permissions"></a>Berechtigungen von Exchange-Dienstadministratoren

Verwalten sämtlicher Aspekte des Produkts Exchange.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.directory/groups/unified/appRoleAssignments/update | Aktualisieren der groups.unified-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/unified/basic/update | Aktualisieren der Basiseigenschaften von Office 365-Gruppen |
| microsoft.directory/groups/unified/create | Erstellen von Office 365-Gruppen |
| microsoft.directory/groups/unified/delete | Löschen von Office 365-Gruppen |
| microsoft.directory/groups/unified/members/update | Aktualisieren der Mitgliedschaft von Office 365-Gruppen |
| microsoft.directory/groups/unified/owners/update | Aktualisieren des Besitzers von Office 365-Gruppen |
| microsoft.office365.exchange/allEntities/allTasks | Verwalten sämtlicher Aspekte von Exchange Online. |
| microsoft.office365.network/performance/allProperties/read | Lesen von Seiten zur Netzwerkleistung in Admin Center von M365 |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.usageReports/allEntities/read | Lesen von Office 365-Nutzungsberichten. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="external-id-user-flow-administrator-permissions"></a>Berechtigungen von B2C-Benutzerflowadministratoren mit externer ID

Erstellen und Verwalten aller Aspekte von Benutzerflows

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.aad.b2c/userFlows/allTasks | Erstellen und Konfigurieren von Benutzerflows in Azure Active Directory B2C |

### <a name="external-id-user-flow-attribute-administrator-permissions"></a>Berechtigungen von Administratoren für Benutzerflowattribute mit externer ID

Erstellen und Verwalten des Attributschemas für alle Benutzerabläufe

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.aad.b2c/userAttributes/allTasks | Lesen und Konfigurieren von Benutzerattributen in Azure Active Directory B2C |

### <a name="external-identity-provider-administrator-permissions"></a>Berechtigungen von externen Identitätsanbieteradministratoren

Konfigurieren von Identitätsanbietern für die Verwendung in einem direkten Verbund

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.aad.b2c/identityProviders/allTasks | Lesen und Konfigurieren von Identitätsanbietern in Azure Active Directory B2C |

### <a name="global-reader-permissions"></a>Berechtigungen von Benutzern mit der Rolle „Globaler Leser“
Benutzer mit dieser Rolle können alles lesen, was ein globaler Administrator lesen kann, aber nichts bearbeiten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der [Rollenbeschreibung](#global-reader) weiter oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.commerce.billing/allEntities/read    | Lesen sämtlicher Aspekte der Abrechnung. |
| microsoft.directory/administrativeUnits/basic/read    | Lesen der Basiseigenschaften für administrativeUnits in Azure Active Directory |
| microsoft.directory/administrativeUnits/members/read    | Lesen der administrativeUnits.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/basic/read    | Lesen der Basiseigenschaften für Anwendungen in Azure Active Directory |
| microsoft.directory/applications/owners/read    | Lesen der applications.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/policies/read    | Lesen der applications.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/contacts/basic/read    | Lesen der Basiseigenschaften für Kontakte in Azure Active Directory |
| microsoft.directory/contacts/memberOf/read    | Lesen der contacts.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/contracts/basic/read    | Lesen der Basiseigenschaften für Verträge in Azure Active Directory |
| microsoft.directory/devices/basic/read    | Lesen der Basiseigenschaften für Geräte in Azure Active Directory |
| microsoft.directory/devices/memberOf/read    | Lesen der devices.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/devices/registeredOwners/read    | Lesen der devices.registeredOwners-Eigenschaft in Azure Active Directory |
| microsoft.directory/devices/registeredUsers/read    | Lesen der devices.registeredUsers-Eigenschaft in Azure Active Directory |
| microsoft.directory/directoryRoles/basic/read    | Lesen der Basiseigenschaften für directoryRoles in Azure Active Directory |
| microsoft.directory/directoryRoles/eligibleMembers/read    | Lesen der directoryRoles.eligibleMembers-Eigenschaft in Azure Active Directory |
| microsoft.directory/directoryRoles/members/read    | Lesen der directoryRoles.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/domains/basic/read    | Lesen der Basiseigenschaften für Domänen in Azure Active Directory |
| microsoft.directory/groups/appRoleAssignments/read    | Lesen der groups.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/basic/read    | Lesen der Basiseigenschaften für Gruppen in Azure Active Directory |
| microsoft.directory/groups/hiddenMembers/read    | Lesen der groups.hiddenMembers-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/memberOf/read    | Lesen der groups.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/members/read    | Lesen der groups.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/owners/read    | Lesen der groups.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/settings/read    | Lesen der groups.settings-Eigenschaft in Azure Active Directory |
| microsoft.directory/groupSettings/basic/read    | Lesen der Basiseigenschaften für groupSettings in Azure Active Directory |
| microsoft.directory/groupSettingTemplates/basic/read    | Lesen der Basiseigenschaften für groupSettingTemplates in Azure Active Directory |
| microsoft.directory/oAuth2PermissionGrants/basic/read    | Lesen der Basiseigenschaften für oAuth2PermissionGrants in Azure Active Directory |
| microsoft.directory/organization/basic/read    | Lesen der Basiseigenschaften für die Organisation in Azure Active Directory |
| microsoft.directory/organization/trustedCAsForPasswordlessAuth/read    | Lesen der organizations.trustedCAsForPasswordlessAuth-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/standard/read    | Lesen der Standardrichtlinien in Azure Active Directory. |
| microsoft.directory/roleAssignments/basic/read    | Lesen der Basiseigenschaften für roleAssignments in Azure Active Directory |
| microsoft.directory/roleDefinitions/basic/read    | Lesen der Basiseigenschaften für roleDefinitions in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignedTo/read    | Lesen der servicePrincipals.appRoleAssignedTo-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignments/read    | Lesen der servicePrincipals.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/basic/read    | Lesen der Basiseigenschaften für servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/memberOf/read    | Lesen der servicePrincipals.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/oAuth2PermissionGrants/basic/read    | Lesen der servicePrincipals.oAuth2PermissionGrants-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/ownedObjects/read    | Lesen der servicePrincipals.ownedObjects-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/owners/read    | Lesen der servicePrincipals.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/policies/read    | Lesen der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read    | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |
| microsoft.directory/subscribedSkus/basic/read    | Lesen der Basiseigenschaften für subscribedSkus in Azure Active Directory |
| microsoft.directory/users/appRoleAssignments/read    | Lesen der users.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/basic/read    | Lesen der Basiseigenschaften für Benutzer in Azure Active Directory |
| microsoft.directory/users/directReports/read    | Lesen der users.directReports-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/manager/read    | Lesen der users.manager-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/memberOf/read    | Lesen der users.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/oAuth2PermissionGrants/basic/read    | Lesen der users.oAuth2PermissionGrants-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/ownedDevices/read    | Lesen der users.ownedDevices-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/ownedObjects/read    | Lesen der users.ownedObjects-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/registeredDevices/read    | Lesen der users.registeredDevices-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/strongAuthentication/read    | Lesen der Eigenschaften der strengen Authentifizierung (z.B. MFA-Anmeldeinformationen). |
| microsoft.office365.exchange/allEntities/read    | Lesen sämtlicher Aspekte von Exchange Online. |
| microsoft.office365.messageCenter/messages/read    | Lesen von Nachrichten in microsoft.office365.messageCenter |
| microsoft.office365.messageCenter/securityMessages/read    | Lesen von securityMessages in microsoft.office365.messageCenter |
| microsoft.office365.network/performance/allProperties/read | Lesen von Seiten zur Netzwerkleistung in Admin Center von M365 |
| microsoft.office365.protectionCenter/allEntities/read    | Lesen sämtlicher Aspekte von Office 365 Protection Center. |
| microsoft.office365.securityComplianceCenter/allEntities/read    | Lesen aller Standardeigenschaften in microsoft.office365.securityComplianceCenter. |
| microsoft.office365.usageReports/allEntities/read    | Lesen von Office 365-Nutzungsberichten. |
| microsoft.office365.webPortal/allEntities/standard/read    | Lesen der Standardeigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="groups-administrator-permissions"></a>Berechtigungen von Gruppenadministratoren
Kann alle Aspekte von Gruppen und Gruppeneinstellungen wie Benennungs- und Ablaufrichtlinien verwalten.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/groups/basic/read | Lesen der Standardeigenschaften für Gruppen in Azure Active Directory.  |
| microsoft.directory/groups/basic/update | Aktualisieren der Basiseigenschaften für Gruppen in Azure Active Directory |
| microsoft.directory/groups/create | Erstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/createAsOwner | Erstellen von Gruppen in Azure Active Directory Der Ersteller wird als erster Besitzer hinzugefügt, und das erstellte Objekt wird auf das Kontingent von 250 erstellten Objekten angerechnet, das für den Ersteller gilt. |
| microsoft.directory/groups/delete | Löschen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/hiddenMembers/read | Lesen der groups.hiddenMembers-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/members/update | Aktualisieren der groups.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/owners/update | Aktualisieren der groups.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/restore | Wiederherstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/settings/update | Aktualisieren der groups.settings-Eigenschaft in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.messageCenter/messages/read | Lesen von Nachrichten in microsoft.office365.messageCenter |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="guest-inviter-permissions"></a>Berechtigungen von Gasteinladenden
Einladen von Gastbenutzernunabhängig von der Einstellung „Mitglieder können Gäste einladen“.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/users/appRoleAssignments/read | Lesen der users.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/basic/read | Lesen der Basiseigenschaften für Benutzer in Azure Active Directory |
| microsoft.directory/users/directReports/read | Lesen der users.directReports-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/inviteGuest | Einladen von Gastbenutzern in Azure Active Directory. |
| microsoft.directory/users/manager/read | Lesen der users.manager-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/memberOf/read | Lesen der users.memberOf-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/oAuth2PermissionGrants/basic/read | Lesen der users.oAuth2PermissionGrants-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/ownedDevices/read | Lesen der users.ownedDevices-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/ownedObjects/read | Lesen der users.ownedObjects-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/registeredDevices/read | Lesen der users.registeredDevices-Eigenschaft in Azure Active Directory |

### <a name="helpdesk-administrator-permissions"></a>Berechtigungen von Helpdeskadministratoren

Zurücksetzen von Kennwörtern für Nicht-Administratoren und Helpdeskadministratoren.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/devices/bitLockerRecoveryKeys/read | Lesen der devices.bitLockerRecoveryKeys-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/invalidateAllRefreshTokens | Kennzeichnen sämtlicher Aktualisierungstoken für Benutzer in Azure Active Directory als ungültig. |
| microsoft.directory/users/password/update | Aktualisieren der Kennwörter für alle Benutzer in Azure Active Directory. Weitere Informationen finden Sie in der Onlinedokumentation. |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="hybrid-identity-administrator-permissions"></a>Berechtigungen von Hybrididentitätsadministratoren

Aktivieren, Bereitstellen, Konfigurieren, Verwalten und Überwachen von Cloudbereitstellungs- und Authentifizierungsdiensten sowie Durchführen von Troubleshooting für diese 

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.directory/applications/audience/update  | Aktualisieren der applications.audience-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/authentication/update | Aktualisieren der applications.authentication-Eigenschaft in Azure Active Directory  |
| microsoft.directory/applications/basic/update | Aktualisieren der Basiseigenschaften für Anwendungen in Azure Active Directory |
| microsoft.directory/applications/create | Erstellen von Anwendungen in Azure Active Directory |
| microsoft.directory/applications/credentials/update | Aktualisieren der applications.credentials-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/delete | Löschen von Anwendungen in Azure Active Directory |
| microsoft.directory/applications/owners/update | Aktualisieren der applications.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/permissions/update | Aktualisieren der applications.permissions-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/policies/update | Aktualisieren der applications.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/applicationTemplates/instantiate | Instanziieren von Kataloganwendungen über Anwendungsvorlagen |
| microsoft.directory/auditLogs/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Überwachungsprotokolle (auditLogs) in Azure Active Directory |
| microsoft.directory/cloudProvisioning/allProperties/allTasks | Lesen und Konfigurieren aller Eigenschaften des Azure AD-Cloudbereitstellungsdiensts |
| microsoft.directory/federatedAuthentication/allProperties/allTasks | Verwalten aller Aspekte von Active Directory-Verbunddienste (AD FS) oder von Drittanbieterverbunden in Azure AD |
| microsoft.directory/organization/dirSync/update | Aktualisieren der organization.dirSync-Eigenschaft in Azure Active Directory |
| microsoft.directory/passwordHashSync/allProperties/allTasks | Verwalten aller Aspekte der Kennworthashsynchronisierung (PHS) in Azure AD |
| microsoft.directory/passThroughAuthentication/allProperties/allTasks | Verwalten aller Aspekte der Pass-Through-Authentifizierung (PTA) in Azure AD |
| microsoft.directory/seamlessSSO/allProperties/allTasks | Verwalten aller Aspekte des nahtlosen einmaligen Anmeldens (SSO) in Azure AD |
| microsoft.directory/servicePrincipals/audience/update | Aktualisieren der servicePrincipals.audience-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/authentication/update | Aktualisieren der servicePrincipals.authentication-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/basic/update | Aktualisieren der Basiseigenschaften für servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/create | Erstellen von servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/credentials/update | Aktualisieren der servicePrincipals.credentials-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/delete | Löschen von servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/owners/update | Aktualisieren der servicePrincipals.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/permissions/update | Aktualisieren der servicePrincipals.permissions-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/policies/update | Aktualisieren der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/synchronizationJobs/manage | Verwalten aller Aspekte von Synchronisierungsaufträgen in Azure AD |
| microsoft.directory/servicePrincipals/synchronizationSchema/manage | Verwalten aller Aspekte des Synchronisierungsschemas in Azure AD |
| microsoft.directory/servicePrincipals/synchronizationCredentials/manage | Verwalten aller Aspekte von Synchronisierungsanmeldeinformationen in Azure AD |
| microsoft.directory/servicePrincipals/tag/update | Aktualisieren der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |
| microsoft.office365.messageCenter/messages/read | Lesen von Nachrichten in microsoft.office365.messageCenter |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="insights-administrator-permissions"></a>Berechtigungen der Rolle „Insights Administrator“

Hat administrativen Zugriff in der M365-Insights-App. 

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.insights/allEntities/allTasks | Verwalten sämtlicher Aspekte von Insights. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="insights-business-leader-permissions"></a>Berechtigungen der Rolle „Insights Business Leader“

Kann Dashboards und Erkenntnisse über die M365-Insights-App anzeigen und freigeben.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.insights/reports/read | Anzeigen von Berichten und Dashboards in der Insights-App. |
| microsoft.insights/programs/update | Bereitstellen und Verwalten von Programmen in der Insights-App. |

### <a name="intune-service-administrator-permissions"></a>Berechtigungen von Intune-Dienstadministratoren

Verwalten sämtlicher Aspekte des Produkts Intune.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/contacts/basic/update | Aktualisieren der Basiseigenschaften für Kontakte in Azure Active Directory |
| microsoft.directory/contacts/create | Erstellen von Kontakten in Azure Active Directory |
| microsoft.directory/contacts/delete | Löschen von Kontakten in Azure Active Directory |
| microsoft.directory/devices/basic/update | Aktualisieren der Basiseigenschaften für Geräte in Azure Active Directory |
| microsoft.directory/devices/bitLockerRecoveryKeys/read | Lesen der devices.bitLockerRecoveryKeys-Eigenschaft in Azure Active Directory |
| microsoft.directory/devices/create | Erstellen von Geräten in Azure Active Directory |
| microsoft.directory/devices/delete | Löschen von Geräten in Azure Active Directory |
| microsoft.directory/devices/registeredOwners/update | Aktualisieren der devices.registeredOwners-Eigenschaft in Azure Active Directory |
| microsoft.directory/devices/registeredUsers/update | Aktualisieren der devices.registeredUsers-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/appRoleAssignments/update | Aktualisieren der groups.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/basic/update | Aktualisieren der Basiseigenschaften für Gruppen in Azure Active Directory |
| microsoft.directory/groups/create | Erstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/createAsOwner | Erstellen von Gruppen in Azure Active Directory Der Ersteller wird als erster Besitzer hinzugefügt, und das erstellte Objekt wird auf das Kontingent von 250 erstellten Objekten angerechnet, das für den Ersteller gilt. |
| microsoft.directory/groups/delete | Löschen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/hiddenMembers/read | Lesen der groups.hiddenMembers-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/members/update | Aktualisieren der groups.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/owners/update | Aktualisieren der groups.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/restore | Wiederherstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/settings/update | Aktualisieren der groups.settings-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/appRoleAssignments/update | Aktualisieren der users.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/basic/update | Aktualisieren der Basiseigenschaften für Benutzer in Azure Active Directory |
| microsoft.directory/users/manager/update | Aktualisieren der users.manager-Eigenschaft in Azure Active Directory |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.intune/allEntities/allTasks | Verwalten sämtlicher Aspekte von Intune. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="kaizala-administrator-permissions"></a>Berechtigungen von Kaizala-Administratoren

Kann Einstellungen für Microsoft Kaizala verwalten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen von Office 365 Admin Center. |

### <a name="license-administrator-permissions"></a>Berechtigungen von Lizenzadministratoren

Kann Produktlizenzen für Benutzer und Gruppen verwalten.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/users/assignLicense | Verwalten der Lizenzen für Benutzer in Azure Active Directory |
| microsoft.directory/users/usageLocation/update | Aktualisieren der users.usageLocation-Eigenschaft in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |

### <a name="lync-service-administrator-permissions"></a>Berechtigungen von Lync-Dienstadministratoren

Verwalten sämtlicher Aspekte des Produkts Skype for Business.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.skypeForBusiness/allEntities/allTasks | Verwalten sämtlicher Aspekte von Skype for Business Online |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.usageReports/allEntities/read    | Lesen von Office 365-Nutzungsberichten. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |


### <a name="message-center-privacy-reader-permissions"></a>Berechtigungen von Nachrichtencenter-Datenschutzleseberechtigten

Kann Nachrichtencenter-Beiträge, Nachrichten zum Datenschutz, Gruppen, Domänen und Abonnements lesen.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.messageCenter/messages/read | Lesen von Nachrichten in microsoft.office365.messageCenter |
| microsoft.office365.messageCenter/securityMessages/read | Lesen von securityMessages in microsoft.office365.messageCenter |

### <a name="message-center-reader-permissions"></a>Berechtigungen von Nachrichtencenter-Leseberechtigten
Lesen von Nachrichten und Updates für die Organisation ausschließlich im Office 365-Nachrichtencenter. 

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.messageCenter/messages/read | Lesen von Nachrichten in microsoft.office365.messageCenter |

### <a name="modern-commerce-user-permissions"></a>Berechtigungen der Rolle „Modern Commerce User“
Kann kommerzielle Käufe für ein Unternehmen, eine Abteilung oder ein Team verwalten. 

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.commerce.billing/partners/read | Lesen der Partnereigenschaft der O365-Abrechnung. |
| microsoft.commerce.volumeLicenseServiceCenter/allEntities/allTasks | Verwalten aller Aspekte von Volume Licensing Service Center. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Anzeigen eigener Office 365-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |


### <a name="network-administrator-permissions"></a>Berechtigungen von Netzwerkadministratoren
Verwalten von Netzwerkstandorten und überprüfen von Erkenntnissen zum Entwurf des Unternehmensnetzwerks für Microsoft 365-SaaS-Anwendungen (Software-as-a-Service).

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.office365.network/performance/allProperties/read | Lesen von Seiten zur Netzwerkleistung in Admin Center von M365  |
| microsoft.office365.network/locations/allProperties/allTasks | Lesen und Konfigurieren von Eigenschaften der Netzwerkstandorte für jeden Standort |

### <a name="office-apps-administrator-permissions"></a>Office-Apps-Administratorberechtigungen
Verwalten von Clouddiensten für Office-Apps (einschließlich Richtlinien- und Einstellungsverwaltung) sowie von Funktionen zum Auswählen, Aufheben der Auswahl und Veröffentlichen von Inhalten zu neuen Features auf Endbenutzergeräten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.messageCenter/messages/read | Lesen von Nachrichten in microsoft.office365.messageCenter |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.userCommunication/allEntities/allTasks | Lesen von Meldungen zu neuen Features und Aktualisieren der Sichtbarkeit. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="partner-tier1-support-permissions"></a>Berechtigungen des Partnersupports der Ebene 1

Verwenden Sie diese Rolle nicht – sie ist nicht zur allgemeinen Verwendung vorgesehen.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/contacts/basic/update | Aktualisieren der Basiseigenschaften für Kontakte in Azure Active Directory |
| microsoft.directory/contacts/create | Erstellen von Kontakten in Azure Active Directory |
| microsoft.directory/contacts/delete | Löschen von Kontakten in Azure Active Directory |
| microsoft.directory/groups/create | Erstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/createAsOwner | Erstellen von Gruppen in Azure Active Directory Der Ersteller wird als erster Besitzer hinzugefügt, und das erstellte Objekt wird auf das Kontingent von 250 erstellten Objekten angerechnet, das für den Ersteller gilt. |
| microsoft.directory/groups/members/update | Aktualisieren der groups.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/owners/update | Aktualisieren der groups.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/appRoleAssignments/update | Aktualisieren der users.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/assignLicense | Verwalten der Lizenzen für Benutzer in Azure Active Directory |
| microsoft.directory/users/basic/update | Aktualisieren der Basiseigenschaften für Benutzer in Azure Active Directory |
| microsoft.directory/users/delete | Löschen von Benutzern in Azure Active Directory |
| microsoft.directory/users/invalidateAllRefreshTokens | Kennzeichnen sämtlicher Aktualisierungstoken für Benutzer in Azure Active Directory als ungültig. |
| microsoft.directory/users/manager/update | Aktualisieren der users.manager-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/password/update | Aktualisieren der Kennwörter für alle Benutzer in Azure Active Directory. Weitere Informationen finden Sie in der Onlinedokumentation. |
| microsoft.directory/users/restore | Wiederherstellen gelöschter Benutzerkonten in Azure Active Directory. |
| microsoft.directory/users/userPrincipalName/update | Aktualisieren der users.userPrincipalName-Eigenschaft in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="partner-tier2-support-permissions"></a>Berechtigungen des Partnersupports der Ebene 2

Verwenden Sie diese Rolle nicht – sie ist nicht zur allgemeinen Verwendung vorgesehen.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/contacts/basic/update | Aktualisieren der Basiseigenschaften für Kontakte in Azure Active Directory |
| microsoft.directory/contacts/create | Erstellen von Kontakten in Azure Active Directory |
| microsoft.directory/contacts/delete | Löschen von Kontakten in Azure Active Directory |
| microsoft.directory/domains/allTasks | Erstellen und Löschen von Domänen und Lesen und Aktualisieren der Standardeigenschaften in Azure Active Directory |
| microsoft.directory/groups/create | Erstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/delete | Löschen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/members/update | Aktualisieren der groups.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/restore | Wiederherstellen von Gruppen in Azure Active Directory |
| microsoft.directory/organization/basic/update | Aktualisieren der Basiseigenschaften für die Organisation in Azure Active Directory |
| microsoft.directory/users/appRoleAssignments/update | Aktualisieren der users.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/assignLicense | Verwalten der Lizenzen für Benutzer in Azure Active Directory |
| microsoft.directory/users/basic/update | Aktualisieren der Basiseigenschaften für Benutzer in Azure Active Directory |
| microsoft.directory/users/delete | Löschen von Benutzern in Azure Active Directory |
| microsoft.directory/users/invalidateAllRefreshTokens | Kennzeichnen sämtlicher Aktualisierungstoken für Benutzer in Azure Active Directory als ungültig. |
| microsoft.directory/users/manager/update | Aktualisieren der users.manager-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/password/update | Aktualisieren der Kennwörter für alle Benutzer in Azure Active Directory. Weitere Informationen finden Sie in der Onlinedokumentation. |
| microsoft.directory/users/restore | Wiederherstellen gelöschter Benutzerkonten in Azure Active Directory. |
| microsoft.directory/users/userPrincipalName/update | Aktualisieren der users.userPrincipalName-Eigenschaft in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="password-administrator-permissions"></a>Berechtigungen von Kennwortadministratoren

Kann Kennwörter für Nicht-Administratoren und Kennwortadministratoren zurücksetzen.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/users/password/update | Aktualisieren der Kennwörter für alle Benutzer in Azure Active Directory. Weitere Informationen finden Sie in der Onlinedokumentation. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="power-bi-service-administrator-permissions"></a>Berechtigungen von Power BI-Dienstadministratoren

Verwalten sämtlicher Aspekte des Produkts Power BI.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>
| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.powerApps.powerBI/allEntities/allTasks | Verwalten sämtlicher Aspekte von Power BI. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |


### <a name="power-platform-administrator-permissions"></a>Power Platform-Administratorberechtigungen

Kann alle Aspekte von Microsoft Dynamics 365, PowerApps und Microsoft Flow erstellen und verwalten. 

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>
| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.dynamics365/allEntities/allTasks | Verwalten sämtlicher Aspekte von Dynamics 365. |
| microsoft.flow/allEntities/allTasks | Verwalten aller Aspekte von Microsoft Flow. |
| microsoft.powerApps/allEntities/allTasks | Verwalten aller Aspekte von PowerApps. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="printer-administrator-permissions"></a>Berechtigungen von Druckadministratoren

Verwalten sämtlicher Aspekte von Druckern und Druckerconnectors.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>
| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.print/allEntities/allProperties/allTasks | Erstellen und Löschen von Druckern und Connectors sowie Lesen und Aktualisieren aller Eigenschaften in Microsoft Print |

### <a name="printer-technician-permissions"></a>Berechtigungen von Druckertechnikern

Registrieren von Druckern, Aufheben ihrer Registrierung und Aktualisieren des Druckerstatus.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>
| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.print/connectors/allProperties/read | Lesen aller Eigenschaften von Connectors in Microsoft Print |
| microsoft.azure.print/printers/allProperties/read | Lesen aller Eigenschaften von Druckern in Microsoft Print |
| microsoft.azure.print/printers/basic/update | Aktualisieren grundlegender Eigenschaften von Druckern in Microsoft Print |
| microsoft.azure.print/printers/register | Registrieren von Druckern in Microsoft Print |
| microsoft.azure.print/printers/unregister | Aufheben der Registrierung von Druckern in Microsoft Print |

### <a name="privileged-authentication-administrator-permissions"></a>Berechtigungen von privilegierten Authentifizierungsadministratoren

Darf Informationen zur Authentifizierungsmethode für alle Benutzer (mit und ohne Administratorrechte) anzeigen, festlegen und zurücksetzen.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/users/invalidateAllRefreshTokens | Kennzeichnen sämtlicher Aktualisierungstoken für Benutzer in Azure Active Directory als ungültig. |
| microsoft.directory/users/strongAuthentication/update | Aktualisieren der Eigenschaften der strengen Authentifizierung (z. B. MFA-Anmeldeinformationen). |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.directory/users/password/update | Aktualisieren von Kennwörtern für alle Benutzer in der Office 365-Organisation. Weitere Informationen finden Sie in der Onlinedokumentation. |

### <a name="privileged-role-administrator-permissions"></a>Berechtigungen von Administratoren für privilegierte Rollen

Kann Rollenzuweisungen in Azure AD sowie sämtliche Aspekte von Privileged Identity Management verwalten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/groupsAssignableToRoles/allProperties/update | Aktualisieren von Gruppen, bei denen die isAssignableToRole-Eigenschaft in Azure Active Directory auf TRUE festgelegt ist |
| microsoft.directory/groupsAssignableToRoles/create | Erstellen von Gruppen, bei denen die isAssignableToRole-Eigenschaft in Azure Active Directory auf TRUE festgelegt ist |
| microsoft.directory/groupsAssignableToRoles/delete | Löschen von Gruppen, bei denen die isAssignableToRole-Eigenschaft in Azure Active Directory auf TRUE festgelegt ist |
| microsoft.aad.privilegedIdentityManagement/allEntities/allTasks | Erstellen und Löschen aller Ressourcen und Lesen und Aktualisieren von Standardeigenschaften in microsoft.aad.privilegedIdentityManagement |
| microsoft.directory/servicePrincipals/appRoleAssignedTo/allTasks | Lesen und Konfigurieren der servicePrincipals.appRoleAssignedTo-Eigenschaft in Azure Active Directory. |
| microsoft.directory/servicePrincipals/oAuth2PermissionGrants/allTasks | Lesen und Konfigurieren der servicePrincipals.oAuth2PermissionGrants-Eigenschaft in Azure Active Directory. |
| microsoft.directory/administrativeUnits/allProperties/allTasks | Erstellen und Verwalten von Verwaltungseinheiten (einschließlich Mitgliedern). |
| microsoft.directory/roleAssignments/allProperties/allTasks | Erstellen und Verwalten von Rollenzuweisungen. |
| microsoft.directory/roleDefinitions/allProperties/allTasks | Erstellen und Verwalten von Rollendefinitionen. |

### <a name="reports-reader-permissions"></a>Berechtigungen von Berichtleseberechtigten

Lesen von Anmeldungs- und Überwachungsberichten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/auditLogs/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Überwachungsprotokolle (auditLogs) in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.office365.usageReports/allEntities/read | Lesen von Office 365-Nutzungsberichten. |

### <a name="search-administrator-permissions"></a>Berechtigungen von Suchadministratoren

Kann alle Aspekte der Microsoft Search-Einstellungen erstellen und verwalten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.office365.messageCenter/messages/read | Lesen von Nachrichten in microsoft.office365.messageCenter |
| microsoft.office365.search/allEntities/allProperties/allTasks | Erstellen und Löschen aller Ressourcen sowie Lesen und Aktualisieren aller Eigenschaften in „microsoft.office365.search“. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="search-editor-permissions"></a>Berechtigungen von Such-Editoren

Kann redaktionelle Inhalte wie Lesezeichen, Fragen und Antworten, Standorte und Grundrisse erstellen und verwalten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.office365.messageCenter/messages/read | Lesen von Nachrichten in microsoft.office365.messageCenter |
| microsoft.office365.search/content/allProperties/allTasks | Erstellen und Löschen von Inhalten sowie Lesen und Aktualisieren aller Eigenschaften in „microsoft.office365.search“. |

### <a name="security-administrator-permissions"></a>Berechtigungen von Sicherheitsadministratoren

Kann Sicherheitsinformationen und -berichte lesen und die Konfiguration in Azure AD und Office 365 verwalten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.directory/applications/policies/update | Aktualisieren der applications.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/auditLogs/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Überwachungsprotokolle (auditLogs) in Azure Active Directory |
| microsoft.directory/devices/bitLockerRecoveryKeys/read | Lesen der devices.bitLockerRecoveryKeys-Eigenschaft in Azure Active Directory |
| microsoft.directory/identityProtection/allProperties/read | Lesen aller Ressourcen in microsoft.aad.identityProtection |
| microsoft.directory/identityProtection/allProperties/update | Aktualisieren aller Ressourcen in microsoft.aad.identityProtection |
| microsoft.directory/policies/basic/update | Aktualisieren der Basiseigenschaften für Richtlinien in Azure Active Directory |
| microsoft.directory/policies/create | Erstellen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/delete | Löschen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/owners/update | Aktualisieren der policies.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/tenantDefault/update | Aktualisieren der policies.tenantDefault-Eigenschaft in Azure Active Directory |
| microsoft.directory/privilegedIdentityManagement/allProperties/read | Lesen aller Ressourcen in microsoft.aad.privilegedIdentityManagement |
| microsoft.directory/servicePrincipals/policies/update | Aktualisieren der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |
| microsoft.office365.protectionCenter/allEntities/read | Lesen sämtlicher Aspekte von Office 365 Protection Center. |
| microsoft.office365.protectionCenter/allEntities/update | Aktualisieren aller Ressourcen in microsoft.office365.protectionCenter |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="security-operator-permissions"></a>Berechtigungen von Sicherheitsoperatoren

Erstellt und verwaltet Sicherheitsereignisse.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.advancedThreatProtection/allEntities/read | Lesen und Konfigurieren von Azure AD Advanced Threat Protection. |
| microsoft.directory/cloudAppSecurity/allProperties/allTasks | Lesen und Konfigurieren von Microsoft Cloud App Security-Daten. |
| microsoft.directory/identityProtection/allProperties/read | Lesen aller Ressourcen in microsoft.aad.identityProtection |
| microsoft.directory/privilegedIdentityManagement/allProperties/read | Lesen aller Ressourcen in microsoft.aad.privilegedIdentityManagement |
| microsoft.intune/allEntities/allTasks | Verwalten sämtlicher Aspekte von Intune. |
| microsoft.office365.securityComplianceCenter/allEntities/allTasks | Lesen und Konfigurieren von Security & Compliance Center. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.windows.defenderAdvancedThreatProtection/allEntities/read | Lesen und Konfigurieren von Windows Defender Advanced Threat Protection. |

### <a name="security-reader-permissions"></a>Berechtigungen von Benutzern mit Leseberechtigung für Sicherheitsfunktionen

Lesen von Sicherheitsinformationen und Berichten in Azure AD und Office 365.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/auditLogs/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Überwachungsprotokolle (auditLogs) in Azure Active Directory |
| microsoft.directory/devices/bitLockerRecoveryKeys/read | Lesen der devices.bitLockerRecoveryKeys-Eigenschaft in Azure Active Directory |
| microsoft.directory/policies/conditionalAccess/basic/read | Lesen der policies.conditionalAccess-Eigenschaft in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |
| microsoft.aad.identityProtection/allEntities/read | Lesen aller Ressourcen in microsoft.aad.identityProtection |
| microsoft.aad.privilegedIdentityManagement/allEntities/read | Lesen aller Ressourcen in microsoft.aad.privilegedIdentityManagement |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.protectionCenter/allEntities/read | Lesen sämtlicher Aspekte von Office 365 Protection Center. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |

### <a name="service-support-administrator-permissions"></a>Berechtigungen von Dienstsupportadministratoren

Lesen von Service Health-Informationen und Verwalten von Supporttickets.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

### <a name="sharepoint-service-administrator-permissions"></a>Berechtigungen von SharePoint-Dienstadministratoren

Verwalten sämtlicher Aspekte des SharePoint-Diensts.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.directory/groups/unified/appRoleAssignments/update | Aktualisieren der groups.unified-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/unified/basic/update | Aktualisieren der Basiseigenschaften von Office 365-Gruppen |
| microsoft.directory/groups/unified/create | Erstellen von Office 365-Gruppen |
| microsoft.directory/groups/unified/delete | Löschen von Office 365-Gruppen |
| microsoft.directory/groups/unified/members/update | Aktualisieren der Mitgliedschaft von Office 365-Gruppen |
| microsoft.directory/groups/unified/owners/update | Aktualisieren des Besitzers von Office 365-Gruppen |
| microsoft.office365.network/performance/allProperties/read | Lesen von Seiten zur Netzwerkleistung in Admin Center von M365 |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.sharepoint/allEntities/allTasks | Erstellen und Löschen aller Ressourcen und Lesen und Aktualisieren von Standardeigenschaften in microsoft.office365.sharepoint |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.usageReports/allEntities/read    | Lesen von Office 365-Nutzungsberichten. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="teams-communications-administrator-permissions"></a>Berechtigungen von Teams-Kommunikationsadministratoren

Kann Anruf- und Besprechungsfunktionen im Microsoft Teams-Dienst verwalten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.usageReports/allEntities/read | Lesen von Office 365-Nutzungsberichten. |

### <a name="teams-communications-support-engineer-permissions"></a>Berechtigungen von Supporttechnikern für die Teams-Kommunikation

Kann Kommunikationsprobleme in Teams mithilfe von erweiterten Tools behandeln.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |

### <a name="teams-communications-support-specialist-permissions"></a>Berechtigungen von Supportfachleuten für die Teams-Kommunikation

Kann Kommunikationsprobleme in Teams mithilfe von allgemeinen Tools behandeln.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |

### <a name="teams-service-administrator-permissions"></a>Berechtigungen von Teams-Dienstadministratoren

Kann den Microsoft Teams-Dienst verwalten.

> [!NOTE]
> Diese Rolle verfügt über zusätzliche Berechtigungen außerhalb von Azure Active Directory. Weitere Informationen finden Sie in der Rollenbeschreibung oben.
>
>

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.directory/groups/hiddenMembers/read | Lesen der groups.hiddenMembers-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/unified/appRoleAssignments/update | Aktualisieren der groups.unified-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/unified/basic/update | Aktualisieren der Basiseigenschaften von Office 365-Gruppen |
| microsoft.directory/groups/unified/create | Erstellen von Office 365-Gruppen |
| microsoft.directory/groups/unified/delete | Löschen von Office 365-Gruppen |
| microsoft.directory/groups/unified/members/update | Aktualisieren der Mitgliedschaft von Office 365-Gruppen |
| microsoft.directory/groups/unified/owners/update | Aktualisieren des Besitzers von Office 365-Gruppen |
| microsoft.office365.network/performance/allProperties/read | Lesen von Seiten zur Netzwerkleistung in Admin Center von M365 |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |
| microsoft.office365.usageReports/allEntities/read | Lesen von Office 365-Nutzungsberichten. |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |

### <a name="user-administrator-permissions"></a>Berechtigungen von Benutzeradministratoren
Dieser Administrator kann alle Aspekte von Benutzern und Gruppen verwalten, einschließlich der Kennwortzurücksetzung für eingeschränkte Administratoren.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/appRoleAssignments/create | Erstellen von appRoleAssignments in Azure Active Directory |
| microsoft.directory/appRoleAssignments/delete | Löschen von appRoleAssignments in Azure Active Directory |
| microsoft.directory/appRoleAssignments/update | Aktualisieren von appRoleAssignments in Azure Active Directory |
| microsoft.directory/contacts/basic/update | Aktualisieren der Basiseigenschaften für Kontakte in Azure Active Directory |
| microsoft.directory/contacts/create | Erstellen von Kontakten in Azure Active Directory |
| microsoft.directory/contacts/delete | Löschen von Kontakten in Azure Active Directory |
| microsoft.directory/groups/appRoleAssignments/update | Aktualisieren der groups.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/basic/update | Aktualisieren der Basiseigenschaften für Gruppen in Azure Active Directory |
| microsoft.directory/groups/create | Erstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/createAsOwner | Erstellen von Gruppen in Azure Active Directory Der Ersteller wird als erster Besitzer hinzugefügt, und das erstellte Objekt wird auf das Kontingent von 250 erstellten Objekten angerechnet, das für den Ersteller gilt. |
| microsoft.directory/groups/delete | Löschen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/hiddenMembers/read | Lesen der groups.hiddenMembers-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/members/update | Aktualisieren der groups.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/owners/update | Aktualisieren der groups.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/restore | Wiederherstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/settings/update | Aktualisieren der groups.settings-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/appRoleAssignments/update | Aktualisieren der users.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/assignLicense | Verwalten der Lizenzen für Benutzer in Azure Active Directory |
| microsoft.directory/users/basic/update | Aktualisieren der Basiseigenschaften für Benutzer in Azure Active Directory |
| microsoft.directory/users/create | Erstellen von Benutzern in Azure Active Directory |
| microsoft.directory/users/delete | Löschen von Benutzern in Azure Active Directory |
| microsoft.directory/users/invalidateAllRefreshTokens | Kennzeichnen sämtlicher Aktualisierungstoken für Benutzer in Azure Active Directory als ungültig. |
| microsoft.directory/users/manager/update | Aktualisieren der users.manager-Eigenschaft in Azure Active Directory |
| microsoft.directory/users/password/update | Aktualisieren der Kennwörter für alle Benutzer in Azure Active Directory. Weitere Informationen finden Sie in der Onlinedokumentation. |
| microsoft.directory/users/restore | Wiederherstellen gelöschter Benutzerkonten in Azure Active Directory. |
| microsoft.directory/users/userPrincipalName/update | Aktualisieren der users.userPrincipalName-Eigenschaft in Azure Active Directory |
| microsoft.azure.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren von Azure Service Health |
| microsoft.azure.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Azure-Supporttickets |
| microsoft.office365.webPortal/allEntities/basic/read | Lesen der Basiseigenschaften für alle Ressourcen in microsoft.office365.webPortal. |
| microsoft.office365.serviceHealth/allEntities/allTasks | Lesen und Konfigurieren des Office 365-Dienststatus. |
| microsoft.office365.supportTickets/allEntities/allTasks | Erstellen und Verwalten von Office 365-Supporttickets. |

## <a name="role-template-ids"></a>Rollenvorlagen-IDs

Rollenvorlagen-IDs werden hauptsächlich von Microsoft Graph-API- oder PowerShell-Benutzern verwendet.

Graph displayName | Anzeigename des Azure-Portals | directoryRoleTemplateId
----------------- | ------------------------- | -------------------------
Anwendungsadministrator | Anwendungsadministrator | 9B895D92-2CD3-44C7-9D02-A6AC2D5EA5C3
Anwendungsentwickler | Anwendungsentwickler | CF1C38E5-3621-4004-A7CB-879624DCED7C
Authentifizierungsadministrator | Authentifizierungsadministrator | c4e39bd9-1100-46d3-8c65-fb160da0071f
Azure DevOps-Administrator | Azure DevOps-Administrator | e3973bdf-4987-49ae-837a-ba8e231c7286
Azure Information Protection-Administrator | Azure Information Protection-Administrator | 7495fdc4-34c4-4d15-a289-98788ce399fd
B2C-IEF-Schlüsselsatzadministrator | B2C-IEF-Schlüsselsatzadministrator | aaf43236-0c0d-4d5f-883a-6955382ac081
B2C-IEF-Richtlinienadministrator | B2C-IEF-Richtlinienadministrator | 3edaf663-341e-4475-9f94-5c398ef6c070
Abrechnungsadministrator | Rechnungsadministrator | b0f54661-2d74-4c50-afa3-1ec803f12efe
Cloudanwendungsadministrator | Cloudanwendungsadministrator | 158c047a-c907-4556-b7ef-446551a6b5f7
Cloudgeräteadministrator | Cloudgeräteadministrator | 7698a772-787b-4ac8-901f-60d6b08affd2
Unternehmensadministrator | Globaler Administrator | 62e90394-69f5-4237-9190-012177145e10
Complianceadministrator | Complianceadministrator | 17315797-102d-40b4-93e0-432062caca18
Compliancedatenadministrator | Compliancedatenadministrator | e6d1a23a-da11-4be4-9570-befc86d067a7
Administrator für den bedingten Zugriff | Administrator für den bedingten Zugriff | b1be1c3e-b65d-4f19-8427-f6fa0d97feb9
CRM-Dienstadministrator | Dynamics 365-Administrator | 44367163-eba1-44c3-98af-f5787879f96a
Genehmigende Person für den LockBox-Kundenzugriff | Genehmigende Person für den Kunden-Lockbox-Zugriff | 5c4f9dcd-47dc-4cf7-8c9a-9e4207cbfc91
Desktop Analytics-Administrator | Desktop Analytics-Administrator | 38a96431-2bdf-4b4c-8b6e-5d3d8abac1a4
Geräteadministratoren | Geräteadministratoren | 9f06204d-73c1-4d4c-880a-6edb90606fd8
Geräteeinbindung | Als veraltet markiert | 9c094953-4995-41c8-84c8-3ebb9b32c93f
Geräte-Manager | Als veraltet markiert | 2b499bcd-da44-4968-8aec-78e1674fa64d
Gerätebenutzer | Als veraltet markiert | d405c6df-0af8-4e3b-95e4-4d06e542189e
Rolle „Verzeichnis lesen“ | Rolle „Verzeichnis lesen“ | 88d8e3e3-8f55-4a1e-953a-9b9898b8876b
Konten zur Verzeichnissynchronisierung | Nicht angezeigt, da keine Verwendung erfolgen soll | d29b2b05-8046-44ba-8758-1e26182fcf32
Verzeichnis schreiben | Verzeichnis schreiben | 9360feb5-f418-4baa-8175-e2a00bac4301
Exchange-Dienstadministrator | Exchange-Administrator | 29232cdf-9323-42fd-ade2-1d097af3e4de
Administrator für Benutzerflows mit externer ID | Administrator für Benutzerflows mit externer ID | 6e591065-9bad-43ed-90f3-e9424366d2f0
Administrator für Benutzerflowattribute mit externer ID | Administrator für Benutzerflowattribute mit externer ID | 0f971eea-41eb-4569-a71e-57bb8a3eff1e
Externer Identitätsanbieteradministrator | Externer Identitätsanbieteradministrator | be2f45a1-457d-42af-a067-6ec1fa63bc45
Globaler Leser | Globaler Leser | f2ef992c-3afb-46b9-b7cf-a126ee74c451
Gruppenadministrator | Gruppenadministrator | fdd7a751-b60b-444a-984c-02652fe8fa1c 
Gasteinladender | Gasteinladender | 95e79109-95c0-4d8e-aee3-d01accf2d47b
Helpdeskadministrator | Helpdesk-Administrator | 729827e3-9c14-49f7-bb1b-9608f156bbb8
Hybrididentitätsadministrator | Hybrididentitätsadministrator | 8ac3fc64-6eca-42ea-9e69-59f4c7b60eb2
Insights Administrator | Insights Administrator | eb1f4a8d-243a-41f0-9fbd-c7cdf6c5ef7c
Insights Business Leader | Insights Business Leader | 31e939ad-9672-4796-9c2e-873181342d2d
Intune-Dienstadministrator | Intune-Administrator | 3a2c62db-5318-420d-8d74-23affee5d9d5
Kaizala-Administrator | Kaizala-Administrator | 74ef975b-6605-40af-a5d2-b9539d836353
Lizenzadministrator | Lizenzadministrator | 4d6ac14f-3453-41d0-bef9-a3e0c569773a
Lync-Dienstadministrator | Skype for Business-Administrator | 75941009-915a-4869-abe7-691bff18279e
Nachrichtencenter-Datenschutzleseberechtigter | Nachrichtencenter-Datenschutzleseberechtigter | ac16e43d-7b2d-40e0-ac05-243ff356ab5b
Nachrichtencenter-Leser | Nachrichtencenter-Leser | 790c1fb9-7f7d-4f88-86a1-ef1f95c05c1b
Modern Commerce User | Modern Commerce User | d24aef57-1500-4070-84db-2666f29cf966
Netzwerkadministrator | Netzwerkadministrator | d37c8bed-0711-4417-ba38-b4abe66ce4c2
Office-Apps-Administrator | Office-Apps-Administrator | 2b745bdf-0803-4d80-aa65-822c4493daac
Partnersupport der Ebene 1 | Nicht angezeigt, da keine Verwendung erfolgen soll | 4ba39ca4-527c-499a-b93d-d9b492c50246
Partnersupport der Ebene 2 | Nicht angezeigt, da keine Verwendung erfolgen soll | e00e864a-17c5-4a4b-9c06-f5b95a8d5bd8
Kennwortadministrator | Kennwortadministrator | 966707d0-3269-4727-9be2-8c3a10f19b9d
Power BI-Dienstadministrator | Power BI-Administrator | a9ea8996-122f-4c74-9520-8edcd192826c
Power Platform-Administrator | Power Platform-Administrator | 11648597-926c-4cf3-9c36-bcebb0ba8dcc
Druckeradministrator | Druckeradministrator | 644ef478-e28f-4e28-b9dc-3fdde9aa0b1f
Druckertechniker | Druckertechniker | e8cef6f1-e4bd-4ea8-bc07-4b8d950f4477
Privilegierter Authentifizierungsadministrator | Privilegierter Authentifizierungsadministrator | 7be44c8a-adaf-4e2a-84d6-ab2649e08a13
Administrator für privilegierte Rollen | Administrator für privilegierte Rollen | e8611ab8-c189-46e8-94e1-60213ab1f814
Meldet Reader | Berichtsleser | 4a5d8f65-41da-4de4-8968-e035b65339cf
Suchadministrator | Suchadministrator | 0964bb5e-9bdb-4d7b-ac29-58e794862a40
Such-Editor | Such-Editor | 8835291a-918c-4fd7-a9ce-faa49f0cf7d9
Sicherheitsadministrator | Sicherheitsadministrator | 194ae4cb-b126-40b2-bd5b-6091b380977d
Sicherheitsoperator | Sicherheitsoperator | 5f2222b1-57c3-48ba-8ad5-d4759f1fde6f
Sicherheitsleseberechtigter | Sicherheitsleseberechtigter | 5d6b6bb7-de71-4623-b4af-96380a352509
Dienstunterstützungsadministrator | Dienstunterstützungsadministrator | f023fd81-a637-4b56-95fd-791ac0226033
SharePoint-Dienstadministrator | SharePoint-Administrator | f28a1f50-f6e7-4571-818b-6a12f2af6b6c
Teams-Kommunikationsadministrator | Teams-Kommunikationsadministrator | baf37b3a-610e-45da-9e62-d9d1e5e8914b
Teams-Kommunikationssupporttechniker | Teams-Kommunikationssupporttechniker | f70938a0-fc10-4177-9e90-2178f8765737
Teams-Kommunikationssupportspezialist | Teams-Kommunikationssupportspezialist | fcf91098-03e3-41a9-b5ba-6f0ec8188a12
Teams-Dienstadministrator | Teams-Dienstadministrator | 69091246-20e8-4a56-aa4d-066075b2a7a8
Benutzer | Nicht angezeigt, weil keine Verwendung erfolgen kann | a0b1b346-4d3e-4e8b-98f8-753987be4970
Benutzerkontoadministrator | Benutzeradministrator | fe930be7-5e62-47db-91af-98c3a49a38b1
Geräteeinbindung am Arbeitsplatz | Als veraltet markiert | c34f683f-4d5a-4403-affd-6615e00e3a7f

## <a name="deprecated-roles"></a>Veraltete Rollen

Die folgenden Rollen sollten nicht verwendet werden. Sie sind veraltet und werden aus Azure AD entfernt.

* Ad-hoc-Lizenzadministrator
* Geräteeinbindung
* Geräte-Manager
* Gerätebenutzer
* Benutzererstellung mit E-Mail-Überprüfung
* Postfachadministrator
* Geräteeinbindung am Arbeitsplatz

## <a name="roles-not-shown-in-the-portal"></a>Im Portal nicht angezeigte Rollen

Nicht jede Rolle, die von PowerShell oder der MS Graph-API zurückgegeben wird, wird Azure-Portal angezeigt. Diese Unterschiede sind in der folgenden Tabelle aufgelistet.

API-Name | Name im Azure-Portal | Notizen
-------- | ------------------- | -------------
Unternehmensadministrator | Globaler Administrator | [Name zur besseren Verständlichkeit geändert](directory-assign-admin-roles.md#role-template-ids)
CRM-Dienstadministrator | Dynamics 365-Administrator | [Gibt das aktuelle Produktbranding wieder](directory-assign-admin-roles.md#role-template-ids)
Geräteeinbindung | Als veraltet markiert | [Dokumentation zu veralteten Rollen](directory-assign-admin-roles.md#deprecated-roles)
Geräte-Manager | Als veraltet markiert | [Dokumentation zu veralteten Rollen](directory-assign-admin-roles.md#deprecated-roles)
Gerätebenutzer | Als veraltet markiert | [Dokumentation zu veralteten Rollen](directory-assign-admin-roles.md#deprecated-roles)
Konten zur Verzeichnissynchronisierung | Nicht angezeigt, da keine Verwendung erfolgen soll | [Dokumentation zu Konten für die Verzeichnissynchronisierung](directory-assign-admin-roles.md#directory-synchronization-accounts)
Verzeichnis schreiben | Nicht angezeigt, da keine Verwendung erfolgen soll | [Dokumentation zu Verzeichnisschreibberechtigten](directory-assign-admin-roles.md#directory-writers)
Gastbenutzer | Nicht angezeigt, weil keine Verwendung erfolgen kann  | Nicht verfügbar
Lync-Dienstadministrator | Skype for Business-Administrator | [Gibt das aktuelle Produktbranding wieder](directory-assign-admin-roles.md#role-template-ids)
Partnersupport der Ebene 1 | Nicht angezeigt, da keine Verwendung erfolgen soll | [Dokumentation zum Partnersupport der Ebene 1](directory-assign-admin-roles.md#partner-tier1-support)
Partnersupport der Ebene 2 | Nicht angezeigt, da keine Verwendung erfolgen soll | [Dokumentation zum Partnersupport der Ebene 2](directory-assign-admin-roles.md#partner-tier2-support)
Eingeschränkter Gastbenutzer | Nicht angezeigt, weil keine Verwendung erfolgen kann | Nicht verfügbar
Benutzer | Nicht angezeigt, weil keine Verwendung erfolgen kann | Nicht verfügbar
Geräteeinbindung am Arbeitsplatz | Als veraltet markiert | [Dokumentation zu veralteten Rollen](directory-assign-admin-roles.md#deprecated-roles)

## <a name="next-steps"></a>Nächste Schritte

* Weitere Informationen zum Zuweisen eines Benutzers als Administrator eines Azure-Abonnements finden Sie unter [Verwalten des Zugriffs mit Azure-Rollen (Azure RBAC)](../../role-based-access-control/role-assignments-portal.md)
* Informationen zum Steuern des Zugriffs auf Ressourcen in Microsoft Azure finden Sie unter [Grundlegendes zu den verschiedenen Rollen](../../role-based-access-control/rbac-and-directory-admin-roles.md)
* Ausführliche Informationen zur Beziehung zwischen Abonnements und einem Azure AD-Mandanten oder eine Anleitung zum Zuordnen oder Hinzufügen eines Abonnements finden Sie unter [Zuordnen oder Hinzufügen eines Azure-Abonnements zu Ihrem Azure Active Directory-Mandanten](../fundamentals/active-directory-how-subscriptions-associated-directory.md).
