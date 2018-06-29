---
title: 'Instalação do primeiro Exchange server na organização não pode ser delegada: Exchange 2013 Help'
TOCTitle: Instalação do primeiro Exchange server na organização não pode ser delegada
ms:assetid: d451581b-6161-4e95-99f1-03dac8313fae
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.delegatedmailboxfirstinstall(v=EXCHG.150)
ms:contentKeyID: 50486709
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instalação do primeiro Exchange server na organização não pode ser delegada

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2014-11-05_

A Instalação do Microsoft Exchange Server 2013 não pode continuar, pois o usuário conectado não possui as permissões de conta necessárias para instalar o primeiro servidor Exchange 2013 na organização.

Embora a Instalação do Exchange 2013 permita o uso da delegação para instalar funções de servidor sucessivas, a Instalação exige que o usuário conectado seja membro do grupo de segurança de Administradores de Empresa do Windows quando o primeiro servidor Exchange 2013 da organização é instalado. Isso é necessário porque a Instalação do Exchange 2013 cria e configura objetos no contêiner da Organização do Exchange no Active Directory durante a instalação.


> [!TIP]
> Se você não tiver preparado o esquema do Active Directory para o Exchange 2013, o usuário conectado também deverá ser membro do grupo de segurança Administradores de Esquema do Windows. Como alternativa, outro usuário membro do grupo Administradores de Esquema do Windows pode preparar o esquema do Active Directory antes da instalação do Exchange 2013.



Para resolver esse problema, adicione o usuário conectado como membro do grupo de segurança Administradores de Empresa. Ou faça logon em uma conta que seja membro do grupo de segurança Administradores de Empresa. Em seguida, execute novamente a Instalação do Exchange 2013.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

