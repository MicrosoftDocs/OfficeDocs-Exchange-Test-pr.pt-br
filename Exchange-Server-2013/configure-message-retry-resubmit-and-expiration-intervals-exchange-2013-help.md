---
title: 'Configurar intervalos de repetição, reenvio e expiração de mensagem: Exchange 2013 Help'
TOCTitle: Configurar intervalos de repetição, reenvio e expiração de mensagem
ms:assetid: 5420124f-aa4c-4702-b493-40a9a7edb786
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998043(v=EXCHG.150)
ms:contentKeyID: 51407859
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar intervalos de repetição, reenvio e expiração de mensagem

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-12-16_

No Microsoft Exchange Server 2013, você pode configurar intervalos de repetição, reenvio e expiração de mensagem no serviço de transporte nos servidores de caixa de correio e nos servidores de transporte de borda. Para obter descrições dessas configurações, consulte [Intervalos de repetição, reenvio e expiração de mensagem](message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Serviço de transporte" e entradas de "Servidor de transporte de borda" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use EdgeTransport.exe.config para configurar a contagem de repetição de falha de fila, o intervalo de repetição de falha de fila, o intervalo de repetição de fila de entrega de caixa de correio e o tempo ocioso máximo antes de reenviar intervalo.

Para configurar a contagem de repetição de falha de fila, o intervalo de repetição de falha de fila, o intervalo de repetição de fila de entrega de caixa de correio e o tempo ocioso máximo até reenviar intervalo você modificar chaves no arquivo de configuração de aplicativo da %ExchangeInstallPath%Bin\\EdgeTransport.exe.config XML no servidor de caixa de correio ou servidor de transporte de borda. Você pode salvar esse arquivo de alterações são aplicadas depois que você reiniciar o serviço de transporte do Microsoft Exchange. Quando você reiniciar esse serviço, o fluxo de emails no servidor é interrompido temporariamente.

1.  Em uma janela de prompt de comando no servidor de caixa de correio ou servidor de transporte de borda, abra o arquivo EdgeTransport.exe.config no bloco de notas executando o seguinte comando:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Localize as chaves a seguir na seção `<appSettings>` .
    
        <add key="QueueGlitchRetryCount" value="<Integer>" />
        <add key="QueueGlitchRetryInterval" value="<hh:mm:ss>" />
        <add key="MailboxDeliveryQueueRetryInterval" value="<hh:mm:ss>" />
        <add key="MaxIdleTimeBeforeResubmit" value="<hh:mm:ss>" />
    
    Este exemplo altera o problema de fila repetir contagem como 6, o intervalo de repetição de falha de fila para 30 segundos, o intervalo de repetição de fila de entrega da caixa de correio para 3 minutos e o tempo ocioso máximo até reenvia final do intervalo de seis horas.
    
        <add key="QueueGlitchRetryCount" value="6" />
        <add key="QueueGlitchRetryInterval" value="00:00:30" />
        <add key="MailboxDeliveryQueueRetryInterval" value="00:03:00" />
        <add key="MaxIdleTimeBeforeResubmit" value="6:00:00" />

3.  Quando tiver terminado, salve e feche o arquivo EdgeTransport.exe.config.

4.  Reinicie o serviço de Transporte do Microsoft Exchange executando o seguinte comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Configurar as tentativas de repetição Falha transitória, o intervalo de repetição de falha transitória e o intervalo de repetição de falha de conexão de saída

As tentativas de repetição Falha transitória Especifica o número de tentativas de conexão serão tentados após as tentativas de conexão controladas pelas chaves `QueueGlitchRetryCount` e `QueueGlitchRetryInterval` tiverem falhado. O número de tentativas de repetição de falha transitória padrão é 6. O intervalo válido de entrada para esse parâmetro é de 0 a 15. Se você definir o número de falha transitória repetir tentativas como 0, a próxima tentativa de conexão é controlada pelo *intervalo de repetição de falha de conexão de saída*.

O intervalo de repetição de falha transitória Especifica o intervalo entre cada tentativa de conexão que é especificado pelo número de tentativas de repetição de falha temporária. No serviço de transporte em um servidor de caixa de correio, o intervalo de repetição de falha transitória padrão é 5 minutos. Em um servidor de transporte de borda, o intervalo de repetição de falha transitória padrão é 10 minutos.

O intervalo de repetição de falha de conexão de saída Especifica o intervalo de repetição de tentativas de conexão de saída que falharam anteriormente. As tentativas de conexão falhou anteriormente são controladas pelas tentativas de repetição Falha transitória e o intervalo de repetição de falha temporária. O valor padrão para a falha de conexão de saída repetir o intervalo em que o transporte de serviço em um servidor de caixa de correio é de 10 minutos. O valor padrão em um servidor de transporte de borda é 30 minutos.

## Usar o EAC para configurar as tentativas de repetição Falha transitória, o intervalo de repetição de falha transitória ou o intervalo de repetição de falha de conexão de saída

1.  No Centro de administração do Exchange (EAC), clique em **servidores** \> **servidores**, selecione o servidor, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição")e, em seguida, clique em **limites de transporte**.

2.  Na seção **repete**, insira um valor para **(segundos) do intervalo de repetição de falha de conexão de saída**, o **(minutos) do intervalo de repetição de falha transitória** ou a **Falha transitória tentativas de repetição**.

3.  Quando você tiver concluído, clique em **Salvar**.

## Usar o Shell para configurar as tentativas de repetição Falha transitória, o intervalo de repetição de falha transitória e o intervalo de repetição de falha de conexão de saída

Use a sintaxe a seguir para configurar as tentativas de repetição Falha transitória, o intervalo de repetição de falha transitória e o intervalo de repetição de falha de conexão de saída no serviço de transporte em um servidor de caixa de correio ou em um servidor de transporte de borda.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

Este exemplo altera os valores a seguir no servidor de caixa de correio chamado Mailbox01: no servidor de transporte de borda Exchange01.

  - O número de tentativas de repetição de falha transitória é definido para 8.

  - O intervalo de repetição de falha transitória é definido como 1 minuto.

  - O intervalo de repetição de falha de conexão de saída é definido como 45 minutos.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!TIP]
