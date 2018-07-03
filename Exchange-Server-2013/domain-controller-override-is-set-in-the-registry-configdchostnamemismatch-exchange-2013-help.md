---
title: 'Substituição de controlador de domínio está definida no Registry_ConfigDCHostNameMismatch: Exchange 2013 Help'
TOCTitle: Substituição de controlador de domínio está definida no Registry_ConfigDCHostNameMismatch
ms:assetid: 3aef5470-d510-4b59-a4b6-36d274a984ae
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.configdchostnamemismatch(v=EXCHG.150)
ms:contentKeyID: 50485353
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Substituição de controlador de domínio está definida no Registry\_ConfigDCHostNameMismatch

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-15_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque falhou ao tentar usar o controlador de domínio especificado. Um controlador de domínio tenha sido mapeado estaticamente no registro.

A instalação do Exchange 2007 requer que o controlador de domínio especificado no comando setup corresponder o controlador de domínio que tenha sido mapeado estaticamente usando uma substituição de registro.

Para resolver esse problema, execute a instalação novamente, especificando o controlador de domínio estaticamente mapeada para o **/DomainController: \<***FQDN of thestatically mapped domain controller***\>** parâmetro.

Para obter mais informações sobre DSAccess e detecção de serviços de diretório, consulte o artigo da Base de Conhecimento Microsoft 250570, "Diretório Server detecção e DSAccess uso do serviço" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=250570](https://go.microsoft.com/fwlink/?linkid=3052&kbid=250570)).

