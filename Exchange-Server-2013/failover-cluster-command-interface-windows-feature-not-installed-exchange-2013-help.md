---
title: 'Recurso de Cluster de failover Command Interface Windows não instalado'
TOCTitle: Recurso de Cluster de failover Command Interface Windows não instalado
ms:assetid: 0d839514-5ab7-497d-8945-41392b4c3980
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.rsatclusteringcmdinterfaceinstalled(v=EXCHG.150)
ms:contentKeyID: 51407835
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recurso de Cluster de failover Command Interface Windows não instalado

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2014-12-03_

A Instalação do Microsoft Exchange Server 2013 não pode prosseguir porque o computador local não tem um recurso do Windows necessário. Você precisará instalar esse recurso do Windows para continuar a Instalação do Exchange 2013

Exchange 2013 A instalação exige que o recurso de **Interface de Cluster de Failover do comando** Windows ser instalado no computador antes de continuar a instalação.

Execute este procedimento para instalar o recurso do Windows neste computador. Se o recurso exigir uma reinicialização para concluir a instalação, será necessário sair da Instalação do Exchange 2013, reiniciar e recomeçar a Instalação.


> [!NOTE]
> Talvez seja necessário instalar recursos ou atualizações adicionais do Windows para continuar a Instalação do Exchange 2013. Para obter uma lista completa dos recursos e atualizações exigidos do Windows, confira <A href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</A>.



1.  Abra o Windows PowerShell no computador local.

2.  Execute o seguinte comando para instalar o recurso de Windows necessário.
    
    ```powershell
Install-WindowsFeature RSAT-Clustering-CmdInterface
```

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

