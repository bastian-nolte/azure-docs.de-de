---
title: Erstellen einer Sicherung einer Azure Red Hat OpenShift 4-Clusteranwendung mithilfe von Velero
description: Hier erfahren Sie, wie Sie mithilfe von Velero eine Sicherung Ihrer Azure Red Hat OpenShift-Clusteranwendungen erstellen.
ms.service: container-service
ms.topic: article
ms.date: 06/22/2020
author: troy0820
ms.author: b-trconn
keywords: aro, openshift, az aro, red hat, cli
ms.custom: mvc
ms.openlocfilehash: 40a915531aa58567b17a774a15504dc92770479f
ms.sourcegitcommit: 7fe8df79526a0067be4651ce6fa96fa9d4f21355
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87854122"
---
# <a name="create-an-azure-red-hat-openshift-4-cluster-application-backup"></a>Erstellen einer Sicherung einer Azure Red Hat OpenShift 4-Clusteranwendung

In diesem Artikel erfahren Sie, wie Sie Ihre Umgebung für das Erstellen einer Sicherung einer Azure Red Hat OpenShift 4-Clusteranwendung vorbereiten. Sie lernen Folgendes:

> [!div class="checklist"]
> * Einrichten der erforderlichen Komponenten und Installieren der erforderlichen Tools
> * Erstellen einer Azure Red Hat OpenShift 4-Anwendungssicherung

Wenn Sie die CLI lokal installieren und verwenden möchten, müssen Sie für dieses Tutorial mindestens Version 2.6.0 der Azure CLI ausführen. Führen Sie `az --version` aus, um die Version zu ermitteln. Informationen zum Durchführen einer Installation oder eines Upgrades finden Sie bei Bedarf unter [Installieren der Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).

## <a name="before-you-begin"></a>Voraussetzungen

### <a name="install-velero"></a>Installieren von Velero

