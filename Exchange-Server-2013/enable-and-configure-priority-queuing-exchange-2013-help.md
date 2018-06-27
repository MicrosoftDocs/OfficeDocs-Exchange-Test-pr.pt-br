---
title: 'Habilitar e configurar o enfileiramento prioritário: Exchange 2013 Help'
TOCTitle: Habilitar e configurar o enfileiramento prioritário
ms:assetid: 1975d85d-2f1d-4852-8d19-e74ba4ba3853
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ891104(v=EXCHG.150)
ms:contentKeyID: 51407841
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar e configurar o enfileiramento prioritário

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-12-16_

*Fila de prioridades* é um recurso do Microsoft Exchange Server 2013 que habilita a prioridade de mensagens configurada pelo remetente no Microsoft Outlook ou no Outlook Web Access a fim de influenciar o processamento da mensagem pelo serviço de Transporte no servidor de Caixa de Correio. Quando a fila de prioridades é habilitada, mensagens com Alta prioridade são transmitidas aos seus destinos antes das mensagens com Prioridade normal, e estas são transmitidas antes das que têm Baixa prioridade. Para obter mais informações, consulte [Enfileiramento prioritário](priority-queuing-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Permissões do Exchange não se aplicam aos procedimentos neste tópico. Esses procedimentos são realizados no sistema operacional do Exchange Server.

  - As alterações salvas no arquivo de configuração de aplicativo EdgeTransport.exe.config são aplicadas após a reinicialização do serviço de Transporte do Microsoft Exchange.

  - Quando você reinicia o serviço de Transporte do Microsoft Exchange, o fluxo de mensagens no servidor é temporariamente interrompido.

  - Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Prompt de Comando para habilitar e configurar a fila de prioridades no arquivo EdgeTransport.exe.config

1.  Em uma janela do Prompt de Comando, abra o arquivo de configuração de aplicativo EdgeTransport.exe.config no Bloco de notas executando o seguinte comando:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Localize as chaves a seguir na seção `<appSettings>`.
    
        <add key="PriorityQueuingEnabled" value="false" />
        <add key="MaxPerDomainHighPriorityConnections" value="3" />
        <add key="MaxPerDomainNormalPriorityConnections" value="15" />
        <add key="MaxPerDomainLowPriorityConnections" value="2" />
        <add key="HighPriorityMessageExpirationTimeout" value="8:00:00" />
        <add key="NormalPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="LowPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="HighPriorityDelayNotificationTimeout" value="00:30:00" />
        <add key="NormalPriorityDelayNotificationTimeout" value="4:00:00" />
        <add key="LowPriorityDelayNotificationTimeout" value="8:00:00" />
        <add key="MaxHighPriorityMessageSize" value="250KB" />
    
    Para habilitar a fila de prioridades no serviço de Transporte no servidor de Caixa de Correio, use o seguinte valor:
    
        <add key="PriorityQueuingEnabled" value="true" />
    
    Configure os valores restantes da fila de prioridades ou deixe os valores padrão.

3.  Quando terminar, salve e feche o arquivo EdgeTransport.exe.config.

4.  Reinicie o serviço de Transporte do Microsoft Exchange executando o seguinte comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Como saber se funcionou?

Para verificar se você habilitou e configurou com êxito a fila de prioridades, faça o seguinte:

1.  Verifique se a chave **PriorityQueueinEnabled** no arquivo EdgeTransport.exe.config tem o valor `"true"`.

2.  Use o Outlook para criar uma mensagem de teste de alta prioridade maior do que o valor especificado pela chave **MaxHighPriorityMessageSize**, e verifique se a mensagem chega como uma mensagem de prioridade normal.

3.  Tente confirmar se as mensagens de prioridade mais alta chegam antes das mensagens de prioridade mais baixa enviadas ao mesmo destinatário ou destino. Você pode tentar usar várias caixas de correio para enviar simultaneamente múltiplas mensagens de teste parecidas com valores de prioridade diferentes para o mesmo destinatário.

