---
title: 'Configurar o rastreamento de pipeline: Exchange 2013 Help'
TOCTitle: Configurar o rastreamento de pipeline
ms:assetid: 10293c83-2157-474e-840d-942e064a4672
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ916678(v=EXCHG.150)
ms:contentKeyID: 52058789
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o rastreamento de pipeline

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-08_

O rastreamento de pipeline captura cópias de mensagens de email à medida que elas se movimentam pelo pipeline de transporte no serviço Transporte ou no serviço Transporte de Caixa de Correio no servidor de Caixa de Correio ou nos servidores de Transporte de Borda.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão do procedimento: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entradas "Serviço de Transporte" e "Serviço de Transporte de Caixa de Correio" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - O rastreamento de pipeline copia o conteúdo completo de mensagens de email enviadas do endereço de email do remetente. Para evitar exposição indesejada de informações confidenciais, defina permissões de segurança adequadas no local da pasta de rastreamento de pipeline.

  - Não habilite o rastreamento de pipeline por períodos de tempo prolongados. O rastreamento de pipeline cria vários arquivos de instantâneos de mensagem que se acumulam rapidamente. Monitore sempre o espaço disponível em disco quando o rastreamento de pipeline estiver habilitado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Habilitar e configurar o rastreamento de pipeline

## Etapa 1: Use o shell para configurar o endereço de remetente do rastreamento de pipeline

Use a sintaxe a seguir para configurar o endereço do remetente do rastreamento de pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingSenderAddress <SMTPAddress | "<>">

Este exemplo configura o rastreamento de pipeline a fim de capturar instantâneos de todas as mensagens enviadas pelo remetente chris@contoso.com no serviço de Transporte no servidor de Caixa de Correio chamado Mailbox01.

    Set-TransportService Mailbox01 -PipelineTracingSenderAddress chris@contoso.com

Esse exemplo configura o rastreamento de pipeline para fazer a captura de tela de todas as mensagens geradas pelo sistema e recebidas pelo serviço de transporte no servidor de caixas de correio chamado Mailbox2.

    Set-TransportService Mailbox02 -PipelineTracingSenderAddress "<>"


> [!WARNING]
> A configuração do rastreamento de pipeline para capturar todas as mensagens geradas pelo servidor em um serviço de transporte pode colocar uma carga considerável sobre o servidor e consumir rapidamente o espaço em disco disponível. Monitore sempre o espaço disponível em disco quando o rastreamento de pipeline estiver habilitado.



## Etapa 2: (Opcional) Use o Shell para especificar uma pasta de rastreamento de pipeline personalizada

A pasta do rastreamento de pipeline padrão não existe até que você habilite o rastreamento de pipeline, e as mensagens que atendem aos critérios especificados por você usando o parâmetro *PipelineTracingSenderAddress* passam pelo serviço de transporte no servidor. Para o serviço de Transporte em um servidor de Caixa de Correio, o local padrão é `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`. Para o serviço de Transporte de Caixa de Correio em um servidor de Caixa de Correio, o local padrão é `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`. Se você especificar um caminho personalizado, o caminho deverá ser no servidor Exchange local.

Use a sintaxe a seguir para configurar a pasta de rastreamento de pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingPath <LocalFilePath>

Esse exemplo define a pasta de rastreamento de pipeline para o serviço de Transporte no servidor de Caixa de Correio chamado Mailbox01 como D:\\Hub\\Pipeline Tracing.

    Set-TransportService Mailbox01 -PipelineTracingPath "D:\Hub\Pipeline Tracing"

## Etapa 3: Use o shell para ativar o rastreamento de pipeline

Por padrão, o rastreamento de pipeline está desabilitado em todos os servidores do Exchange. Quando você habilita o rastreamento de pipeline, está habilitando o rastreamento de pipeline no serviço de transporte especificado apenas no servidor do Exchange especificado. Antes de habilitar o rastreamento de pipeline, é necessário especificar o endereço do remetente, conforme especificado na Etapa 1.

Use a seguinte sintaxe para ativar o rastreamento de pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $true

Esse exemplo habilita o rastreamento de pipeline no serviço de Transporte no servidor de Caixa de Correio chamado Mailbox01.

    Set-TransportService Mailbox01 -PipelineTracingEnabled $true

## Como saber se funcionou?

Para verificar se você configurou com êxito o rastreamento de pipeline, faça o seguinte:

1.  Execute o seguinte comando:
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracing*

2.  Verifique se os valores exibidos são os valores que você configurou.

3.  Verifique a pasta do rastreamento de pipeline para o serviço Transporte ou o serviço Transporte de Caixa de Correio e verifique se os arquivos de instantâneo de mensagem estão sendo criados na pasta.

## Desabilitar o rastreamento de pipeline

Devido às preocupações de espaço em disco e segurança associadas ao rastreamento de pipeline, o rastreamento de pipeline é uma ação temporária para fins de diagnóstico ou solução de problemas. Sempre que você habilitar o rastreamento de pipeline, lembre-se sempre de desabilitá-lo depois de concluir.

Use a seguinte sintaxe para desabilitar o rastreamento de pipeline.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $false

Esse exemplo desabilita o rastreamento de pipeline no serviço de Transporte no servidor de Caixa de Correio chamado Mailbox01.

    Set-TransportService Mailbox01 -PipelineTracingEnabled $false

## Como saber se funcionou?

Para verificar se você desabilitou com êxito o rastreamento de pipeline, faça o seguinte:

1.  Execute o seguinte comando:
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracingEnabled

2.  Verifique se o valor do parâmetro *PipelineTracingEnabled* é $false.

3.  Verifique a pasta de rastreamento de pipeline e se os arquivos de instantâneo de mensagem não estão mais sendo criados na pasta.

