---
title: 'Defina a duração de mensagem máximo de um parceiro de visualização da caixa postal: Exchange 2013 Help'
TOCTitle: Defina a duração de mensagem máximo de um parceiro de visualização da caixa postal
ms:assetid: 18f928ff-f4cc-4eed-a466-de13388780b3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff630912(v=EXCHG.150)
ms:contentKeyID: 51407842
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Defina a duração de mensagem máximo de um parceiro de visualização da caixa postal

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-13_

É possível definir a duração máxima das mensagens de um parceiro de Visualização da caixa postal em uma política de caixa de correio da UM (Unificação de Mensagens). Após ter definido a duração máxima da mensagem, a configuração será aplicada a todos os usuários habilitados para UM que estão vinculados àquela política de caixa de correio.


> [!TIP]
> Use o Shell para definir a duração máxima de mensagem para um parceiro de Visualização da caixa postal.



Para obter mais informações sobre o programa de parceria de Visualização de Caixa Postal, consulte [Supervisor de visualização de correio de voz](voice-mail-preview-advisor-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas à Visualização da Caixa Postal, consulte [Procedimentos de visualização da caixa postal de voz](voice-mail-preview-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para configurar a duração máxima de mensagem para um parceiro de Visualização da caixa postal

Este exemplo define a duração máxima de mensagem para um parceiro de Visualização da caixa postal como 300 segundos (5 minutos) em uma diretiva de caixa de correio da UM com o nome de *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300

