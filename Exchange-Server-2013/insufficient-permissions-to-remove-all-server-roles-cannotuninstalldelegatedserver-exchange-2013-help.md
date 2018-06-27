---
title: 'Permissões insuficientes para remover todos os roles_CannotUninstallDelegatedServer de servidor: Exchange 2013 Help'
TOCTitle: Permissões insuficientes para remover todos os roles_CannotUninstallDelegatedServer de servidor
ms:assetid: 214ae6f3-15e7-4337-99e8-40f9547c8e0c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.cannotuninstalldelegatedserver(v=EXCHG.150)
ms:contentKeyID: 50485167
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões insuficientes para remover todos os roles\_CannotUninstallDelegatedServer de servidor

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque a falha ao tentar desinstalar todas as funções de servidor.

A instalação do Exchange 2007 requer que o usuário que está conectado ao desinstalar todas as funções de servidor seja um membro do grupo Administradores de empresa ou os grupos de administradores de organização do Exchange.

Para resolver esse problema, conceda permissões de administrador de organização do Exchange do usuário conectado ou registrá-los no grupo Administradores de empresa, ou faça logon com uma conta que tenha essas permissões e execute novamente o programa de instalação do Exchange 2007.

Para obter mais informações sobre as permissões do Active Directory necessária ao Microsoft Exchange, consulte "Trabalhando com o Active Directory permissões no Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

