---
title: 'Configurar manualmente o fluxo de emails do servidor de transporte de borda'
TOCTitle: Configurar manualmente o fluxo de emails do servidor de transporte de borda
ms:assetid: cb4cc165-6c09-44ab-a95f-167ae8ed2485
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn606261(v=EXCHG.150)
ms:contentKeyID: 61183358
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar manualmente o fluxo de emails do servidor de transporte de borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-02-21_

Este tópico descreve os procedimentos para alterar manualmente a configuração do modo de gerenciamento de fluxo de emails pelo Servidor de Transporte de Borda. Esses procedimentos abrangem cenários específicos; a menos que sua organização tenha necessidades específicas para alterar manualmente a configuração, o uso da configuração padrão ao inscrever-se nos servidores de Transporte de Borda é preferido.

**Sumário**

Manually configure Send connectors

Intra-Organization Send Connectors

Create additional Send connectors after Edge subscription

Reasons to suppress automatic creation of Send connectors

Partition mail flow

Route outbound email to a smart host

Configure Send connectors for external relay domains

## Configuração manual dos Conectores de envio

É possível modificar manualmente a configuração de um conector de Envio. Por exemplo, se você precisar direcionar os emails de saída por meio de um host inteligente, é possível suprimir a criação automática de um conector de Envio e configurar manualmente um conector de Envio para a Internet.

## Conectores de Envio dentro da organização

O Conector de Envio dentro da organização é um conector de Envio implícito e oculto que é automaticamente computado pelo Exchange e habilita o serviço de Transporte nos servidores de Caixa de correio na mesma organização para retransmitir mensagens um ao outro sem usar conectores de Envio explícitos. Como há um objeto de configuração com uma associação de site do Active Directory no Active Directory para uma Inscrição de Borda, o conector de Envio dentro da organização também será usado para retransmitir mensagens a esse servidor de Transporte de Borda.

Apenas servidores de Caixa de Correio localizados no site do Active Directory inscrito podem transferir emails diretamente do servidor de Transporte de Borda inscrito ou para ele. Se você tiver uma floresta de vários sites do Active Directory e o Exchange for implantado em mais de um site, os servidores de Caixa de Correio em sites não inscritos direcionarão os emails de saída para o site inscrito. Um servidor de Caixa de Correio no site inscrito direcionará emails de saída para o servidor de Transporte de Borda.

## Criar conectores de Envio adicionais após a Inscrição de Borda

Depois que um servidor de Transporte de Borda é inscrito em um site do Active Directory, os cmdlets de criação e alteração de conectores de Envio no servidor de Transporte de Borda são desabilitados. Se você quiser criar um conector de Envio cujo servidor de origem é o servidor de Transporte de Borda, é possível criar o conector de Envio dentro da organização do Exchange. É possível especificar uma ou mais Inscrições de Borda como o servidor de origem para um conector de Envio. Não é possível especificar os servidores de Caixa de Correio e as Inscrições de Borda como servidores de origem para o mesmo conector de Envio. O conector de Envio será replicado para a instância do AD LDS, no servidor de Transporte de Borda que está configurado como um servidor de origem na próxima vez que os dados de configuração forem sincronizados pelo EdgeSync. Se você listar mais de uma Inscrição de Borda como um servidor de origem, será feito o balanceamento de carga das conexões com esse Conector de Envio entre os servidores de Transporte de Borda inscritos. Os servidores de Transporte de Borda precisam ser inscritos no meso site do Active Directory para que o balanceamento de carga ocorra. Se as Inscrições de Borda em sites diferentes do Active Directory estiverem configuradas como servidores de origem no mesmo conector de Envio, os servidores de Transporte de Borda direcionarão apenas para o servidor de origem mais próximo.

Será necessário criar manualmente os conectores de Envio se:

  - Você suprimiu a criação automática de conectores de Envio da Internet ou de entrada.

  - Você aceitou os domínios em sua organização que estão configurados como domínios de retransmissão externos.

## Motivos para suprimir a criação automática de conectores de Envio

