---
title: 'Habilitar a funcionalidade anti-spam em servidores de caixa de correio: Exchange 2013 Help'
TOCTitle: Habilitar a funcionalidade anti-spam em servidores de caixa de correio
ms:assetid: 59d22c5e-64bc-4879-8ad1-364862b6ba11
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201691(v=EXCHG.150)
ms:contentKeyID: 50485667
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar a funcionalidade anti-spam em servidores de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-01-23_

No Microsoft Exchange Server 2013, os seguintes agentes antispam estão disponíveis no serviço Transporte nos servidores de caixa de correio, mas não estão instalados por padrão:

  - Agente de Filtro de Conteúdo

  - Agente de ID de Remetente

  - Agente de Filtro por Remetente

  - Agente de análise de protocolo para reputação do remetente

Porém, você pode instalar esses agentes antispam em um servidor de caixa de correio usando um script no Shell de Gerenciamento do Exchange. Geralmente, você instalaria os agentes antispam em um servidor de caixa de correio apenas se sua organização aceitasse todas as mensagens de entrada sem filtragem antispam prévia.


> [!TIP]
> Embora o agente Filtro de Destinatários esteja disponíveis em servidores de caixas de correio, você não deve configurá-lo. Quando um filtro de destinatários, em um servidor de caixas de correio, detecta um destinatário inválido ou bloqueado em uma mensagem contendo outros destinatários válidos, a mensagem é rejeitada. Entretanto, o agente do Filtro de Destinatário é ativado por padrão, e não está configurado para bloquear qualquer destinatário. Para obter mais informações, consulte <A href="manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md">Gerenciar filtragem por destinatário nos servidores de transporte de borda</A>.



O que acontece se você instalar os agentes antispam disponíveis no serviço Transporte em um servidor de caixa de correio, mas também tiver outros agentes antispam operando nas mensagens antes que elas alcancem o servidor de caixa de correio? Por exemplo, e se você tiver um servidor Transporte de Borda na rede de perímetro? Os agentes antispam no servidor de caixa de correio reconhecem os valores de cabeçalhos X do antispam que são adicionados às mensagens por outros agentes antispam do Exchange, e as mensagens que contêm esses cabeçalhos X passam diretamente, sem ser verificadas novamente. Porém, pesquisas de destinatários realizadas pelo agente de Filtro de Destinatários ocorrerão novamente no servidor de caixa de correio.

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configuração de Transporte" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - O agente do Filtro de Conexão e o agente do Filtro de Anexos não estão disponíveis nos servidores de caixa de correio. Eles só estão disponíveis em um servidor de Transporte de Borda. Porém, o agente de Malware só é instalado e habilitado por padrão em um servidor de Caixa de Correio. Para mais informações, consulte [Proteção antimalware](anti-malware-protection-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: usar o Shell para executar o script Install-AntispamAgents.ps1

Execute o seguinte comando:

    & $env:ExchangeInstallPath\Scripts\Install-AntiSpamAgents.ps1

## Como saber se essa etapa funcionou?

Você sabe que essa etapa funcionou quando o script é executado sem erros e pede a você que reinicie o serviço Transporte do Microsoft Exchange.

## Etapa 2: usar o Shell para reiniciar o serviço Transporte do Microsoft Exchange

Execute o seguinte comando:

    Restart-Service MSExchangeTransport

## Como saber se essa etapa funcionou?

Você sabe que essa etapa funcionou quando o serviço Transporte do Microsoft Exchange é reiniciado sem erros.

## Etapa 3: usar o Shell para especificar os servidores SMTP internos na organização

Você precisa especificar os endereços IP dos servidores SMTP internos que devem ser ignorados pelo agente de identificação do remetente. Na verdade, você precisa especificar o endereço IP de pelo menos um servidor SMTP interno. Se o servidor de caixa de correio no qual você está executando os agentes antispam for o único servidor SMTP em sua organização, especifique o endereço IP desse computador.

Para adicionar os endereços IP de servidores SMTP internos sem afetar os valores existentes, execute este comando:

    Set-TransportConfig -InternalSMTPServers @{Add="<ip address1>","<ip address2>"...}

Este exemplo adiciona os endereços de servidor SMTP internos 10.0.1.10 e 10.0.1.11 à configuração de transporte de sua organização.

    Set-TransportConfig -InternalSMTPServers @{Add="10.0.1.10","10.0.1.11"}

## Como saber se essa etapa funcionou?

Para confirmar se você especificou corretamente o endereço IP de pelo menos um servidor SMTP interno, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-TransportConfig | Format-List InternalSMTPServers

2.  Confirme se o endereço IP de pelo menos um servidor SMTP interno válido é exibido.

