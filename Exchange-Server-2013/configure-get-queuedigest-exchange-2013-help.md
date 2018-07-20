---
title: 'Configurar Get-QueueDigest: Exchange 2013 Help'
TOCTitle: Configurar Get-QueueDigest
ms:assetid: f730c520-4ba5-4a15-8846-132bff500bb8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn505733(v=EXCHG.150)
ms:contentKeyID: 59635887
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar Get-QueueDigest

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-12-16_

O cmdlet **Get-QueueDigest** permite que você exiba as informações sobre algumas ou todas as filas na sua organização do Exchange usando somente um comando.

Por padrão, os resultados retornados pelo cmdlet **Get-QueueDigest** são de um a dois minutos atrás. Estes valores são controlados pelas seguintes configurações:

  - **QueueLoggingInterval key in EdgeTransport.exe.config**   Esta chave especifica a frequência com a qual os dados da fila são registrados e está disponível para **Get-QueueDigest**. O valor padrão é `00:01:00` (um minuto). Para especificar um valor, insira-o como um período de tempo: *hh:mm:ss* onde *h* = horas, *m* = minutos, e *s* = segundos. Por padrão, esta chave não está presente no arquivo EdgeTransport.exe.config.

  - **QueueDiagnosticsAggregationInterval parameter on Set-TransportConfig**   Este parâmetro especifica a frequência com a qual os dados da fila são compartilhados entre os servidores de Caixa de Correio. O valor padrão é `00:01:00` (um minuto). Para especificar um valor, insira-o como um período de tempo: *hh:mm:ss* onde *h* = horas, *m* = minutos, e *s* = segundos.

A soma dos valores da chave **QueueLoggingInterval** e do parâmetro *QueueDiagnosticsAggregationInterval* determinam a idade máxima dos resultados retornados por **Get-QueueDigest**.

Além disso, o **Get-QueueDigest** retorna também resultados baseados de formas diferentes no tipo de fila e no status da fila. Por exemplo, as seguintes filas são exibidas nos resultados desde que elas contenham pelo menos uma mensagem:

  - A Fila de envio, a Fila inalcançável e a fila de mensagens suspeitas (filas persistentes).

  - As filas de entrega no estado Suspenso (filas suspensas manualmente por um administrador).

Por padrão, as filas de entrega que possuem o status de Ativa, Conectando, Pronta ou Tente Novamente são retornadas nos resultados somente se a fila tiver 10 ou mais mensagens. O valor é controlado pela chave **QueueLoggingThreshold** no arquivo EdgeTransport.exe.config. Você pode especificar um valor inteiro maior ou menor. Por padrão, esta chave não está presente no arquivo EdgeTransport.exe.config.

## O que você precisa saber antes de começar?

  - Tempo estimado para finalização: 15 minutos

  - Para ver as permissões do Exchange você precisa executar o **Set-TransportConfig** no Shell de Gerenciamento do Exchange, consulte a entrada "Configuração de transporte" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - As permissões do Exchange não são aplicáveis para modificação do arquivo EdgeTransport.exe.config e para reiniciar o serviço Microsoft Exchange Transport. Estes procedimentos são realizados no sistema operacional do Exchange Server.

  - As alterações salvas para o arquivo EdgeTransport.exe.config são aplicadas após você reiniciar o serviço Microsoft Exchange Transport. Quando você reinica o serviço, o fluxo de email no servidor é temporariamente interrompido.

  - Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.

  - As alterações feitas usando o **Set-TransportConfig** afetam todos os servidores de Caixa de Correio da sua organização. As alterações feitas no arquivo EdgeTransport.exe.config afetam somente o servidor local de Caixa de Correio.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Configure o Get-QueueDigest

1.  Em uma janela do Prompt de Comando, abra o arquivo EdgeTransport.exe.config no Bloco de Notas executando o comando a seguir:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Adicione uma ou ambas as chaves a seguir na seção `<appSettings>`.
    
        <add key="QueueLoggingThreshold" value="<integer>" />
        <add key="QueueLoggingInterval" value="<hh:mm:ss>" />
    
    Por exemplo, para definir o valor de **QueueLoggingThreshold** como 1 e o valor de **QueueLoggingInterval** para 30 segundos, use os seguintes valores:
    
        <add key="QueueLoggingThreshold" value="1" />
        <add key="QueueLoggingInterval" value="00:00:30" />

3.  Ao finalizar, salve e feche o arquivo EdgeTransport.exe.config.

4.  Reinicie o serviço Microsoft Exchange Transport executando o comando a seguir:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

5.  Para alterar o valor do parâmetro *QueueDiagnosticsAggregationInterval* no Shell de Gerenciamento do Exchange, use a seguinte sintaxe:
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval <hh:mm:ss>
    
    Por exemplo, para alterar o valor para 30 segundos, execute o comando a seguir:
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval 00:00:30

## Como saber se funcionou?

Para verificar se você configurou com sucesso o **Get-QueueDigest**, faça o seguinte:

1.  Verifique os valores das chaves **QueueLoggingThreshold** e **QueueLoggingInterval** no arquivo EdgeTransport.exe.config. Se as chaves não estiverem presentes, os valores padrões serão usados.

2.  Verifique o valor do parâmetro *QueueDiagnosticsAggregationInterval* executando o comando a seguir:
    
        Get-TransportConfig | Format-List *queue*

