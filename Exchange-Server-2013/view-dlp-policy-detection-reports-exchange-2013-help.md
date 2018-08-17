---
title: 'Exibir relatórios de detecção de política DLP: Exchange 2013 Help'
TOCTitle: Exibir relatórios de detecção de política DLP
ms:assetid: 5c3f1cf6-d8c7-4d83-bb24-641ea9d50cbc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150520(v=EXCHG.150)
ms:contentKeyID: 50484714
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir relatórios de detecção de política DLP

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-16_

Gerenciamento de detecção política do prevention (DLP) de perda de dados amplamente define as atividades que uma organização executa a fim de identificar, investigar e resolver violações de política DLP. Para gerenciar incidentes, você precisa ter acesso às informações que identifica o que foi detectado pelo suas políticas de DLP. Essas informações de detecção são integradas com dados de Exchange Server 2013 Microsoft existentes e formatos de log para que você pode aproveitar a um sistema de rich existente de dados para gerenciar seus incidentes de fluxo de email.

Para obter informações sobre como criar um relatório de incidente juntamente com um evento de detecção de única política, consulte [Criar relatórios de incidentes para detecções de política DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md). Para obter mais informações sobre logs de mensagem, consulte [Acompanhar mensagens com notificações de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).


> [!NOTE]
> Exchange 2013: DLP é um recurso premium que exige uma licença dos Serviços da Enterprise CAL do Exchange. Para saber mais sobre CALs e sobre licenciamento de servidor, confira o artigo <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licenciamento do Exchange Server</A>.



## Informações de auditoria

Dados relacionados ao gerenciamento de detecção de DLP no Exchange são integrados ao logs, de controle de mensagens, também conhecido como notificações de entrega. Os recursos reutilizar grande parte do log framework disponível no sistema existente. Para obter informações gerais, incluindo Noções básicas sobre a estrutura dos arquivos de log de controle de mensagens, verifique o conteúdo existente em [Understanding Message Tracking](message-tracking-exchange-2013-help.md) ou [Acompanhar mensagens com notificações de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).

O relatório de entrega é um log detalhado de todas as atividades de mensagem, como as mensagens são transferidas para e de um computador que está executando o serviço de transporte em um servidor de caixa de correio. A log de acompanhamento de mensagens podem ser acessada por meio do Shell de gerenciamento do Exchange usando o cmdlet **Get-MessageTrackingLog** . Dados DLP são integrados ao relatório de entrega seguindo as convenções e formatos de dados existente.

## Formato de log de dados

Logs de rastreamento de mensagens contêm dados dos agentes envolvidos no processamento do conteúdo de fluxo de email. Para DLP, o agente de regra de transporte (TRA) é usado para invocar a verificação do conteúdo da mensagem de profundidade e aplicar as políticas definidas como parte de ETRs. O evento AgentInfo existente é usado para adicionar DLP entradas no log de acompanhamento de mensagens relacionadas.

O nome do agente será **TRA** ou **Agente de regras de transporte** no evento AgentInfo. Um único evento AgentInfo será registrado por mensagem descrevendo o processamento de DLP aplicado à mensagem. O campo **CustomData** do campo de entrada do log de controle de mensagens é onde os dados DLP registrados pelo agente de regras de transporte serão exibida. Este campo pode conter várias entradas: linha de informações cliente quanto de classificação de dados de um para cada classificação de dados encontrada em uma linha de monitoramento de integridade para cada regra que excede o limite de carga ou tempo de execução, linha de uma regra para cada regra que se aplica à mensagem e a mensagem.

Exemplo da entrada de log DLP é exibido aqui. O resultado foi formatado para exibir as cadeias de caracteres em linhas separadas com novas linhas entre.

Fonte: AGENTE

EventId: AGENTINFO

CustomData: S:TRA = DC | dcid = 41BFDBC6C9D811E0816A3CD34824019B | contagem = 10 | conf = 77;

