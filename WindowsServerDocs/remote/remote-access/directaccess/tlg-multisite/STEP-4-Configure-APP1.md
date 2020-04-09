---
title: Schritt 4 App1 konfigurieren
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 7000e80f-31b1-43c5-b51e-1469d26909e5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8011d85f742ebde5fc2013bb483546133e1618ec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861583"
---
# <a name="step-4-configure-app1"></a>Schritt 4 App1 konfigurieren

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Konfigurieren Sie die statische IPv6-Adressierung und die Gatewayeinstellungen, um App1 den Zugriff auf das Subnetz 2-Corpnet zu aktivieren  
  
- So konfigurieren Sie das Standard Gateway und den DNS-Server Bei der Konfiguration für mehrere Standorte wird der Computer ROUTER1 als Standard Gateway verwendet. Konfigurieren Sie das Standard Gateway auf App1.  
  
## <a name="to-configure-the-default-gateway-and-dns-server"></a>So konfigurieren Sie das Standard Gateway und den DNS-Server  
  
1.  Klicken Sie in der Server-Manager Konsole auf **lokaler Server**, und klicken Sie dann im Bereich **Eigenschaften** neben **verkabelte Ethernet-Verbindung**auf den Link.  
  
2.  Klicken Sie im Fenster **Netzwerkverbindungen** mit der rechten Maustaste auf **verkabelte Ethernet-Verbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaften für verkabelte Ethernet-Verbindung** auf **Internet Protokoll Version 4 (TCP/IPv4)** , und klicken Sie dann auf **Eigenschaften**.  
  
4.  Geben Sie im **Standard Gateway** **10.0.0.254**ein, und geben Sie in **Alternativer DNS-Server** **10.2.0.1 bis**ein, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie im Dialogfeld **Eigenschaften für verkabelte Ethernet-Verbindung** auf **Internet Protokoll Version 6 (TCP/IPv6)** , und klicken Sie dann auf **Eigenschaften**.  
  
6.  Geben Sie unter **Standard Gateway**den Wert **2001: db8:1:: FE ein**. Geben Sie im **alternativen DNS-Server** **2001: db8:2:: 1 ein**, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie im Dialogfeld **Eigenschaften für verkabelte Ethernet-Verbindung** auf **Schließen**, und schließen Sie dann das Fenster **Netzwerkverbindungen** .  
  


