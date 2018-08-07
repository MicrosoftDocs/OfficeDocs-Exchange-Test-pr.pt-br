---
title: 'Domínio do Active Directory está no modo misto : Exchange 2013 Help'
TOCTitle: Domínio do Active Directory é misto mode_PrepareDomainModeMixed
ms:assetid: 97c9f480-7a2b-482e-8f51-f7b965fe1556
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.preparedomainmodemixed(v=EXCHG.150)
ms:contentKeyID: 50486177
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domínio do Active Directory é misto mode\_PrepareDomainModeMixed

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque um domínio existente do Active Directory não estiver definido como modo nativo do Microsoft Windows® ° 2000 Server ou superior.

Instalação do Exchange 2007 irá criar grupos de segurança universais só pode existir no modo nativo do Windows 2000 Server ou melhor, domínios.

Para resolver esse problema, siga estas etapas para aumentar o nível funcional do domínio nível para pelo menos o Windows 2000 Server nativo e, em seguida, execute novamente a instalação do Exchange 2007.

Para aumentar o nível funcional do domínio

1.  Abra domínios do Active Directory e relações de confiança.

2.  Na árvore de console, clique com botão direito no domínio para o qual você deseja elevar funcionalidade e clique em **Aumentar nível funcional do domínio**.

3.  Em **Selecione um nível funcional de domínio disponível**, use um dos seguintes procedimentos:
    
      - Para aumentar o nível funcional do domínio para nativo do Windows 2000 Server, clique em **Windows 2000 nativo** e clique em **aumentar**.
    
      - Para aumentar o nível funcional do domínio para o Windows Server® 2003, clique em **Windows Server 2003** e, em seguida, clique em **Elevar.**


> [!WARNING]
> <BR>Se você tiver ou terão controladores de domínio executando o Windows NT® 4.0 e versões anteriores, não eleve o nível funcional do domínio para nativo do Windows 2000 Server. Depois que o nível funcional do domínio é definido como nativo do Windows 2000 Server, ele não pode ser alterado volta ao servidor do Windows 2000 misto.<BR>Se você tiver ou terão controladores de domínio executando o Windows NT 4.0 e versões anterior ou o Windows 2000 Server, não eleve o nível funcional do domínio para o Windows Server 2003. Após o nível funcional do domínio é definido para o Windows Server 2003, ele não pode ser alterado voltar ao Windows 2000 Server misto ou nativo do Windows 2000 Server.


