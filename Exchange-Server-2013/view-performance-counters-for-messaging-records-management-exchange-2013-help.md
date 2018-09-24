---
title: 'Contadores de desempenho do modo de exibição de registros de mensagens'
TOCTitle: Contadores de desempenho do modo de exibição de gerenciamento de registros de mensagens
ms:assetid: ec374d31-2797-4f8b-8c96-3839d01a662c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb397227(v=EXCHG.150)
ms:contentKeyID: 51407932
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contadores de desempenho do modo de exibição de gerenciamento de registros de mensagens

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2009-12-09_

Você pode usar o Monitor de desempenho (Perfmon.exe) e Windows confiabilidade para selecionar e exibir os contadores de desempenho para mensagens (MRM) de gerenciamento de registros. Usando os contadores de desempenho, é possível monitorar Assistente de pasta gerenciada enquanto ele é executado em processos MRM consomem muitos recursos.

Para obter uma lista de contadores de desempenho para MRM, consulte [Contadores de desempenho para gerenciamento de registros de mensagens](performance-counters-for-https://docs.microsoft.com/pt-br/exchange/security-and-compliance/messaging-records-management/messaging-records-management).

Procurando outras tarefas relacionadas ao monitoramento MRM? Confira [Gerenciamento de registros de mensagens de monitoramento](monitoring-https://docs.microsoft.com/pt-br/exchange/security-and-compliance/messaging-records-management/messaging-records-management).

## Use o Monitor de desempenho e confiabilidade do Windows para exibir os contadores de desempenho para MRM

Para executar este procedimento, a conta utilizada deve ser delegada a associação ao grupo Administradores local.

1.  Para iniciar Windows confiabilidade e desempenho do sistema, clique em **Iniciar**, clique em **Executar** e, em seguida, digite **perfmon**.

2.  Na árvore de console, navegue até **Ferramentas de monitoramento** \> **Monitor de desempenho**.

3.  Clique no botão de sinal de adição (+) na barra de ferramentas. A caixa de diálogo **Adicionar contadores** aparece.

4.  Na lista **Selecionar contadores do computador**, selecione uma das seguintes opções:
    
      - Se você estiver realizando este procedimento em um computador local, selecione **\< computador Local \>**. Esta é a seleção padrão.
    
      - Se você estiver realizando este procedimento remotamente, selecione o servidor que você deseja monitorar.

5.  Na lista de contadores de desempenho, expanda **Assistentes do MSExchange - por banco de dados** ou o **Assistente de MSExchange com pasta gerenciada**.

6.  Selecione os contadores de desempenho que você deseja monitorar.

7.  Contadores de desempenho em **Assistentes do MSExchange - por banco de dados**, para exibir os contadores para todos os bancos de dados de caixa de correio, nas **instâncias do objeto selecionado**, clique em **todas as instâncias**. Ou, para especificar um ou mais bancos de dados de caixa de correio, selecione instâncias da lista.

8.  Adicionar contadores selecionados, para que os contadores são exibidos no Monitor de desempenho e Windows confiabilidade e começar a coleta de dados de desempenho, clique em **Adicionar**.

