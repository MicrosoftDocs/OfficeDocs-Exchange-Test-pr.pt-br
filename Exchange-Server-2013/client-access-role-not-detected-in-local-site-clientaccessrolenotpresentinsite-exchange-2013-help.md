---
title: 'Função acesso para cliente não detectada no local site_ClientAccessRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: Função acesso para cliente não detectada no local site_ClientAccessRoleNotPresentInSite
ms:assetid: b5bfc6af-9c55-46c0-a293-6078b64e87dd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.clientaccessrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50486453
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Função acesso para cliente não detectada no local site\_ClientAccessRoleNotPresentInSite

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 exibido esse aviso porque não foi detectado um direito de acesso para cliente existente no site do serviço de diretório Active Directory® local.

Você optou por instalar o servidor de caixa de correio função antes de uma instância da função acesso para cliente está instalada no site do Active Directory.

A função de servidor acesso para cliente aceita conexões ao seu servidor Exchange 2007 de uma variedade de clientes diferentes. Clientes de software, como o Microsoft Outlook Express e Eudora usam conexões de POP3 ou IMAP4 para se comunicar com o Exchange server. Clientes de hardware, como os dispositivos móveis, usam o ActiveSync, POP3 ou IMAP4 para se comunicar com o Exchange server.

Se os usuários acessarem suas caixas de entrada usando qualquer cliente que não seja Microsoft Office Outlook®, você deve instalar a função de servidor acesso para cliente em sua organização do Exchange.

Os usuários poderão fazer logon com o Outlook em suas caixas de correio, mas não será possível usar o Outlook Web Access ou dispositivos móveis contra a mesma caixa de correio, até que uma função acesso para cliente esteja presente no site do Active Directory local.

