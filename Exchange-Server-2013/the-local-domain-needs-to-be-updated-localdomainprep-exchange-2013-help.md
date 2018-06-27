---
title: 'O domínio local precisa ser updated_LocalDomainPrep: Exchange 2013 Help'
TOCTitle: O domínio local precisa ser updated_LocalDomainPrep
ms:assetid: f33e6785-e85a-495e-a124-ebcb2b763e75
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.localdomainprep(v=EXCHG.150)
ms:contentKeyID: 50486988
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O domínio local precisa ser updated\_LocalDomainPrep

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque o usuário conectado a conta não tem as permissões necessárias para a preparação do domínio.

A instalação do Exchange requer que o usuário que está conectado ao **Setup /PrepareDomain** é executado ser membro dos grupos Administradores de domínio e os administradores de organização do Exchange ou o grupo de administradores de empresa.

Para resolver esse problema, conceder permissões de administrador da organização do Exchange e administradores de domínio de usuário conectado, registrá-los no grupo Administradores de empresa ou faça logon com uma conta que tenha essas permissões e execute novamente o programa de instalação do Exchange 2007.

Para obter mais informações sobre as permissões do Active Directory que são necessários ao Microsoft Exchange, consulte "Trabalhando com o Active Directory permissões no Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

