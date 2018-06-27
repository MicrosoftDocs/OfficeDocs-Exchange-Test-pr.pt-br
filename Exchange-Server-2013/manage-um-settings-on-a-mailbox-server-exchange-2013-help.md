---
title: 'Gerenciar configurações de Unificação de mensagens em um servidor de caixa de correio: Exchange 2013 Help'
TOCTitle: Gerenciar configurações de Unificação de mensagens em um servidor de caixa de correio
ms:assetid: 6df4853d-21d2-473f-b0ca-ebc996d8794a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998815(v=EXCHG.150)
ms:contentKeyID: 50556219
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMServerPropertiesPropertyPage
ms.translationtype: MT
---

# Gerenciar configurações de Unificação de mensagens em um servidor de caixa de correio

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-11_

Após instalar o servidor de Caixa de Correio que está sendo executado no serviço de Unificação de Mensagens do Microsoft Exchange, você pode configurar várias opções, incluindo o número de chamadas simultâneas, as portas de escuta dos protocolos TCP e TLS, o status e o modo de inicialização da UM.


> [!IMPORTANT]
> Não é necessário que os servidores de Caixa de Correio sejam adicionados a um plano de discagem de Unificação de Mensagens (UM) para que se possa processar chamadas para UM, exceto quando você está integrando UM e Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server. Por padrão, todos os servidores de Caixa de Correio de uma organização estão disponíveis para atender as chamadas recebidas.



Para conhecer tarefas de gerenciamento adicionais relacionadas a Unificação de Mensagens e a servidores de Caixa de Correio, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidor de Caixa de Correio (serviço de UM)" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se o servidor de Caixa de Correio está instalado no mesmo computador que um servidor de Acesso para Cliente ou em um computador separado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o Shell para configurar as propriedades de Unificação de Mensagens em um servidor de Caixa de Correio

Este exemplo remove um servidor de Caixa de Entrada sob o nome `MyMailboxServer` de todos os planos de discagem do protocolo SIP.

    Set-UMService -Identity MyMailboxServer -DialPlans $null

Este exemplo adiciona o servidor de Caixa de Correio sob o nome `MyMailboxServer` para um plano de discagem de UM SIP sob o nome `MySIPDialPlanName` e também define o número máximo de chamadas de voz entrantes

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -MaxCalls 150 

Este exemplo define o modo de inicialização como Duplo em um servidor de Caixa de Correio chamado `MyUMServer`.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -UMStartUpMode -Dual 

## Usar o Shell para exibir as propriedades do servidor de Caixa de Correio

Este exemplo exibe uma lista de todos os servidores de Caixa de Correio.

    Get-UMService

Este exemplo exibe uma lista formatada das propriedades para o servidor de Caixa de Correio sob o nome `MyMailboxServer`.

    Get-UMService -Identity MyMailboxServer | Format-List

