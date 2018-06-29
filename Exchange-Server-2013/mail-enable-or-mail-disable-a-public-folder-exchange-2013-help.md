---
title: 'Email habilitar ou desabilitar email uma pasta pública: Exchange 2013 Help'
TOCTitle: Email habilitar ou desabilitar email uma pasta pública
ms:assetid: 3d69f76d-ff3c-46c1-b962-6a1baa425d8a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997560(v=EXCHG.150)
ms:contentKeyID: 50485364
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Email habilitar ou desabilitar email uma pasta pública

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-06-15_

Pastas públicas são projetadas para acesso compartilhado e oferecem uma maneira fácil e eficaz de coletar, organizar e compartilhar informações com outras pessoas em seu grupo de trabalho ou organização. Habilitar email de uma pasta pública permite que os usuários postem à pasta pública, enviando uma mensagem de email para ele. Quando uma pasta pública é configurações adicionais habilitados para email se tornam disponíveis para a pasta pública no Exchange admin center (EAC), como endereços de email e cotas de email. No Shell, antes que uma pasta pública que esteja habilitado para email, você use o cmdlet **Set-PublicFolder** para gerenciar todas as respectivas configurações. Depois que a pasta pública está habilitado para email, use cmdlets **Set-MailPublicFolder** e o **Set-PublicFolder** para gerenciar as configurações.

Se desejar que os usuários da Internet para enviar email para uma pasta pública habilitada para email, você precisará definir permissões de adição usando o cmdlet **Add-PublicFolderClientPermission** .

Para conhecer tarefas de gerenciamento adicionais relacionadas ao gerenciamento de pastas públicas, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas, consulte [Procedimentos de pasta pública no Office 365 e Exchange Online](https://technet.microsoft.com/pt-br/library/jj966272\(v=exchg.150\)).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para garantir que os usuários na Internet podem enviar mensagens de email para uma pasta pública habilitada para email, a pasta pública deve ter pelo menos a permissão de acesso de *CreateItems* concedido à conta anônima. Se você deseja saber como fazer isso, confira Permitir que os usuários anônimos para enviar email para uma pasta pública habilitada para email.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pastas públicas" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para habilitar email ou desabilitar email uma pasta pública

1.  Navegue até **Pastas públicas** \> **Pastas públicas**.

2.  Na exibição de lista, selecione a pasta pública que deseja mala-habilitar ou desabilitar de email.

3.  No painel de detalhes, em **configurações de email**, clique em **Habilitar** ou **Desabilitar**.

4.  Uma caixa de aviso exibida perguntando que se você tiver certeza você deseja habilitar ou desabilitar o email para a pasta pública. Clique em **Sim** para continuar.

Se desejar que os usuários externos para enviar emails para essa pasta pública, certifique-se de que executar as etapas em Permitir que os usuários anônimos para enviar email para uma pasta pública habilitada para email.

## Use o Shell para ativar o email de uma pasta pública

Este exemplo habilita para email a pasta pública Help Desk.

    Enable-MailPublicFolder -Identity "\Help Desk"

Os relatórios de pasta pública na pasta pública Marketing habilita para email neste exemplo, mas oculta a pasta das listas de endereços.

    Enable-MailPublicFolder -Identity "\Marketing\Reports" -HiddenFromAddressListsEnabled $True

Se desejar que os usuários externos para enviar emails para essa pasta pública, certifique-se de que executar as etapas em Permitir que os usuários anônimos para enviar email para uma pasta pública habilitada para email.

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Enable-MailPublicFolder](https://technet.microsoft.com/pt-br/library/aa998824\(v=exchg.150\)).

## Use o Shell para desabilitar email uma pasta pública

Este exemplo desabilita para email a Marketing\\Reports de pasta pública.

    Disable-MailPublicFolder -Identity "\Marketing\Reports"

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Disable-MailPublicFolder](https://technet.microsoft.com/pt-br/library/bb123781\(v=exchg.150\)).

## Permitir que usuários anônimos enviar email para uma pasta pública habilitada para email

Você pode usar Outlook ou o Shell para definir permissões em conta de uma pasta pública anônima. Você não pode usar o EAC para definir as permissões da conta anônima.

**Use Outlook para definir permissões para a conta anônima**

1.  Abra Outlook usando uma conta que é recebida permissões de proprietário na pasta pública habilitada para email para que você deseja que usuários anônimos enviar email para.

2.  Navegue até **pastas públicas - \< nome do usuário \>**.

3.  Navegue até a pasta pública que você deseja alterar.

4.  Com o botão direito na pasta pública, clique em **Propriedades** e, em seguida, selecione a guia **permissões**.

5.  Selecione a conta **anônimo**, selecione **criar itens** em **gravação** e clique em **OK**.

**Use o Shell para definir permissões para a conta anônima**

Este exemplo define o `CreateItems` permissão à conta anônimo da pasta pública "Comentário do cliente" habilitados para email.

    Add-PublicFolderClientPermission "\Customer Feedback" -AccessRights CreateItems -User Anonymous

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Add-PublicFolderClientPermission](https://technet.microsoft.com/pt-br/library/bb124743\(v=exchg.150\)).

