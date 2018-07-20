---
title: 'Alternar um Servidor: Exchange 2013 Help'
TOCTitle: Alternar um Servidor
ms:assetid: ffcefd56-b0a0-4229-9011-fff4197b7c74
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298187(v=EXCHG.150)
ms:contentKeyID: 62523827
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alternar um Servidor

 

_**Aplica-se a:** Exchange Server 2013 SP1_

_**Tópico modificado em:** 2014-06-23_

Uma alternância de servidor é uma tarefa que você executa para mover todas as cópias de banco de dados de caixa de correio ativas de seu servidor de caixa de correio atual para um ou mais servidores de caixa de correio em um grupo de disponibilidade de banco de dados (DAG). Essa tarefa poderia ser executada como parte da preparação para um período de inatividade agendado para o servidor de Caixa de correio selecionado.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 30 segundos por base de dados.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de disponibilidade do banco de dados" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o EAC para realizar uma alternância de servidor

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

1.  No EAC, vá até **Servidores** \> **servidores**.

2.  Selecione o servidor de Caixa de Correio em que deseja executar uma alternância.

3.  No painel de ações, selecione **Alternância do Servidor**.

4.  Na página **Alternância de Servidor**, execute um dos seguintes procedimentos:
    
    1.  Aceite a configuração padrão **Escolher um servidor de destino automaticamente** (neste caso, o sistema seleciona automaticamente o melhor servidor de Caixa de Correio para cada banco de dados que esteja sendo alternado) e clique em **salvar**.
    
    2.  Clique em **Usar o servidor especificado como destino para alternância**, clique em **Procurar** para selecionar um servidor de Caixa de Correio e, em seguida, clique em **salvar**.

5.  Quando a alternância for concluída, clique em **fechar** para sair da página de **Alternância de Servidor**.

## Use o Shell para realizar uma alternância de servidor

Este exemplo realiza uma alternância para o servidor de Caixa de Correio MBX1. O sistema automaticamente seleciona o melhor servidor de caixa de correio para cada banco de dados ativo no MBX1.

    Move-ActiveMailboxDatabase -Server MBX1

Este exemplo realiza uma alternância para o servidor de Caixa de Correio MBX1. Quando o comando estiver completo, o MBX5 hospeda a cópia ativa do banco de dados que estava previamente ativo no MBX4.

    Move-ActiveMailboxDatabase -Server MBX4 -ActivateOnServer MBX5

Para obter informações detalhadas de sintaxes e de parâmetros, consulte [Move-ActiveMailboxDatabase](https://technet.microsoft.com/pt-br/library/dd298068\(v=exchg.150\)).

