---
title: 'Configurar a autenticação OAuth com o SharePoint 2013 e Lync 2013: Exchange 2013 Help'
TOCTitle: Configurar a autenticação OAuth com o SharePoint 2013 e Lync 2013
ms:assetid: ca3c78a3-80cc-4df2-859f-0106bbd57a07
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ649094(v=EXCHG.150)
ms:contentKeyID: 50486623
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a autenticação OAuth com o SharePoint 2013 e Lync 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-03-03_

Exchange Server 2013 permite que outros aplicativos usem OAuth para autenticar para o Exchange. Os aplicativos devem ser configurados como aplicativos de parceiros no Exchange 2013.

No Exchange 2013, a configuração OAuth com aplicativos de parceiros tais como SharePoint 2013 e Lync Server 2013 é suportada somente ao utilizar o script `Configure-EnterpriseApplication.ps1`. Ao automatizar a tarefa, o script torna mais fácil configurar a autenticação com aplicativos de parceiros e reduz os erros de configuração. Esse script executa as seguintes tarefas:

1.  Configure um aplicativo de parceiro empresarial que auto-reporta tokens OAuth para autenticação com êxito para o Exchange.

2.  Atribui funções RBAC (Role Based Access Control - Controle de Acesso Baseado em Funções) para que aplicativos de parceiros o autorizem a utilizar aplicativos específicos Exchange Web Services.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - O aplicativo de parceiro deve publicar um documento de metadados autenticado para que o Exchange 2013 estabeleça uma confiança direta a esse aplicativo e aceite pedidos de autenticação.

  - Para ver exemplos desse tópico, use o seguinte local padrão do diretório `\Scripts`. `C:\Program Files\Microsoft\Exchange Server\V15\Scripts`.

  - Entrada Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Aplicativos de parceiros - configuração" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Configurar a autenticação OAuth com um aplicativo de parceiro

Esse procedimento usa o script `Configure-EntepririseApplication.ps1` para configurar a autenticação OAuth com aplicativos de parceiros. O acesso aos recursos depende das permissões atribuídas ao aplicativo de parceiro e/ou usuário que ele representa por usar o RBAC.

Depois de configurar a autenticação OAuth do Exchange, o aplicativo de parceiro pode usar os recursos do Exchange 2013. Se o Exchange 2013 também precisa acessar recursos oferecidos por um aplicativo de parceiro, você deve configurar uma autenticação OAuth no aplicativo de parceiro.

Este exemplo configura a autenticação OAuth para SharePoint 2013.

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://sharepoint.contoso.com/_layouts/15/metadata/json/1 -ApplicationType SharePoint

Este exemplo configura a autenticação OAuth para Lync Server 2013.

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://lync.contoso.com/metadata/json/1 -ApplicationType Lync

## Como saber se funcionou?

Para verificar se você configurou com êxito um aplicativo de parceiro empresarial para autenticar para o Exchange 2013, execute o cmdlet [Get-PartnerApplication](https://technet.microsoft.com/pt-br/library/jj218721\(v=exchg.150\)) no Shell para retomar a configuração. Você pode ainda executar o cmdlet [Test-OAuthConnectivity](https://technet.microsoft.com/pt-br/library/jj218623\(v=exchg.150\)) para testar a conectividade OAuth com um aplicativo de parceiro para um usuário.

## Mais informações

  - Em implantações híbridas, você pode usar a autenticação OAuth entre sua organização local do Exchange 2013 e a organização do Exchange Online. Para obter mais informações, consulte [Usando a autenticação OAuth para suportar a Descoberta Eletrônica em uma implantação híbrida do Exchange](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md).

  - Em implantações locais, você pode configurar a autenticação entre servidores entre o Exchange 2013 e o SharePoint 2013 de modo que os administradores e agentes de conformidade possam usar a Central de descoberta eletrônica no SharePoint 2013 para pesquisar caixas de correio do Exchange 2013. Para obter mais informações, consulte [Configurar o Exchange para o SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

