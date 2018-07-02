---
title: 'Investigar a qualidade de áudio de chamadas de voz para um usuário: Exchange 2013 Help'
TOCTitle: Investigar a qualidade de áudio de chamadas de voz para um usuário
ms:assetid: 0c945886-3cfa-423e-9b46-0d6b1584a145
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659059(v=EXCHG.150)
ms:contentKeyID: 50556142
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Investigar a qualidade de áudio de chamadas de voz para um usuário

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-21_

Se um usuário relatar problemas com a qualidade de áudio de suas chamadas de Unificação de Mensagens (UM), você pode usar o relatório de Logs de Chamadas de Usuário para ajudá-lo a entender a causa dos problemas.


> [!TIP]
> A qualidade de áudio de uma chamada pode ser afetada por fatores que não são abordados nos relatórios. Por exemplo, se os servidores do Exchange estiverem experimentando altas cargas de memória ou de CPU, os usuários podem relatar baixa qualidade de chamada mesmo que os relatórios mostrem excelente qualidade de áudio.



Para tarefas adicionais relacionadas aos relatórios de UM, consulte [Procedimentos de relatórios de Unificação de mensagens](um-reports-procedures-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Cmdlets de dados de chamada de UM e relatórios de resumo", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o EAC para obter os logs de chamada de um usuário habilitado para UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") \> **Logs de Chamada do Usuário**.

2.  Clique em **Selecionar um usuário** e selecione o usuário do qual você deseja os dados.

3.  Para obter mais detalhes sobre a qualidade de áudio de uma linha do relatório, selecione a linha e clique em **Detalhes de qualidade do áudio**. As seguintes informações estão disponíveis:
    
      - **DATA E HORA**   A data e a hora da chamada, no fuso horário que o usuário selecionado definiu no Outlook Web App.
    
      - **USUÁRIO**   O usuário selecionado.
    
      - **PLANO DE DISCAGEM DE UM**   O plano de discagem para a chamada.
    
      - **GATEWAY IP DE UM**   O gateway IP de UM que foi utilizado na chamada.
    
      - **CODEC DE ÁUDIO**   O codec de áudio utilizado durante a chamada.
    
      - **NMOS**   A NMOS (pontuação média de opinião de rede) da chamada. A NMOS indica a qualidade do áudio da chamada em uma escala numérica de 1 a 5, sendo 5 excelente.
        

        > [!TIP]
        > A pontuação NMOS máxima possível para uma chamada depende do codec de áudio que está sendo usado. A NMOS pode não estar disponível para chamadas muito curtas com menos de 10 segundos de duração.

    
      - **DEGRADAÇÃO DE NMOS**   A quantidade de degradação de áudio da pontuação NMOS do maior valor possível para o codec de áudio em utilização. Por exemplo, se o valor de degradação de NMOS de uma chamada fosse 1,2 e a NMOS relatada para a chamada fosse de 3,3, a NMOS máxima para essa chamada seria de 4,5 (1,2 + 3,3).
    
      - **TREMULAÇÃO**   A variação média na chegada de pacotes de dados da chamada.
    
      - **PERDA DE PACOTE**   A porcentagem média de perda de pacotes de dados da chamada selecionada. A perda de pacote é uma indicação da confiabilidade da conexão.
    
      - **VIAGEM DE IDA E VOLTA**   A pontuação média da viagem de ida e volta, em milissegundos, do áudio na chamada selecionada. A pontuação da viagem de ida e volta mede a latência da conexão.
    
      - **DURAÇÃO DA PERDA DE INTERMITÊNCIA**   A duração média da perda de pacote durante intermitências de perdas da chamada selecionada.

