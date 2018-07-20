---
title: 'Função de transporte de Hub não detectada no local site_BridgeheadRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: Função de transporte de Hub não detectada no local site_BridgeheadRoleNotPresentInSite
ms:assetid: f318c947-81a8-4c18-975a-0f1e7868042a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.bridgeheadrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50486995
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Função de transporte de Hub não detectada no local site\_BridgeheadRoleNotPresentInSite

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

A instalação do Microsoft® Exchange Server 2007 exibe esse aviso, porque não foi detectada uma função de servidor de transporte de Hub existente no site do serviço de diretório Active Directory® local.

Você optou por instalar o servidor de caixa de correio função antes de uma instância da função de transporte de Hub está instalada no site do Active Directory.

Serviços de transporte de Hub do Exchange 2007 são implantados dentro do Active Directory da sua organização. Alça de serviços de transporte de Hub, fluxo de todos os emails dentro da organização, aplica regras de roteamento de fluxo de email organizacional e são responsável para entrega de mensagens para a caixa de correio do destinatário.

Os usuários poderão fazer logon em suas caixas de correio, mas o email não pode ser enviado ou recebido deste servidor de caixa de correio até que uma função de transporte de Hub está instalada.

