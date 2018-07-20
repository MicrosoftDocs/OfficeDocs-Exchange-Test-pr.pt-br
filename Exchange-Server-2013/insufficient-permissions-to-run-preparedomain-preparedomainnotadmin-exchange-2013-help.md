---
title: 'Permissões insuficientes para executar /PrepareDomain_PrepareDomainNotAdmin: Exchange 2013 Help'
TOCTitle: Permissões insuficientes para executar /PrepareDomain_PrepareDomainNotAdmin
ms:assetid: c33a2bc0-5b07-49b8-a1c1-53baa4933d44
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.preparedomainnotadmin(v=EXCHG.150)
ms:contentKeyID: 50486571
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões insuficientes para executar /PrepareDomain\_PrepareDomainNotAdmin

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque a tentativa de executar o processo de **/PrepareDomain** falhou. O usuário conectado tem permissões insuficientes para executar o processo de **/PrepareDomain**.

A instalação do Exchange 2007 requer que o usuário que está conectado ao executar o processo de **/PrepareDomain** ser membro do grupo Administradores de domínio para o domínio a ser preparado e um membro do grupo Administradores de empresa.

Para resolver esse problema, conceda ao usuário conectado no grupo permissões para o domínio que está sendo preparado Admins de domínio e registrá-los em grupos de administradores de empresa ou faça logon com uma conta que tenha essas permissões e execute novamente o programa de instalação do Exchange 2007.

Para obter mais informações sobre as permissões do Active Directory que são necessários ao Microsoft Exchange, consulte "Trabalhando com o Active Directory permissões no Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

