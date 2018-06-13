---
title: 'Servidores de transporte de borda com implantações híbridas: Exchange 2013 Help'
TOCTitle: Servidores de transporte de borda com implantações híbridas
ms:assetid: 166b1490-5c56-40df-a17b-e8bb36224fd9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh134662(v=EXCHG.150)
ms:contentKeyID: 50487108
ms.date: 04/26/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servidores de transporte de borda com implantações híbridas

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2018-04-16_

A função opcional de servidor de Transporte de Borda geralmente é implantada em um computador localizado na rede de perímetro de uma organização do Exchange e é projetada para minimizar a superfície de ataque da organização. A função de servidor de Transporte de Borda gerencia todo o fluxo de mensagens voltado para a Internet, que fornece retransmissão SMTP e serviços de host inteligente para os servidores locais internos do Exchange em sua organização.

## Servidores de Transporte de Borda em organizações de implantação híbrida baseadas no Exchange

As organizações do Exchange 2016 que queiram usar os servidores de Transporte de Borda podem optar por implantar servidores de Transporte de Borda que executam a versão mais recente do Exchange 2016, Exchange 2013 ou Exchange 2010. Use os servidores de Transporte de Borda se você não quiser expor servidores internos do Exchange diretamente à Internet. Quando você implanta um servidor de Transporte de Borda em uma implantação híbrida, o Exchange Online se conecta ao seu servidor de Transporte de Borda por meio do serviço do Exchange Online Protection para entregar as mensagens. O servidor de Transporte de Borda entrega então as mensagens para o servidor de Caixa de Correio do Exchange local onde se encontra a caixa de correio do destinatário.


> [!IMPORTANT]
> Não coloque servidores, serviços ou dispositivos que processem ou modifiquem o tráfego SMTP entre os servidores Exchange no local e o Office 365. A proteção do fluxo de emails entre a organização do Exchange no local e o Office 365 depende das informações contidas nas mensagens enviadas entre a organização. Firewalls que permitem o tráfego SMTP através da porta TCP 25 sem modificação são compatíveis. Se um servidor, um serviço ou um dispositivo processar uma mensagem entre a organização do Exchange no local e o Office 365, essa informação será removida. Se isso acontecer, a mensagem não será mais considerada interna da sua organização e estará sujeita a regras de diário, transporte e filtro antispam, bem como a outras políticas que podem não se aplicar a ela.




> [!IMPORTANT]
> Se você tiver outros servidores de Transporte de Borda do Exchange em outros locais que não têm suporte para transporte híbrido, eles não precisarão ser atualizados para dar suporte à implantação híbrida. No entanto, se no futuro você desejar que o EOP se conecte a servidores de Transporte de Borda adicionais para transporte híbrido, eles deverão estar executando a versão mais recente do Exchange 2016, Exchange 2010 ou Exchange 2013.



## Adicionar um servidor Transporte de Borda para uma implantação híbrida

Implantar um servidor de Transporte de Borda em sua organização local quando você configura uma implantação híbrida é opcional. Ao configurar sua implantação híbrida, o assistente de Configuração Híbrida permite que você selecione um ou mais servidores locais e internos do Exchange ou que selecione um ou mais servidores Transporte de Borda locais para manipular o transporte de email híbrido com a organização do Exchange Online.

Quando você adiciona um servidor de Transporte de Borda à sua implantação híbrida, ele se comunica com a EOP em nome dos servidores internos do Exchange. O servidor de Transporte de Borda atua como uma retransmissão entre os servidores internos do Exchange e o EOP para mensagens de saída da organização local para a organização do Exchange Online. O servidor de Transporte de Borda também atua como uma retransmissão entre os servidores internos do Exchange para mensagens de entrada da organização do Exchange Online para a organização local. A segurança de toda a conexão gerenciada anteriormente pelos servidores internos do Exchange é gerenciada agora pelo servidor de Transporte de Borda. A busca de destinatário, as políticas de conformidade e outra inspeção de mensagem continuam sendo feitas nos servidores internos do Exchange.

Ao adicionar um servidor Transporte de Borda à sua implantação híbrida, não é necessário rotear emails enviados através dele entre usuários locais e destinatários na Internet. Somente as mensagens enviadas entre o local e as organizações do Exchange Online são roteadas através do servidor Transporte de Borda.

## Fluxo de mensagens sem um servidor Transporte de Borda

O processo e o diagrama a seguir descrevem o caminho que as mensagens adotam entre uma organização local e o Exchange Online quando não há servidor Transporte de Borda implantado:

1.  As mensagens de entrada da organização local para destinatários na organização do Exchange Online são enviadas de uma caixa de correio em um servidor interno do Exchange.

2.  O servidor do Exchange envia a mensagem diretamente ao EOP.

3.  O EOP entrega a mensagem para a organização do Exchange Online.

As mensagens enviadas da organização do Exchange Online para os destinatários na organização local seguem a rota inversa.

**Fluxo de mensagens em uma implantação híbrida sem um servidor Transporte de Borda implantado**

![Fluxo de mensagens híbridas sem um servidor de Transporte de Borda](images/Hh134662.a95b4d1e-fd4a-4952-b891-22f84c9e71a3(EXCHG.150).png "Fluxo de mensagens híbridas sem um servidor de Transporte de Borda")

## Fluxo de mensagens com um servidor Transporte de Borda

O processo a seguir descreve o caminho que as mensagens adotam entre uma organização local e o Exchange Online quando há um servidor de Transporte de Borda implantado. As mensagens da organização local para destinatários na organização do Exchange são enviadas do servidor interno do Exchange:

1.  As mensagens da organização do local para destinatários na organização Online do Exchange são enviadas de uma caixa de correio em um servidor interno do Exchange.

2.  O servidor do Exchange envia a mensagem para um servidor de Transporte de Borda que executa uma versão com suporte e a versão do Exchange.

3.  O servidor de Transporte de Borda envia a mensagem para o EOP.

4.  O EOP entrega a mensagem para a organização do Exchange Online.

As mensagens enviadas da organização do Exchange Online para os destinatários na organização local seguem a rota inversa.

**Fluxo de mensagens em uma implantação híbrida com um servidor de Transporte de Borda implantado**

![Fluxo de emails híbrido com um servidor de Transporte de Borda](images/Hh134662.821fe099-56f5-4501-8e1a-e184ba07a653(EXCHG.150).png "Fluxo de emails híbrido com um servidor de Transporte de Borda")

