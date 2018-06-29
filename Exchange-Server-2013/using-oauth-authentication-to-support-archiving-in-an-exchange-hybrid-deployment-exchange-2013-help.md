---
title: 'Usando a autenticação OAuth para suportar o Arquivamento em uma implantação híbrida do Exchange: Exchange 2013 Help'
TOCTitle: Usando a autenticação OAuth para suportar o Arquivamento em uma implantação híbrida do Exchange
ms:assetid: deb882b1-1ae2-40f3-a71c-423fafe3d66a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn689104(v=EXCHG.150)
ms:contentKeyID: 62247362
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usando a autenticação OAuth para suportar o Arquivamento em uma implantação híbrida do Exchange

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Se você estiver em uma implantação híbrida do Exchange 2013 e usar o EOA (Arquivamento do Exchange Online) para Exchange Server, será necessário configurar a autenticação OAuth entre suas organizações local e do Exchange Online após a atualização para a Atualização Cumulativa 5 do Exchange 2013 (CU5). O EOA permite que você tenha um arquivamento baseado em nuvem para os usuários com caixas de correio locais. Nesse cenário, o assistente de MRM (Gerenciamento de Direitos de Mensagem) em seu servidor de caixa de correio local aplica as políticas de arquivamento e move as mensagens automaticamente da caixa de correio de um usuário para o arquivamento com base na nuvem. No Exchange 2013 CU5, ele usa a autenticação OAuth.

Para obter instruções detalhadas sobre a configuração da autenticação OAuth, consulte [Configurar a autenticação OAuth entre organizações do Exchange e do Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## O que é autenticação OAuth?

A autenticação OAuth é um protocolo de autenticação de servidor para servidor que permite que aplicativos autentiquem uns aos outros. Com a autenticação OAuth, as credenciais e senhas do usuário não são transferidas de um computador para outro. Em vez disso, a autenticação e a autorização são baseadas na troca de tokens de segurança. Esses tokens concedem acesso a um conjunto específico de recursos por um período determinado.

Autenticação OAuth geralmente envolve três partes: um servidor de autorização único e os dois territórios que precisam se comunicar umas com as outras. Tokens de segurança são emitidos pelo servidor de autorização (também conhecido como um security token servidor) para os dois territórios que precisam se comunicar; Verifique se estes tokens, que communications provenientes de um realm deve ser confiável para o realm de outro. Ao usar a autenticação OAuth entre uma organização do Exchange no local e o Exchange Online, a função do servidor de autorização é fornecida pelo Serviços de Controle de Acesso (ACS) do Azure Active Directory em sua organização do Office 365. Por exemplo, durante uma pesquisa de descoberta eletrônica entre locais, ACS do Azure Active Directory emite tokens que verificar se um administrador ou responsável de conformidade do Exchange locais organização é capaz de acessar caixas de correio na organização do Exchange Online e vice-versa.

## Configurando a autenticação OAuth para oferecer suporte ao Arquivamento

Conforme indicado anteriormente, consulte [Configurar a autenticação OAuth entre organizações do Exchange e do Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md) para obter instruções de configuração da autenticação OAuth a fim de suportar o Arquivamento em uma implantação híbrida do Exchange.

Se o OAuth não estiver configurado para sua implantação híbrida do Exchange, não será possível usar as políticas de arquivamento para mover os itens automaticamente de uma caixa de correio principal de um usuário em sua organização local para o arquivamento com base em nuvem do usuário no Exchange Online.

## Mais informações

  - Você também precisa configurar a autenticação OAuth para executar pesquisas de Descoberta Eletrônica entre instalações de suas caixas de correio local e baseadas na nuvem em uma única pesquisa de Descoberta Eletrônica. Consulte [Usando a autenticação OAuth para suportar a Descoberta Eletrônica em uma implantação híbrida do Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md).

  - Você também pode configurar a autenticação OAuth para permitir que outros aplicativos, como o SharePoint 2013 e o Lync Server 2013, autentiquem no Exchange 2013. Para obter mais informações, consulte [Configurar a autenticação OAuth com o SharePoint 2013 e Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

  - Você pode configurar a autenticação entre servidores entre o Exchange 2013 e o SharePoint 2013 de modo que os administradores e responsáveis pela conformidade possam usar o Centro de Descoberta Eletrônica no SharePoint 2013 para pesquisar caixas de correio do Exchange 2013. Para obter mais informações, consulte [Configurar o Exchange para o SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

  - Você pode configurar uma implantação híbrida do Exchange usando o Assistente de configuração híbrida no Exchange 2013. Para uma lista de verificação de configuração implantação híbrida personalizada, passo a passo, consulte o [Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=277105).

