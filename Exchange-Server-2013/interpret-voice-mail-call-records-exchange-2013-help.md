---
title: 'Interpretar os registros de chamadas de correio de voz: Exchange 2013 Help'
TOCTitle: Interpretar os registros de chamadas de correio de voz
ms:assetid: 368d9c58-61a2-43d5-8189-d3469a9e2a8d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659061(v=EXCHG.150)
ms:contentKeyID: 50556162
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interpretar os registros de chamadas de correio de voz

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Para exibir informações detalhadas sobre chamadas manipuladas pelos servidores Exchange em um dia específico, exporte os dados de chamada desse dia de um relatório de Estatísticas de Chamada. Os dados de chamada diária, que estão disponíveis para os últimos 90 dias, podem ajudar você a diagnosticar problemas com a qualidade de áudio ou chamadas rejeitadas e fornecer informações para auditorias ou relatórios sobre seus servidores Exchange em sua organização.

Para tarefas adicionais relacionadas aos relatórios da UM, consulte [Procedimentos de relatórios de Unificação de mensagens](um-reports-procedures-exchange-2013-help.md).

## Usar o EAC para exportar registros de chamadas da UM diárias

1.  No EAC, navegue até **Unificação de mensagens** \> **Mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") \> **Estatísticas de chamada**.

2.  Em **Exibir**, clique em **Diária (90 dias)** e depois selecione o plano de discagem de UM ou um gateway IP da UM, ou ambos, se desejar. O relatório é atualizado automaticamente conforme você escolhe as opções.

3.  Selecione o dia do qual deseja exportar os registros de chamada e clique em **Exportar Dia**.

4.  Na caixa de confirmação **Download de Arquivo**, clique em **Abrir** ou **Salvar**.
    
    O arquivo exportado será denominado um\_cdr\_*AAAA-MM-DD*.csv, onde *AAAA-MM-DD* representa o ano, o mês e o dia em que o relatório foi executado.
    

    > [!TIP]
    > Na página de relatórios, é possível baixar um modelo do Microsoft Excel para utilizar para importar o arquivo .csv de um dia específico.



5.  Use um aplicativo como o Excel para processar o arquivo .csv e criar seus próprios relatórios personalizados.

## Interpretar dados de chamada da UM

Os dados de chamada de UM que você exporta inclui as informações detalhadas a seguir sobre cada chamada manipulada pelo UM em determinado dia.


