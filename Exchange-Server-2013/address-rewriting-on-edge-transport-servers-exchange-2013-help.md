---
title: 'Reconfiguração de servidores de transporte de borda: Exchange 2013 Help'
TOCTitle: Reconfiguração nos servidores de transporte de borda de endereço
ms:assetid: 23f1eaf6-247a-4671-ad72-aae19d9b511d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996806(v=EXCHG.150)
ms:contentKeyID: 61060556
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Reconfiguração nos servidores de transporte de borda de endereço

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

A reconfiguração do endereço modifica endereços de email de remetentes e destinatários em mensagens que entram ou saem da sua organização por meio de um servidor de Transporte de Borda. Dois agentes de transporte no servidor de Transporte de Borda oferecem a funcionalidade de reconfiguração: o Agente de Entrada de Reconfiguração de Endereço e o Agente de Saída de Reconfiguração de Endereço. O principal motivo para reconfiguração de endereço em mensagens de saída é apresentar um único domínio de email consistente para destinatários externos. O principal motivo para reconfiguração de endereço em mensagens de entrada é entregar mensagens para o destinatário correto.

A *entrada de reconfiguração de endereço* que você cria especifica os endereços internos (os endereços de email que você deseja alterar) e os endereços externos (os endereços de email finais desejados). Você pode especificar se endereços de email são reconfigurados em mensagens de entrada e de saída, ou somente em mensagens de saída. Você pode criar entradas de gravação de endereço para um único usuário (cris@contoso.com para suporte@contoso.com), todos os usuários em um único domínio (contoso.com para fabrikam.com) ou para usuários em vários subdomínios com exceções (\*.fabrikam.com para contoso.com, exceto legal.fabrikam.com).


> [!IMPORTANT]
> Independentemente de como você planeja usar a reconfiguração de endereço, será necessário verificar se os endereços de email resultantes são exclusivos em sua organização de forma que você não termine com duplicatas. Isso acontece porque a reconfiguração de endereço não verifica a exclusividade de um endereço de email reconfigurado.



**Conteúdo**

Address rewriting scenarios

Message properties modified by address rewriting

What address rewriting doesn't change

Considerations for outbound-only address rewriting

Considerations for inbound and outbound address rewriting

Considerations for rewriting addresses in multiple domains

Priority of address rewrite entries

Digitally signed, encrypted, and rights-protected messages

## Cenários para reconfiguração de endereço

Os cenários a seguir são exemplos de como você pode usar a reconfiguração de endereço:

  - **Consolidação de grupos**   Algumas organizações segmentam seus negócios internos em domínios separados que são baseados em requisitos técnicos ou comerciais. Essa configuração pode fazer com que as mensagens de email pareçam vir de grupos separados ou, até mesmo, de organizações separadas.
    
    O exemplo a seguir mostra como uma organização, a Contoso, Ltd., pode ocultar seus subdomínios de destinatários externos:
    
      - Mensagens de saída dos domínios northamerica.contoso.com, europe.contoso.com e asia.contoso.com são reconfiguradas para parecer que originaram de um único domínio contoso.com. Todas as mensagens são reconfiguradas conforme são transmitidas através de servidores de Transporte de Borda que fornecem conectividade SMTP entre toda a organização e a Internet.
    
      - Mensagens de entrada para destinatários de contoso.com são retransmitidas pelo servidor de Transporte de Borda para um servidor de Caixa de Correio. A mensagem é entregue para o destinatário correto com base no endereço de proxy configurado na caixa de correio do destinatário.

  - **Fusões e aquisições**   Uma empresa adquirida pode continuar a operar como uma unidade comercial independente, mas o administrador de email pode usar a reconfiguração de endereço para fazer com que as duas organizações pareçam ser uma única organização integrada.
    
    O exemplo a seguir mostra como a Contoso, Ltd. poderia ocultar o domínio de email da nova empresa adquirida, a Fourth Coffee:
    
      - A Contoso, Ltd. deseja que todas as mensagens de saída da organização do Exchange da Fourth Coffee pareçam ser originadas da Contoso.com. Todas as mensagens de ambas as organizações são enviadas através dos servidores de Transporte de Borda da Contoso, Ltd., onde as mensagens de email são reconfiguradas de *usuário*@fourthcoffee.com para *usuário*@contoso.com.
    
      - Mensagens de entrada para *usuário*@contoso.com são reconfiguradas e roteadas para caixas de correio de *usuário*@fourthcoffee.com. Mensagens de entrada que são enviadas para *usuário*@fourthcoffee.com são roteadas diretamente para servidores de email da Fourth Coffee.

  - **Parceiros**   Muitas organizações usam parceiros externos para fornecer serviços para seus clientes, outras organizações ou para a própria organização. Para evitar confusões, a organização pode substituir o domínio de email da organização do parceiro por seu próprio domínio de email.
    
    O exemplo a seguir mostra como a Contoso, Ltd. pode ocultar o domínio de email de um parceiro:
    
      - A Contoso, Ltd. oferece suporte para a grande organização Wingtip Toys. A Wingtip Toys deseja uma experiência unificada para seus clientes e requer que todas as mensagens originadas da equipe de suporte da Contoso, Ltd. apareçam como se tivessem sido enviadas pela Wingtip Toys. Todas as mensagens de saída relacionadas à Wingtip Toys são enviadas através de seus servidores de Transporte de Borda e todos os endereços de email de contoso.com são reconfigurados para endereços de email de wingtiptoys.com.
    
      - Mensagens de entrada para support@wingtiptoys.com são aceitas pelos servidores de Transporte de Borda da Wingtip Toy, reconfiguradas e, então, roteadas para o endereço de email support@contoso.com.

