---
title: 'Reputação do remetente e o agente de análise de protocolo: Exchange 2013 Help'
TOCTitle: Reputação do remetente e o agente de análise de protocolo
ms:assetid: c4c34235-d545-41e7-ac2f-1dd43aaa3708
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124512(v=EXCHG.150)
ms:contentKeyID: 50486577
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Reputação do remetente e o agente de análise de protocolo

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-16_

Reputação do remetente é parte da funcionalidade de antispam do Exchange que bloqueia as mensagens de acordo com muitas características do remetente. Reputação do remetente depende de dados persistentes sobre o remetente para determinar qual ação, se houver, para receber uma mensagem de entrada. O agente de análise de protocolo é o subjacentes para a funcionalidade de reputação do remetente.

Quando você configura os agentes anti-spam em um servidor Exchange, os agentes de atuam em mensagens de forma cumulativa para reduzir o número de mensagens não solicitadas que entram na organização.

**Sumário**

Cálculo do nível de reputação do remetente

Uso de SRL

Habilitando e configurando a detecção de abrem servidores proxy

Definindo o limite de bloqueio SRL

## Cálculo do nível de reputação do remetente

Um nível de reputação do remetente (SRL) é calculado a partir as seguintes estatísticas:

  - **Análise HELO/EHLO**   Os comandos HELO e EHLO SMTP servem para fornecer o nome de domínio, por exemplo, Contoso.com, ou endereço IP do servidor de envio SMTP para o servidor SMTP de recebimento. Usuários mal-intencionados ou *Remetentes de spam*, frequentemente falsificar a instrução HELO/EHLO de diversas maneiras. Por exemplo, eles digitam um endereço IP que não coincidir com o endereço IP que originou a conexão. Os remetentes de spam também colocar os domínios que são conhecidos ser suportados localmente no servidor de recebimento na instrução HELO em uma tentativa de aparecem como se os domínios estão na organização. Em outros casos, os remetentes de spam alterar o domínio que é passado na instrução HELO. O comportamento típico de um usuário legítimo pode ser a usar um conjunto diferente, mas relativamente constante, domínios em suas declarações HELO.
    
    Portanto, análise da instrução HELO/EHLO em uma base por remetente pode indicar que o remetente está provavelmente um remetente de spam. Por exemplo, um remetente que fornece muitos instruções HELO/EHLO exclusivas diferentes em um período de tempo específico é mais provável de ser um remetente de spam. Remetentes que consistentemente fornecem um endereço IP na instrução HELO que não corresponder ao endereço IP de origem conforme determinado pelo agente de filtro de Conexão também são mais prováveis de ser remetentes de spam. Remetentes remotos que consistentemente, forneça um nome de domínio local na instrução HELO que esteja na mesma organização do Exchange server também são mais prováveis de ser remetentes de spam.

  - **Pesquisa de DNS reverso**   Reputação do remetente também verifica se o endereço IP de origem do qual o remetente transmitidas a mensagem corresponde ao nome de domínio registrado que envia o remetente no comando HELO ou EHLO SMTP.
    
    Reputação do remetente executa uma consulta DNS reversa enviando-se o endereço IP de origem no DNS. O resultado retornado por DNS é o nome de domínio que está registrado usando o autoridade de nomeação para esse endereço IP de domínio. Reputação do remetente compara o nome de domínio que é retornado pelo DNS para o nome de domínio que o remetente enviado no comando HELO/EHLO SMTP. Se os nomes de domínio não coincidirem, o remetente é provavelmente um remetente de spam e a classificação de SRL geral para o remetente é aumentada.
    
    O agente de ID de remetente executa uma tarefa semelhante, mas o sucesso do agente de ID de remetente depende de remetentes legítimos para atualizar sua infra-estrutura DNS para identificar todos os servidores SMTP envio de email em suas organizações. Executando uma pesquisa inversa de DNS, você pode ajudar a identificar possíveis remetentes de spam.

  - **Classificações de análise de SCL em mensagens de um remetente específico**   Quando o agente de filtro de conteúdo processa uma mensagem, ele atribui uma classificação de nível de confiança de spam (SCL) à mensagem. A classificação SCL é um número de 0 a 9. Uma classificação de SCL maior indica que uma mensagem é mais provável de ser spam. Dados sobre cada remetente e classificações de SCL que suas mensagens geram é persistente para análise por reputação do remetente. Reputação do remetente calcula estatísticas sobre um remetente de acordo com a taxa entre todas as mensagens desse remetente que tinha uma classificação de SCL baixa no passado e todas as mensagens desse remetente que tinha uma classificação de SCL alta no passado. Além disso, o número de mensagens que têm uma classificação de SCL alta que o remetente tiver enviado do último dia é aplicado de SRL geral.

  - **Abra o remetente teste de proxy**   Um *proxy de abrir* é um servidor de proxy que aceite solicitações de conexão de qualquer pessoa em qualquer lugar e encaminha o tráfego como se originou-se de hosts de local. Servidores proxy retransmitam o tráfego TCP por meio de hosts de firewall para fornecer acesso transparente do usuário aplicativos através do firewall. Como proxy protocolos são leve e independente dos protocolos de aplicativo do usuário, os proxies podem ser usados por muitos serviços diferentes. Proxies também podem ser usados para compartilhar uma conexão de Internet único por vários hosts. Proxies geralmente são configurados para que somente hosts confiáveis dentro do firewall podem cruzar através de proxies. Um remetente legítimo pode ser um proxy aberto por causa um erro de configuração não intencional ou malware.
    
    Proxies abertos fornecem uma maneira ideal para os usuários mal-intencionados ocultar suas identidades verdadeiras e início de negação de ataques de serviço (DoS) ou enviem spam. À medida que mais servidores de proxy estiver configurados para ser aberto por padrão, os proxies abertos tornaram mais comuns. Além disso, usuários mal-intencionados podem usar vários proxies abertos juntos para ocultar o endereço IP de origem do remetente.
    
    Quando reputação do remetente realiza um teste de proxy aberto, ele faz isso por formatação de uma solicitação SMTP na tentativa de conexão de volta para o servidor do Exchange do proxy aberto. Se uma solicitação de SMTP for recebida do proxy, reputação do remetente verifica se o proxy é um proxy aberto e atualiza a estatística de teste de proxy aberto para esse remetente.

