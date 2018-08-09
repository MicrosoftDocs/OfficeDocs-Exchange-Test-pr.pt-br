---
title: 'Não há suporte para instalação em contr. de domínio com perm. divididas do AD'
TOCTitle: Não há suporte para a instalação em controladores de domínio com o Active Directory dividir permissões
ms:assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.installondcinadsplitpermissionmode(v=EXCHG.150)
ms:contentKeyID: 50486174
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não há suporte para a instalação em controladores de domínio com o Active Directory dividir permissões

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-11-12_

Microsoft Exchange Server 2013 instalação detectou que você está tentando executar a instalação em um controlador de domínio do Active Directory e uma das opções a seguir for verdadeira:

  - A organização do Exchange já está configurada para divididas permissões do Active Directory.

  - Você selecionou o divididas opção de permissões no Exchange 2013 a instalação do Active Directory.

A instalação do Exchange 2013 em controladores de domínio não é suportada quando a organização do Exchange estiver configurada para divididas permissões do Active Directory.

Se você quiser instalar Exchange 2013 em um controlador de domínio, você deve configurar a organização do Exchange para permissões de divisão de controle de acesso com base da função (RBAC) ou compartilhado.


> [!IMPORTANT]
> Não recomendamos a instalação Exchange 2013 nos controladores de domínio do Active Directory. Para obter mais informações, consulte <A href="installing-exchange-on-a-domain-controller-is-not-recommended-exchange-2013-help.md">Instalando o Exchange em um controlador de domínio não é recomendado</A>.



Se você quiser continuar usando divididas permissões do Active Directory, você deve instalar Exchange 2013 em um servidor membro.

Para obter mais informações sobre a divisão e permissões compartilhadas no Exchange 2013, consulte os tópicos a seguir:

[Compreendendo as permissões de divisão](understanding-split-permissions-exchange-2013-help.md)

[Configure o Exchange 2013 para permissões de divisão](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)

[Configurar o Exchange 2013 para permissões compartilhadas](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