S:Tra = DC | dcid = C7ECCBA0CA0011E0B6C00B124924019B | contagem = 3 | conf = 81;

S:Tra = CI | sndOverride = ou | apenas = motivo comercial;

S:TRA=CI|sndOverride=fp;

S:TRA=ETR|ruleId=FC2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=PrependSubject|action=Encrypt|sev=2|mode=audit|dcid=41BFDBC6C9D811E0816A3CD34824019B|sndOverride=or;

S:TRA=ETR|ruleId=AB2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=Encrypt|sev=1|mode=enabled|dcid=C7ECCBA0CA0011E0B6C00B124924019B|sndOverride=fp;

S:TRA=ETRP|ruleId=C27D21EECA0311E0BCB896154924019B|LoadW=200|LoadC=100|ExecW=5500|ExecC=200;

O agente de regras de transporte exige agrupamento da regra ID, data de DLP ID da política (opcional), modificado pela última vez, action, severity, modo, detectada a classificação de dados (opcional) e substituição de remetente (opcional) com base na ID da regra (indicado pelo "TRA = ETR" na linha de log). Ele também requer a ID de classificação de dados, contagem e nível de confiança de classificações sejam agrupados por nome de classificação (indicado pelo "TRA = DC" na linha de log).

Agrupamentos adicionais incluem a ID de classificação de dados, substituição do remetente (opcional) e substituir justificativa (opcional) com base na ID de classificação de dados para todas as classificações que foram detectados no cliente (indicado pelo "TRA = CI" na linha de log). O agente de regras de transporte também requer a ID da regra, carga parede relógio (opcional), relógio de carga da CPU (opcional), relógio de parede de execução (opcional) e execução CPU relógio (opcional) ser agrupadas por ID de regra para todas as regras que excedem o carregamento ou execução parede ou CPU relógio limites (indicado pelo "TRA = ETRP" na linha de log).

