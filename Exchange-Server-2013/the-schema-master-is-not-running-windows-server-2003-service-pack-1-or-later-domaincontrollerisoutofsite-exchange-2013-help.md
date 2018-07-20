---
title: 'Mestre de esquema não está executando Windows Server 2003 Service Pack 1 ou later_DomainControllerIsOutOfSite: Exchange 2013 Help'
TOCTitle: Mestre de esquema não está executando Windows Server 2003 Service Pack 1 ou later_DomainControllerIsOutOfSite
ms:assetid: 5edbe0b8-7610-4a52-aaaa-38c6a99e7e53
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.domaincontrollerisoutofsite(v=EXCHG.150)
ms:contentKeyID: 50485704
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mestre de esquema não está executando Windows Server 2003 Service Pack 1 ou later\_DomainControllerIsOutOfSite

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque o controlador de domínio atribuída que a função Active Directory directory service esquema mestre, também conhecido como flexíveis operações de mestre único (FSMO), não está executando Microsoft Windows Server 2003 Service Pack 1 (SP1) ou uma versão posterior.

Instalação do Exchange 2007 requer que o controlador de domínio que serve como o esquema FSMO executado Windows Server 2003 SP1 ou posterior.

O FSMO controla todas as atualizações e modificações no esquema do Active Directory.

Para resolver esse problema, execute um ou mais dos seguintes procedimentos:

  - Atualizar o controlador de domínio FSMO para Windows Server 2003 SP1 ou posterior e execute novamente o programa de instalação do Microsoft Exchange.

  - Se houver um controlador de domínio FSMO executando o Microsoft Windows Server 2003 Service Pack 1 (SP1) ou uma versão posterior na organização do Exchange, execute a instalação do Exchange 2007 com o parâmetro /domaincontroller apontando para o controlador de domínio FSMO:
    
    \[*/DomainController*ou */dc\<FQDN of domain controller\>*\]
    
    Use o parâmetro */DomainController* para especificar o controlador de domínio usar para ler e gravar Active Directory durante a instalação. Você pode usar o NetBIOS ou o formato do domínio totalmente qualificado (FQDN) do nome.

Para obter o service pack mais recente para o Windows Server 2003, consulte o "TechCenter do Windows Server" ([https://go.microsoft.com/fwlink/?LinkId=45315](https://go.microsoft.com/fwlink/?linkid=45315)).

Para obter mais informações sobre parâmetros de instalação do Exchange Server 2007, consulte "Como para instalar o Exchange 2007 no modo autônomo" ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)) na documentação do produto Exchange Server 2007.