Voltar ao início

## Propriedades de mensagem modificadas por reconfiguração de endereço

Uma mensagem de email SMTP padrão consiste em um *envelope de mensagem* e no conteúdo da mensagem. O envelope da mensagem contém informações necessárias para a transmissão e a entrega da mensagem entre servidores de email SMTP. O conteúdo da mensagem contém campos de cabeçalho de mensagem que são coletivamente denominados *cabeçalho de mensagem* e o corpo da mensagem. O envelope da mensagem está descrito no RFC 2821 e o cabeçalho da mensagem, no RFC 2822.

Quando um remetente redige uma mensagem de email e a envia para entrega, a mensagem contém as informações básicas necessárias para estar em conformidade com os padrões SMTP, como um remetente, um destinatário, a data e a hora em que a mensagem foi redigida, uma linha de assunto opcional e um corpo de mensagem opcional. Essas informações estão contidas na própria mensagem e, por definição, no cabeçalho da mensagem.

O serviço de email do remetente gera um envelope de mensagem para a mensagem usando as informações sobre o remetente e o destinatário encontradas no cabeçalho da mensagem. Depois, transmite a mensagem para a Internet para entrega ao servidor de email do destinatário. Os destinatários nunca veem o envelope da mensagem, pois ele é gerado pelo processo de transmissão da mensagem e não faz parte realmente da mensagem.

A reconfiguração de endereço altera um endereço de email reconfigurando campos específicos no cabeçalho da mensagem ou no envelope da mensagem. A reconfiguração de endereço altera vários campos em mensagens de saída, mas somente um campo em mensagens de email de entrada. A tabela a seguir mostra quais campos de cabeçalho SMTP são reconfigurados em mensagens de entrada e de saída.

### Campos de mensagem reconfigurados em mensagens de saída e de entrada

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do campo</th>
<th>Local</th>
<th>Mensagens de saída</th>
<th>Mensagens de entrada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MAIL FROM</strong></p></td>
<td><p>Envelope de mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não regravado</p></td>
</tr>
<tr class="even">
<td><p><strong>RCPT TO</strong></p></td>
<td><p>Envelope de mensagem</p></td>
<td><p>Não reconfigurado</p></td>
<td><p>Reconfigurado</p></td>
</tr>
<tr class="odd">
<td><p><strong>Para</strong></p></td>
<td><p>Cabeçalho da mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não reconfigurado</p></td>
</tr>
<tr class="even">
<td><p><strong>Cc</strong></p></td>
<td><p>Cabeçalho da mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não reconfigurado</p></td>
</tr>
<tr class="odd">
<td><p><strong>De</strong></p></td>
<td><p>Cabeçalho da mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não reconfigurado</p></td>
</tr>
<tr class="even">
<td><p><strong>Remetente</strong></p></td>
<td><p>Cabeçalho da mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não reconfigurado</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reply-To</strong></p></td>
<td><p>Cabeçalho da mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não reconfigurado</p></td>
</tr>
<tr class="even">
<td><p><strong>Return-Receipt-To</strong></p></td>
<td><p>Cabeçalho da mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não reconfigurado</p></td>
</tr>
<tr class="odd">
<td><p><strong>Disposition-Notification-To</strong></p></td>
<td><p>Cabeçalho da mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não reconfigurado</p></td>
</tr>
<tr class="even">
<td><p><strong>Resent-From</strong></p></td>
<td><p>Cabeçalho da mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não reconfigurado</p></td>
</tr>
<tr class="odd">
<td><p><strong>Resent-Sender</strong></p></td>
<td><p>Cabeçalho da mensagem</p></td>
<td><p>Reconfigurado</p></td>
<td><p>Não reconfigurado</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## O que a reconfiguração de endereço não altera

