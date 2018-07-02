---
title: 'Firewall de cabeçalho: Exchange 2013 Help'
TOCTitle: Firewall de cabeçalho
ms:assetid: 9b148f7b-47a9-4379-a55b-8d5310c1772f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232136(v=EXCHG.150)
ms:contentKeyID: 52058860
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Firewall de cabeçalho

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

No Microsoft Exchange Server 2013, *firewall de cabeçalho* é um mecanismo que remove os campos de cabeçalho específico de mensagens de entrada e saídas. Existem dois tipos diferentes de campos de cabeçalho que são afetados pelo firewall de cabeçalho:

  - **Cabeçalhos X**   Um *cabeçalho X* é um campo de cabeçalho não oficiais, definido pelo usuário. X-cabeçalhos não são especificamente mencionados na RFC 2822, mas o uso de um campo de cabeçalho indefinido começando com **X-** tornou-se uma maneira aceita para adicionar campos de cabeçalho não oficiais a uma mensagem. Mensagens de aplicativos, como o antispam, antivírus e mensagens de servidores podem adicionar seus próprios cabeçalhos X a uma mensagem. No Exchange, os campos de cabeçalho X contêm detalhes sobre as ações que são executadas na mensagem pelo serviço de transporte, como o nível de confiança de spam (SCL), os resultados e status de processamento das regras de filtragem de conteúdo. Revelar essas informações a fontes não autorizadas poderia representar um risco de segurança.

  - **Cabeçalhos de roteamento**   Cabeçalhos de roteamento são campos de cabeçalho SMTP padrão que são definidos no RFC 2821 e no RFC 2822. Cabeçalhos de roteamento carimbar uma mensagem usando informações sobre os servidores de mensagens diferentes que foram usadas para entregar a mensagem ao destinatário. Cabeçalhos de roteamento que são inseridos nas mensagens por usuários mal-intencionados podem falsificar o caminho de roteamento que uma mensagem percorrida para acessar um destinatário.

Firewall de cabeçalho impede a falsificação desses cabeçalhos X relacionados ao Exchange por removê-los de mensagens de entrada que entram na organização do Exchange de fontes não confiáveis. Firewall de cabeçalho impede a divulgação desses cabeçalhos X relacionados ao Exchange por removê-los de mensagens de saída enviadas a destinos não confiáveis fora da organização do Exchange. O firewall de cabeçalho também impede a falsificação de cabeçalhos de roteamento padrão que são usados para controlar o histórico de roteamento de uma mensagem.

**Sumário**

Campos de cabeçalho de mensagem afetados pelo firewall de cabeçalho no Exchange

Como o firewall do cabeçalho é aplicada para conectores de recebimento e conectores de envio

Firewall de cabeçalho para mensagens de entrada nos conectores de recebimento

Firewall de cabeçalho para mensagens de saída nos conectores de envio

Firewall de cabeçalho para outras fontes de mensagem

X-cabeçalhos da organização e da floresta cabeçalhos X no Exchange

## Campos de cabeçalho de mensagem afetados pelo firewall de cabeçalho no Exchange

