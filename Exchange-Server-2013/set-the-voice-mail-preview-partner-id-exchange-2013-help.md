---
title: 'Defina a ID de parceiro de visualização da caixa postal: Exchange 2013 Help'
TOCTitle: Defina a ID de parceiro de visualização da caixa postal
ms:assetid: ab98c320-9952-47a7-b141-ddfc2c0ad419
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff630924(v=EXCHG.150)
ms:contentKeyID: 51407894
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Defina a ID de parceiro de visualização da caixa postal

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-13_

Você pode definir uma ID de parceiro de visualização da caixa postal em uma diretiva de caixa de correio de Unificação de mensagens (UM). Depois de configurar o ID de parceiro de visualização da caixa postal em uma diretiva de caixa de correio UM, a configuração se aplicará a todos os usuários habilitados para Unificação de mensagens que são vinculados com essa política de caixa de correio.


> [!TIP]
> Você deve usar o Shell para definir a ID do parceiro de visualização da caixa postal.



Para obter mais informações sobre o programa de parceria de Visualização de Caixa Postal, consulte [Supervisor de visualização de correio de voz](voice-mail-preview-advisor-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a visualização da caixa postal, consulte [Procedimentos de visualização da caixa postal de voz](voice-mail-preview-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o Shell para definir a ID de parceiro de visualização da caixa postal em uma diretiva de caixa de correio UM

Este exemplo define a ID de parceiro de visualização da caixa postal como CON123-2010 em uma diretiva de caixa de correio de UM chamado *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy 
    -VoiceMailPreviewPartnerAssignedID CON123-2010