> Os parâmetros <EM>TransientFailureRetryCount</EM> e <EM>TransientFailureRetryInterval</EM> também estão disponíveis no cmdlet <STRONG>Set-FrontEndTransportService</STRONG> para o serviço de Front End Transport nos servidores de acesso para cliente.



## Configurar as tentativas de repetição Falha transitória, o intervalo de repetição de falha transitória e o intervalo de repetição de falha de conexão de saída

## Usar o EAC para configurar as tentativas de repetição Falha transitória, o intervalo de repetição de falha transitória e o intervalo de repetição de falha de conexão de saída

1.  No EAC, clique em **servidores** \> **servidores**, selecione o servidor, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição")e, em seguida, clique em **limites de transporte**.

2.  Na seção **repete**, insira um valor para **(segundos) do intervalo de repetição de falha de conexão de saída**, o **(minutos) do intervalo de repetição de falha transitória** ou a **Falha transitória tentativas de repetição**.

3.  Quando você tiver concluído, clique em **Salvar**.

## Usar o Shell para configurar as tentativas de repetição Falha transitória, o intervalo de repetição de falha transitória e o intervalo de repetição de falha de conexão de saída

Use a sintaxe a seguir para configurar as tentativas de repetição Falha transitória, o intervalo de repetição de falha transitória e o intervalo de repetição de falha de conexão de saída no serviço de transporte em um servidor de caixa de correio ou em um servidor de transporte de borda.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

Este exemplo altera os valores a seguir no servidor de caixa de correio chamado Mailbox01: no servidor de transporte de borda Exchange01.

  - O número de tentativas de repetição de falha transitória é definido para 8.

  - O intervalo de repetição de falha transitória é definido como 1 minuto.

  - O intervalo de repetição de falha de conexão de saída é definido como 45 minutos.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!TIP]
> Os parâmetros <EM>TransientFailureRetryCount</EM> e <EM>TransientFailureRetryInterval</EM> também estão disponíveis no cmdlet <STRONG>Set-FrontEndTransportService</STRONG> para o serviço de Front End Transport nos servidores de acesso para cliente.



## Use o Shell para configurar o intervalo de repetição de mensagem

