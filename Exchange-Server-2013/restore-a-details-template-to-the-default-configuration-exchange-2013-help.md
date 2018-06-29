---
title: 'Restaurar um modelo de detalhes para a configuração padrão: Exchange 2013 Help'
TOCTitle: Restaurar um modelo de detalhes para a configuração padrão
ms:assetid: 84c5f49b-614d-4f0e-8701-0979a2eb90bf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232102(v=EXCHG.150)
ms:contentKeyID: 50486021
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Restaurar um modelo de detalhes para a configuração padrão

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-12_

O Editor de modelos de detalhes não contém um botão de **Desfazer**, nem é possível usar um atalho de teclado para uma ação de desfazer. Para desfazer uma adição feitas no modelo, você deve usar a tecla DELETE. Para desfazer uma exclusão, você deve reaplicar a configuração. Você também pode reverter às configurações originais saindo do Editor de modelos de detalhes sem salvar suas alterações. Se você quiser desfazer alterações depois de ter salvado, você pode restaurar o modelo. Quando você restaura um modelo, toda a personalização é perdida e o modelo é restaurado para sua configuração original.

Este tópico explica como usar a caixa de ferramentas do Exchange 2013 ou Exchange Shell de gerenciamento para restaurar um modelo de detalhes para sua configuração padrão.

Para saber mais sobre os modelos de detalhes, consulte [Modelos de detalhes](details-templates-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Modelos de detalhes" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use a caixa de ferramentas do Exchange para restaurar um modelo de detalhes para sua configuração padrão

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na **Caixa de ferramentas do Exchange**, clique em **Editor de modelos de detalhes** e, no painel de ações, clique em **Open Tool**.

3.  No **Editor de modelos de detalhes**, no painel de detalhes, selecione o modelo que você deseja restaurar e, em seguida, no painel de ações, clique em **Restaurar**.

4.  Clique em **Sim** para confirmar que você deseja restaurar o modelo para seu estado original. Todas as personalizações serão perdidas.

## Use o Shell para restaurar um modelo de detalhes para sua configuração padrão

Este restaurações de exemplo o inglês dos Estados Unidos contata o modelo de detalhes.

    Restore-DetailsTemplate -Identity "en-US\Contact"

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Restore-DetailsTemplate](https://technet.microsoft.com/pt-br/library/bb125188\(v=exchg.150\)).