O exemplo a seguir é uma lista completa dos campos de dados. Todos os dados no MTL é tipo cadeia de caracteres. Coluna formato descreve como reconhecer cada campo no Log de rastreamento de mensagem. Coluna de campo opcional especifica quais campos podem não estar conectado ao corresponde a uma regra. Coluna DLP específica mostra quais campos são específicos para o recurso DLP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Nome do campo</strong></p></td>
<td><p><strong>Descrição</strong></p></td>
<td><p><strong>Formato</strong></p></td>
<td><p><strong>Campo opcional</strong></p></td>
<td><p><strong>DLP específico</strong></p></td>
</tr>
<tr class="even">
<td><p>TRA</p></td>
<td><p>Agente de regras de transporte; Digite AgentName</p></td>
<td><p>TRA = DC, ETR, CI ou ETRP</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>DC</p></td>
<td><p>Classificação de dados; Digite o nome do grupo</p></td>
<td><p>TRA = DC</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>ETR</p></td>
<td><p>Regra de transporte do Exchange; Digite o nome do grupo</p></td>
<td><p>TRA = ETR</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>CI</p></td>
<td><p>Informações do cliente, tipo groupName</p></td>
<td><p>TRA = CI</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>ETRP</p></td>
<td><p>Desempenho de regra de transporte do Exchange; Digite o nome do grupo</p></td>
<td><p>TRA = ETRP</p></td>
<td><p>Opcional</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>dcid</p></td>
<td><p>ID da classificação de dados</p></td>
<td><p>dcid = GUID</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Contagem</p></td>
<td><p>Contagem da classificação de dados</p></td>
<td><p>Contagem = inteiro</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>conf</p></td>
<td><p>Nível de confiança da classificação de dados</p></td>
<td><p>conf = inteiro (%)</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>sndOverride</p></td>
<td><p>Substituição de remetente; o campo é opcional.</p>
<p>No TRA = CI linha, quando o campo é definido como &quot;ou&quot; significa que a classificação de dados foi substituída. Se o campo for definido como &quot;fp&quot; significa que a classificação de dados foi relatada como um falso positivo.</p>
<p>No TRA = linha ETR, quando o campo é definido como &quot;ou&quot; significa a regra ou parte da regra foi substituída. Se o campo é definido como &quot;fp&quot; significa a regra ou parte da regra foi relatado como um falso positivo.</p></td>
<td><p>sndOverride = ou ou fp</p>
<p>Onde &quot;ou&quot; substituição representa e &quot;fp&quot; significa falso positivo. O campo sndOverride está presente quando um usuário final tinha relatou uma substituição ou um falso positivo para uma regra.</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>apenas</p></td>
<td><p>Justificativa; o campo é opcional e só estará disponível quando o campo de substituição do remetente é igual a &quot;ou&quot; no TRA = CI linha. Justificativa texto fornecido pelo usuário final como o motivo pelo qual a classificação de dados deve ser substituída.</p></td>
<td><p>= apenas a cadeia de caracteres de entrada justificativa IW</p>
<p>Campo justificativa é registrado somente quando uma substituição de relatórios do usuário final.</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>ruleId</p></td>
<td><p>ID de uma regra</p></td>
<td><p>ruleId=GUID</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>dlpId</p></td>
<td><p>Identificação de uma política de DLP. O campo é opcional. Se não houver nenhuma dlpId a regra não pertence a uma política de DLP.</p></td>
<td><p>dlpId=GUID</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>ST</p></td>
<td><p>Última data de modificação de uma regra</p></td>
<td><p>Santa = a data e hora UTC</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>ação</p></td>
<td><p>Ação executada por uma regra; poderia ter várias ações por regra</p></td>
<td><p>ação = ação única</p>
<p>Se houver várias ações aplicadas para uma regra, haverá vários campos de ação.</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>sev</p></td>
<td><p>Gravidade da auditoria da regra</p></td>
<td><p>sev = 1, 2 ou 3</p>
<p>Onde 1 representa baixa, 2 é medium e 3 significa que alta.</p></td>
<td><p>Opcional</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>modo</p></td>
<td><p>Estado da regra quando ele estava choque (imposição, auditoria ou auditandnotify).</p></td>
<td><p>modo = auditoria, auditandnotify ou imposição</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>loadW</p></td>
<td><p>Carregar um relógio de parede; o campo é opcional</p></td>
<td><p>loadW = tempo em ms</p></td>
<td><p>Opcional</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>loadC</p></td>
<td><p>Carregar Clock de CPU; o campo é opcional</p></td>
<td><p>loadC = tempo em ms</p></td>
<td><p>Opcional</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>execW</p></td>
<td><p>Executar o relógio parede; o campo é opcional</p></td>
<td><p>execW = tempo em ms</p></td>
<td><p>Opcional</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>execC</p></td>
<td><p>Executar o relógio da CPU; o campo é opcional</p></td>
<td><p>execC = tempo em ms</p></td>
<td><p>Opcional</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>id da mensagem</p></td>
<td><p>ID da mensagem</p></td>
<td><p>id da mensagem = ID de mensagem</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>data-hora</p></td>
<td><p>Data e hora em que a mensagem foi enviada em tempo universal</p></td>
<td><p>Data / hora = a data e hora UTC</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>endereço do remetente</p></td>
<td><p>Endereço de email especificado no campo de remetente</p></td>
<td><p>endereço do remetente = endereço de Email</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>endereço do destinatário</p></td>
<td><p>E-mail de destino dos destinatários da mensagem</p></td>
<td><p>endereço do destinatário = endereço de Email</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>assunto da mensagem</p></td>
<td><p>Dados encontrados no campo assunto da mensagem</p></td>
<td><p>assunto da mensagem = string de assunto de entrada do usuário final</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
</tbody>
</table>


## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Criar relatórios de incidentes para detecções de política DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)

[Acompanhar mensagens com notificações de entrega](track-messages-with-delivery-reports-exchange-2013-help.md)

