---
title: 'Serviço de disponibilidade no Exchange 2013: Exchange 2013 Help'
TOCTitle: Serviço de disponibilidade no Exchange 2013
ms:assetid: 9722dea2-2bf8-437c-85c0-3ab65b8a07b9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232134(v=EXCHG.150)
ms:contentKeyID: 52058859
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Serviço de disponibilidade no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

O serviço de Disponibilidade do Exchange 2013 torna as informações de disponibilidade acessíveis aos clientes do Microsoft Outlook e do Outlook Web App. O serviço de Disponibilidade melhora o agendamento dos operadores de informações e a experiência de agendamento de reuniões, oferecendo informações de disponibilidade seguras, consistentes e atualizadas.

O Outlook e o Outlook Web App usam o serviço de Disponibilidade para executar as seguintes tarefas:

  - Recuperar informações atuais de disponibilidade nas caixas de correio do Exchange 2013

  - Recuperar informações atuais de disponibilidade nas demais organizações do Exchange 2013

  - Recuperar informações de disponibilidade publicadas nas pastas públicas para as caixas de correio dos servidores que têm versões anteriores do Exchange

  - Exibir o horário de trabalho dos participantes

  - Mostrar sugestões de horário para reuniões

**Sumário**

Overview of the Availability service

Information about away status

Availability service API

Availability service Network Load Balancing

Methods used to retrieve free/busy information

## Visão geral do serviço de Disponibilidade

O serviço de disponibilidade recupera informações de livre/ocupado diretamente a partir da caixa de correio de destino para usuários em Exchange 2013, Exchange 2010 ou Exchange 2007 e pode ser configurado para recuperar informações de disponibilidade para usuários em versões anteriores do Exchange. Para topologias que possuem Exchange 2007, Exchange 2010 ou Exchange 2013 caixas de correio na qual todos os clientes estiverem executando o Outlook 2007 ou superior, o serviço de disponibilidade é usado para recuperar informações de livre/ocupado.

O Outlook usa o serviço de Descoberta Automática do Exchange para obter a URL do serviço de Disponibilidade. Para obter mais informações sobre o serviço de Descoberta Automática, consulte [Serviço de descoberta automática](autodiscover-service-for-exchange-2013.md).

Você pode usar o Shell de Gerenciamento do Exchange para configurar o serviço de Disponibilidade. Você não pode usar o Centro de Administração do Exchange (EAC) para configurar o serviço de Disponibilidade.

## Informações sobre o status de ausência

O serviço de Disponibilidade também fornece acesso a mensagens de respostas automáticas que os usuários enviam quando estão ausentes do escritório ou quando vão permanecer inacessíveis por um período de tempo maior.

Os operadores de informações usam o recurso Respostas Automáticas (que antes era conhecido como Ausência Temporária) no Outlook e no Outlook Web App para alertar outras pessoas quando não estão disponíveis para responder a mensagens de email. Com essa funcionalidade fica mais fácil configurar e gerenciar mensagens de resposta automática para operadores de informações e administradores.

## API do serviço de Disponibilidade

O serviço de Disponibilidade faz parte da interface de programação do Exchange 2013. Ele está disponível como um serviço Web para permitir que desenvolvedores criem ferramentas de terceiros para fins de integração.

## Balanceamento de Carga de Rede do serviço de Disponibilidade

O uso do NLB (Balanceamento de Carga de Rede) em seus servidores de Acesso para Cliente que executam o serviço de Disponibilidade pode melhorar o desempenho e a confiabilidade para seus usuários que confiam nas informações de disponibilidade. O Outlook descobre a URL do serviço de Disponibilidade usando o serviço de Descoberta Automática. Para usar o NLB com o serviço de Disponibilidade, é preciso fazer alterações em sua configuração.

A URL interna é usada na intranet e a URL externa é usada na Internet. Se quiser usar a mesma URL para tráfego interno e externo, verifique se o DNS está configurado corretamente para rotear o tráfego interno diretamente para a URL interna. Verifique também se a URL está acessível interna e externamente. Para que os serviços de Descoberta Automática e Disponibilidade funcionem, o DNS precisa estar configurado para que mail.\<*nome de domínio*\>.com e autodiscover.mail.\<*nome de domínio*\>.com apontem para o IP virtual (VIP) da sua solução de balanceamento de carga, onde \<*nome de domínio*\> é o nome do seu domínio.


> [!NOTE]
> Para obter mais informações, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=45959">Network carga balanceamento Technical Reference</A> e <A href="https://go.microsoft.com/fwlink/p/?linkid=49315">Clusters de balanceamento de carga de rede</A>. Você também pode pesquisar por sites de software de balanceamento de carga de terceiros.



## Métodos usados para recuperar informações de disponibilidade

A tabela a seguir lista os diferentes métodos usados para recuperar informações de disponibilidade em topologias de floresta única diferentes.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Cliente</th>
<th>Caixa de correio recuperando informações de disponibilidade em execução</th>
<th>Caixa de correio de destino em execução</th>
<th>Método de recuperação de disponibilidade</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>O serviço de Disponibilidade lê informações de disponibilidade na caixa de correio de destino.</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>Exchange 2010 ou Exchange 2007</p></td>
<td><p>O serviço de Disponibilidade lê informações de disponibilidade na caixa de correio de destino.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2010 ou Exchange 2007</p></td>
<td><p>Exchange 2003</p></td>
<td><p>O serviço de Disponibilidade estabelece conexões HTTP com o diretório virtual /public da caixa de correio do Exchange 2003.</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 ou Exchange 2007</p></td>
<td><p>Outlook Web App em Exchange 2010 ou Outlook Web Access no Exchange 2007 chama a API de serviço de disponibilidade, que lê as informações de disponibilidade da caixa de correio de destino.</p></td>
</tr>
</tbody>
</table>

