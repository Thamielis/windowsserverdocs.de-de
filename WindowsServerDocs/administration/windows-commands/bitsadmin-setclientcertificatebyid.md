---
title: bitsadmin setclientcertificatebyid
description: Referenz Artikel für den Befehl "bizadmin setclientcertificatebyid", der den Bezeichner des Client Zertifikats angibt, das für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung verwendet werden soll.
ms.topic: reference
ms.assetid: 8585a7a1-7472-437b-b04a-a11925782a3a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: aa49c0fc93972ce447c114ec20722afe67ca5dda
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89631029"
---
# <a name="bitsadmin-setclientcertificatebyid"></a>bitsadmin setclientcertificatebyid

Gibt den Bezeichner des Client Zertifikats an, das für die Client Authentifizierung in einer HTTPS-Anforderung (SSL) verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /setclientcertificatebyid <job> <store_location> <store_name> <hexadecimal_cert_id>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| store_location | Gibt den Speicherort eines Systemspeicher an, der zum Nachschlagen des Zertifikats verwendet werden soll, einschließlich:<ul><li>CURRENT_USER</li><li>LOCAL_MACHINE</li><li>CURRENT_SERVICE</li><li>DIENSTE</li><li>BENUTZER</li><li>CURRENT_USER_GROUP_POLICY</li><li>LOCAL_MACHINE_GROUP_POLICY</li><li>LOCAL_MACHINE_ENTERPRISE.</li></ul> |
| store_name | Der Name des Zertifikats Speicher, einschließlich:<ul><li>CA (Zertifizierungsstellen Zertifikate)</li><li>Meine (persönliche Zertifikate)</li><li>Root (Stamm Zertifikate)</li><li>SPC (Software Herausgeber Zertifikat).</li></ul> |
| hexadecimal_cert_id | Eine hexadezimale Zahl, die den Hash des Zertifikats darstellt. |

## <a name="examples"></a>Beispiele

So geben Sie den Bezeichner des Client Zertifikats an, das für die Client Authentifizierung in einer HTTPS (SSL)-Anforderung für den Auftrag mit dem Namen *mydownloadjob*verwendet werden soll:

```
bitsadmin /setclientcertificatebyid myDownloadJob BG_CERT_STORE_LOCATION_CURRENT_USER MY A106B52356D3FBCD1853A41B619358BD
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
