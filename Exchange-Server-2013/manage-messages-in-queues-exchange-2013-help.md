---
title: 'Gerenciar mensagens em filas: Exchange 2013 Help'
TOCTitle: Gerenciar mensagens em filas
ms:assetid: 83358884-6036-4e91-87a8-35200541874d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123535(v=EXCHG.150)
ms:contentKeyID: 51407884
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar mensagens em filas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-05-07_

Na Microsoft Exchange Server 2013, você pode usar o Visualizador de Filas na Caixa de Ferramentas do Exchange ou o Shell de Gerenciamento do Exchange para gerenciar as mensagens em filas. Para mais informações sobre como usar os cmdlets de gerenciamento da mensagen no Shell de Gerenciamento do Exchange, consulte [Usar o Shell de gerenciamento do Exchange para gerenciar filas](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Filas" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Remover mensagens de filas

Uma mensagem enviada para vários destinatários pode estar localizada em mais do que uma fila. Para remover uma mensagem de mais de uma fila numa única operação, precisa de usar um filtro. Você pode selecionar se enviará uma notificação de falha na entrega quando remover mensagens de uma fila. Você não pode remover uma mensagem da fila de Envio.

## Usar o Visualizador de Filas na Caixa de Ferramentas para remover mensagens

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de email**, clique duas vezes em **Visualizador de Filas** para abrir a ferramenta em uma nova janela.

3.  No Visualizador de Filas, clique na guia **Mensagens**. Será exibida uma lista de todas as mensagens no servidor ao qual você está conectado. Para ajustar a ação para uma única fila, clique na guia **Filas**, clique duas vezes no nome da fila e clique na guia *Servidor\\Fila* que será exibida.

4.  Selecione uma ou mais mensagens na lista, clique com o botão direito do mouse e, em seguida, selecione **Remover Mensagens (com notificação de falha na entrega)** ou **Remover Mensagens (sem notificação de falha na entrega)**. Será exibida uma caixa de diálogo que confirmará a ação selecionada, perguntando **Deseja continuar?** Clique em **Sim**.

5.  Para remover todas as mensagens de uma determinada fila, clique na guia **Filas**. Selecione uma fila, clique nela com o botão direito do mouse e selecione **Remover Mensagens (com notificação de falha na entrega)** ou **Remover Mensagens (sem notificação de falha na entrega)**. Será exibida uma caixa de diálogo que confirmará a ação selecionada, perguntando **Deseja continuar?** Clique em **Sim**.
    

    > [!NOTE]
    > Se você estiver trabalhando com uma lista filtrada, a página exibida talvez não inclua todos os itens no filtro. Nesse caso, uma tela exibirá a mensagem: <STRONG>Esta ação afetará todos os itens nesta página. Para expandir o escopo dessa ação para incluir todos os itens neste filtro, selecione a caixa a seguir antes de clicar em OK.</STRONG>



## Usar o Shell para remover mensagens

Para remover mensagens de filas, use a seguinte sintaxe.

    Remove-Message <-Identity MessageIdentity | -Filter {MessageFilter}> -WithNDR <$true | $false>

Este exemplo remove mensagens nas filas com o assunto "Win Big" sem enviar uma notificação de falha na entrega.

    Remove-Message -Filter {Subject -eq "Win Big"} -WithNDR $false

Este exemplo remove a mensagem com a ID de mensagem 3 da fila que não pode ser acessada no servidor Mailbox01 e envia uma notificação de falha na entrega.

    Remove-Message -Identity Mailbox01\Unreachable\3 -WithNDR $true

## Como saber se funcionou?

Para verificar se removeu mensagens de filas com êxito, siga um dos seguintes passos:

  - No Visualizador de Filas, escolha a fila ou crie um filtro para confirmar que as mensagens já não existem.

  - Use o cmdlet **Get-Message** com os parâmetros *Queue* ou *Filter* para confirmar que as mensagens já não existem. Para mais informações, consulte [Get-Message](https://technet.microsoft.com/pt-br/library/bb124738\(v=exchg.150\)).

## Retomar mensagens em filas

É possível reiniciar uma mensagem que atualmente tem um status Suspenso. Ao reiniciar uma mensagem, você habilita a sua entrega. Se você reiniciar uma mensagem que está localizada na fila de mensagens inviáveis, a mensagem será enviada ao categorizador para processamento. Uma mensagem enviada para vários destinatários pode estar localizada em várias filas. Para continuar uma mensagem em mais de uma fila em uma única operação, use um filtro.

## Usar o Visualizador de Filas na Caixa de Ferramentas do Exchange para retomar mensagens

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de email**, clique duas vezes em **Visualizador de Filas** para abrir a ferramenta em uma nova janela.

3.  No Visualizador de Filas, clique na guia **Mensagens**. Será exibida uma lista de todas as mensagens no servidor ao qual você está conectado. Para ajustar a ação para focalizar uma única fila, clique na guia **Filas**, clique duas vezes no nome da fila e clique na guia *Servidor\\Fila* que aparecer.

4.  Clique em **Criar Filtro** e insira a expressão do filtro da seguinte maneira:
    
    1.  Selecione **Status** na lista suspensa de propriedades da mensagem.
    
    2.  Selecione **É Igual a** na lista suspensa de operadores de comparação.
    
    3.  Selecione **Suspenso** na lista suspensa de valores.

5.  Clique em **Aplicar Filtro**. Todas as mensagens que têm um status Suspenso são exibidas.

6.  Selecione uma ou mais mensagens na lista, clique com o botão direito e selecione **Continuar**.

## Usar o Shell para retomar mensagens

Para retomar mensagens, use a seguinte sintaxe:

    Resume-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

Este exemplo retoma todas as mensagens que estão sendo enviadas de qualquer remetente no domínio Contoso.com.

    Resume-Message -Filter {FromAddress -eq "*contoso.com"}

Este exemplo retoma a mensagem com o ID de mensagem 3 na fila inacessível no servidor Hub01.

    Resume-Message -Identity Hub01\Unreachable\3

Para reenviar mensagens a partir da fila de mensagens suspeitas, faça o seguinte:

## Como saber se funcionou?

Para confirmar que você retomou mensagens em filas com êxito, siga um dos seguintes passos:

  - No Visualizador de Filas, escolha ou crie um filtro para confirmar que as mensagens já não estão suspensas.

  - Use o cmdlet **Get-Message** com os parâmetros *Queue* ou *Filter* para confirmar que as mensagens já não estão suspensas. Para mais informações, consulte [Get-Message](https://technet.microsoft.com/pt-br/library/bb124738\(v=exchg.150\)).

Note que se você não conseguir encontrar a mensagem em qualquer fila no servidor, provavelmente significa que a mensagem passou ao salto seguinte com êxito.

## Mensagens suspensas em filas

Ao suspender uma mensagen, você evita a entrega da mesma. Se uma mensagem que aparece na fila já estiver na entrega, ela não será suspensa. A entrega continuará e o estado da mensagem será **PendingSuspend**. Se a entrega falhar, a mensagem retornará à fila e então será suspensa. Não é possível suspender uma mensagem que esteja na fila Envio ou na fila de mensagens suspeitas.

Uma mensagem enviada para vários destinatários pode estar localizada em várias filas. Para suspender uma mensagem em mais do que uma fila numa única operação, você precisa de um filtro.

## Usar o Visualizador de Filas na Caixa de Ferramentas do Exchange para suspender mensagens

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de email**, clique duas vezes em **Visualizador de Filas** para abrir a ferramenta em uma nova janela.

3.  No Visualizador de Filas, clique na guia **Mensagens**. Será exibida uma lista de todas as mensagens no servidor ao qual você está conectado. Para limitar a exibição a uma única fila, clique na guia **Filas**, clique duas vezes no nome da fila e clique na guia *Servidor\\Fila* que aparecer.

4.  Selecione uma ou mais mensagens, clique com o botão direito do mouse e selecione **Suspender**.

## Usar o Shell para suspender mensagens

Para suspender mensagens, use a seguinte sintaxe:

    Suspend-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

Este exemplo suspende todas as mensagens nas filas que provêm de qualquer remetente no domínio contoso.com.

    Suspend-Message -Filter {FromAddress -eq "*contoso.com"}

Este exemplo suspende a mensagem com a ID de mensagem 3 da fila que não pode ser acessada no servidor Mailbox01:

    Suspend-Message -Identity Mailbox01\Unreachable\3

## Como saber se funcionou?

Para confirmar se suspendeu mensagens na fila com êxito, siga um dos seguintes passos:

  - No Visualizador de Filas, escolha a fila ou crie um filtro para confirmar que as mensagens estão suspensas.

  - Use o cmdlet **Get-Message** com os parâmetros *Queue* ou *Filter* para confirmar que as mensagens estão suspensas. Para mais informações, consulte [Get-Message](https://technet.microsoft.com/pt-br/library/bb124738\(v=exchg.150\)).

