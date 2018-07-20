---
title: 'Revise as chamadas de correio de voz em sua organização: Exchange 2013 Help'
TOCTitle: Revise as chamadas de correio de voz em sua organização
ms:assetid: f6fdbe17-d1d2-442a-aa13-06b908d9c33a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659073(v=EXCHG.150)
ms:contentKeyID: 50556316
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Revise as chamadas de correio de voz em sua organização

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode usar o relatório de estatísticas de chamada para exibir informações sobre o tipo e o status de chamadas de entrada manipuladas pelos servidores do Exchange em sua organização. O relatório apresenta informações estatísticas sobre as chamadas encaminhadas para ou realizadas pela Unificação de mensagens (UM) para sua organização. Você pode usar essas informações para rastrear o uso de planejamento da capacidade, monitorar e solucionar problemas de disponibilidade e a qualidade de áudio da UNIFICAÇÃO de mensagens e solucionar problemas de chamadas com falha.

Este tópico responde a essas perguntas:

  - How do I get call statistics for UM?

  - How do I interpret UM call statistics?

Para tarefas adicionais relacionadas aos relatórios da UM, consulte [Procedimentos de relatórios de Unificação de mensagens](um-reports-procedures-exchange-2013-help.md).

## Como obter as estatísticas de chamada do UM?

1.  No Centro de administração do Exchange (EAC), clique em **Unificação de mensagens** \> **mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") \> **estatísticas de chamadas**.

2.  Escolha as informações que você deseja incluir no relatório. O relatório é atualizado automaticamente conforme você selecionar qualquer uma das seguintes opções:
    
      - **Mostrar**   Escolha qual tipo de estatísticas de chamada para exibir:
        
          - **Diariamente (90 dias)**   Selecione diariamente para ver detalhes de todas as chamadas nos últimos 90 dias.
        
          - **Mensalmente (12 meses)**   Selecione mensal para ver um resumo das chamadas por mês nos últimos 12 meses.
        
          - **Todos os**   Selecione tudo para ver as estatísticas de combinado de todas as chamadas recebidas desde UM tratamento de chamadas.
    
      - **Plano de Discagem do UM**   Se deseja limitar os dados do relatório somente a chamadas em um plano de discagem do UM específico, selecione esse plano de discagem.
    
      - **Gateway IP do UM**   Se deseja limitar os dados do relatório somente a chamadas de um gateway IP do UM específico, selecione esse gateway. Se você selecionar um plano de discagem do UM primeiro, somente os gateways IP do UM associados ao plano de discagem do UM selecionado estarão disponíveis na lista.

3.  Para obter mais detalhes sobre a qualidade de áudio para uma linha no relatório, selecione a linha e clique em **Detalhes de qualidade de áudio**. Para obter mais informações sobre como interpretar a qualidade do áudio, consulte [Investigar a qualidade de áudio de chamadas de voz em sua organização](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md).

4.  Para copiar o relatório para a área de transferência, clique em **Copiar**.

5.  Para relatórios de diários, você pode exportar os detalhes de um dia específico para um arquivo. csv.
    
    1.  Selecione o dia e clique em **Exportar dia**.
    
    2.  Na caixa de confirmação **Download de Arquivo**, clique em **Abrir** ou **Salvar**.
    
    O arquivo exportado será denominado um\_cdr\_*YYYY-MM-DD*. csv, onde *YYYY-MM-DD* é o ano, mês e dia em que o relatório foi executado. Para obter mais informações, consulte [Interpretar os registros de chamadas de correio de voz](interpret-voice-mail-call-records-exchange-2013-help.md).
    

    > [!TIP]
    > Na página de relatórios, é possível baixar um modelo do Microsoft Excel para utilizar para importar o arquivo .csv de um dia específico.



Voltar ao início

## Como interpretar as estatísticas de chamada do UM?

O relatório de Estatísticas de Chamada do UM inclui as seguintes informações:

  - **Data**   A data de UTC para os dados de chamada. O formato de data depende do tipo de relatório que você escolheu e suas configurações de localidade. Você pode escolher entre as seguintes opções:
    
      - **--- **  Todas as chamadas são exibidas.
    
      - **MMM/AA**   O mês das chamadas. Por exemplo, 13/Jan.
    
      - **MM/DD/AA**   O dia das chamadas. Por exemplo, 23/6/13.

  - **TOTAL**   O número total de chamadas do plano de discagem do UM selecionado ou do gateway IP do UM dessa data.

  - **MENSAGEM DE VOZ**   Percentual de chamadas de entrada atendidas pelo UM em nome dos usuários nas quais o chamador deixou uma mensagem de voz.

  - **PERDIDA**   A porcentagem de chamadas de entrada atendidas pela Unificação de mensagens em nome de usuários em que os chamadores não deixaram uma mensagem de voz, resultando em uma notificação de chamada perdida.

  - **OUTLOOK VOICE ACCESS**   A porcentagem de chamadas de entrada onde os usuários entrou Unificação de mensagens (e foram autenticados) para acessar seus emails, calendários e mensagens de voz.

  - **Saída**   A porcentagem de chamadas que foram realizadas ou transferidas pela Unificação de mensagens em nome de usuários autenticados ou. Essa estatística inclui tipo localizar-Me, tocar no telefone e tocar no telefone saudações tipos de chamada.

  - **ATENDEDOR AUTOMÁTICO**   Percentual de chamadas de entrada que foram atendidas por atendedores automáticos do UM.

  - **FAX**   Percentual de chamadas de entrada que foram redirecionadas para um parceiro de fax.

  - **Outra**   A porcentagem de qualquer outras entradas ou inseridas chamadas que não se enquadram em qualquer uma das categorias acima. Essas chamadas incluem as chamadas feitas para números do Outlook Voice Access onde os usuários não entrar e não foram autenticados.

  - **Falha ou REJEITADA**   A porcentagem de chamadas que falharam ou foram rejeitadas pelo Unificação de mensagens. Observe que as chamadas com falha não são contadas duas vezes. Por exemplo, se uma chamada para o Outlook Voice Access falhar, ele é apenas contado como uma chamada de falha e não como uma chamada do Outlook Voice Access.

  - **QUALIDADE DO ÁUDIO**   Uma representação gráfica da qualidade geral do áudio no período de tempo selecionado na organização.

Voltar ao início

## Para obter mais informações

[Investigar a qualidade de áudio de chamadas de voz em sua organização](investigate-the-audio-quality-of-voice-calls-in-your-organization-exchange-2013-help.md)

[Interpretar os registros de chamadas de correio de voz](interpret-voice-mail-call-records-exchange-2013-help.md)

