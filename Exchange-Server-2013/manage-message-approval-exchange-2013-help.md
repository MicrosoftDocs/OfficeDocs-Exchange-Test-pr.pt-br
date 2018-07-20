---
title: 'Gerenciar a aprovação de mensagens: Exchange 2013 Help'
TOCTitle: Gerenciar a aprovação de mensagens
ms:assetid: 43a89f71-8002-4cb0-b3c8-1c2b2597f227
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd297936(v=EXCHG.150)
ms:contentKeyID: 50485471
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar a aprovação de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-05-04_

Em alguns casos, faz sentido ter um segundo conjunto de olhos em uma mensagem antes que a mensagem é entregue. Como administrador Exchange, você pode configurar isso. Esse processo é chamado de *moderação*e aprovador é chamado *moderador*. Dependendo de qual as mensagens precisam de aprovação, você pode usar uma das duas abordagens:

  - Alterar as propriedades do grupo de distribuição

  - Criar uma regra de fluxo de email

Este artigo explica:

  - Como decidir qual abordagem aprovação usar

  - Como funciona o processo de aprovação

Para saber como implementar cenários comuns, consulte [Cenários comuns de aprovação de mensagem](common-message-approval-scenarios-exchange-2013-help.md).

## Como decidir qual abordagem aprovação usar

Aqui está uma comparação entre as duas abordagens para aprovação de mensagens.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>O que você deseja fazer?</th>
<th>Abordagem</th>
<th>Primeira etapa</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Crie um grupo de distribuição moderada onde todas as mensagens ao grupo devem ser aprovadas.</p></td>
<td><p>Configure a aprovação de mensagens para o grupo de distribuição.</p></td>
<td><p>Vá para Centro de administração do Exchange (EAT) &gt; <strong>destinatários</strong> &gt; <strong>grupos</strong>, edite o grupo de distribuição e selecione <strong>aprovação de mensagens</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Exigir aprovação para mensagens que correspondam a critérios específicos ou que são enviadas para uma pessoa específica.</p></td>
<td><p>Crie uma regra de transporte usando a ação <strong>encaminhar a mensagem para aprovação</strong>.</p>
<p>Você pode especificar critérios de mensagem, incluindo padrões de texto, remetentes e destinatários. Seus critérios também podem conter para exceções.</p></td>
<td><p>Vá para o EAC &gt; <strong>fluxo de emails</strong> &gt; <strong>regras</strong>.</p></td>
</tr>
</tbody>
</table>


Retornar ao início

## Como funciona o processo de aprovação

Quando alguém envia uma mensagem para uma pessoa ou grupo que exija aprovação, se estiver usando o Outlook Web Access, eles são notificados de que sua mensagem pode ser atrasada.

![Mensagem mostrando uma notificação de aprovação de mensagem](images/Dd297936.80e2e5f1-0a1e-4c37-9076-794581155405(EXCHG.150).png "Mensagem mostrando uma notificação de aprovação de mensagem")

Moderador recebe um email com uma solicitação para aprovar ou rejeitar a mensagem. O texto da mensagem inclui botões para aprovar ou rejeitar a mensagem e o anexo inclui a mensagem original para analisar.

![Mensagem de solicitação de aprovação, incluindo anexo](images/Dd297936.bf517f5a-b10e-40df-a48a-403b395b5962(EXCHG.150).png "Mensagem de solicitação de aprovação, incluindo anexo")

Moderador pode aceitar uma das três ações:

![Fluxo de trabalho mostrando as opções para aprovar uma mensagem](images/Dd297936.dc7a6ca9-c67d-487a-8713-4d628e07f4b3(EXCHG.150).png "Fluxo de trabalho mostrando as opções para aprovar uma mensagem")

1.  Se aprovada, a mensagem se depara aos destinatários pretendidos originais. O remetente original não será notificado.

2.  Se rejeitada, uma mensagem de rejeição é enviada ao remetente. Moderador pode adicionar uma explicação:
    
    ![Aviso de rejeição, com comentários do moderador](images/Dd297936.a663d36a-c67d-4155-b8f6-4b5dc8e105d9(EXCHG.150).png "Aviso de rejeição, com comentários do moderador")  

3.  Se o aprovador exclui ou ignora a mensagem de aprovação, uma mensagem de expiração é enviada ao remetente. Isso acontece depois de dois dias em Exchange Online e cinco dias em Exchange Server 2013. (No Exchange Server 2013, você pode alterar esse período de tempo).

