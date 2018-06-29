---
title: 'Exibir propriedades de mensagem na fila no Visualizador de filas: Exchange 2013 Help'
TOCTitle: Exibir propriedades de mensagem na fila no Visualizador de filas
ms:assetid: 9d15d8b8-e061-4288-9354-df58e282fb6b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123934(v=EXCHG.150)
ms:contentKeyID: 50486227
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.Edge.SystemManager.MessagePropertyPage
ms.translationtype: MT
---

# Exibir propriedades de mensagem na fila no Visualizador de filas

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2013-01-17_

Você pode usar o Visualizador de filas na caixa de ferramentas do Exchange para exibir as propriedades de uma mensagem que está na fila de entrega.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Filas" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você também pode usar o cmdlet Get-Message no Shell de gerenciamento do Exchange para exibir propriedades de mensagem adicionais que não estão visíveis no Visualizador de filas. Para obter mais informações, consulte [Filtros de mensagens](message-filters-exchange-2013-help.md) e [Usar o Shell de gerenciamento do Exchange para gerenciar filas](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Visualizador de filas na caixa de ferramentas do Exchange para exibir as propriedades de uma mensagem

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de email**, clique duas vezes em **Visualizador de Filas** para abrir a ferramenta em uma nova janela.

3.  No Visualizador de filas, selecione a guia de **mensagens** para ver a lista de mensagens que estão atualmente na fila de entrega em sua organização.

4.  Clique com o botão a mensagem cujas propriedades você deseja exibir e selecione **Propriedades**.

5.  
    
    Na guia **Geral** exibe as seguintes informações detalhadas sobre a mensagem:
    
      - **Identidade**    Esse campo mostra o número inteiro que representa uma mensagem específica. A identidade da mensagem é atribuída pelo banco de dados de fila quando a mensagem é recebida para processamento. Você pode incluir uma identidade de fila e de servidor opcional para identificar uma instância exclusiva da mensagem.
    
      - **Assunto**    Esse campo mostra o assunto de uma mensagem e é expresso como uma cadeia de caracteres de texto. O valor é obtido do campo de cabeçalho `Subject:` .
    
      - **ID de mensagem da Internet**    Esse campo mostra o valor do campo de cabeçalho `MessageID:` . O valor dessa propriedade é expresso como um GUID, seguido pelo endereço SMTP do servidor de envio, como neste exemplo: 67D754D6103DC4FB3BA6BC7205DACABA61231@exchange.contoso.com
    
      - **Endereço de**    Esse campo mostra o endereço SMTP do remetente da mensagem. Esse valor é obtido do MAIL FROM: no envelope da mensagem.
    
      - **Status**    Esse campo mostra o status atual da mensagem. Uma mensagem pode ter um dos seguintes valores de status:
        
          - **Ativo**    Se a mensagem estiver em uma fila de entrega, a mensagem está sendo entregue ao seu destino. Se a mensagem estiver na fila de envio, a mensagem está sendo processada pelo categorizador.
        
          - **Pendente Remove**    A mensagem foi excluída pelo administrador, mas já estava na entrega. A mensagem será excluída se a entrega termina em um erro dizendo que faz com que a mensagem para entrar novamente na fila. Caso contrário, entrega continuará.
        
          - **Pendente suspender**    A mensagem foi suspensa pelo administrador, mas já estava na entrega. A mensagem será suspenso se a entrega termina em um erro dizendo que faz com que a mensagem para entrar novamente na fila. Caso contrário, entrega continuará.
        
          - **Pronto**    A mensagem está aguardando na fila e está pronta para ser processado.
        
          - **Repetir**    A última tentativa de conexão falhou para a fila na qual essa mensagem está localizada. A mensagem está aguardando a próxima tentativa de fila.
        
          - **Suspenso**    A mensagem foi suspensa pelo administrador.
    
      - **Tamanho (KB)**    Esse campo mostra o tamanho da mensagem arredondado até o mais próximo quilobyte (KB).
    
      - **Nome da fonte de mensagem**    Esse campo mostra o nome do componente que enviou a mensagem para a fila.
    
      - **IP de origem**    Esse campo mostra o endereço IP do servidor externo que enviou a mensagem para a organização Exchange.
    
      - **SCL**    Esse campo mostra a classificação de SCL (nível) de confiança de spam da mensagem. Entradas SCL válidas são números inteiros de 0 a 9 ou -1. Uma entrada SCL vazia indica que a mensagem ainda não foram processada pelo agente de filtro de conteúdo.
    
      - **Data recebido**    Esse campo mostra a data / hora em que a mensagem foi recebida pelo servidor que mantém a fila na qual a mensagem está localizada.
    
      - **Tempo de expiração**    Esse campo mostra a data / hora quando a mensagem expirará e será excluída da fila se a mensagem não pode ser entregue.
    
      - **Último erro**    Esse campo mostra o último erro que foi registrado para uma mensagem.
    
      - **ID da fila**    Esse campo mostra a identidade da fila que contém a mensagem. A identidade da fila é expresso no formulário *Server\\destination*, onde o *destino* é um grupo de entrega, o destino de roteamento, o nome da fila persistente ou o identificador do banco de dados de fila. O identificador do banco de dados de fila é representado como um inteiro e pode ser determinado, exibindo as propriedades de mensagem.
    
      - **Destinatários**    Esse campo mostra a lista de destinatários aos quais a mensagem for endereçada.
    
      - **Contagem de repetição**    Esse campo mostra o número de vezes que a entrega de uma mensagem para um destino foi tentada.

6.  
    
    A guia **Informações do destinatário** exibe as seguintes informações sobre os destinatários da mensagem:
    
      - **Endereço**    Esse campo mostra o endereço SMTP do destinatário da mensagem. Este valor é obtido do `RCPT TO:` no envelope da mensagem.
    
      - **Status**    Esse campo mostra o status atual da mensagem. Uma mensagem pode ter um dos seguintes valores de status:
        
          - **Ativo**    Se a mensagem estiver em uma fila de entrega, a mensagem está sendo entregue ao seu destino. Se a mensagem estiver na fila de envio, a mensagem está sendo processada pelo categorizador.
        
          - **Pendente Remove**    A mensagem foi excluída pelo administrador, mas já estava na entrega. A mensagem será excluída se a entrega termina em um erro dizendo que faz com que a mensagem para entrar novamente na fila. Caso contrário, entrega continuará.
        
          - **Pendente suspender**    A mensagem foi suspensa pelo administrador, mas já estava na entrega. A mensagem será suspenso se a entrega termina em um erro dizendo que faz com que a mensagem para entrar novamente na fila. Caso contrário, entrega continuará.
        
          - **Pronto**    A mensagem está aguardando na fila e está pronta para ser processado.
        
          - **Repetir**    A última tentativa de conexão falhou para a fila na qual essa mensagem está localizada. A mensagem está aguardando a próxima tentativa de fila.
        
          - **Suspenso**    A mensagem foi suspensa pelo administrador.
    
      - **Último erro**    Esse campo mostra o último erro que foi registrado para uma mensagem.

## Use o Shell para exibir as propriedades de uma mensagem

Você pode usar o cmdlet **Get-Message** para exibir as propriedades de uma mensagem que atualmente está na fila de entrega. O exemplo a seguir tabula o endereço do remetente, destinatários, assunto e informações de data de recebimento de todas as mensagens que estão em estado retry no momento:

    Get-Message -IncludeRecipientInfo -Filter {Status -eq "Retry"} | Format-Table FromAddress,Recipients,Subject,DateReceived

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-Message](https://technet.microsoft.com/pt-br/library/bb124738\(v=exchg.150\)).

