---
title: 'Cenários comuns de bloqueio de anexo: Exchange 2013 Help'
TOCTitle: Cenários comuns de bloqueio de anexo
ms:assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn950026(v=EXCHG.150)
ms:contentKeyID: 65210901
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cenários comuns de bloqueio de anexo

 

_**Aplica-se a:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Tópico modificado em:**2017-02-23_

Sua organização pode exigir que determinados tipos de mensagens seja bloqueados ou rejeitados de forma que atenda aos requisitos legais ou normativos ou para implementar as necessidades de negócios específicos. Aqui estão alguns exemplos de cenários comuns para bloquear todos os anexos que você pode configurar usando regras de transporte no Exchange:

  -  O exemplo 1: Bloquear mensagens com anexos e notificar o remetente

  -  Exemplo 2: Notificar se destina a destinatários quando uma mensagem de entrada for bloqueada

  -  Exemplo 3: Modificar a linha de assunto para notificações

  -  O exemplo 4: Aplicar uma regra com um limite de tempo

Para exemplos adicionais, mostrando como bloquear anexos específicos, consulte:

  - [Usar regras de transporte para inspecionar anexos de mensagens](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013)

  - [Usar regras de fluxo de email para inspecionar anexos de mensagens no Office 365](https://technet.microsoft.com/pt-br/library/jj919236\(v=exchg.150\)) (Exchange Online, Proteção do Exchange Online)

O filtro de malware inclui um filtro de tipos de anexo comuns. Na Centro de administração do Exchange (EAC), vá para a **proteção**, clique em **New** (![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")), para adicionar filtros. No portal do Exchange Online, navegue até **proteção** e, em seguida, selecione o **Filtro de Malware**.

Para começar a implementar qualquer um desses cenários para bloquear certos tipos de mensagem:

1.  Entrar com o Centro de administração do Exchange.

2.  Vá para **fluxo de emails** \>**regras**.

3.  Clique em **New** (![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")) e, em seguida, selecione **criar uma nova regra**.

4.  Na caixa **nome**, especifique um nome para a regra e, em seguida, clique em **mais opções**.

5.  Selecione as condições e ações que você deseja.

**Observação:** no EAC do, o menor tamanho de anexo que você pode inserir é 1 quilobyte, que deve detectar a maioria dos anexos. No entanto, se você deseja detectar cada anexo possível de qualquer tamanho, você precisará usar o PowerShell para ajustar o tamanho de anexo para 1 byte depois de criar a regra no EAC. Para saber como abrir o Shell de Gerenciamento do Exchange em sua organização Exchange local, confira [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)).Para saber como usar o Windows PowerShell para se conectar ao Exchange Online, confira o artigo [Conectar-se ao Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).Para saber como usar o Windows PowerShell para se conectar ao Proteção do Exchange Online, confira o artigo [Conectar-se ao PowerShell do Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=627290).

Substitua *\<Rule Name\>* pelo nome da regra existente e execute o seguinte comando para definir o tamanho de anexo como 1 byte:

    Set-TransportRule -Identity "<Rule Name>" -AttachmentSizeOver 1B

Após você ajustar o tamanho de anexo para 1 byte, o valor que é exibido para a regra no EAC é **0,00 KB**.

## O exemplo 1: Bloquear mensagens com anexos e notificar o remetente

Se você não quiser que as pessoas na sua organização para enviar ou receber anexos, você pode configurar uma regra de transporte para bloquear todas as mensagens com anexos.

Neste exemplo, todas as mensagens enviadas de ou para a organização com anexos serão bloqueadas.

![Regra que bloqueia todos os anexos](images/Dn950026.38094183-166f-4ba5-a9cf-242e7d0f4e04(EXCHG.150).png "Regra que bloqueia todos os anexos")

Se tudo o que você deseja fazer é bloquear a mensagem, você talvez queira parar o processamento de regra após esta regra é correspondida. Role para baixo a caixa de diálogo regra e marque a caixa de seleção **Parar o processamento de mais regras**.

## Exemplo 2: Notificar destinado a destinatários quando uma mensagem de entrada for bloqueada

Se você deseja rejeitar uma mensagem, mas permitir que o destinatário pretendido saiba o que aconteceu, você pode usar a ação **notificar o destinatário com uma mensagem**.

Você pode incluir espaços reservados na mensagem de notificação para que ele inclua informações sobre a mensagem original. Os espaços reservados devem ser colocados entre sinais de dois por cento (%) e quando a mensagem de notificação é enviada, os espaços reservados são substituídos pelas informações da mensagem original. Você também pode usar HTML básico, como \< br, \> \< b \> \< i, \> e \< img \> na mensagem.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Tipo de informação</strong></p></td>
<td><p><strong>Espaço reservado</strong></p></td>
</tr>
<tr class="even">
<td><p>Remetente da mensagem.</p></td>
<td><p>% % De % %</p></td>
</tr>
<tr class="odd">
<td><p>Destinatários listados na linha &quot;Para&quot;.</p></td>
<td><p>% % Para % %</p></td>
</tr>
<tr class="even">
<td><p>Destinatários listados na linha &quot;Cc&quot;.</p></td>
<td><p>% % Cc % %</p></td>
</tr>
<tr class="odd">
<td><p>Assunto da mensagem original.</p></td>
<td><p>% % Assunto % %</p></td>
</tr>
<tr class="even">
<td><p>Cabeçalhos da mensagem original. Este é semelhante à lista de cabeçalhos em uma notificação de status de entrega (DSN) gerado para a mensagem original.</p></td>
<td><p>% % Cabeçalhos de % %</p></td>
</tr>
<tr class="odd">
<td><p>Data em que a mensagem original foi enviada.</p></td>
<td><p>%%MessageDate%%</p></td>
</tr>
</tbody>
</table>


Neste exemplo, todas as mensagens que contêm anexos e são enviadas para pessoas dentro da organização são bloqueadas e o destinatário será notificado.

![Regra que notifica os destinatários quando uma mensagem de entrada é bloqueada](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Regra que notifica os destinatários quando uma mensagem de entrada é bloqueada")

## Exemplo 3: Modificar a linha de assunto para notificações

Quando uma notificação é enviada ao destinatário, a linha de assunto é o assunto da mensagem original. Se você deseja modificar o assunto, de forma que ele fique mais claro ao destinatário, você deve usar as duas regras de transporte:

  - A primeira regra adiciona a palavra "não entregue" ao início do assunto de todas as mensagens com anexos.

  - A segunda regra bloqueia a mensagem e envia uma mensagem de notificação para o remetente usando o novo assunto da mensagem original.


> [!IMPORTANT]
> As duas regras devem ter condições idênticas. Regras são processadas na ordem, para que a primeira regra adiciona a palavra "não entregue" e a segunda regra bloqueia a mensagem e notifica o destinatário.



Aqui está o que a primeira regra será semelhante se você deseja adicionar "não entregue" ao assunto:

![Regra que precede Não é possível entregar em mensagens com anexos](images/Dn950026.2552b0bd-c69d-48b4-9e69-267fcaf20e70(EXCHG.150).png "Regra que precede Não é possível entregar em mensagens com anexos")

E a segunda regra faz o bloqueio e a notificação (a mesma regra do exemplo 2):

![Regra que notifica os destinatários quando uma mensagem de entrada é bloqueada](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Regra que notifica os destinatários quando uma mensagem de entrada é bloqueada")

## Exemplo 4: Aplicar uma regra com um limite de tempo

Se você tiver um ataque de malware, convém aplicar uma regra com um limite de tempo para que você bloquear temporariamente anexos. Por exemplo, a seguinte regra tem um dia de início e parada e a hora:

![Regra mostrando um limite de tempo](images/Dn950026.bdc8c4d8-72fa-4c5b-97f2-5fe76d50e643(EXCHG.150).png "Regra mostrando um limite de tempo")

## Consulte também


[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)  


[Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\))  
[Regras de fluxo de emails (regras de transporte) no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/dn271424\(v=exchg.150\))