Por padrão, o intervalo de repetição de mensagem é `00:15:00` ou 15 minutos. Recomendamos que você não modifique o valor padrão, a menos que o suporte e atendimento ao cliente Microsoft recomendará a fazer isso.

Use a sintaxe a seguir para definir o intervalo de repetição de mensagem.

    Set-TransportService <ServerIdentity> -MessageRetryInterval <dd.hh:mm:ss>

Este exemplo altera o intervalo de repetição de mensagem como 20 minutos no servidor de caixa de correio chamado Mailbox01.

    Set-TransportService Mailbox01 -MessageRetryInterval 00:20:00

## Definir as configurações de tempo limite DSN de atraso

Você pode usar o EAC ou o Shell para configurar o intervalo de tempo limite de notificação de DSN de atraso. Essa configuração é aplicada somente o servidor de transporte de local. Você só pode usar o Shell para habilitar ou desabilitar o envio de mensagens DSN atraso para remetentes internos e externos. Essas configurações são aplicadas a todos os servidores de transporte na sua organização.


> [!TIP]
> Nos servidores de transporte de Hub Exchange 2007, todos os parâmetros <EM>ExternalDSN*</EM> e <EM>InternalDSN*</EM> estão disponíveis no cmdlet <STRONG>Set-TransportServer</STRONG> , não o cmdlet <STRONG>Set-TransportConfig</STRONG> . Se você tiver quaisquer servidores de transporte de Hub Exchange 2007 em sua organização, você precisará fazer alterações nesses valores usando o cmdlet <STRONG>Set-TransportServer</STRONG> em cada servidor de transporte de Hub Exchange 2007.



## Usar o EAC para configurar o intervalo de tempo limite de notificação do atraso DSN mensagem

1.  No EAC, clique em **servidores** \> **servidores**, selecione o servidor, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição")e, em seguida, clique em **limites de transporte**.

2.  Na seção **notificações**, digite um valor para **Notificar remetente quando a mensagem foi adiada após (horas)**.

3.  Quando você tiver concluído, clique em **Salvar**.

## Use o Shell para configurar o intervalo de tempo limite de notificação do atraso DSN mensagem

Use a sintaxe a seguir para definir o intervalo de repetição de mensagem.

    Set-TransportService <ServerIdentity> -DelayNotificationTimeout <dd.hh:mm:ss>

Este exemplo altera o intervalo de tempo limite de notificação do atraso DSN mensagem como seis horas no servidor de caixa de correio chamado Mailbox01.

    Set-TransportService Mailbox01 -DelayNotificationTimeout 06:00:00

## Usar o Shell para habilitar ou desabilitar o envio de notificações de DSN atraso aos remetentes das mensagens interno ou externo

Use a sintaxe a seguir para definir as configurações de notificação de DSN de atraso.

    Set-TransportConfig -ExternalDelayDSNEnabled <$true | $false> -InternalDelayDSNEnabled <$true |$false>

Este exemplo impede que o envio de mensagens de notificação do atraso DSN para remetentes externos.

    Set-TransportConfig -ExternalDelayDSNEnabled $false

Este exemplo impede que o envio de mensagens de notificação de DSN atraso para remetentes internos.

    Set-TransportConfig -InternalDelayDSNEnabled $false

## Configurar o intervalo de tempo limite de expiração de mensagem

## Usar o EAC para configurar o intervalo de tempo limite de expiração de mensagem

1.  No EAC, clique em **servidores** \> **servidores**, selecione o servidor, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição")e, em seguida, clique em **limites de transporte**.

2.  Na seção de **expiração de mensagem**, digite um valor para **tempo máximo desde o envio de (dias)**.

3.  Quando você tiver concluído, clique em **Salvar**.

## Use o Shell para configurar o intervalo de tempo limite de expiração de mensagem

Para configurar o intervalo de tempo limite de expiração de mensagem, use a seguinte sintaxe.

    Set-TransportService <ServerIdentity> -MessageExpirationTimeout <dd.hh:mm:ss>

Este exemplo altera o intervalo de tempo limite de expiração de mensagem para 4 dias no servidor Exchange chamado Mailbox01.

    Set-TransportService Mailbox01 -MessageExpirationTimeout 4.00:00:00