> [!TIP]
> No relatório de Estatísticas de Chamada, os dias estão no horário UTC.



  - **CallStartTime   **A data e a hora em que a UM manipulou a chamada, em UTC. A data e a hora UTC é representada no seguinte formato: *AAAA-MM-DD hh:mm:SSZ*, em que *AAAA* = ano, *MM* = mês, *DD* = dia, *hh* = hora, no tempo de 24 horas, *mm* = minutos, ss = segundos. Z significa Zulu, que é uma maneira de denotar UTC (como +*hh*:*mm* ou -*hh*:*mm*, que fornece a diferença de horário de UTC). Como os horários de todas as chamadas nesse relatório estejam em UTC, sempre haverá o Z.
    
    Por exemplo, para uma chamada feita em 23.06.13, às 14:23, o horário de início será mostrado como 23.06.13 14:23:11Z.

  - **Tipo de chamada   **O tipo de chamada:
    
      - **Mensagens de Voz de Atendimento de Chamadas**   A chamada não foi atendida e foi encaminhada aos servidores Exchange e o chamador deixou uma mensagem de voz.
    
      - **Chamada Perdida de Atendimento de Chamadas**   A chamada não foi atendida e foi encaminhada aos servidores Exchange e o chamador não deixou uma mensagem de voz.
    
      - **Acesso de Assinante**   Foi feita uma chamada para o número de acesso de assinante. O chamador entrou e foi autenticado para a UM com seu ramal e senha para acessar mensagens de email, calendários e mensagens de voz pelo telefone.
    
      - **Atendedor Automático**   A chamada foi atendida por um atendedor automático da UM. Essas chamadas geralmente são aquelas em que o chamador discou o número de telefone principal de sua organização.
    
      - **Fax**  Foi recebida uma chamada em que foi detectado um tom de fax. Se você configurou parceiros de fax, essa chamada foi enviada ao parceiro.
    
      - **PlayOnPhone:**  Uma chamada feita pela UM porque o usuário clicou no botão Tocar no Telefone em uma mensagem de voz no Microsoft Outlook Web App ou Outlook.
    
      - **Localize-me**   Uma chamada de saída foi feita pela UM como resultado de uma regra Localize-me em uma regra de atendimento de chamada.
    
      - **Número Piloto Não Autenticado**   Uma chamada foi feita para o número do Outlook Voice Access. O chamador não entrou e não foi autenticado.
    
      - **Gravação de Saudações**   Uma chamada foi feita pela UM para registrar saudações pessoais para um usuário.
    
      - **Nenhum**   Uma chamada foi feita, mas o tipo não foi definido.

  - **CallIdentity** A identidade da chamada SIP, conforme fornecida pelo gateway IP da UM.

  - **ParentCallIdentity** A Identidade da Sessão SIP da sessão que originou essa chamada. Essa caixa é usada ao usar o recurso Localize-me das Regras de Atendimento de Chamadas ou chamadas da transferência de chamadas, incluindo transferências entre atendedores automáticos da UM.

  - **UMServerName** O nome do servidor de Caixa de Correio que manipula a chamada, se houver. Essa informação será fornecida somente quando você tiver um servidor de Caixa de Correio no local.

  - **DialPlanName** O plano de discagem de UM que manipulou a chamada.

  - **Duração de Chamada** A duração total da chamada.

  - **IPGatewayAddress** O nome de domínio totalmente qualificado (FQDN) do gateway IP que manipulou a chamada.

  - **CalledPhoneNumber** O número do telefone ou endereço SIP do destinatário pretendido da chamada (para usuários em planos de discagem SIP com Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server) .

  - **CallerPhoneNumber** O número de telefone ou endereço de SIP do chamador.

  - **OfferResult** O status da chamada:
    
      - **Atendidas**   O UM atendeu ou realizou com êxito uma chamada. A chamada não foi transferida nem redirecionada. Essas chamadas incluem chamadas concluídas no Outlook Voice Access, Tocar no Telefone ou atendedores automáticos de UM e chamadas que a UM manipulou quando o ramal chamado não atendeu o telefone.
    
      - **Com Falha**   O UM aceitou ou realizou uma chamada, mas a chamada falhou. Essas chamadas incluem chamadas onde o número ou endereço chamado está ocupado, não responde ou não existe; em que o chamador desligou antes que a chamada fosse completada; em que o plano de discagem de UM ou as configurações de política de caixa de correio da UM impediram a chamada; ou onde o gateway VoIP ou PBX IP do sistema telefônico não puderam ser alcançados.
    
      - **Rejeitadas**   O UM rejeitou a chamada, normalmente devido a um erro de configuração. Essas chamadas incluem chamadas onde o gateway IP da UM não está associado a um plano de discagem da UM ou onde há problemas de incompatibilidade.
    
      - **Redirecionadas**   A UM aceitou a chamada, mas a redirecionou para outro servidor de Caixa de Correio. Essas chamadas incluem chamadas onde o chamador usou o menu da UM para chamar um contato no diretório ou nos contatos pessoais, ou onde o chamador chamou um número do Outlook Voice Access usando um número de telefone que não está associado à caixa de correio do usuário. Nesses casos, a UM transfere a chamada para o servidor Exchange que está associado a essa conta do usuário.
    
      - **Nenhum**   O status da chamada é desconhecido.

  - **DropCallReason** O motivo pelo qual a chamada foi desconectada, se a UM puder determinar o motivo. Por exemplo, se o chamador desligou, será mostrado Desligamento Polido.

  - **ReasonForCall** Como a chamada foi conectada:
    
      - **Direct**   O chamador discou diretamente o número chamado.
    
      - **DivertForward**   O chamador discou um número e a pessoa chamada redirecionou a chamada para uma caixa postal de UM.
    
      - **DivertBusy**  O chamador discou um número e o telefone estava ocupado, assim, a chamada foi redirecionada para a caixa postal da UM.
    
      - **DivertNoAnswer **  O chamador discou um número e a pessoa não atendeu, assim, a chamada foi redirecionada para a caixa postal de UM.
    
      - **Saída**   A chamada foi feita por uma UM, por exemplo, para reproduzir uma mensagem de voz usando Tocar no Telefone.
    
      - **Nenhum**   Nenhum motivo foi relatado para a chamada.

  - **DialedString** O endereço ou o número de telefone da pessoa para quem essa chamada foi dirigida ou transferida. Esse valor também se refere ao endereço ou número de telefone chamado para chamadas Tocar no Telefone.

  - **CallerMailboxAlias** O alias da caixa de correio (a parte do endereço de email que precede o símbolo @) do chamador. Esse valor estará disponível apenas se o chamador entrou no Outlook Voice Access.

  - **CallerMailboxAlias** O alias do destinatário pretendido da chamada, se o destinatário for um usuário habilitado para UM.

  - **Nome do Atendedor Automático** O nome do atendedor automático relacionado a essa chamada.

  - **Pontuação NMOS** A NMOS (pontuação média de opinião de rede) da chamada. A NMOS indica a qualidade do áudio da chamada em uma escala numérica de 1 a 5, sendo 5 excelente.
    

    > [!TIP]
    > <STRONG>Observação</STRONG>&nbsp;&nbsp;&nbsp;A NMOS máxima possível para uma chamada depende do codec de áudio que está sendo usado. A NMOS pode não estar disponível para chamadas muito curtas com menos de 10 segundos de duração.



  - **NMOSDegradation** A quantidade de degradação de áudio da pontuação NMOS do maior valor possível para o codec de áudio que está sendo utilizado. Por exemplo, se o valor de degradação de NMOS de uma chamada fosse 1,2 e a NMOS relatada para a chamada fosse de 3,3, a NMOS máxima para essa chamada seria de 4,5 (1,2 + 3,3).

  - **Tremulação NMOSDegradation** A degradação de NMOS total devido à tremulação.

  - **NMOSDegradation PacketLoss** A degradação de NMOS total devido à perda de pacote.

  - **Tremulação   **A variação média na chegada de pacotes de dados da chamada.

  - **PacketLoss    **A porcentagem média da perda de pacote de dados para a chamada selecionada. A perda de pacote é uma indicação da confiabilidade da conexão.

  - **Viagem de Ida e Volta** A pontuação média de viagem de ida e volta, em milissegundos, do áudio na chamada selecionada. A pontuação da viagem de ida e volta mede a latência da conexão.

  - **BurstDensity   **A porcentagem de pacotes perdidos e descartados em um período de intermitência (taxa alta de perda).

  - **Duração do Intervalo da Intermitência   **A duração média da perda de pacote durante intermitências de perdas para a chamada selecionada.

  - **Codec de Áudio   **O codec de áudio usado durante a chamada.

