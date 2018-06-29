---
title: 'Criar uma política de caixa de correio do Outlook Web App: Exchange 2013 Help'
TOCTitle: Criar uma política de caixa de correio do Outlook Web App
ms:assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335191(v=EXCHG.150)
ms:contentKeyID: 50485308
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma política de caixa de correio do Outlook Web App

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2013-05-30_

Você pode criar uma política de caixa de correio do Outlook Web App para aplicar um conjunto comum de configurações de política. As políticas de caixa de correio do Outlook Web App são úteis para aplicar e padronizar configurações, por exemplo, configurações de anexo, para grupos de usuários específicos.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar esse cmdlet, você precisa ter permissões. Embora todos os parâmetros para este cmdlet estejam listados neste tópico, talvez você não tenha acesso a alguns parâmetros, caso eles não estejam incluídos nas permissões atribuídas a você. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caíxa de correio do Outlook Web App", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar uma política de caixa de correio do Outlook Web App

1.  No EAC, clique em **Permissões** \> **Políticas do Outlook Web App**.

2.  Clique no botão **Nova**.

3.  
    
    Digite um nome para a sua política.

4.  
    
    Use as caixas de seleção para habilitar ou desabilitar recursos. Por padrão, são exibidos os recursos mais comuns. Para ver todos os recursos que podem ser habilitados ou desabilitados, clique em **Mais opções**.
    

    > [!TIP]
    > As configurações de recursos para políticas de caixa de correio do Outlook Web App substituem as configurações de diretório virtual do Outlook Web App. É possível alterar configurações de segmentação para usuários específicos usando o cmdlet <STRONG>Set-CASMailbox</STRONG> no Shell.



5.  Clique em **Salvar** para salvar a política.

## Usar o Shell para criar uma diretiva de caixa de correio do Aplicativo Web Outlook

Este exemplo cria uma política de caixa de correio do Outlook Web App denominada `Policy1`.

  - No Shell, execute o comando a seguir.
    
        New-OwaMailboxPolicy -Name Policy1

Para obter mais informações sobre sintaxe e parâmetros, consulte [New-OwaMailboxPolicy](https://technet.microsoft.com/pt-br/library/dd351067\(v=exchg.150\)). Para obter informações sobre como usar o Shell para configurar uma política de caixa de correio do Outlook Web App, consulte [Set-OwaMailboxPolicy](https://technet.microsoft.com/pt-br/library/dd297989\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se criou com êxito uma política de caixa de correio do Outlook Web App:

  - No EAC, clique em **Permissões** \> **Políticas do Outlook Web App** e procure sua nova política de caixa de correio.

