---
title: 'Proteção contra spam: Exchange 2013 Help'
TOCTitle: Proteção contra spam
ms:assetid: 6af88a08-687d-40b1-8b22-80704184403d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ218660(v=EXCHG.150)
ms:contentKeyID: 50485773
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Proteção contra spam

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-06_

*Os remetentes de spam*ou Remetentes mal-intencionado, usam uma variedade de técnicas para enviar e-mails indesejados em sua organização. Nenhuma ferramenta única ou processo pode eliminar todo o spam. No entanto, o Microsoft Exchange Server 2013 fornece uma abordagem em camadas, multipronged e multifacetada à redução dessas mensagens indesejadas. O Exchange usa agentes de transporte para oferecer proteção contra spam, e os agentes internos que estão disponíveis no Exchange 2013 são relativamente inalterados desde o Microsoft Exchange Server 2010.

Para obter mais recursos anti-spam e facilitar o gerenciamento, você pode optar por comprar o Microsoft Proteção do Exchange Online (EOP). Para obter uma comparação dos recursos do EOP e Exchange 2013, consulte [Benefícios e recursos antispam do Exchange Online Protection no Exchange Server 2013](benefits-of-anti-spam-features-in-exchange-online-protection-over-exchange-server-2013-exchange-2013-help.md). Para saber mais sobre a proteção antispam Office 365, consulte [Proteção contra Spam do Office 365 Email](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us).

Para informações sobre as capacidades antimalware incorporadas no Exchange 2013, consulte [Proteção antimalware](anti-malware-protection-exchange-2013-help.md).

**Conteúdo**

Anti-spam agents on Mailbox servers

Anti-spam agents on Edge Transport servers

Anti-spam stamps

Strategy for anti-spam approach

## Agentes antispam nos servidores de Caixa de Correio