Os seguintes tipos de cabeçalhos X e cabeçalhos de roteamento são afetados pelo firewall de cabeçalho:

  - **X-cabeçalhos da organização**   Esses campos de cabeçalho X começam com **X-MS-Exchange-Organization-**.

  - **X-cabeçalhos de floresta**   Esses campos de cabeçalho X começam com **X-MS-Exchange-Forest-**.
    
    Para obter exemplos de organização cabeçalhos X e X cabeçalhos de floresta, consulte a seção X-cabeçalhos da organização e da floresta cabeçalhos X no Exchange no final deste tópico.

  - **Received: cabeçalhos de roteamento**   Uma instância diferente do campo cabeçalho é adicionada ao cabeçalho da mensagem por cada servidor de mensagens que são aceitos e encaminhadas a mensagem ao destinatário. O cabeçalho **Received:**  normalmente inclui o nome do servidor de mensagens e um carimbo de data-hora.

  - **Reenviadas-\*: cabeçalhos de roteamento**   Reenviadas cabeçalho campos são campos de cabeçalho informativos que podem ser usados para determinar se uma mensagem foi encaminhada por um usuário. Os campos de cabeçalho resent a seguir estão disponíveis: **Resent-Date:** , **Resent-From:** , **Resent-Sender:** , **Resent-To:** , **Resent-Cc:** , **Resent-Bcc:** e **Resent-Message-ID:** . Os campos **Resent-** são usados para que a mensagem é exibida para o destinatário como se ele foi enviado diretamente pelo remetente original. O destinatário pode exibir o cabeçalho da mensagem para descobrir quem encaminhou a mensagem.

O Exchange usa duas maneiras diferentes para aplicar o firewall de cabeçalho a organização cabeçalhos X, cabeçalhos X e roteamento cabeçalhos que existem em mensagens de floresta:

  - As permissões são atribuídas a conectores de envio ou conectores que podem ser usados para preservar ou remover tipos específicos de cabeçalhos em mensagens quando a mensagem é encaminhado por meio do conector de recebimento.

  - Firewall de cabeçalho automaticamente é implementado para tipos específicos de cabeçalhos em mensagens durante outros tipos de envio da mensagem.

Voltar ao início

## Como o firewall do cabeçalho é aplicada para conectores de recebimento e conectores de envio

Firewall de cabeçalho é aplicado às mensagens que viajam através de conectores de envio e conectores com base nas permissões específicas que são atribuídas aos conectores de recebimento.

Se a permissão é atribuída ao conector de recebimento ou o conector de envio, firewall de cabeçalho não será aplicada às mensagens que viajam através do conector. Os campos de cabeçalho afetados são preservados nas mensagens.

Se a permissão não é atribuído ao conector de recebimento ou o conector de envio, firewall de cabeçalho é aplicada às mensagens que viajam através do conector. Os campos de cabeçalho afetados serão removidos das mensagens.

A tabela a seguir descreve as permissões nos conectores de envio e conectores de recebimento que são usados para aplicar o firewall de cabeçalho e os campos de cabeçalho afetado.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de conector</th>
<th>Permissão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Conector de recebimento</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong></p></td>
<td><p>Esta permissão afeta os campos de cabeçalho X da organização que começam com <strong>X-MS-Exchange-Organization-</strong> em mensagens de entrada.</p></td>
</tr>
<tr class="even">
<td><p>Conector de recebimento</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><p>Esta permissão afeta os campos de cabeçalho X floresta que começam com <strong>X-MS-Exchange-Forest-</strong> em mensagens de entrada.</p></td>
</tr>
<tr class="odd">
<td><p>Conector de recebimento</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Esta permissão afeta <strong>Received:</strong> e <strong>Resent-*:</strong> campos de cabeçalho nas mensagens de entrada de roteamento.</p></td>
</tr>
<tr class="even">
<td><p>Conector de envio</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong></p></td>
<td><p>Esta permissão afeta os campos de cabeçalho X da organização que começam com <strong>X-MS-Exchange-Organization-</strong> em mensagens de saída.</p></td>
</tr>
<tr class="odd">
<td><p>Conector de envio</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><p>Esta permissão afeta os campos de cabeçalho X floresta que começam com <strong>X-MS-Exchange-Forest-</strong> em mensagens de saída.</p></td>
</tr>
<tr class="even">
<td><p>Conector de envio</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Esta permissão afeta <strong>Received:</strong> e <strong>Resent-*:</strong> roteamento campos de cabeçalho nas mensagens de saída.</p></td>
</tr>
</tbody>
</table>


## Firewall de cabeçalho para mensagens de entrada nos conectores de recebimento

