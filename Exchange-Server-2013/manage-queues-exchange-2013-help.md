---
title: 'Gerenciar filas: Exchange 2013 Help'
TOCTitle: Gerenciar filas
ms:assetid: 37f11378-a884-4aff-ab55-689f40a46321
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997263(v=EXCHG.150)
ms:contentKeyID: 51407863
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar filas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-01-31_

No Microsoft Exchange Server 2013, você pode usar o Visualizador de Filas na Caixa de Ferramentas do Exchange ou o Shell de Gerenciamento do Exchange para gerenciar filas. Para obter mais informações sobre o uso de cmdlets de gerenciamento de filas no Shell de Gerenciamento do Exchange, consulte [Usar o Shell de gerenciamento do Exchange para gerenciar filas](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Filas", no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Exibir filas

## Usar o Visualizador de Filas na Caixa de Ferramentas do Exchange para exibir filas

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de email**, clique duas vezes em **Visualizador de Filas** para abrir a ferramenta em uma nova janela.

3.  No Visualizador de Filas, clique na guia **Filas**. É exibida uma lista de todas as filas no servidor ao qual você está conectado.

4.  Você pode usar o link **Exportar Lista** do painel de ações para exportar a lista de filas. Para obter mais informações, consulte [Exportar listas do Visualizador de filas](export-lists-from-queue-viewer-exchange-2013-help.md).

## Usar o Shell para exibir filas

Para exibir filas, use a seguinte sintaxe.

    Get-Queue [-Filter <Filter> -Server <ServerIdentity> -Include <Internal | External | Empty | DeliveryType> -Exclude <Internal | External | Empty | DeliveryType>]

Este exemplo exibe informações básicas sobre todas as filas não vazias no servidor de Caixa de Correio do Exchange 2013 chamado Mailbox01.

```powershell
Get-Queue -Server Mailbox01 -Exclude Empty
```

Este exemplo exibe informações detalhadas para todas as filas com mais de 100 mensagens no servidor de Caixa de Correio no qual o comando é executado.

```powershell
Get-Queue -Filter {MessageCount -gt 100} | Format-List
```

## Use o Shell para exibir informações de resumo de fila em vários servidores Exchange

O cmdlet **Get-QueueDigest** oferece uma exibição agregada de alto nível do estado das filas em todos os servidores dentro de um escopo específico; por exemplo, um DAG, um site do Active Directory, uma lista de servidores ou toda a floresta do Active Directory. Observe que filas em um servidor de Transporte de Borda inscrito na rede de perímetro não são incluídas nos resultados. Além disso, **Get-QueueDigest** está disponível em um servidor de Transporte de Borda, mas os resultados estão restritos a filas no servidor de Transporte de Borda.


> [!TIP]
> Por padrão, o cmdlet <STRONG>Get-QueueDigest</STRONG> exibe as filas de entrega que contenham dez ou mais mensagens e os resultados são de um a dois minutos atrás. Para instruções sobre como alterar estes valores padrões, consulte <A href="configure-get-queuedigest-exchange-2013-help.md">Configurar Get-QueueDigest</A>.



Para exibir informações de resumo sobre filas em vários servidores Exchange, execute o seguinte comando:

    Get-QueueDigest <-Server <ServerIdentity1,ServerIdentity2,..> | -Dag <DagIdentity1,DagIdentity2...> | -Site <ADSiteIdentity1,ADSiteIdentity2...> | -Forest> [-Filter <Filter>]

Este exemplo exibe informações de resumo sobre as filas em todos os servidores de Caixa de Correio do Exchange 2013 no site do Active Directory chamado FirstSite, onde a contagem de mensagens é superior a 100.

```powershell
Get-QueueDigest -Site FirstSite -Filter {MessageCount -gt 100}
```

Este exemplo exibe informações de resumo sobre as filas em todos os servidores de Caixa de Correio do Exchange 2013 no grupo de disponibilidade de banco de dados (DAG) denominado DAG01 onde o status da fila tem o valor **Repetir**.

```powershell
Get-QueueDigest -Dag DAG01 -Filter {Status -eq "Retry"}
```

## Retomar filas

Ao continuar uma fila, você reinicia as atividades de saída de uma fila cujo status é Suspenso. Para que essa ação tenha efeito, a fila deve apresentar o status Suspenso. Quando uma fila é continuada, o status das mensagens dessa fila não é alterado. As mensagens com status Suspenso permanecerão suspensas e não sairão da fila.

## Usar o Visualizador de Filas na Caixa de Ferramentas do Exchange para retomar filas

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de email**, clique duas vezes em **Visualizador de Filas** para abrir a ferramenta em uma nova janela.

3.  No Visualizador de Filas, clique na guia **Filas**. É exibida uma lista de todas as filas no servidor ao qual você está conectado.

4.  Clique em **Criar Filtro** e insira a expressão do filtro da seguinte maneira:
    
    1.  Selecione **Status** na lista suspensa de propriedades da fila.
    
    2.  Selecione **É Igual a** na lista suspensa de operadores de comparação.
    
    3.  Selecione **Suspenso** na lista suspensa de valores.

5.  Clique em **Aplicar Filtro**. Todas as filas do servidor atualmente suspensas são exibidas.

6.  Selecione uma ou mais filas na lista, clique com o botão direito do mouse e selecione **Continuar**.

## Usar o Shell para retomar filas

Para continuar filas, use a seguinte sintaxe.

    Resume-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

Este exemplo retoma todas as filas no servidor local com um status Suspenso.

```powershell
Resume-Queue -Filter {Status -eq "Suspended"}
```

Este exemplo retoma a fila de entrega suspensa chamada contoso.com no servidor denominado Mailbox01.

```powershell
Resume-Queue -Identity Mailbox01\contoso.com
```

## Como saber se funcionou?

Para verificar se você retomou com êxito uma fila, faça o seguinte:

1.  Use o Visualizador de Filas ou o cmdlet **Get-Queue** para localizar a fila que você tentou retomar.

2.  Verifique se a propriedade **Status** da fila não tem o valor `Suspended`.

## Filas de repetição

Quando um servidor de transporte não puder se conectar ao próximo salto, a fila de entrega será colocada em um status de repetição. Ao repetir uma fila de repetição utilizando o Visualizador de Filas ou o Shell, você força uma tentativa de conexão imediata e substitui o horário da próxima tentativa agendado. Se a conexão não for bem-sucedida, o cronômetro do intervalo de repetição será reiniciado. A fila de entrega deve estar no status Repetição para que essa ação entre em vigor.

## Usar o Visualizador de Filas na Caixa de Ferramentas do Exchange para repetir uma fila

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de email**, clique duas vezes em **Visualizador de Filas** para abrir a ferramenta em uma nova janela.

3.  No Visualizador de Filas, clique na guia **Filas**. É exibida uma lista de todas as filas no servidor ao qual você está conectado.

4.  Clique em **Criar Filtro** e insira a expressão do filtro da seguinte maneira:
    
    1.  Selecione **Status** na lista suspensa de propriedades da fila.
    
    2.  Selecione **É Igual a** na lista suspensa de operadores de comparação.
    
    3.  Selecione **Repetir** na lista suspensa de valores.

5.  Clique em **Aplicar Filtro**. Todas as filas com um status atual **Repetir** são exibidas.

6.  Selecione uma ou mais filas da lista. Clique com o botão direito e, em seguida, selecione **Repetir Fila**. Se a tentativa de conexão obtiver êxito, o status da fila será alterado para **Ativo**. Se nenhuma conexão for estabelecida, a fila permanecerá em um status **Repetir** e o horário da próxima tentativa será atualizado.

## Use o Shell para repetir uma fila

Para repetir filas, use a seguinte sintaxe.

    Retry-Queue <-Identity QueueIdentity | -Filter QueueFilter [-Server ServerIdentity]>

Este exemplo repete todas as filas no servidor local com o status Repetir.

```powershell
Retry-Queue -Filter {status -eq "retry"}
```

Este exemplo repete a fila chamada contoso.com que está no estado `Retry` no servidor denominado Mailbox01.

```powershell
Retry-Queue -Identity Mailbox01\contoso.com
```

## Como saber se funcionou?

Para verificar se você repetiu com êxito uma fila, faça o seguinte:

1.  Use o Visualizador de Filas ou o cmdlet **Get-Queue** para localizar a fila que você tentou repetir.

2.  Verifique se a propriedade **LastRetryTime** da fila corresponde à hora em que você tentou repetir a fila.

## Reenviar mensagens em filas

O reenvio de uma fila é semelhante a repeti-la, exceto que as mensagens são enviadas de volta para a fila Envio para que o categorizador as reprocesse. É possível reenviar mensagens com os seguintes status:

  - As filas de entrega com o status Repetir. As mensagens nas filas não devem estar no estado Suspenso.

  - Mensagens na fila de mensagens Inacessíveis que não estão no estado Suspenso.

  - Mensagens na fila de mensagens suspeitas.

## Usar o Shell para reenviar mensagens

Para reenviar mensagens, use a sintaxe a seguir.

    Retry-Queue <-Identity QueueIdentity | -Filter {Status -eq "Retry"} -Server ServerIdentity> -Resubmit $true

Este exemplo reenvia todas as mensagens localizadas em todas as filas de entrega com o status Repetir no servidor denominado Mailbox01.

```powershell
Retry-Queue -Filter {Status -eq "Retry"} -Server Mailbox01 -Resubmit $true
```

Este exemplo reenvia todas as mensagens localizadas na fila Inacessível no servidor Mailbox01.

```powershell
Retry-Queue -Identity Mailbox01\Unreachable -Resubmit $true
```

## Reenviar mensagens localizadas na fila de mensagens suspeitas

Você reenvia mensagens na fila de mensagens suspeitas ao retomar a mensagem. Você pode usar o Visualizador de Filas ou o Shell para reenviar mensagens da fila de mensagens suspeitas. Observe que a fila de mensagens suspeitas só estará visível no Visualizador de Filas quando houver mensagens na fila de mensagens suspeitas.


> [!TIP]
> A fila de mensagens suspeitas contém mensagens consideradas perigosas para o sistema Exchange após uma falha do servidor. As mensagens podem ser genuinamente prejudiciais em seu conteúdo ou formato. Como alternativa, elas podem ser vítimas de um agente mal escrito que travou o servidor do Exchange enquanto ele estava processando as mensagens supostamente inválidas. Se você não tiver certeza quanto à segurança das mensagens na fila de mensagens suspeitas, exporte as mensagens para arquivos para examiná-las. Para obter mais informações, consulte <A href="export-messages-from-queues-exchange-2013-help.md">Exportar mensagens de filas</A>.



## Usar o Visualizador de Filas na Caixa de Ferramentas do Exchange para reenviar mensagens na fila de mensagens suspeitas

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de email**, clique duas vezes em **Visualizador de Filas** para abrir a ferramenta em uma nova janela.

3.  No Visualizador de Filas, clique na guia **Filas**. É exibida uma lista de todas as filas no servidor ao qual você está conectado.

4.  Clique na fila de mensagens suspeitas. No painel de ações, selecione **Exibir Mensagens**.

5.  Selecione uma ou mais mensagens na lista, clique com o botão direito e selecione **Continuar**.

## Usar o Shell para reenviar mensagens na fila de mensagens suspeitas

Para reenviar uma mensagem da fila de mensagens suspeitas, execute as etapas a seguir.

1.  Localize a identidade da mensagem ao executar o comando a seguir.
    
    ```powershell
Get-Message -Queue Poison | Format-Table Identity
```

2.  Use a identidade da mensagem da etapa anterior no comando a seguir.
    
    ```powershell
Resume-Message <PoisonMessageIdentity>
```
    
    Este exemplo retoma uma mensagem da fila de mensagens suspeitas que tem o valor de Identidade da mensagem 222.
    
    ```powershell
Resume-Message 222
```

## Como saber se funcionou?

Para verificar se você reenviou com êxito uma mensagem da fila de mensagens suspeitas, faça o seguinte:

1.  Use o Visualizador de filas ou o cmdlet **Get-Queue** para exibir a fila de mensagens suspeitas onde você tentou reenviar a mensagem.

2.  Verifique se a mensagem não está mais na fila de mensagens suspeitas. Observe que uma fila de mensagens suspeitas vazia não aparece no Visualizador de Filas ou no cmdlet **Get-Queue**. Portanto, se a mensagem reenviada foi a única mensagem da fila de mensagens suspeitas, e se a fila de mensagens suspeitas não estiver mais visível, essa também é uma indicação de um reenvio de mensagem com êxito.

## Suspender filas

Ao suspender uma fila, você evita que mensagens deixem a fila, mas não altera o status das mensagens na fila. As mensagens que forem entregues por meio de SMTP-send terminarão as operações. Você pode suspender uma fila para interromper o fluxo de mensagens e, depois, suspender uma ou mais mensagens da fila. Quando você continuar a fila, as mensagens que foram suspensas não deixarão a fila.

Você pode suspender uma fila que tenha um status Ativo ou Repetir. Você também pode suspender a fila Inacessível e a fila de Envio.

Se você suspender a fila de mensagens inacessíveis, os itens não serão reenviados para o categorizador quando atualizações de configuração forem recebidas pelo servidor de transporte até que a fila continue. Se você suspender a fila de Envio, as mensagens só serão escolhidas pelo categorizador depois que a fila continuar.

## Usar o Visualizador de Filas na Caixa de Ferramentas do Exchange para suspender uma fila

1.  Clique em **Iniciar** \> **Todos os Programas** \> **Microsoft Exchange 2013** \> **Caixa de Ferramentas do Exchange**.

2.  Na seção **Ferramentas de fluxo de email**, clique duas vezes em **Visualizador de Filas** para abrir a ferramenta em uma nova janela.

3.  No Visualizador de Filas, clique na guia **Filas**. É exibida uma lista de todas as filas no servidor ao qual você está conectado. Você pode criar um filtro para exibir somente filas que atendam a critérios específicos.

4.  Selecione uma ou mais filas, clique com o botão direito do mouse e selecione **Suspender**.

## Use o shell para suspender uma fila

Para suspender uma fila, use a sintaxe a seguir.

    Suspend-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

Este exemplo suspende todas as filas do servidor local que tiverem uma contagem de mensagens igual ou superior a 1.000 e o status Repetir.

```powershell
Suspend-Queue -Filter {MessageCount -ge 1000 -and Status -eq "Retry"}
```

Este exemplo suspende a fila chamada contoso.com no servidor denominado Mailbox01.

```powershell
Suspend-Queue -Identity Mailbox01\contoso.com
```

## Como saber se funcionou?

Para verificar se você suspendeu com êxito uma fila, faça o seguinte:

1.  Use o Visualizador de Filas ou o cmdlet **Get-Queue** para localizar a fila que você tentou suspender.

2.  Verifique se a propriedade **Status** da fila tem o valor `Suspended`.

