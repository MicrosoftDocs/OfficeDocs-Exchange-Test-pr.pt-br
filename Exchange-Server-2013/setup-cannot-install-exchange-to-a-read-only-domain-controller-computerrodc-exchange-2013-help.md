---
title: 'Não é possível instalar o Exchange para um controller_ComputerRODC de domínio somente leitura: Exchange 2013 Help'
TOCTitle: Não é possível instalar o Exchange para um controller_ComputerRODC de domínio somente leitura
ms:assetid: 4934d755-65be-47e2-86b0-6ea1ab148a96
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.computerrodc(v=EXCHG.150)
ms:contentKeyID: 50485524
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não é possível instalar o Exchange para um controller\_ComputerRODC de domínio somente leitura

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar a instalação porque o computador de destino é um controlador de domínio somente leitura (RODC).

Os controladores de domínio somente leitura são um recurso do Active Directory do Windows Server 2008. O RODC é a opção que pode ser instalada em locais remotos que talvez tenham níveis mais baixos de segurança física de instalação de um tipo de controlador de domínio.

A instalação do Exchange requer acesso de gravação para o computador de instalação de destino.

Para resolver esse problema, selecione um computador de instalação de destino que não é designado como um RODC e execute novamente a instalação.

