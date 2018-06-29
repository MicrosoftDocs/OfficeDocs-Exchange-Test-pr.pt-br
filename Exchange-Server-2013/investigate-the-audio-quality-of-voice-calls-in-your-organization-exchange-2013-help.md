---
title: 'Investigar a qualidade de áudio de chamadas de voz em sua organização: Exchange 2013 Help'
TOCTitle: Investigar a qualidade de áudio de chamadas de voz em sua organização
ms:assetid: 8a87694b-1678-4a01-859f-5ad3b2c73db5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659069(v=EXCHG.150)
ms:contentKeyID: 50556238
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Investigar a qualidade de áudio de chamadas de voz em sua organização

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-21_

Se sua organização está tendo problemas com a qualidade de áudio de chamadas de Unificação de mensagens (UM) e mensagens de caixa postal, use o relatório de estatísticas de chamada para ajudá-lo a entender o que está causando os problemas.


> [!TIP]
> A qualidade de áudio de uma chamada pode ser afetada por fatores que não são abordados nos relatórios. Por exemplo, se os seus servidores Exchange estiver ocorrendo uma carga pesada de memória ou a carga da CPU, os usuários podem relatar qualidade de chamadas ruins, embora os relatórios mostram excelente qualidade de áudio.



Para tarefas adicionais relacionadas a estatísticas de chamadas, consulte [Procedimentos de relatórios de Unificação de mensagens](um-reports-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Cmdlets de dados de chamada de UM e relatórios de resumo", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o EAC para obter as estatísticas de qualidade de áudio para sua organização

1.  No EAC, navegue até **Unificação de mensagens** \> **mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") \> **estatísticas de chamadas**.

2.  Escolha as estatísticas de chamada para incluir no relatório. O relatório é atualizado automaticamente conforme você selecionar qualquer uma das opções a seguir.
    
      - **Mostrar**   Escolha qual tipo de estatísticas de chamada para exibir:
        
          - **Diariamente (90 dias)**   Selecione diariamente para ver detalhes de todas as chamadas nos últimos 90 dias.
        
          - **Mensalmente (12 meses)**   Selecione mensal para ver um resumo das chamadas por mês nos últimos 12 meses.
        
          - **Todos os**   Selecione tudo para ver as estatísticas de combinado de todas as chamadas recebidas desde UM tratamento de chamadas.
    
      - **Plano de Discagem do UM**   Se deseja limitar os dados do relatório somente a chamadas em um plano de discagem do UM específico, selecione esse plano de discagem.
    
      - **Gateway IP de UM**   Se você deseja limitar os dados do relatório para chamadas somente em um gateway IP de UM específico, selecione esse gateway IP de UM. Se você selecionar um plano de discagem de Unificação de mensagens pela primeira vez, somente os gateways IP de UM associados com o plano de discagem de Unificação de mensagens selecionado estão disponíveis na lista.

3.  Para obter mais detalhes sobre a qualidade de áudio de uma linha do relatório, selecione a linha e clique em **Detalhes de qualidade do áudio**. As seguintes informações estão disponíveis:
    
      - **Data e hora**   A data de UTC e a hora em que as estatísticas de chamada foram capturadas.
    
      - **Plano de DISCAGEM de Unificação de mensagens**   O plano de discagem para as chamadas incluídos nas estatísticas.
    
      - **GATEWAY IP de UM**   Gateway IP de UM que recebeu a incluídos nas estatísticas de chamadas.
    
      - **NMOS**   A NMOS (pontuação média de opinião de rede) da chamada. A NMOS indica a qualidade do áudio da chamada em uma escala numérica de 1 a 5, sendo 5 excelente.
        

        > [!TIP]
        > O máximo NMOS possíveis para uma chamada depende do codec de áudio que está sendo usado. O NMOS podem não estar disponíveis para chamadas muito curtas que são menos de 10 segundos.

    
      - **DEGRADAÇÃO DE NMOS**   A quantidade de degradação de áudio da pontuação NMOS do maior valor possível para o codec de áudio em utilização. Por exemplo, se o valor de degradação de NMOS de uma chamada fosse 1,2 e a NMOS relatada para a chamada fosse de 3,3, a NMOS máxima para essa chamada seria de 4,5 (1,2 + 3,3).
    
      - **TREMULAÇÃO**   A variação média na chegada de pacotes de dados da chamada.
    
      - **PERDA DE PACOTE**   A porcentagem média de perda de pacotes de dados da chamada selecionada. A perda de pacote é uma indicação da confiabilidade da conexão.
    
      - **VIAGEM DE IDA E VOLTA**   A pontuação média da viagem de ida e volta, em milissegundos, do áudio na chamada selecionada. A pontuação da viagem de ida e volta mede a latência da conexão.
    
      - **DURAÇÃO DA PERDA DE INTERMITÊNCIA**   A duração média da perda de pacote durante intermitências de perdas da chamada selecionada.
    
      - **Número de amostras**   O número de chamadas que foram amostra para calcular as médias.

4.  Para métricas de qualidade de áudio detalhadas para chamadas específicas, consulte [Investigar a qualidade de áudio de chamadas de voz para um usuário](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md).