Reputação do remetente pesa cada uma dessas estatísticas e calcula um SRL para cada remetente. O SRL é um número de 0 a 9 que prevê a probabilidade de que um remetente específico é um remetente de spam ou usuário malicioso caso contrário. Um valor 0 indica que o remetente não é provável que haja um remetente de spam; um valor de 9 indica que o remetente está provavelmente um remetente de spam.

Você pode configurar um limite de bloqueio de 0 a 9 no qual remetente reputação emite uma solicitação para o agente do filtro de remetente e, portanto, bloqueia o remetente de enviar uma mensagem na organização. Quando um remetente for bloqueado, o remetente é adicionado à lista de remetentes bloqueados por um período configurável. Como as mensagens bloqueadas são tratadas depende da configuração do agente do filtro de remetente. As seguintes ações são as opções para lidar com as mensagens bloqueadas:

  - Rejeitar

  - Excluir e arquivar

  - Aceitar e marcar como um remetente bloqueado

Se um remetente é incluído na lista de bloqueios de IP ou serviço de reputação de IP do Microsoft, o reputação do remetente emite uma solicitação imediata para o agente de filtro de remetente para bloquear o destinatário. Para se beneficiar dessa funcionalidade, você deve habilitar e configurar o serviço de atualização do Microsoft Exchange Anti-spam.

Por padrão, a reputação do remetente define uma classificação 0 para remetentes que ainda não foram analisados. Depois que um remetente tiver enviado 20 ou mais mensagens, reputação do remetente calcula um SRL que baseia-se as estatísticas de listados anteriormente neste tópico.

Voltar ao início

## Uso de SRL

