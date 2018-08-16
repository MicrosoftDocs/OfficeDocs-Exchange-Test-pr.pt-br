---
title: 'Configurar o Exchange para o SharePoint eDiscovery Center: Exchange 2013 Help'
TOCTitle: Configurar o Exchange para o SharePoint eDiscovery Center
ms:assetid: 795c1a3b-295c-4ee5-ade9-52cf3fda3f19
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ218665(v=EXCHG.150)
ms:contentKeyID: 50485972
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o Exchange para o SharePoint eDiscovery Center

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

A Microsoft Exchange Server 2013 inclui recursos que funcionam com o Microsoft SharePoint Server 2013 e o Microsoft Lync Server 2013, conhecidos como *aplicativos de parceiros*. Para se certificar de que esses aplicativos de parceiros consigam acessar os recursos um do outro, é necessário configurar a autenticação de servidor para servidor.

Este tópico mostra como configurar a autenticação de servidor-para-servidor entre Exchange 2013 e SharePoint 2013 para que usuários possam usar o Centro de descoberta eletrônica em SharePoint 2013 para pesquisar o conteúdo de caixa de correio Exchange Server 2013. Para ativar completamente essa funcionalidade, você deve concluir as etapas adicionais no SharePoint 2013. Para obter detalhes, consulte [Configurar o eDiscovery no SharePoint 2013](https://go.microsoft.com/fwlink/?linkid=257727).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 30 minutos.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - É suportada a instalação do Exchange 2013 e SharePoint 2013 em diferentes domínios e florestas. Não é necessária uma relação de confiança entre o Windows Exchange e florestas do SharePoint, porque nessa circunstância, o Exchange e o SharePoint contarão com o protocolo OAuth 2.0 para confiar um no outro.

  - O site SharePoint 2013 precisa estar configurado para utilizar SSL (Secure Sockets Layer).

  - O [Exchange Web Services Managed API](https://go.microsoft.com/fwlink/?linkid=257726) deve ser instalado em cada servidor que está executando o SharePoint 2013. Redefina o servidor de informações da Internet (IIS) após a instalação.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Configurar a autenticação de servidor para servidor para o Exchange 2013 em um servidor que executa o SharePoint Server 2013

Execute o comando abaixo para definir o Exchange 2013 como um emissor confiável de token de segurança no SharePoint 2013.

    New-SPTrustedSecurityTokenIssuer -Name Exchange -MetadataEndPoint https://<Exchange Server Name or FQDN>/autodiscover/metadata/json/1

## Etapa 2: Configurar a autenticação de servidor para servidor para o SharePoint 2013 em um servidor que executa o Exchange 2013

Execute esta etapa em um servidor Exchange 2013. Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Aplicativos de parceiros - configurar" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

Execute este comando para configurar o aplicativo de parceiro do SharePoint.

    cd c:\'Program Files'\Microsoft\'Exchange Server'\V15\Scripts
    .\Configure-EnterprisePartnerApplication.ps1 -AuthMetadataUrl <path to SharePoint AuthMetadataUrl> -ApplicationType SharePoint

## Etapa 3: Adicionar usuários autorizados ao grupo de funções Gerenciamento de Descoberta

Adicionar usuários que precisem realizar uma pesquisa de Descoberta Eletrônica usando o SharePoint 2013 ao grupo de funções do Gerenciamento de Descoberta no Exchange 2013. Para obter detalhes, consulte [Atribuir permissões de descoberta eletrônica no Exchange](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md).


> [!CAUTION]
> Adicionar usuários ao grupo de funções Gerenciamento de Descoberta permite que eles utilizem a Descoberta Eletrônica In-loco para pesquisar todas as caixas de correio do Exchange 2013 e acessem conteúdo de e-mail potencialmente confidencial em caixas de correio de usuários. Por padrão, essa permissão não está atribuída a nenhum usuário, incluindo membros da grupo de funções Gerenciamento da Organização. Consulte os departamentos jurídicos ou de recursos humanos da sua organização antes de atribuir essa permissão a um usuário.


