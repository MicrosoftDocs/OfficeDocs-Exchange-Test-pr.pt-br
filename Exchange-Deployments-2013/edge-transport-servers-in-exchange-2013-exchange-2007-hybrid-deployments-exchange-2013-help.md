---
title: 'Servidores de Transporte de Borda nas implantações híbridas do Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Servidores de Transporte de Borda nas implantações híbridas do Exchange 2013/Exchange 2007
ms:assetid: 4e4d7c19-78b8-44bb-bdff-3ea97ea59a5d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn151300(v=EXCHG.150)
ms:contentKeyID: 54651996
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servidores de Transporte de Borda nas implantações híbridas do Exchange 2013/Exchange 2007

Este tópico está em andamento.  

_**Aplica-se a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Os servidores Transporte de Borda no Microsoft Exchange são implantados na rede de perímetro local da organização. Eles são computadores que não ingressaram em domínios e que lidam com o fluxo de email voltado para a Internet, agindo como retransmissores SMTP e host inteligente para servidores Exchange na sua rede interna.

Organizações do Exchange 2013 que desejam usar os servidores Transporte de Borda com a opção de implantação de servidores Transporte de Borda do Exchange Server 2013 ou servidores Transporte de Borda do Exchange 2010 executando o Service Pack 3 (SP3) para o Exchange 2010. Use os servidores Transporte de Borda se você não deseja expor os serviços internos de caixa de correio ou de acesso para cliente do Exchange 2013 diretamente na Internet.

Saiba mais sobre a função de servidor Transporte de Borda do Exchange 2013 em [Servidores de Transporte de Borda](https://technet.microsoft.com/pt-br/library/bb124701\(v=exchg.150\)).

Saiba mais sobre a Exchange 2010 função servidor Transporte de Borda em [Visão Geral da Função Servidor Transporte de Borda](http://go.microsoft.com/fwlink/p/?linkid=183473).

## Servidores Transporte de Borda em organizações de implantação híbrida baseadas no Exchange 2013

Mensagens roteadas entre as organizações locais e online do Exchange em uma implantação híbrida exigem que o serviço Microsoft Exchange Online Protection (EOP), em nome do Exchange Online, conecte-se diretamente aos servidores Transporte de Borda que executam o Exchange 2013 ou o Exchange 2010 SP3.


> [!IMPORTANT]
> Se você tem outros servidores Transporte de Borda do Exchange 2010 em outros locais que não tratam de transporte híbrido, eles não precisam ser atualizados para o Exchange 2010 SP3. No entanto, se no futuro você desejar que o EOP se conecte a servidores Transporte de Borda adicionais para transporte híbrido, eles deverão ser atualizados com o Exchange 2010SP3 ou para os servidores Transporte de Borda do Exchange 2013.



## Adicionar um servidor Transporte de Borda para uma implantação híbrida

Implantar um servidor Transporte de Borda em sua organização local quando você configura uma implantação híbrida é opcional. Ao configurar sua implantação híbrida, o assistente de Configuração Híbrida permite que você selecione um ou mais servidores de Acesso para Cliente ou de Caixa de Correio para o transporte de mensagens híbrido, ou que selecione um ou mais servidores Transporte de Borda locais para manipular o transporte de mensagens híbrido com a organização do Exchange Online.

Quando você adiciona um servidor Transporte de Borda à sua implantação híbrida, ele se comunica com o EOP em nome dos servidores de caixa de correio e de Acesso para Cliente internos do Exchange 2013. O servidor Transporte de Borda atua como uma retransmissão entre o servidor de caixa de correio local e o EOP para mensagens de saída da organização local para o Exchange Online. O servidor Transporte de Borda também atua como uma retransmissão entre o servidor de Acesso para Cliente local para mensagens de entrada da organização do Exchange Online para a organização local. A segurança de toda a conexão gerenciada anteriormente pelo servidor de Acesso para Cliente é gerenciada agora pelo servidor Transporte de Borda. A busca de destinatário, as políticas de conformidade e outra inspeção de mensagem continuam sendo feitas no servidor de Acesso para Cliente.

## Fluxo de mensagens sem um servidor Transporte de Borda

O processo e diagrama a seguir descrevem o caminho que as mensagens adotam entre uma organização local e o Exchange Online quando não há servidor Transporte de Borda implantado:

1.  As mensagens de saída a partir da organização local para destinatários na organização do Exchange Online são enviadas de uma caixa de correio em um servidor de Caixa de Correio do Exchange 2007 para um servidor Transporte de Hub do Exchange 2007.

2.  O servidor Transporte de Hub do Exchange 2007 envia a mensagem para o servidor de caixa de correio do Exchange 2013.

3.  O servidor de caixa de correio do Exchange 2013 envia a mensagem diretamente para a empresa do EOP do Exchange Online.

4.  O EOP entrega a mensagem para a organização do Exchange Online. Neste exemplo, as funções de servidor Caixa de Correio e Acesso para Cliente são instaladas no mesmo servidor Exchange 2013.

As mensagens enviadas da organização do Exchange Online para os destinatários na organização local seguem a rota inversa.

**Fluxo de mensagens em uma implantação híbrida sem um servidor Transporte de Borda implantado**

![Organização local sem o servidor Edge](images/Dn151300.e7206c51-b61c-41e3-a446-9270f131fbaa(EXCHG.150).png "Organização local sem o servidor Edge")

## Fluxo de mensagens com um servidor Transporte de Borda

O processo a seguir descreve o caminho que as mensagens adotam entre uma organização local e o Exchange Online quando há um servidor Transporte de Borda implantado. As mensagens da organização local para destinatários na organização do Exchange Online são enviadas a partir do servidor de Caixa de Correio do Exchange 2007:

1.  As mensagens de saída a partir da organização local para destinatários na organização do Exchange Online são enviadas de uma caixa de correio em um servidor de Caixa de Correio do Exchange 2007 para um servidor Transporte de Hub do Exchange 2007.

2.  O servidor Transporte de Hub do Exchange 2007 envia a mensagem para o servidor de caixa de correio do Exchange 2013.

3.  O servidor de Caixa de Correio do Exchange 2013 envia a mensagem para um servidor Transporte de Borda do Exchange 2013 ou Exchange 2010 SP3

4.  O servidor Transporte de Borda envia a mensagem para a empresa do EOP do Exchange Online.

5.  O EOP entrega a mensagem para a organização do Exchange Online. Neste exemplo, as funções de servidor Caixa de Correio e Acesso para Cliente são instaladas no mesmo servidor Exchange 2013.

As mensagens enviadas da organização do Exchange Online para os destinatários na organização local seguem a rota inversa.

**Fluxo de mensagens em uma implantação híbrida com um servidor Transporte de Borda do Exchange 2013 ou 2010 SP3 implantado**

![Organização local com o servidor Edge](images/Dn151300.91bf5390-c4d7-4aa9-b911-0c1c559d4365(EXCHG.150).png "Organização local com o servidor Edge")