Normalmente, você habilita os agentes antispam em um servidor de caixa de correio, se a sua organização não tiver um servidor de Transporte de Boda ou não fizer nenhuma filtragem antispam anterior, antes de aceitar a mensagens de entrada. Para mais informações, consulte [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

Como todos os agentes de transporte, a cada agente antispam é atribuído um valor de prioridade. Um valor mais baixo indica uma prioridade mais alta, então, normalmente, um agente antispam com prioridade 1 irá agir em uma mensagem antes de um agente antispam com prioridade 9. Entretanto, o evento SMTP em que o agente antispam é registrado também é muito importante para determinar a ordem em que os agentes antispam agem nas mensagens. Um agente antispam de baixa prioridade registrado em um evento SMTP mais cedo na pipeline de transporte irá agir em uma mensagem antes de um agente antispam de alta prioridade registrado em um evento SMTP mais tarde na pipeline de transporte.

Com base no valor de prioridade padrão do agente antispam e no evento de SMTP na pipeline de transporte em que o agente antispam é registrado, a lista a seguir descreve os agentes e a ordem padrão em que eles são aplicados a mensagens no servidor de Caixa de Correio:

1.  **Agente de Filtro de Remetente**   A filtragem de remetente compara o remetente no comando SMTP MAIL FROM: a uma lista de remetentes ou domínios de remetentes definida pelo administrador que estão proibidos de enviar mensagens à organização a fim de determinar a ação que será executada em uma mensagem de entrada, caso necessário. Para mais informações, consulte [Filtragem por remetente](sender-filtering-exchange-2013-help.md).

2.  **Agente da ID de Remetente**   A ID de Remetente depende do endereço IP do servidor do remetente e do PRA (Endereço Responsável pela Expressão) do remetente para determinar se o remetente é falsificado ou não. Para mais informações, consulte [ID de remetente](sender-id-exchange-2013-help.md).

3.  **Agente de Filtro de Conteúdo**   A filtragem de conteúdo avalia o conteúdo de uma mensagem. Para mais informações, consulte [Filtragem de conteúdo](content-filtering-exchange-2013-help.md).
    
    A quarentena de spam é um recurso do agente do Filtro de Conteúdo que reduz o risco de perder mensagens legítimas incorretamente classificadas como spam. A quarentena de spam fornece um local de repositório temporário para mensagens que estão identificadas como spam e que não devem ser entregues a uma caixa de correio de usuário dentro da organização. Para mais informações, consulte [Quarentena de spam](spam-quarantine-exchange-2013-help.md).
    
    A filtragem de conteúdo também age no recurso de agregação de lista segura. A agregação de lista segura coleta dados das listas seguras antispam que os usuários do Microsoft Outlook e do Outlook Web App configuram e disponibiliza esses dados para o agente do Filtro de Conteúdo. Para mais informações, consulte [Agregação de Lista Segura](safelist-aggregation-exchange-2013-help.md).

4.  **Agente de Análise de Protocolo**   O Agente de Análise de Protocolo é o agente subjacente que implementa a funcionalidade de reputação do remetente. A reputação do remetente se baseia em dados persistentes sobre o endereço IP do servidor de envio para determinar qual ação, se houver alguma, será tomada quando receber uma mensagem. Um nível de reputação do remetente (SRL) é calculado a partir de diversas características do remetente derivadas de análise de mensagem e testes externos. Para mais informações, consulte [Reputação do remetente e o agente de análise de protocolo](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).

Voltar ao início

## Anti-spam agents on Edge Transport servers

Se sua organização tiver um servidor de transporte de borda instalado na rede de perímetro, todos os agentes antispam que estão disponíveis em um servidor de caixa de correio são instalados e ativados por padrão no servidor de transporte de borda. No entanto, os seguintes agentes antispam estão disponíveis apenas em um servidor de transporte de borda:

  - **Agente de filtragem de conexão**   Filtragem de conexão verifica se o endereço IP do servidor remoto que está tentando enviar mensagens para determinar qual ação, caso haja alguma, para receber uma mensagem de entrada. Filtragem de conexão usa uma lista de bloqueios de IP, lista de IPS permitidos, serviços de provedor de lista de bloqueios de IP e os serviços de provedor de lista de IPS permitidos para determinar se o IP da conexão deve ser bloqueado ou permitido. Para obter mais informações, consulte [Nos servidores de transporte de borda de filtragem de Conexão](connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

  - **Agente de Filtro de Destinatário**   A filtragem de destinatário compara os destinatários da mensagem no comando SMTP RCPT TO: a uma lista de Bloqueio de Destinatários definida pelo administrador. Se for encontrada uma correspondência, a mensagem não terá permissão para entrar na organização. O filtro de destinatários também compara destinatários em mensagens de entrada no diretório de destinatários local para determinar se ela está endereçada a destinatários válidos. Quando uma mensagem não é dirigida a destinatários válidos, ela é rejeitada. Para mais informações, consulte [Filtragem de destinatário nos servidores de Transporte de Borda](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).
    

    > [!TIP]
    > Embora o agente do filtro de destinatário esteja disponível em servidores de caixa de correio, você não deve configurá-lo. Quando o filtro de destinatários em um servidor de caixa de correio detecta um destinatário inválido ou bloqueado em uma mensagem que contém a outros destinatários válidos, a mensagem será rejeitada. Se você instalar os agentes antispam em um servidor de caixa de correio, o agente do filtro de destinatário é habilitado por padrão. No entanto, ele não está configurado para bloquear qualquer destinatários.



  - **Agente de filtragem de anexo**   Filtragem de anexo bloqueia as mensagens com base no tipo de conteúdo de MIME do arquivo, extensão de nome de arquivo ou nome de arquivo de anexo. Você pode configurar para bloquear uma mensagem e seu anexo, para remover o anexo e permitir a mensagem a passagem ou excluir silenciosamente a mensagem e seus anexos de filtragem de anexos. Para obter mais informações, consulte [Filtragem de anexos nos servidores de transporte de borda](attachment-filtering-on-edge-transport-servers-exchange-2013-help.md).

Com base no valor prioritário do agente antispam, e no caso de SMTP no pipeline de transporte onde o antispam for registrado, esta é a ordem padrão na qual os agentes antispam são aplicados no servidor de Transporte de Borda:

1.  Agente de Filtragem de Conexão

2.  Agente de Filtro por Remetente

3.  Agente de Filtro de Destinatários

4.  Agente de ID de Remetente

5.  Agente de Filtro de Conteúdo

6.  Agente de análise de protocolo para reputação do remetente

7.  Agente de filtragem de anexo

Voltar ao início

## Carimbos anti-spam

Carimbos antispam ajudam a diagnosticar problemas relacionados a spam através da aplicação de metadados de diagnóstico, ou carimbos, como informações específicas do remetente, resultados de validação do quebra-cabeça e resultados da filtragem de conteúdo, a mensagens na medida em que elas passam pelos recursos antispam que filtram mensagens de entrada provenientes da Internet. Para mais informações, consulte [Carimbos anti-spam](anti-spam-stamps-exchange-2013-help.md).

Voltar ao início

## Estratégia para a abordagem antispam

Sua estratégia para configurar os recursos antispam e estabelecer a intensidade de suas configurações do agente antispam requer planejamento e cálculo cuidadosos. Se você definir todos os filtros de recursos antispam com os níveis mais agressivos e configurar todos os recursos antispam para que rejeitem todas as mensagens suspeitas, provavelmente você rejeitará mensagens que não são spam. Por outro lado, se não definir os filtros antispam em um nível suficientemente alto e não definir o limite do nível de confiança de spam (SCL) baixo o suficiente, provavelmente você não verá uma redução na quantidade de spam que entra em sua organização.

É uma prática recomendada rejeitar uma mensagem quando o Exchange detectar uma mensagem inválida através do agente de Filtragem de Conexão, agente de Filtro de Destinatário ou agente de Filtro de Remetente. Esse método é mais adequado do que colocar essas mensagens em quarentena ou atribuir-lhes metadados, como carimbos antispam. Os agentes de Filtragem de Conexão e de Filtro de Destinatário bloqueiam automaticamente as mensagens identificadas pelos respectivos filtros. O agente de Filtro de Remetente é configurável.

Essa prática é recomendada, pois o nível de confiança de spam subjacente na filtragem de conexão, na filtragem de destinatário ou na filtragem de remetente é relativamente alto. Por exemplo, com filtragem de remetente, em que o administrador tenha configurado remetentes específicos para serem bloqueados, não há motivo para atribuir os dados da filtragem de remetente a essas mensagens e continuar a processá-las. Na maioria das organizações, as mensagens bloqueadas devem ser rejeitadas. (Se não quiser rejeitar as mensagens, coloque-as na Lista de Rementente Bloqueados.)

A mesma lógica se aplica aos serviços de lista de bloqueios em tempo real e à filtragem de destinatário, embora a confiança subjacente não seja tão alta quanto a da Lista de Bloqueios de IP. Você deve observar que quanto mais uma mensagem percorre o caminho de fluxo de mensagens, tanto mais alta é a probabilidade de falsos positivos, pois os recursos antispam estão avaliando mais variáveis. Portanto, você pode perceber que, se configurar os primeiros recursos antispam na cadeia antispam com mais intensidade, poderá reduzir a maior parte de seu spam. Assim, economizará processamento, largura de banda e recursos de disco para processar mensagens mais ambíguas.

Por último, você deve planejar monitorar a eficácia geral dos recursos antispam. Com monitoramento cuidadoso, você pode continuar ajustando os recursos antispam para funcionar em seu ambiente de modo adequado. Com esse método, planeje uma configuração não muito agressiva dos recursos antispam no início. Esse método permite reduzir o número de falsos positivos. À medida que monitorar e ajustar os recursos antispam, você poderá se tornar mais agressivo em relação ao tipo de spam e aos ataques de spam detectados por sua organização.

Voltar ao início

## Consulte também


[Proteção do Office 365 Email contra Spam](https://support.office.com/en-us/article/office-365-email-anti-spam-protection-6a601501-a6a8-4559-b2e7-56b59c96a586?ui=en-us%26rs=en-us%26ad=us)

