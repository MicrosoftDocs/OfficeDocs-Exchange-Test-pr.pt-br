---
title: 'Não é possível determinar o nome de site_InvalidADSite o Active Directory: Exchange 2013 Help'
TOCTitle: Não é possível determinar o nome de site_InvalidADSite o Active Directory
ms:assetid: ef96e077-08a0-4108-9f7d-0d61758abcd4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.invalidadsite(v=EXCHG.150)
ms:contentKeyID: 50486963
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não é possível determinar o nome de site\_InvalidADSite o Active Directory

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque este servidor não parece pertencer a um site do serviço de diretório Active Directory® válido.

Instalação do Microsoft Exchange requer que o servidor que é usado para a instalação do Exchange 2007 pertence a um site do Active Directory válido.

Para resolver esse problema, verifique se o servidor local é um membro de um site do Active Directory válido e execute novamente o programa de instalação do Exchange Server 2007.

Você pode usar a opção **/DsGetSite** da ferramenta de linha de comando Nltest.exe para verificar e exibir a associação do site. Para obter mais informações, consulte "Nltest.exe: NLTest Overview" na "Ferramentas e coleção de configurações" da *Referência técnica do Windows Server 2003* ([https://go.microsoft.com/fwlink/?LinkId=27734](https://go.microsoft.com/fwlink/?linkid=27734)).

Para obter mais informações sobre como solucionar problemas do Active Directory, consulte "Solucionando problemas de operações do Active Directory" na *Windows Server 2003: operações* (<https://go.microsoft.com/fwlink/?linkid=68099>).