Reputação do remetente atua em mensagens durante duas fases da sessão SMTP:

  - **Em the MAIL FROM: comando SMTP**   Reputação do remetente atua em uma mensagem somente se a mensagem foi bloqueada ou caso contrário, acionada pelo agente Filtro de Conexão, o agente de filtro de remetente, agente Filtro de destinatário ou agente de ID de remetente. Nesse caso, reputação do remetente recupera a classificação de SRL atual do remetente do perfil do remetente que tem persistentes sobre esse remetente no servidor Exchange. Depois que essa classificação será recuperada e avaliada, a configuração do servidor Exchange dita o comportamento que ocorre em uma conexão específica de acordo com o limite de bloqueio.

  - **Após o comando de SMTP "final dos dados"**   Final de comando de SMTP de transferência (**EOD**) de dados recebe quando todos os dados reais de mensagem são enviados. Nesse momento na sessão SMTP, muitos dos agentes antispam tem processado a mensagem. Como um produto derivado do processamento anti-spam, as estatísticas que depende de reputação do remetente são atualizadas. Portanto, reputação do remetente tem os dados para calcular ou recalcular uma classificação de SRL para o emissor.

Para saber mais, confira [Gerenciar reputação do remetente](manage-sender-reputation-exchange-2013-help.md).

Voltar ao início

## Habilitando e configurando a detecção de abrem servidores proxy

Reputação do remetente avalia várias características do remetente para calcular uma SRL. Entre as características que avalia de reputação do remetente são os resultados de um teste para servidores de proxy aberto. Frequentemente, remetentes de spam rotear mensagens através dos servidores de proxy aberto na Internet. Por roteamento spam por meio de servidores de proxy aberto, remetentes podem enviar mensagens que parecem se originar de um servidor diferente do seu próprio.

Quando a reputação do remetente calcula um SRL, reputação do remetente tenta se conectar ao endereço IP de origem do remetente usando uma variedade de protocolos de proxy comuns, como SOCKS4, SOCKS5, HTTP, Telnet, Cisco e Wingate. Reputação do remetente formata uma solicitação de protocolo específico na tentativa de conexão volta para o servidor de transporte de borda do servidor de proxy aberto usando uma solicitação de SMTP. Se uma solicitação de SMTP é recebida do servidor proxy, reputação do remetente verifica se o servidor proxy é um servidor de proxy aberto e ajusta a classificação de SRL acordo com esse resultado. Por padrão, a detecção de servidores de proxy aberto está habilitada na reputação do remetente.

Para obter mais informações sobre como habilitar e configurar a detecção de servidores de proxy aberto, consulte [Gerenciar reputação do remetente](manage-sender-reputation-exchange-2013-help.md).

Voltar ao início

## Definindo o limite de bloqueio SRL

O SRL é um número de 0 a 9 que prevê a probabilidade de que um remetente específico é um remetente de spam ou usuário malicioso caso contrário. Você deve definir um limite para bloqueio de SRL do emissor. Esse limite de bloqueio SRL define o valor SRL que deve ser excedido para reputação do remetente bloquear um remetente. Por padrão, o SRL é definido como 7. Você deve monitorar a eficácia do agente no nível padrão. Você pode achar que você pode ajustar o valor para atender às necessidades da sua organização. Se você definir outros agentes antispam agressivamente, você poderá definir um maior limite de SRL para reputação do remetente que ocorreria se os outros agentes antispam não foram definidos agressivamente. Para obter mais informações sobre como ajustar configurações antispam, de modo que eles funcionam juntos para reduzir o spam, consulte [Proteção contra spam](anti-spam-protection-exchange-2013-help.md).

Em um servidor de transporte de borda, se o limite de bloqueio SRL for excedido para um determinado remetente, reputação do remetente adiciona o remetente à lista de bloqueios de IP no agente de filtro de Conexão. Às vezes, os remetentes de spam enviar lotes de spam de um único remetente. Neste cenário, se reputação do remetente calcula um SRL que excede o limite de bloqueio SRL, o remetente é adicionado à lista de bloqueios de remetente por um período configurável de tempo. A duração padrão é 24 horas. Após 24 horas, o remetente é removido da lista de bloqueios de remetente e pode enviar mensagens novamente.

Quando um remetente é adicionado à lista de bloqueios de IP, reputação do remetente exclui o perfil para o emissor. Reputação do remetente exclui o perfil porque o perfil de existente do remetente bloqueado indica que o SRL do remetente excede o limite de bloqueio SRL. Isso causaria o remetente bloqueado a ser adicionado à lista de bloqueios de IP novamente assim que a duração de bloqueio de remetente termina.

Para saber mais, confira [Gerenciar reputação do remetente](manage-sender-reputation-exchange-2013-help.md).

Voltar ao início

