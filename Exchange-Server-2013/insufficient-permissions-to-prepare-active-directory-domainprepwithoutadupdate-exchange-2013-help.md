---
title: 'Permissões insuficientes para preparar o Active Directory_DomainPrepWithoutADUpdate: Exchange 2013 Help'
TOCTitle: Permissões insuficientes para preparar o Active Directory_DomainPrepWithoutADUpdate
ms:assetid: 4283c4b9-983f-460e-a5de-42b2772eae0d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.domainprepwithoutadupdate(v=EXCHG.150)
ms:contentKeyID: 50485460
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões insuficientes para preparar o Active Directory\_DomainPrepWithoutADUpdate

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque a preparação do domínio tentada falhou.

A instalação do Exchange requer que o serviço de diretório do Active Directory modificadas para o Exchange Server 2007 antes de domínios no Active Directory podem ser preparados.

A conta utilizada para executar o comando **setup /PrepareAD** tem permissões insuficientes para executar esse comando, mesmo que ele apareça deve pertencer ao grupo Administradores de empresa. A conta pode ter expirado.

Para resolver esse problema, verifique se a conta de usuário que fez logon é válida e pertence ao grupo Administradores de empresa ou log com uma conta que tenha essas permissões e execute novamente o **setup /PrepareAD**.

Para obter mais informações sobre como executar o processo de PrepareAD, consulte "Como para preparar e domínios do Active Directory" ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)).

Para obter mais informações sobre as permissões do Active Directory que são necessários ao Microsoft Exchange, consulte "Trabalhando com o Active Directory permissões no Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

