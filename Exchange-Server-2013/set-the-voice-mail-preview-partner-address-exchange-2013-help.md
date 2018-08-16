---
title: 'Definir o endereço do parceiro de visualização da caixa postal'
TOCTitle: Definir o endereço do parceiro de visualização da caixa postal
ms:assetid: 57fbed1e-1b14-4939-95e6-ef7c072f32a9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff630917(v=EXCHG.150)
ms:contentKeyID: 51407862
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir o endereço do parceiro de visualização da caixa postal

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-13_

É possível definir um endereço de parceiro da Visualização da Caixa Postal em uma política de caixa de correio da UM (Unificação de Mensagens). Após a definição do endereço de parceiro da Visualização da Caixa Postal em uma política de caixa de correio da UM, a configuração será aplicada a todos os usuários habilitados para UM que estiverem vinculados àquela política de caixa de correio.


> [!NOTE]
> Use o Shell para definir um endereço de parceiro da Visualização da Caixa Postal.



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



## Usar o Shell para definir o endereço de parceiro da Visualização da Caixa Postal em uma política de caixa de correio da UM

Este exemplo define o endereço de parceiro da Visualização da Caixa Postal como exumvmp@fabrikam.com em uma política de caixa de correio da UM denominada *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com

