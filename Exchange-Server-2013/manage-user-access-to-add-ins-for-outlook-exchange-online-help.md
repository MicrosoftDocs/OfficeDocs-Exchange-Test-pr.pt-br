---
title: 'Gerenciar o acesso de usuário aos aplicativos para Outlook: Exchange 2013 Help'
TOCTitle: Gerenciar o acesso de usuário aos aplicativos para Outlook
ms:assetid: e5833dec-a23a-439e-ac03-92671817bff8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ943757(v=EXCHG.150)
ms:contentKeyID: 52058898
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar o acesso de usuário aos aplicativos para Outlook

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2018-04-17_

Você pode usar o EAC ou o Exchange Online PowerShell para gerenciar o acesso de usuário aos suplementos do Outlook.

  - Usando o Centro de administração do Exchange (EAC), você pode gerenciar configurações de acesso de suplemento básico para seus usuários em um nível organizacional. Por exemplo, você pode configurar se um suplemento está habilitado ou desabilitado para seus usuários. Você também pode especificar se um suplemento é obrigatório ou opcional para seus usuários.

  - Com o Exchange Online PowerShell, você pode gerenciar todas as configurações que você pode usar com o EAC, bem como outras configurações. Por exemplo, você pode limitar a disponibilidade a usuários específicos na sua organização.

Para tarefas de gerenciamento adicionais, consulte [Aplicativos para Outlook](add-ins-for-outlook-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para saber como usar o Windows PowerShell para se conectar ao Exchange Online, confira o artigo [Conectar-se ao Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Add-ins for Outlook" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Especificar se um suplemento está disponível, habilitado ou desabilitado

## Usar o EAC para especificar se um suplemento está disponível, habilitado ou desabilitado

1.  No EAC, navegue até **organização** \> **suplementos**.

2.  Na exibição de lista, selecione o suplemento que você deseja alterar as configurações para e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Se você não desejar que os usuários usem o suplemento, desmarque a caixa de seleção **tornar este suplemento disponível aos usuários em sua organização** e clique em **Salvar**.

4.  Se desejar que os usuários possam usar o add-in, selecione **tornar este suplemento disponível aos usuários em sua organização** e selecione a opção desejada.
    
      - **Opcional, ativado por padrão**    Use esta configuração se quiser permitir que os usuários desativar o suplemento.
    
      - **Opcional, desativado por padrão**    Use esta configuração se quiser permitir que os usuários ativem o add-in.
    
      - **é obrigatória, sempre habilitada. Os usuários não é possível desabilitar este suplemento** Use esta configuração se não quiser que seus usuários para desativar o suplemento.

5.  Clique em **Salvar**.

## Use o PowerShell do Exchange Online para especificar se um suplemento está disponível, habilitado ou desabilitado

Você pode usar o PowerShell do Exchange Online para especificar se um suplemento está disponível, habilitado ou desabilitado.


> [!TIP]
> Execute o seguinte comando para pesquisar os nomes de exibição e as IDs de suplemento para todos os suplementos do Outlook instalado para sua organização.



    Get-app -Organizationadd-in | Format-List DisplayName,add-inID

Se quiser que um suplemento seja desativado e fique oculto para todos os seus usuários, execute o seguinte comando.

    Set-app <add-in ID> -Organizationadd-in -Enabled $false

Se você deseja que o suplemento a ser habilitada por padrão, mas quer que os usuários possam desativá-lo, execute o seguinte comando.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Enabled

Se você deseja que o suplemento a ser desabilitado por padrão, mas quer que os usuários possam ativá-lo, execute o seguinte comando.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser Disabled

Se quiser que o suplemento seja obrigatório para seus usuários, execute o seguinte comando.

    Set-app <add-in ID> -Organizationadd-in -Enabled $true -DefaultStateForUser AlwaysEnabled

Para detalhadas sobre sintaxe e parâmetros, consulte [Set-App](https://technet.microsoft.com/pt-br/library/jj218630\(v=exchg.150\)).

## Como saber se funcionou?

1.  No EAC, navegue até **organização** \> **suplementos**.

2.  Revise os valores nas colunas **User Default** e **Provided To**.

Ou

1.  A partir do Exchange Online PowerShell, execute `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*`.

2.  Revise os valores de **DefaultStateForUser** e **Enabled**.

## Limitar a disponibilidade a usuários específicos

## Usar o PowerShell do Exchange Online para limitar a disponibilidade a usuários específicos

Se você quiser apenas os membros de seu grupo de distribuição de equipe de Marketing possam usar o suplemento do LinkedIn, execute os seguintes comandos.

    $a = Get-DistributionGroupMember Marketing

    Set-app <add-in ID for the LinkedIn add-in> -Organizationadd-in -ProvidedTo SpecificUsers -UserList $a.Identity -DefaultStateForUser Enabled}

Para detalhadas sobre sintaxe e parâmetros, consulte [Set-App](https://technet.microsoft.com/pt-br/library/jj218630\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se limitou corretamente o acesso a usuários específicos, faça o seguinte:

1.  A partir do Exchange Online PowerShell, execute `Get-app -Organizationadd-in | Format-List DisplayName,add-inId,Enabled,Default*,ProvidedTo,UserList`.

2.  Revise o valor de **ProvidedTo**.

