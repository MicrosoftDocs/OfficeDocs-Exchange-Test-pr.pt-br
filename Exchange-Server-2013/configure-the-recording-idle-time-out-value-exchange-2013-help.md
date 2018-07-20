---
title: 'Configure o valor de tempo limite ocioso de gravação: Exchange 2013 Help'
TOCTitle: Configure o valor de tempo limite ocioso de gravação
ms:assetid: a7fb9a09-fde9-447d-ad2c-95598405e99b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423550(v=EXCHG.150)
ms:contentKeyID: 50486308
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configure o valor de tempo limite ocioso de gravação

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-11_

Você pode especificar o número de segundos de silêncio que o sistema permite quando uma mensagem de voz está sendo registrada antes que a chamada é encerrada. Na maioria das organizações, este valor deve ser definido como o padrão de 5 segundos.

Esse valor pode ser definido de 2 a 10. A definição desse valor muito baixo pode causar o sistema desconectar chamadores antes que eles tiver terminado, deixando suas mensagens de voz. A definição desse valor muito alto permite silencia longas em mensagens de voz.

Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar o valor de tempo limite ocioso de gravação

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Em **configurações**, em **gravação ocioso tempo limite (segundos)**, digite o número em segundos.

5.  Clique em **Salvar**.

## Usar o Shell para configurar o valor de tempo limite ocioso de gravação

Este exemplo define o valor de tempo limite ocioso de gravação como 10 para um plano de discagem de UM chamado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -RecordingIdleTimeout 10

