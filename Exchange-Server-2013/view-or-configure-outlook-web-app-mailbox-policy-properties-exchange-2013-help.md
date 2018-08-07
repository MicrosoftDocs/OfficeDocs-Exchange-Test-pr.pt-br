---
title: 'Exibir/configurar propriedades de política de cx. correio do Outlook Web App'
TOCTitle: Exibir ou configurar as propriedades de diretiva de caixa de correio do Outlook Web App
ms:assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351097(v=EXCHG.150)
ms:contentKeyID: 50486524
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir ou configurar as propriedades de diretiva de caixa de correio do Outlook Web App

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-04-13_

Depois de criar uma política de caixa de correio Outlook Web App, você pode configurar uma variedade de opções para controlar os recursos disponíveis aos usuários em Outlook Web App. Por exemplo, você pode habilitar ou desabilitar regras de caixa de entrada ou criar uma lista de tipos de arquivo permitidos anexos.

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio do Outlook Web App", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para exibir ou configurar políticas de caixa de correio do Outlook Web App

1.  No EAC, clique em **Permissões** \> **Políticas do Outlook Web App**.

2.  No painel de resultados, clique para selecionar a política de caixa de correio que você deseja exibir ou configurar.

3.  Clique no botão **Editar**.

4.  
    
    Na guia **Geral**, você pode exibir e editar o nome da política.

5.  
    
    Na guia **recursos**, use as caixas de seleção para habilitar ou desabilitar recursos. Por padrão, os recursos mais comuns são exibidos. Para ver todos os recursos que podem ser habilitados ou desabilitados, clique em **mais opções**.
    

    > [!TIP]
    > As configurações de recursos para políticas de caixa de correio do Outlook Web App substituem as configurações de diretório virtual do Outlook Web App. É possível alterar configurações de segmentação para usuários específicos usando o cmdlet <STRONG>Set-CASMailbox</STRONG> no Shell.



6.  
    
    Na guia **Acesso a arquivos**, use as caixas de seleção de **acesso direto a arquivos** para configurar o acesso a arquivo e exibindo as opções para os usuários. Acesso ao arquivo permite que um usuário abrir ou visualizar o conteúdo dos arquivos anexados a uma mensagem de email.
    
    Acesso a arquivos pode ser controlado com base em se um usuário tiver feito logon em um computador público ou particular. A opção para os usuários selecionem o acesso do computador particular ou computador público está disponível somente quando você estiver usando autenticação baseada em formulários. Todos os outros formulários padrão de autenticação de acesso de computador particular.

7.  Na guia **Acesso Offline**, use os botões de opção para configurar a disponibilidade de acesso offline.

8.  Clique em **Salvar** para atualizar a política.

## Use o Shell para configurar políticas de caixa de correio do Outlook Web App

Este exemplo habilita o acesso de calendário na diretiva de caixa de correio padrão.

    Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-OwaMailboxPolicy](https://technet.microsoft.com/pt-br/library/dd297989\(v=exchg.150\)).

## Use o Shell para exibir as políticas de caixa de correio do Outlook Web App

Este exemplo recupera as propriedades de de diretiva de caixa de correio `Executives`Outlook Web App em que a organização `Fabrikam`.

    Get-OwaMailboxPolicy -Identity Fabrikam\Executives

Para obter mais informações sobre sintaxe e parâmetros, consulte [Get-OwaMailboxPolicy](https://technet.microsoft.com/pt-br/library/dd351095\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você teve êxito ao editar uma política de caixa de correio Outlook Web App:

1.  No EAC, clique em **permissões** \> **Políticas do Outlook Web App** e escolha uma diretiva de caixa de correio específico Outlook Web App.

2.  Clique no botão **Editar** para exibir as propriedades da diretiva de caixa de correio.

3.  Clique em **Salvar** ou **Cancelar**, para fechar a página de Propriedades.