A mensagem que está aguardando aprovação temporariamente obtém armazenada em uma caixa de correio do sistema chamada a *caixa de correio de arbitragem*. Até que o moderador decide aprovar ou rejeitar a mensagem, exclui a mensagem de aprovação ou permite que a mensagem de aprovação expirar, a mensagem original é mantida na caixa de correio de arbitragem.

Retornar ao início

## Perguntas e respostas

**Qual é a diferença entre o aprovador e o proprietário de um grupo de distribuição?**

O proprietário de um grupo de distribuição é responsável por gerenciar a associação ao grupo de distribuição, mas ele não poderá moderar as mensagens enviadas a ele. Por exemplo, uma pessoa de IT pode ser o proprietário de um grupo de distribuição chamado todos os funcionários, mas apenas o gerente de recursos humanos pode ser definido como moderador.

**O que acontece quando o moderador ou aprovador envia uma mensagem ao grupo de distribuição?**

A mensagem se depara diretamente ao grupo, ignorando o processo de aprovação.

**O que acontece quando apenas um subconjunto de destinatários precisa aprovação?**

Você pode enviar uma mensagem para um grupo de destinatários quando apenas um subconjunto dos destinatários exige aprovação. Considere a possibilidade de uma mensagem é enviada aos 12 destinatários, um dos quais é um grupo de distribuição moderada. A mensagem automaticamente é dividida em duas cópias. Uma mensagem é entregue imediatamente aos 11 destinatários que não exijam aprovação, e a segunda mensagem é enviada para o processo de aprovação para o grupo de distribuição moderada. Se uma mensagem destina-se a mais de um destinatário moderado, uma cópia separada da mensagem é automaticamente criada para cada destinatário moderado e cada cópia passa pelo processo de aprovação apropriado.

**O que ocorre se o meu grupo de distribuição contém moderados destinatários que exijam aprovação?**

Um grupo de distribuição pode incluir destinatários moderados que também exigem aprovação. Nesse caso, depois que a mensagem para o grupo de distribuição particular for aprovada, ocorrerá um processo de aprovação separado para cada destinatário moderado que seja membro do grupo de distribuição. No entanto, você também pode habilitar a aprovação automática dos membros do grupo de distribuição, depois que a mensagem para o grupo de distribuição moderada for aprovada. Para fazer isso, você pode usar o parâmetro *BypassNestedModerationEnabled* no cmdlet [Set-DistributionGroup](https://technet.microsoft.com/pt-br/library/bb124955\(v=exchg.150\)) .

**É esse processo diferente se temos nossos próprios servidores do Exchange?**

Por padrão, uma caixa de correio de arbitragem é usada para cada organização do Exchange. Se você possui seus próprios servidores Exchange e precisa de mais caixas de correio de arbitragem para balanceamento de carga, siga as instruções para adicionar caixas de correio de arbitragem em [Gerenciar e solucionar problemas de aprovação de mensagens](manage-and-troubleshoot-message-approval-exchange-2013-help.md). Caixas de correio de arbitragem são caixas de correio do sistema e não exigem uma licença do Exchange.


> [!TIP]
> <STRONG>Se você tiver Exchange 2007:</STRONG> Microsoft Exchange Server 2007 não oferece suporte a destinatários moderados. Se uma mensagem enviada a um grupo de distribuição moderada é expandida em um servidor de transporte de Hub Exchange 2007, a mensagem ignora a moderação e é entregue a todos os membros do grupo de distribuição. Se você tiver servidores de transporte de Hub Exchange 2007 em sua organização do Exchange, você não deixe designar um servidor de caixa de correio Exchange Server 2013 como o servidor de expansão de grupos de distribuição moderada. Isso garante que todas as mensagens enviadas para o grupo de distribuição são moderadas.



Retornar ao início

## Precisa de mais informações?

[Gerenciar regras de fluxo de emails](manage-mail-flow-rules-exchange-2013-help.md)

[Referência rápida do Shell de gerenciamento do Exchange para o Exchange 2013](exchange-management-shell-quick-reference-for-exchange-2013-exchange-2013-help.md)

[PowerShell do Exchange Online](https://technet.microsoft.com/pt-br/library/jj200677\(v=exchg.150\))

