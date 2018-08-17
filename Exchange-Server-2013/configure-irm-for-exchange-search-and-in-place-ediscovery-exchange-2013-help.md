---
title: 'Configurar IRM para Descoberta Eletrônica In-loco e pesquisa do Exchange'
TOCTitle: Configurar o IRM para descoberta eletrônica In-loco e de pesquisa do Exchange
ms:assetid: d96790e9-93ad-4a56-b90f-2dbfa2f2073c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg588319(v=EXCHG.150)
ms:contentKeyID: 50486805
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o IRM para descoberta eletrônica In-loco e de pesquisa do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-16_

No Microsoft Exchange Server 2013, você pode configurar o gerenciamento de direitos de informação (IRM) para que Exchange pesquisa pode indexar mensagens protegidas por IRM.

Quando os membros do grupo de função de gerenciamento de descoberta executam uma pesquisa [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md) , mensagens protegidas por IRM são retornadas nos resultados da pesquisa e copiadas para a caixa de correio de descoberta especificada em uma pesquisa. Além disso, os membros do grupo de funções de gerenciamento de descoberta podem usar Outlook Web App para acessar as mensagens protegidas por IRM que foram copiadas para a caixa de correio de descoberta como resultado de pesquisa de descoberta.


> [!NOTE]  
> Membros do grupo de função de gerenciamento de descoberta não podem acessar mensagens protegidas por IRM exportadas-los de uma caixa de correio de descoberta para outra caixa de correio ou para um arquivo. pst. Mensagens protegidas por IRM em uma caixa de correio de descoberta podem ser acessadas usando Outlook Web App.


Para tarefas de gerenciamento adicionais relacionadas a IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Proteção por direitos" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - IRM deve ser configurado em sua organização Exchange 2013. Para saber mais, consulte [Habilitar ou desabilitar o IRM para mensagens internas](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - A caixa de correio de federação deve ser adicionada ao grupo superusuários Active Directory Rights Management Services (AD RMS). Para saber mais, consulte [Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Você não pode usar o Centro de administração do Exchange (EAC) para configurar o IRM no Exchange pesquisa e descoberta eletrônica In-loco. Você deve usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para configurar o IRM para a pesquisa do Exchange

Este exemplo configura o IRM para permitir que Exchange pesquisa para indexar mensagens protegidas por IRM.


> [!NOTE]
> Por padrão, o parâmetro <EM>SearchEnabled</EM> é definido para <CODE>$true</CODE>. Para desabilitar a indexação de mensagens protegidas por IRM, defina-o para <CODE>$false</CODE>. Desabilitando a indexação das mensagens protegidas por IRM impede que eles sejam retornadas nos resultados da pesquisa quando os usuários pesquisar suas caixas de correio ou gerentes de descoberta usam In-Place eDiscovery.



    Set-IRMConfiguration -SearchEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Use o Shell para configurar o IRM para descoberta eletrônica In-loco

Este exemplo permite que os membros do grupo de função de gerenciamento de descoberta para acessar mensagens protegidas por IRM que residem na caixa de correio de descoberta.


> [!NOTE]  
> Por padrão, o parâmetro <EM>EDiscoverySuperUserEnabled</EM> é definido para <CODE>$true</CODE>. Para desabilitar o acesso às mensagens protegidas por IRM para membros do grupo de função de gerenciamento de descoberta, defina-o para <CODE>$false</CODE>.



    Set-IRMConfiguration -EDiscoverySuperUserEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você configurou o IRM com êxito para a pesquisa do Exchange e descoberta eletrônica In-loco, use o cmdlet **Get-IRMConfigurtaion** para recuperar as informações de configuração do IRM. Para obter um exemplo de como recuperar a configuração do IRM, consulte os [Examples](https://technet.microsoft.com/pt-br/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) em **Get-IRMConfiguration**.