Dependendo da topologia de sua organização do Exchange, você pode decidir suprimir a criação automática de conectores de Envio. Os exemplos a seguir descrevem cenários que exigem a supressão da criação automática de conectores de Envio.

## Partição do fluxo de emails

Se você decidir particionar o processamento de emails de entrada e de saída entre dois servidores de Transporte de Borda, um servidor de Transporte de Borda será responsável pelo processamento do fluxo de emails de saída e um segundo servidor de Transporte de Borda será responsável pelo processamento do fluxo de emails de entrada. Para fazer isso, configure a Inscrição de Borda da seguinte maneira:

  - Para o servidor de Transporte de Borda de saída, execute o seguinte comando no servidor de Caixa de Correio.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $false -CreateInternetSendConnector $true

  - Para o servidor de Transporte de Borda de entrada, execute o seguinte comando no servidor de Caixa de Correio.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $true -CreateInternetSendConnector $false

## Direcionar emails de saída para um host inteligente

Se a sua organização do Exchange direcionar todos os emails de saída por meio de um host inteligente, o conector de Envio criado automaticamente não terá a configuração correta.

Execute o seguinte comando no servidor de Caixa de Correio a fim de suprimir a criação automática do conector de Envio para a Internet.

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInternetSendConnector $false

Depois que o processo de Inscrição de Borda for concluído, crie manualmente um conector de Envio para a Internet. Crie o cnector de Evio dentro da organização do Exchange e selecione a Inscrição de Borda como o servidor de origem para o conector. Selecione o tipo de uso `Custom` e configure um ou mais hosts inteligentes. O novo conector de Envio será replicado para a instância do AD LDS no servidor de Transporte de Borda na próxima vez que o EdgeSync sincronizar os dados de configuração. É possível forçar a sincronização imediata do EdgeSync executando o cmdlet **Start-EdgeSynchronization** em um servidor de Caixa de Correio.

Exemplo: Usar o Shell para configurar um conector de Envio para um servidor de Transporte de Borda inscrito a fim de direcionar mensagens para todos os espaços de endereçamento da Internet por meio de um host inteligente. Execute esta tarefa em um servidor de Caixa de Correio dentro da organização do Exchange, não no servidor de Transporte de Borda.

    New-SendConnector -Name "EdgeSync - Site-A to Internet" -Usage Custom -AddressSpaces SMTP:*;100 -DNSRoutingEnabled $false -SmartHosts 192.168.10.1 -SmartHostAuthMechanism None -SourceTransportServers EdgeSubscriptionName


> [!IMPORTANT]
> Esse exemplo não especifica nenhum mecanismo de autenticação de host inteligente. Verifique se você configurou o mecanismo de autenticação correto e forneça todas as credenciais necessárias ao criar um conector de host inteligente em sua própria organização do Exchange.



## Configurar conectores de Envio para domínios de retransmissão externos

Se você tiver domínios aceitos em sua organização do Exchange que estejam configurados como domínios de retransmissão externos, será necessário criar manualmente um conector de Envio para esses espaços de endereçamento. As mensagens que estão sendo entregues para os domínios de retransmissão externos são retransmitidas pelo servidor de Transporte de Borda. O processo de Inscrição de Borda não cria ou configura automaticamente os conectores de Envio para domínios de retransmissão externos. Portanto, você precisa configurar os conectores de Envio para esses domínios e especificar uma ou mais Inscrições de Borda como o servidor de origem para esses conectores de Envio.

O registro do recurso MX do DNS para um domínio de retransmissão externo resolve para seu servidor de Transporte de Borda. Você pode configurar um conector de Envio que retransmita emails para um domínio de retransmissão externo para usar um host inteligente para fins de direcionamento. Se você configurar o conector de Envio para um domínio de retransmissão externo a fim de usar roteamento de DNS, ocorrerá um loop de roteamento. Para obter mais informações sobre domínios de retransmissão externos, consulte [Domínios aceitos](accepted-domains-exchange-2013-help.md).

Voltar ao Início

