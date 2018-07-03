---
title: 'Revise as chamadas de correio de voz para um usuário: Exchange 2013 Help'
TOCTitle: Revise as chamadas de correio de voz para um usuário
ms:assetid: 95768fe3-3ae2-43bd-9cbf-18c3b85c4592
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659070(v=EXCHG.150)
ms:contentKeyID: 50556246
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Revise as chamadas de correio de voz para um usuário

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Logs de chamada do usuário são usados para exibir as seguintes informações sobre usuários de Unificação de mensagens (UM) específicos:

  - Detalhes sobre as chamadas de Unificação de mensagens para um usuário nos últimos 90 dias.

  - Qualidade de áudio de cada chamada. Métricas de qualidade de áudio podem não estar disponíveis para todas as chamadas, porque as métricas dependem de diversos fatores, como o tipo e o comprimento da chamada.

Para tarefas adicionais relacionadas aos relatórios da UM, consulte [Procedimentos de relatórios de Unificação de mensagens](um-reports-procedures-exchange-2013-help.md).

## Como obter os logs de chamada para um usuário habilitado para Unificação de mensagens?

1.  No Exchange Administration Center (EAC), selecione a **Unificação de mensagens** \> **mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") \> **logs de chamada do usuário**.

2.  Clique em **Selecionar um usuário** e selecione o usuário do qual você deseja os dados.

3.  Para obter mais detalhes sobre a qualidade de áudio para uma linha no relatório, selecione a linha e clique em **Detalhes de qualidade de áudio**. Para obter mais informações sobre como interpretar a qualidade do áudio, consulte [Investigar a qualidade de áudio de chamadas de voz para um usuário](investigate-the-audio-quality-of-voice-calls-for-a-user-exchange-2013-help.md).

4.  Para copiar o relatório para a área de transferência, clique em **Copiar todas as linhas na área de transferência.**

## Como posso interpretar o log de chamada do usuário de Unificação de mensagens?

O log de chamada de usuário inclui as seguintes informações para cada chamada:

  - **Data e hora** A data e hora da chamada, no fuso horário que o usuário selecionado tiver definido no Microsoft Outlook Web App.

  - **Duração** Quanto tempo a chamada duração em minutos (MM) e segundos (SS), no seguinte formato: mm: ss.

  - **Tipo de chamada** O tipo de chamada:
    
      - **Atendimento de chamadas**   A chamada não foi atendida e foi encaminhada para os servidores de caixa de correio e o chamador à esquerda de uma mensagem de voz.
    
      - **Chamada de atendimento de chamadas não atendidas**   A chamada não foi atendida e foi encaminhada para os servidores de caixa de correio e o chamador não deixaram uma mensagem de voz.
    
      - **Acesso de Assinante**   Foi feita uma chamada para o número de acesso de assinante. O chamador entrou e foi autenticado para a UM com seu ramal e senha para acessar mensagens de email, calendários e mensagens de voz pelo telefone.
    
      - **Atendedor Automático**   A chamada foi atendida por um atendedor automático da UM. Essas chamadas geralmente são aquelas em que o chamador discou o número de telefone principal de sua organização.
    
      - **Fax**   Uma chamada foi recebida no qual foi detectado um tom de fax. Se você configurou os parceiros de fax, essa chamada foi enviada para o parceiro.
    
      - **PlayonPhone**   Uma chamada feita por UM porque o usuário clicou tocar no botão de telefone em uma mensagem de voz no Microsoft Outlook Web App ou Outlook.
    
      - **FindMe**   Uma chamada de saída foi feita pela Unificação de mensagens como resultado de uma Find Me regra em uma regra de atendimento de chamada.
    
      - **Número Piloto Não Autenticado**   Uma chamada foi feita para o número do Outlook Voice Access. O chamador não entrou e não foi autenticado.
    
      - **Gravação de Saudações**   Uma chamada foi feita pela UM para registrar saudações pessoais para um usuário.
    
      - **Nenhum**   Uma chamada foi feita, mas o tipo não foi definido.

  - **Número de chamada** O número de telefone ou o endereço SIP do chamador.

  - **Número CHAMADO** O número de telefone ou endereço do SIP (para usuários em planos de discagem SIP, como usuários do Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server) do destinatário da chamada.

  - **GATEWAY IP de UM** Gateway IP de UM que recebeu a ligação.

  - **Qualidade de áudio** A qualidade geral de áudio da chamada. Para obter mais detalhes sobre a qualidade do áudio, selecione a linha e clique em **Detalhes de qualidade de áudio**.