A reconfiguração de endereço não altera qualquer campo de cabeçalho de mensagem que interrompa a funcionalidade do SMTP. Por exemplo, a modificação de determinados campos de cabeçalho pode afetar a detecção de loop de roteamento, invalidar a assinatura ou tornar uma mensagem protegida por direitos ilegível. Portanto, os seguintes campos de cabeçalho não são alterados pela reconfiguração de endereço:

  - **Return-Path**

  - **Received**

  - **Message-ID**

  - **X-MS-TNEF-Correlator**

  - **Content-Type Boundary=string**

  - Campos de cabeçalho localizados em partes do corpo MIME

A reconfiguração de endereço ignora domínios que não sejam controlados pela organização do Exchange. Em outras palavras, a reconfiguração de endereço não reconfigura campos de cabeçalho com domínios para os quais a organização do Exchange não seja autoritativa. A reconfiguração desses domínios causaria uma forma incontrolável de retransmissão de mensagem.

A reconfiguração de endereço também não modifica os campos de cabeçalho de mensagens que estejam incorporadas a outra mensagem. Remetentes e destinatários esperam que as mensagens incorporadas permaneçam intactas e sejam enviadas sem modificações, já que as mensagens não acionam regras de transporte que são implementadas entre o remetente e o destinatário.

Voltar ao início

## Considerações sobre a reconfiguração de endereço somente de saída

A reconfiguração de endereço somente de saída em um servidor de Transporte de Borda modifica o endereço de email do remetente quando a mensagem deixa a organização do Exchange. Você pode definir a reconfiguração de endereço somente de saída para um único usuário (chris@contoso.com para suporte@contoso.com) ou para todos os usuários em um único domínio (contoso.com para fabrikam.com). Você precisa definir a reconfiguração de endereço somente de saída para usuários em vários subdomínios (\*.fabrikam.com para .contoso.com).

O endereço de email reconfigurado deve estar definido como um endereço de proxy nos destinatários afetados. Por exemplo, se laura@sales.contoso.com for reconfigurado como laura@contoso.com, o endereço proxy laura@contoso.com deverá ser configurado na caixa de correio da Laura. Isso permite que respostas e mensagens de entrada sejam entregues corretamente.

Voltar ao início

## Considerações sobre reconfiguração de endereço de entrada e de saída

A reconfiguração de endereço de entrada e de saída, ou *bidirecional*, em um servidor de Transporte de Borda modifica o endereço de email do remetente em mensagens que saem da organização do Exchange e modifica o endereço de email do destinatário em mensagens que entram na organização do Exchange.

Você pode definir a reconfiguração de endereço somente de saída para um único usuário (chris@contoso.com para suporte@contoso.com) ou para todos os usuários em um único domínio (contoso.com para fabrikam.com). Você não pode definir a reconfiguração de endereço bidirecional para usuários em vários subdomínios (\*.fabrikam.com para .contoso.com).

Voltar ao início

## Considerações sobre a reconfiguração de endereços de email em vários domínios