A tabela a seguir descreve o aplicativo padrão das permissões de firewall de cabeçalho nos conectores de recebimento.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Permissão</th>
<th>Entidades de segurança do Exchange padrão que possuem a permissão atribuída</th>
<th>Grupo de permissão que tenha as entidades de segurança como membros</th>
<th>Tipo de uso padrão que atribui os grupos de permissão para o conector de recebimento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong> e <strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Servidores de transporte de Hub</p></li>
<li><p>Servidores de Transporte de Borda</p></li>
<li><p>Servidores do Exchange</p>

> [!TIP]
> Nos servidores de transporte de Hub somente


</li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Conta de usuário anônimo</p></td>
<td><p><strong>Anonymous</strong></p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Contas de usuários autenticados</p></td>
<td><p><strong>ExchangeUsers</strong></p></td>
<td><p><code>Client</code> (não disponível em servidores de transporte de borda)</p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Servidores de transporte de Hub</p></li>
<li><p>Servidores de Transporte de Borda</p></li>
<li><p>Servidores do Exchange</p>

> [!TIP]
> Apenas servidores de transporte de Hub


</li>
<li><p>Servidores protegidos externamente</p></li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Conta do servidor de parceiro</p></td>
<td><p><strong>Partner</strong></p></td>
<td><p><code>Internet</code> e <code>Partner</code></p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Firewall de cabeçalho nos conectores de recebimento personalizados

Se você quiser aplicar um firewall de cabeçalho às mensagens em um cenário de conector de recebimento personalizado, use qualquer um dos seguintes métodos:

  - Crie o conector de recebimento com um tipo de uso que aplica automaticamente o firewall de cabeçalho às mensagens. Observe que você pode definir o tipo de uso somente quando você cria o conector de recebimento.
    
      - Para remover cabeçalhos X da organização ou floresta X cabeçalhos de mensagens, crie um conector de recebimento e selecione um tipo de uso que não seja `Internal`.
    
      - Para remover os cabeçalhos de roteamento de mensagens, execute uma das seguintes ações:
        
          - Criar um conector de recebimento e selecione o tipo de uso `Custom`. Não atribua quaisquer grupos de permissão para o conector de recebimento.
        
          - Modificar um conector de recebimento existente e defina o parâmetro *PermissionGroups* como o valor `None`.
        
        Observe que, se você tiver um conector de recebimento que não tenha nenhuma grupos de permissão atribuídos a ele, você precisa adicionar entidades de segurança para o conector de recebimento, conforme descrito na etapa anterior.

  - Use o cmdlet **Remove-ADPermission** para remover a permissão de **Ms-Exch-Accept-Headers-Organization** , a permissão de **Ms-Exch-Accept-Headers-Forest** e a permissão de **Ms-Exch-Accept-Headers-Routing** de uma entidade de segurança que está configurado no conector de recebimento. Esse método não funciona se tiver sido atribuída a permissão para a entidade de segurança usando um grupo de permissão no conector de recebimento, porque você não pode modificar as atribuições de permissões ou a associação de grupo de um grupo de permissão.

  - Use o cmdlet **Add-ADPermission** para adicionar as entidades de segurança apropriadas que são necessárias para o fluxo de emails no conector de recebimento. Certifique-se de que nenhum entidades de segurança tem a permissão de **Ms-Exch-Accept-Headers-Organization** , a permissão de **Ms-Exch-Accept-Headers-Forest** e a permissão de **Ms-Exch-Accept-Headers-Routing** atribuída a eles. Se necessário, use o cmdlet **Add-ADPermission** para negar a permissão de **Ms-Exch-Accept-Headers-Organization** , a permissão de **Ms-Exch-Accept-Headers-Forest** e a permissão **Ms-Exch-Accept-Headers-Routing** para as entidades de segurança que são configuradas no conector de recebimento.

Para obter mais informações, consulte os seguintes tópicos:

  - [Conectores de recebimento](receive-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/pt-br/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/pt-br/library/aa996048\(v=exchg.150\))

