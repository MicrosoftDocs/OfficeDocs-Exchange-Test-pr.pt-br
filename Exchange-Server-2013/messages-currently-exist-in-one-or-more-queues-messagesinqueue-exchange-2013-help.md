---
title: 'Mensagens existem atualmente em um ou mais queues_MessagesInQueue: Exchange 2013 Help'
TOCTitle: Mensagens existem atualmente em um ou mais queues_MessagesInQueue
ms:assetid: 3ffcdc7e-c1b7-49a7-8e5f-b30c0397908d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.messagesinqueue(v=EXCHG.150)
ms:contentKeyID: 50485413
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mensagens existem atualmente em um ou mais queues\_MessagesInQueue

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

A instalação do Microsoft® Exchange Server 2007 exibe esse aviso, pois ao tentar desinstalar uma função de transporte pode causar perda de dados de uma fila de transporte.

A instalação do Exchange 2007 verifica para certificar-se de que as filas dos transportes estiverem vazias, antes que ele remove as funções associadas ao gerenciar essas filas.

Se você remover as funções de transporte antes da entrega de mensagens ainda em filas dos transportes, essas mensagens podem ser mantidas indefinidamente.

Para resolver esse problema, inspecione as filas referenciadas para certificar-se de que eles estiverem vazios de mensagens antes de continuar com a instalação.

Para exibir o conteúdo de uma fila

1.  Abra o Console de gerenciamento do Exchange.

2.  Na árvore do console, clique em **Caixa de Ferramentas**.

3.  No painel de resultados, clique em **Visualizador de filas do Exchange**.

4.  No painel de ações, clique em **Abrir Ferramenta**.

5.  No Visualizador de fila, clique na guia **filas**. É exibida uma lista de todas as filas no servidor ao qual você está conectado.

6.  Clique com o botão a fila que você deseja e selecione **Propriedades** para exibir as propriedades da fila.

Para exibir as mensagens em uma fila

1.  Siga as etapas 1 a 4.

2.  No Visualizador de fila, clique na guia **mensagens**. É exibida uma lista de todas as mensagens no servidor ao qual você está conectado. Para ajustar o modo de exibição para uma única fila, clique na guia **filas**, duas vezes no nome da fila e, em seguida, clique na guia de Server\\Queue que aparece.

3.  Para exibir informações detalhadas sobre uma mensagem, selecione uma mensagem e clique em **Propriedades** no painel de ações.