Quando você mescla vários domínios ou subdomínios internos em um único domínio externo, precisa considerar os seguintes fatores:

  - **Verificar aliases exclusivos**   Todos os aliases de email (a parte à esquerda do símbolo @) devem ser exclusivos entre todos os subdomínios. Por exemplo, se houver um email joe@sales.contoso.com, não poderá haver um email joe@marketing.contoso.com porque os endereços de email reconfigurados para ambos os usuários seriam joe@contoso.com.

  - **Adicionar endereços de proxy**   O endereço de email reconfigurado deve ser configurado como um endereço de proxy para todos os remetentes afetados nos domínios afetados. Por exemplo, se joe@sales.contoso.com for reconfigurado como joe@contoso.com, será preciso adicionar o endereço de proxy joe@contoso.com à caixa de correio de Joe. Isso permite que respostas e mensagens de entrada sejam entregues corretamente.

  - **Contatos de email para organizações que não são do Exchange**   Se você estiver reconfigurando endereços de email de um sistema de email que não é do Exchange, precisa criar contatos de email no Exchange para representar os usuários no sistema de email que não é do Exchange. Esses contatos de email devem conter os endereços de email originais e os endereços de email reconfigurados. Por exemplo, se joe@unix.contoso.com for reconfigurado como joe@contoso.com, você deverá criar um contato de email com joe@unix.contoso.com como o endereço de email externo e joe@contoso.com como o endereço de proxy.

## Verificar aliases exclusivos

Ao reconfigurar endereços de email em vários subdomínios, é preciso garantir que todos os aliases de email sejam exclusivos entre todos os subdomínios. Por exemplo, considere a configuração a seguir:

Os seguintes usuários estão nos subdomínios sales.contoso.com, marketing.contoso.com e research.contoso.com:

  - maria@sales.contoso.com

  - chris@sales.contoso.com

  - david@marketing.contoso.com

  - brian@marketing.contoso.com

  - chris@research.contoso.com

  - adam@research.contoso.com

Suponha que você queira reconfigurar os subdomínios sales.contoso.com, marketing.contoso.com e research.contoso.com como um único domínio contoso.com.

Quando os endereços de email em cada subdomínio são reconfigurados, ocorre um conflito entre chris@sales.contoso.com e chris@research.contoso.com, porque ambos os endereços são reconfigurados como chris@contoso.com. Para resolver esta situação, você precisa alterar o endereço de email de um dos destinatários afetados. Por exemplo, você pode alterar chris@research.contoso.com para christopher@research.contoso.com de forma que o endereço de email seja reconfigurado para christopher@contoso.com.

Voltar ao início

## Prioridade de entradas de reconfiguração de endereço

Se um endereço de email do usuário corresponde a várias entradas de reconfiguração de endereço, o endereço de email só será reconfigurado uma vez com base na correspondência mais próxima. A lista a seguir descreve a ordem de precedência de entradas de reconfiguração de endereço da prioridade mais alta para a prioridade mais baixa:

1.  **Endereços de email individuais**   Uma entrada de reconfiguração de endereço está definida para reconfigurar o endereço de email de john@contoso.com para support@contoso.com.

2.  **Mapeamento de domínio ou subdomínio**   Uma entrada de reconfiguração de endereço está definida para reconfigurar todos os endereços de email de contoso.com para northwindtraders.com, ou todos os endereços de email de sales.contoso.com para contoso.com.

3.  **Mesclagem de domínio**   Uma entrada de reconfiguração de endereço está definida para reconfigurar endereços de email de \*.contoso.com para contoso.com.

Por exemplo, considere um servidor de Transporte de Borda em que as seguintes entradas de reconfiguração de endereço de saída estejam definidas:

  - endereços de email com \*.contoso.com são reconfigurados para contoso.com

  - endereços de email com japan.sales.contoso.com são reconfigurados para contoso.jp

Se masato@japan.sales.contoso.com enviar uma mensagem de email, o endereço será reconfigurado para masato@contoso.jp porque é a entrada que mais corresponde ao endereço de email do remetente.

Voltar ao início

## Mensagens assinadas digitalmente, criptografadas e protegidas por direitos

A reconfiguração de endereço não deverá afetar a maioria das mensagens assinadas, criptografadas ou protegidas por direitos. Se a reconfiguração de endereço invalidar ou alterar o status de segurança desses tipos de mensagens de alguma maneira, a reconfiguração de endereço não será aplicada.

Os valores a seguir podem ser reconfigurados porque as informações não fazem parte da assinatura, da criptografia ou da proteção de direitos da mensagem:

  - Campos no envelope da mensagem

  - Cabeçalhos dos corpos de mensagens de nível superior

Os valores a seguir não podem ser reconfigurados porque as informações fazem parte da assinatura, da criptografia ou da proteção de direitos da mensagem:

  - Campos de cabeçalho localizados dentro de partes do corpo MIME que podem estar assinados

  - O parâmetro de seqüência de limite do tipo de conteúdo MIME

Voltar ao início