Voltar ao início

## Firewall de cabeçalho para mensagens de saída nos conectores de envio

A tabela a seguir descreve o aplicativo padrão das permissões de firewall de cabeçalho nos conectores de envio.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Permissão</th>
<th>Entidades de segurança do Exchange padrão que possuem a permissão atribuída</th>
<th>Tipo de uso padrão que atribui as entidades de segurança para o conector de envio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong> e <strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Servidores de transporte de Hub</p></li>
<li><p>Servidores de Transporte de Borda</p></li>
<li><p>Servidores do Exchange</p>

> [!TIP]
> Nos servidores de transporte de Hub somente


</li>
<li><p>Servidores protegidos externamente</p></li>
<li><p>grupo de segurança universal <strong>ExchangeLegacyInterop</strong></p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Servidores de transporte de Hub</p></li>
<li><p>Servidores de Transporte de Borda</p></li>
<li><p>Servidores do Exchange</p>

> [!TIP]
> Nos servidores de transporte de Hub somente


</li>
<li><p>Servidores protegidos externamente</p></li>
<li><p>grupo de segurança universal <strong>ExchangeLegacyInterop</strong></p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Conta de usuário anônimo</p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Servidores de parceiro</p></td>
<td><p><code>Partner</code></p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Firewall de cabeçalho nos conectores de envio personalizados

Se você deseja aplicar o firewall de cabeçalho a mensagens em um cenário de conector de envio personalizado, use a qualquer um dos seguintes métodos:

  - Crie o conector de envio com um tipo de uso que aplica automaticamente o firewall de cabeçalho às mensagens. Observe que você pode definir o tipo de uso somente quando você cria o conector de envio.
    
      - Para remover cabeçalhos X da organização ou floresta X cabeçalhos de mensagens, crie um conector de envio e selecione um tipo de uso diferente `Internal` ou `Partner`.
    
      - Para remover os cabeçalhos de roteamento de mensagens, crie um conector de envio e selecione o tipo de uso `Custom`. A permissão de **Ms-Exch-Send-Headers-Routing** é atribuída a todos os tipos de uso de conector de envio exceto `Custom`.

  - Remova uma entidade de segurança que atribui a permissão **Ms-Exch-Send-Headers-Organization** , o **Ms-Exch-Send-Headers-Forest**e a permissão de **Ms-Exch-Send-Headers-Routing** do conector.

  - Use o cmdlet **Remove-ADPermission** para remover a permissão de **Ms-Exch-Send-Headers-Organization** , a permissão de **Ms-Exch-Send-Headers-Forest** e a permissão de **Ms-Exch-Send-Headers-Routing** de um dos objetos de segurança que está configurado no conector de envio.

  - Use o cmdlet **Add-ADPermission** para negar a permissão de **Ms-Exch-Send-Headers-Organization** , a permissão de **Ms-Exch-Send-Headers-Forest** e a permissão de **Ms-Exch-Send-Headers-Routing** como uma das entidades de segurança que são configuradas no conector de envio.

Para obter mais informações, consulte os seguintes tópicos:

  - [Conectores de envio](send-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/pt-br/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/pt-br/library/aa996048\(v=exchg.150\))

Voltar ao início

## Firewall de cabeçalho para outras fontes de mensagem

