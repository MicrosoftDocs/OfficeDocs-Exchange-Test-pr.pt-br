---
title: 'Modificar, desabilitar ou remover uma política de compartilhamento'
TOCTitle: Modificar, desabilitar ou remover uma política de compartilhamento
ms:assetid: 714af42d-ca29-4bb4-ac48-f0b3d4fd1c15
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657460(v=EXCHG.150)
ms:contentKeyID: 50485915
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificar, desabilitar ou remover uma política de compartilhamento

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-02-15_

As políticas de compartilhamento permitem que usuários individuais em sua organização do Exchange compartilhem informações de disponibilidade do calendário com outras organizações federadas do Exchange, organizações não federadas do Exchange e usuários individuais da Internet. Durante o curso normal das operações, você pode querer alterar algumas propriedades de políticas de compartilhamento, como modificar regras de compartilhamento, alterar o nível de acesso de disponibilidade, desabilitar temporariamente uma política de compartilhamento ou remover completamente uma política de compartilhamento.

Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md)

Para detalhes sobre como criar uma política de compartilhamento, consulte [Criar uma política de compartilhamento](create-a-sharing-policy-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Calendário e Permissões de Compartilhamento" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para modificar uma política de compartilhamento

1.  Navegue até **organização** \> **compartilhamento**.

2.  Em **Compartilhamento individual**, selecione uma política de compartilhamento e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **política de compartilhamento**, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Em **regra de compartilhamento**, altere as regras de compartilhamento adequadamente. É possível alterar as configurações, como o domínio com que você deseja compartilhar informações e o nível de compartilhamento de compromissos do calendário. Ao finalizar, clique em **salvar** para fechar a caixa de diálogo **regras de compartilhamento**.

5.  Em **política de compartilhamento**, clique em **salvar** para atualizar a política de compartilhamento.

## Usar o EAC para definir uma política de compartilhamento como política de compartilhamento padrão

1.  Navegue até **organização** \> **compartilhamento**.

2.  Em **Compartilhamento Individual**, selecione um compartilhamento de uma política e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **política de compartilhamento**, marque a caixa de seleção **Tornar esta política minha política de compartilhamento padrão**.

4.  Clique em **salvar** para atualizar a política de compartilhamento.

## Usar o EAC para desabilitar uma política de compartilhamento

1.  Navegue até **Organização** \> **Compartilhamento**.

2.  Em **Compartilhamento Individual**, selecione uma política de compartilhamento.

3.  Na coluna **Ativar**, desmarque a caixa de seleção da política de compartilhamento que deseja desativar.

## Usar o EAC para remover uma política de compartilhamento


> [!IMPORTANT]  
> Para que uma política de compartilhamento possa ser removida, antes você deve removê-la de todas as caixas de correio de usuários.



1.  Navegue até **organização** \> **compartilhamento**.

2.  Em **Compartilhamento individual**, selecione uma política de compartilhamento e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

3.  No aviso, clique em **sim** para excluir a política de compartilhamento.

## Usar o Shell para modificar, desabilitar ou remover uma política de compartilhamento

  - Este exemplo modifica a diretiva de compartilhamento Contoso em contoso.com, que é um domínio externo à organização. Essa diretiva permite aos usuários no domínio Contoso exibir informações simples de disponibilidade.
    
    ```powershell
    Set-SharingPolicy -Identity Contoso -Domains 'sales.contoso.com: CalendarSharingFreeBusySimple'
    ```

  - Este exemplo adiciona um segundo domínio à política de compartilhamento Contoso. Ao adicionar um domínio a uma diretiva existente, inclua quaisquer domínios incluídos previamente.
    
    ```powershell
    Set-SharingPolicy -Identity Contoso -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'atlanta.contoso.com: CalendarSharingFreeBusyReviewer', 'beijing.contoso.com: CalendarSharingFreeBusyReviewer'
    ```

  - Este exemplo define a política de compartilhamento Contoso como a política de compartilhamento padrão.
    
    ```powershell
    Set-SharingPolicy -Identity Contoso -Default $True
    ```

  - Este exemplo desabilita a política de compartilhamento Contoso.
    
    ```powershell
    Set-SharingPolicy -Identity "Contoso" -Enabled $False
    ```

  - O primeiro exemplo remove a política de compartilhamento Contoso. O segundo exemplo remove a política de compartilhamento Contoso e suprime a confirmação de que você deseja remover a política.
    
    ```powershell
    Remove-SharingPolicy -Identity Contoso
    ```

    ```powershell
    Remove-SharingPolicy -Identity Contoso -Confirm
    ```

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-SharingPolicy](https://technet.microsoft.com/pt-br/library/dd297931\(v=exchg.150\)) e [Remove-SharingPolicy](https://technet.microsoft.com/pt-br/library/dd351071\(v=exchg.150\)).