Führen Sie zum [Installieren](https://velero.io/docs/master/basic-install/) von Velero auf Ihrem System die für Ihr Betriebssystem empfohlenen Schritte aus.

### <a name="set-up-azure-storage-account-and-blob-container"></a>Einrichten eines Azure-Speicherkontos und eines Blobcontainers

In diesem Schritt wird eine Ressourcengruppe außerhalb der Ressourcengruppe des ARO-Clusters erstellt.  Diese Ressourcengruppe ermöglicht die Beibehaltung der Sicherungen und kann Anwendungen in neuen Clustern wiederherstellen.

```bash
AZURE_BACKUP_RESOURCE_GROUP=Velero_Backups
az group create -n $AZURE_BACKUP_RESOURCE_GROUP --location eastus

AZURE_STORAGE_ACCOUNT_ID="velero$(uuidgen | cut -d '-' -f5 | tr '[A-Z]' '[a-z]')"
az storage account create \
    --name $AZURE_STORAGE_ACCOUNT_ID \
    --resource-group $AZURE_BACKUP_RESOURCE_GROUP \
    --sku Standard_GRS \
    --encryption-services blob \
    --https-only true \
    --kind BlobStorage \
    --access-tier Hot

BLOB_CONTAINER=velero
az storage container create -n $BLOB_CONTAINER --public-access off --account-name $AZURE_STORAGE_ACCOUNT_ID
```

## <a name="set-permissions-for-velero"></a>Festlegen von Berechtigungen für Velero

### <a name="create-service-principal"></a>Erstellen eines Dienstprinzipals

Velero benötigt Berechtigungen zum Ausführen von Sicherungen und Wiederherstellungen. Wenn Sie einen Dienstprinzipal erstellen, erteilen Sie Velero die Berechtigung für den Zugriff auf die Ressourcengruppe, die Sie im vorherigen Schritt definiert haben. Mit diesem Schritt wird die Ressourcengruppe des Clusters abgerufen:

```bash
export AZURE_RESOURCE_GROUP=aro-$(az aro show --name <name of cluster> --resource-group <name of resource group> | jq -r '.clusterProfile.domain')
```


```bash
AZURE_SUBSCRIPTION_ID=$(az account list --query '[?isDefault].id' -o tsv)

AZURE_TENANT_ID=$(az account list --query '[?isDefault].tenantId' -o tsv)
```

```bash
AZURE_CLIENT_SECRET=$(az ad sp create-for-rbac --name "velero" --role "Contributor" --query 'password' -o tsv \
--scopes  /subscriptions/$AZURE_SUBSCRIPTION_ID)
AZURE_CLIENT_ID=$(az ad sp list --display-name "velero" --query '[0].appId' -o tsv)

```

```bash
cat << EOF  > ./credentials-velero.yaml
AZURE_SUBSCRIPTION_ID=${AZURE_SUBSCRIPTION_ID}
AZURE_TENANT_ID=${AZURE_TENANT_ID}
AZURE_CLIENT_ID=${AZURE_CLIENT_ID}
AZURE_CLIENT_SECRET=${AZURE_CLIENT_SECRET}
AZURE_RESOURCE_GROUP=${AZURE_RESOURCE_GROUP}
AZURE_CLOUD_NAME=AzurePublicCloud
EOF
```

## <a name="install-velero-on-azure-red-hat-openshift-4-cluster"></a>Installieren von Velero in einem Azure Red Hat OpenShift 4-Cluster

In diesem Schritt wird Velero in einem eigenen Projekt installiert. Darüber hinaus werden die für Sicherungen und Wiederherstellungen mit Velero erforderlichen [benutzerdefinierten Ressourcendefinitionen](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/) installiert. Vergewissern Sie sich, dass Sie bei einem Azure Red Hat OpenShift v4-Cluster angemeldet sind.


```bash
velero install \
--provider azure \
--plugins velero/velero-plugin-for-microsoft-azure:v1.1.0 \
--bucket $BLOB_CONTAINER \
--secret-file ~/path/to/credentials-velero.yaml \
--backup-location-config resourceGroup=$AZURE_BACKUP_RESOURCE_GROUP,storageAccount=$AZURE_STORAGE_ACCOUNT_ID \
--snapshot-location-config apiTimeout=15m \
--velero-pod-cpu-limit="0" --velero-pod-mem-limit="0" \
--velero-pod-mem-request="0" --velero-pod-cpu-request="0"
```

## <a name="create-a-backup-with-velero"></a>Erstellen einer Sicherung mit Velero

Zum Erstellen einer Anwendungssicherung mit Velero müssen Sie den Namespace einschließen, in dem sich diese Anwendung befindet.  Wenn Sie einen Namespace vom Typ `nginx-example` haben und alle Ressourcen in diesem Namespace in die Sicherung einschließen möchten, führen Sie den folgenden Befehl im Terminal aus:

```bash
velero create backup <name of backup> --include-namespaces=nginx-example
```
Sie können den Status der Sicherung überprüfen, indem Sie Folgendes ausführen:

```bash
oc get backups -n velero <name of backup> -o yaml
```

Bei einer erfolgreichen Sicherung wird `phase:Completed` ausgegeben, und die Objekte werden im Container im Speicherkonto gespeichert.

## <a name="next-steps"></a>Nächste Schritte

In diesem Artikel wurde eine Azure Red Hat OpenShift 4-Clusteranwendung gesichert. Es wurde Folgendes vermittelt:

> [!div class="checklist"]
> * Erstellen einer Sicherung einer OpenShift v4-Clusteranwendung mithilfe von Velero


Im nächsten Artikel erfahren Sie, wie Sie eine Wiederherstellung einer Azure Red Hat OpenShift 4-Clusteranwendung erstellen.

* [Erstellen einer Wiederherstellung einer Azure Red Hat OpenShift 4-Clusteranwendung](howto-create-a-restore.md)