As mensagens podem inserir o pipeline de transporte em um servidor de caixa de correio ou um servidor de transporte de borda sem usar conectores de envio ou conectores de recebimento. Firewall de cabeçalho é aplicado a essas outras fontes de mensagem, conforme descrito na lista a seguir:

  - **Diretório de retirada e repetição**   O diretório de retirada é usado por administradores ou aplicativos para enviar os arquivos de mensagem. O diretório de repetição é usado para reenviar mensagens que tenham sido exportadas de filas de mensagens do Exchange. Para obter mais informações sobre os diretórios de retirada e repetição, consulte [Diretório de retirada e repetição](pickup-directory-and-replay-directory-exchange-2013-help.md).
    
    X-cabeçalhos da organização, X cabeçalhos de floresta e cabeçalhos de roteamento são removidos dos arquivos de mensagem no diretório de retirada.
    
    Cabeçalhos de roteamento são preservados nas mensagens enviadas pelo diretório de repetição.
    
    Se ou não cabeçalhos X da organização e da floresta cabeçalhos X são preservadas ou removidas das mensagens no diretório de repetição são controladas pelo campo de cabeçalho **X-CreatedBy:**  no arquivo de mensagem:
    
      - Se o valor de **X-CreatedBy:**  é `MSExchange15`, cabeçalhos X da organização e da floresta cabeçalhos X serão preservadas nas mensagens.
    
      - Se o valor da **X-CreatedBy:**  não `MSExchange15`, organização cabeçalhos X e floresta cabeçalhos X são removidos do mensagens.
    
      - Se o campo de cabeçalho **X-CreatedBy:**  não existir no arquivo de mensagem, cabeçalhos X da organização e floresta cabeçalhos X são removidos do mensagens.

  - **Diretório de recebimento**   O diretório de recebimento é usado pelo conectores externos nos servidores de caixa de correio para enviar mensagens para os servidores de mensagens que não usam o SMTP para transferir mensagens. Para obter mais informações sobre conectores externos, consulte [Conectores externos](foreign-connectors-exchange-2013-help.md).
    
    X-cabeçalhos da organização e da floresta cabeçalhos X são removidos dos arquivos de mensagem, antes que eles estão colocados no diretório de recebimento.
    
    Cabeçalhos de roteamento são preservados nas mensagens enviadas pelo diretório de recebimento.

  - **Transporte de caixa de correio**   O serviço de transporte de caixa de correio existe nos servidores de caixa de correio para transmitir mensagens de e para caixas de correio em servidores de caixa de correio. Para obter mais informações sobre o serviço de transporte de caixa de correio, consulte [Fluxo de mensagens](mail-flow-exchange-2013-help.md).
    
    X-cabeçalhos da organização, floresta cabeçalhos X e cabeçalhos de roteamento são removidos do mensagens de saída que são enviadas de caixas de correio pelo serviço de envio de transporte de caixa de correio.
    
    Cabeçalhos de roteamento são preservados para mensagens de entrada para os destinatários de caixa de correio pelo serviço de entrega de transporte de caixa de correio. A seguinte organização cabeçalhos X são preservadas para mensagens de entrada para os destinatários de caixa de correio pelo serviço de entrega de transporte de caixa de correio:
    
      - **X-MS-Exchange-Organization-SCL**
    
      - **X-MS-Exchange-Organization-AuthDomain**
    
      - **X-MS-Exchange-Organization-AuthMechanism**
    
      - **X-MS-Exchange-Organization-AuthSource**
    
      - **X-MS-Exchange-Organization-AuthAs**
    
      - **X-MS-Exchange-Organization-OriginalArrivalTime**
    
      - **X-MS-Exchange-Organization-OriginalSize**

  - **Mensagens DSN**   X-cabeçalhos da organização, X cabeçalhos de floresta e cabeçalhos de roteamento são removidos do cabeçalho da mensagem original é anexado à mensagem DSN ou da mensagem original. Para obter mais informações sobre mensagens DSN, consulte [DSNs e notificações de falha na entrega no Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

  - **Envio de agente de transporte**   X-cabeçalhos da organização, X cabeçalhos de floresta e cabeçalhos de roteamento são preservados nas mensagens enviadas pelos agentes de transporte.

Voltar ao início

## X-cabeçalhos da organização e da floresta cabeçalhos X no Exchange

O serviço de transporte nos servidores de caixa de correio ou servidores de transporte de borda inserir os campos de cabeçalho X personalizados em cabeçalho da mensagem.

X-cabeçalhos da organização começam com **X-MS-Exchange-Organization-**. X-cabeçalhos de floresta começam com **X-MS-Exchange-Forest-**. A tabela a seguir descreve alguns dos cabeçalhos X da organização e floresta cabeçalhos X que são usados em mensagens em uma organização do Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cabeçalho X</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Forest-RulesExecuted</strong></p></td>
<td><p>Regras de transporte que atua sobre a mensagem.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-Antispam-Report</strong></p></td>
<td><p>Um resumo dos resultados de um filtro antispam que tiverem sido aplicadas à mensagem pelo agente de filtro de conteúdo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthAs</strong></p></td>
<td><p>Especifica a origem de autenticação. Este cabeçalho X sempre está presente quando a segurança de uma mensagem foi avaliada. Os valores possíveis são <code>Anonymous</code>, <code>Internal</code>, <code>External</code>ou <code>Partner</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthDomain</strong></p></td>
<td><p>Preenchido durante a autenticação de domínio seguro. O valor é o FQDN do domínio remoto autenticado.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthMechanism</strong></p></td>
<td><p>Especifica o mecanismo de autenticação para o envio da mensagem. O valor é um número hexadecimal de 2 dígitos.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthSource</strong></p></td>
<td><p>Especifica o FQDN do computador servidor que avaliada a autenticação da mensagem em nome da organização.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Journal-Report</strong></p></td>
<td><p>Identifica os relatórios de diário no transporte. Assim que a mensagem deixa o serviço de transporte, o cabeçalho se torna <strong>X-MS-Journal-Report</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalArrivalTime</strong></p></td>
<td><p>Identifica a hora de quando a mensagem primeiro inseridos da organização do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Sender</strong></p></td>
<td><p>Identifica o remetente original de uma mensagem em quarentena quando ele primeiro inserido a organização do Exchange.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalSize</strong></p></td>
<td><p>Identifica o tamanho original de uma mensagem em quarentena quando ele primeiro inserido a organização do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Scl</strong></p></td>
<td><p>Identifica o SCL original de uma mensagem em quarentena quando ele primeiro inserido a organização do Exchange.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-PCL</strong></p></td>
<td><p>Identifica o nível de confiança de phishing. Os valores de nível de confiança de phishing possíveis são de 1 a 8. Um valor maior indica uma mensagem suspeita. Para obter mais informações, consulte <a href="anti-spam-stamps-exchange-2013-help.md">Carimbos anti-spam</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Quarantine</strong></p></td>
<td><p>Indica que a mensagem for colocada em quarentena na caixa de correio de quarentena de spam e uma notificação de status de entrega (DSN) foi enviada. Como alternativa, indica que a mensagem foi colocada em quarentena e lançada pelo administrador. Este campo de cabeçalho X impede que a mensagem lançada estão sendo enviados para a caixa de correio de quarentena de spam novamente. Para obter mais informações, consulte <a href="release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md">Liberar mensagens em quarentena da caixa de correio de quarentena de spam</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-SCL</strong></p></td>
<td><p>Identifica o SCL da mensagem. Os possíveis valores SCL são de 0 a 9. Um valor maior indica uma mensagem suspeita. O valor especial -1 isenta na mensagem do processamento pelo agente de filtro de conteúdo. Para obter mais informações, consulte <a href="content-filtering-exchange-2013-help.md">Filtragem de conteúdo</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-SenderIdResult</strong></p></td>
<td><p>Contém os resultados do agente de ID do remetente. O agente de ID de remetente usa a estrutura de diretiva do remetente (SPF) para comparar o endereço IP de origem da mensagem como o domínio que é usado no endereço de email do remetente. Os resultados de ID de remetente são usados para calcular o SCL de uma mensagem. Para obter mais informações, consulte <a href="sender-id-exchange-2013-help.md">ID de remetente</a>.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

