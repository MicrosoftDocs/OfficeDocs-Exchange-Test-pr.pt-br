---
title: 'Configurar serviços de parceiros de visualização da caixa postal para usuários: Exchange 2013 Help'
TOCTitle: Configurar serviços de parceiros de visualização da caixa postal para usuários
ms:assetid: 7bb914ca-5502-4e64-bae5-555034138d8a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff630920(v=EXCHG.150)
ms:contentKeyID: 51407878
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar serviços de parceiros de visualização da caixa postal para usuários

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Você pode configurar um parceiro de visualização da caixa postal em uma diretiva de caixa de correio de Unificação de mensagens (UM). Depois que você configurou a visualização da caixa postal parceiro configurações, como a visualização da caixa postal parceiro ID e a visualização da caixa postal parceiro endereço, em uma diretiva de caixa de correio UM, as configurações que você definir se aplicará a todos os usuários habilitados para Unificação de MENSAGENS que são vinculados com essa política de caixa de correio.


> [!TIP]
> Você deve usar o Shell para configurar um parceiro de visualização da caixa postal.



Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Como fazer isso?

## Etapa 1: Inscrever-se com um serviço de parceiro

Para localizar a lista de parceiros certificados e as instruções detalhadas sobre como se inscrever, consulte [Supervisor de visualização de correio de voz](voice-mail-preview-advisor-exchange-2013-help.md) ou consulte o site da [Microsoft identifique](https://go.microsoft.com/fwlink/p/?linkid=281966) . Depois que você se inscrever, fornecerá o parceiro de visualização da caixa postal é uma ID de parceiro e o endereço SMTP usar para encaminhar as mensagens de voz.

Na etapa 2, você aplicará a ID de parceiro e o endereço SMTP obtido na etapa 1 para as políticas de caixa de correio de Unificação de MENSAGENS necessárias.

## Etapa 2: Definir o parceiro de visualização da caixa postal endereço e ID

Este exemplo define o parceiro de visualização da caixa postal endereço exumvmp@fabrikam.com e a ID de parceiro de visualização da caixa postal para CON123-2010 em uma diretiva de caixa de correio de UM chamado *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com
    -VoiceMailPreviewPartnerAssignedID CON123-2010

## Etapa 3: Configurar visualização da caixa postal parceiro configurações avançadas

Se o parceiro requer configurações personalizadas, convém definir dois parâmetros adicionais para um parceiro de visualização da caixa postal da seguinte maneira:

  - *VoiceMailPreviewPartnerMaxMessageDuration*

  - *VoiceMailPreviewPartnerMaxDeliveryDelay*

Este exemplo define a duração de mensagem máximo para 300 segundos (5 minutos) e o atraso na entrega máximo como 600 segundos (10 minutos) em uma diretiva de caixa de correio UM chamado *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300 -VoiceMailPreviewPartnerMaxDeliveryDelay 600

## Etapa 4: Atribuir um usuário habilitado para a diretiva de caixa de correio de Unificação de MENSAGENS de um parceiro de visualização da caixa postal

Se você deseja configurar o serviço de parceiro de visualização da caixa postal para alguns, mas não todos, usuários habilitados em um UM plano de discagem, você deve criar uma nova política de caixa de correio de Unificação de MENSAGENS e definir as configurações de parceiro. Quando tiver terminado, você pode aplicar a nova política aos usuários selecionados habilitado. Para obter mais informações sobre como atribuir um usuário habilitado para uma diretiva de caixa de correio de UM, consulte os tópicos a seguir:

  - [Atribuir uma política de caixa de correio de Unificação de mensagens](assign-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/pt-br/library/bb124893\(v=exchg.150\))

Para obter mais informações sobre o programa de parceria de Visualização de Caixa Postal, consulte [Supervisor de visualização de correio de voz](voice-mail-preview-advisor-exchange-2013-help.md).

