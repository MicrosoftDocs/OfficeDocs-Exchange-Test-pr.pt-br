---
title: 'Fluxo de mensagens: Exchange 2013 Help'
TOCTitle: Fluxo de mensagens
ms:assetid: 14df5e1a-a5f7-4b0d-ba97-f53b76f0e7e0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996349(v=EXCHG.150)
ms:contentKeyID: 50485074
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Fluxo de mensagens

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

No Microsoft Exchange Server 2013, o fluxo de emails ocorre através do pipeline de transporte. O *pipeline de transporte* é uma coleção de serviços, conexões, componentes e filas que trabalham juntos para rotear todas as mensagens para o categorizador em um serviço de Transporte em um servidor de Caixa de Correio dentro da organização.

Procurando uma lista de todos os tópicos de fluxo de email? Consulte Documentação de fluxo de emails.

Para informações sobre como configurar o fluxo de email em uma organização do Exchange 2013, consulte [Configurar o acesso de cliente e o fluxo de email](configure-mail-flow-and-client-access-exchange-2013-help.md).

**Conteúdo**

O pipeline de transporte

Serviço de transporte em servidores de caixa de correio

Documentação de fluxo de emails

## O pipeline de transporte

O pipeline de transporte consiste nos seguintes arquivos:

  - **Serviço de Transporte de front-end em servidores de Acesso para Cliente**   Esse serviço age como um proxy sem estado para todo o tráfego SMTP externo de entrada e, opcionalmente, de saída para a organização do Exchange 2013. O serviço de Transporte de front-end não inspeciona o conteúdo da mensagem, não se comunica com o serviço de Transporte de Caixa de Correio em servidores de Caixa de Correio e não enfileira nenhuma mensagem localmente.

  - **Serviço de Transporte em servidores de Caixa de Correio**   Esse serviço é praticamente idêntico à função de servidor de Transporte de Hub em versões anteriores do Exchange. O serviço de Transporte cuida de todo o fluxo de emails SMTP para a organização, executa categorização de mensagens e executa inspeção de conteúdo de mensagens. Diferentemente das versões anteriores do Exchange, o serviço de Transporte nunca se comunica diretamente com bancos de dados de caixas de correio. Essa tarefa agora é tratada pelo serviço de Transporte de Caixa de Correio. O serviço de Transporte direciona mensagens entre o serviço de Transporte de Caixa de Correio, o serviço de Transporte e o serviço de Transporte de front-end e, dependendo de sua configuração, o serviço de Transporte em servidores de Transporte de Borda. O serviço de Transporte em servidores de Caixa de Correio será descrito em mais detalhes posteriormente neste tópico.

  - **Serviço de Transporte de Caixa de Correio em servidores de Caixa de Correio**   Esse serviço é executado em dois serviços separados: o serviço de Envio de Transporte de Caixa de Correio e serviço de Entrega de Transporte de Caixa de Correio. O serviço de Entrega de Transporte de Caixa de Correio recebe mensagens SMTP do serviço de Transporte no servidor de Caixa de Correio local ou em outros servidores de Caixa de Correio e se conecta ao banco de dados de caixa de correio local, usando uma chamada de procedimento remoto (RPC) do Exchange para entregar a mensagem. O serviço de Envio de Transporte de Caixa de correio se conecta ao bando de dados de caixa de correio local usando o RPC, para recuperar mensagens, e envia as mensagens por SMTP para o serviço de Transporte no servidor de Caixa de Correio local ou em outros servidores de Caixa de Correio. O serviço de Envio de Transporte de Caixa de Correio tem acesso às mesmas informações de topologia de roteamento que o serviço de Transporte. Assim como o serviço de Transporte de Front End, o serviço de Transporte de Caixa de correio também não coloca as mensagens em fila localmente.

  - **Serviço de Transporte em servidores de Transporte de Borda**   Este serviço é bem semelhante ao serviço de Transporte em servidores de Caixa de Correio. Se você tiver um servidor de Transporte de Borda instalado na rede de perímetro, todos os emails vindos da Internet ou indo para a Internet fluirão pelo servidor de Transporte de Borda do serviço de Transporte. Este serviço será descrito em mais detalhes posteriormente neste tópico.

A figura a seguir exibe os relacionamentos entre os componentes no pipeline de transporte do Exchange 2013.

**Visão geral do pipeline de transporte no Exchange 2013.**

![Diagrama de visão geral do pipeline de transporte](images/Aa996349.6f548b64-6ac2-4e98-9098-69ad6cd9f569(EXCHG.150).gif "Diagrama de visão geral do pipeline de transporte")

## Mensagens de remetentes externos

As mensagens de fora da organização entram no pipeline de transporte através de um conector de Recebimento no serviço de Transporte de front-end de um servidor de Acesso para Cliente, e são roteadas para o serviço de Transporte em um servidor de Caixa de Correio.

Se você tiver um servidor de Transporte de Borda do Exchange 2013 instalado na rede de perímetro, mensagens de fora da organização entram no pipeline de transporte por meio de um conector de Recebimento no serviço de Transporte do servidor de Transporte de Borda. Para onde as mensagens irão a seguir dependerá de como seus servidores externos do Exchange estão configurados.

  - **Servidor de Caixa de Correio e servidor de Acesso para Cliente instalados no mesmo computador**   Nesta configuração, o servidor de Acesso para Cliente é usado para o fluxo de emails de entrada. O email flui do serviço de Transporte no servidor de Transporte de Borda para o serviço de Transporte de front-end no servidor de Acesso para Cliente e, então, para o serviço de Transporte no servidor de Caixa de Correio.

  - **Servidor de Caixa de Correio e servidor de Acesso para Cliente instalados em computadores diferentes**   Nesta configuração, o servidor de Acesso para Cliente é ignorado pelo fluxo de emails de entrada. Os fluxos de email do serviço de Transporte no servidor de Transporte de Borda para o serviço de Transporte no servidor de Caixa de Correio.


> [!TIP]
> Se você tiver um servidor de Transporte do Borda do Exchange 2010 ou do Exchange 2007 na rede de perímetro, o fluxo de emails sempre ocorrerá diretamente entre o servidor de Transporte de Borda e o serviço de Transporte no servidor de Caixa de Correio. Para mais informações, consulte <A href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Usar um Exchange 2010 ou o servidor de transporte de borda 2007 no Exchange 2013</A>.



## Mensagens de remetentes internos

As mensagens SMTP de dentro da organização entram no pipeline de transporte por meio do serviço de Transporte em um servidor de Caixa de Correio, de uma das seguintes maneiras:

  - Por meio de um conector de Recebimento.

  - Do diretório de Retirada ou do diretório de Repetição.

  - Do serviço de Transporte de Caixa de Correio.

  - Por meio de um envio de agente.

A mensagem é direcionada com base no destino de roteamento ou no grupo de entrega. Para obter mais informações, consulte [Roteamento de mensagens](mail-routing-exchange-2013-help.md).

Se a mensagem tiver destinatários externos, será roteada do serviço de Transporte no servidor de Caixa de Correio para a Internet, ou do servidor de Caixa de Correio para o serviço de Transporte de front-end em um servidor de Acesso para Cliente e, então, para a Internet caso o conector de Envio esteja configurado para conexões de saída de proxy por meio do servidor de Acesso para Cliente. Para obter mais informações, consulte [Criar um conector de envio de email enviado para a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md).

Se você tiver um servidor de Transporte de Borda instalado na rede de perímetro, as mensagens com destinatários externos nunca serão roteadas pelo serviço de Transporte de front-end em um servidor de Acesso para Cliente. A mensagem é roteada do serviço de Transporte em um servidor de Caixa de Correio para o serviço de Transporte no servidor de Transporte de Borda.

## Serviço de transporte em servidores de caixa de correio

Todas as mensagens enviadas ou recebidas em uma organização do Exchange 2013 devem ser categorizadas em um serviço de Transporte em um servidor de Caixa de Correio, antes de poderem ser roteadas e entregues. Depois de uma mensagem ter sido categorizada, ela é colocada em uma fila de entrega, para entrega para o banco de dados de caixa de correio de destino, o grupo de disponibilidade de banco de dados (DAG) de destino, site do Active Directory ou floresta do Active Directory ou o domínio de destino fora da organização.

O serviço de Transporte em um servidor de Caixa de Correio consiste nos seguintes componentes e processos:

  - **Recebimento SMTP**   Quando as mensagens forem recebidas pelo serviço de Transporte, a inspeção do conteúdo da mensagem é feita, as regras de transporte são aplicadas e as inspeções antispam e antimalware são executadas, se estiverem habilitadas. A sessão SMTP tem uma série de eventos que trabalham juntos em uma ordem específica, para validar os conteúdos de uma mensagem antes de ela ser aceita. Depois que uma mensagem passou completamente através do recebimento SMTP e não foi rejeitada por eventos de recebimento ou por um agente antispam e antimalware, ela é colocada na fila de Envio.

  - **Envio**   O envio é o processo de colocar as mensagens na Fila de envio. O categorizador retira uma mensagem de cada vez para categorização. O Envio acontece de três maneiras:
    
      - Do Recebimento de SMTP até um conector de Recebimento.
    
      - Através do diretório de Retirada ou do diretório de Repetição. Esses diretórios estão nos servidores de Caixa de Correio e nos servidores de Transporte de Borda. Os arquivos de mensagem formatados corretamente copiados para o Diretório de recebimento ou o Diretório de repetição são colocados diretamente na Fila de envio.
    
      - Através de um agente de transporte.

  - **Categorizador**   O categorizador retira uma mensagem de cada vez da Fila de envio. O categorizador conclui as etapas a seguir:
    
      - Resolução de destinatário, que inclui endereçamento de nível superior, expansão e bifurcação.
    
      - Resolução de roteamento.
    
      - Conversão de conteúdo.
    
    Além disso, são aplicadas as regras de fluxo de mensagens definidas pela organização. Depois de as mensagens terem sido categorizadas, elas são colocadas em uma fila de entrega que é baseada no destino da mensagem. As mensagens são colocadas em fila de acordo com o banco de dados de caixa de correio de destino, DAG, site do Active Directory, floresta do Active Directory ou domínio externo.

  - **Envio SMTP**   O modo como as mensagens são roteadas no serviço de Transporte depende do local dos destinatários da mensagem, em relação ao servidor de Caixa de Correio em que a categorização ocorreu. Foi possível rotear a mensagem para um dos seguintes locais:
    
      - Para o serviço de Transporte de Caixa de Correio no mesmo servidor de Caixa de Correio.
    
      - Para o serviço de Transporte de Caixa de Correio em um servidor de Caixa de Correio diferente que faz parte do mesmo DAG.
    
      - Para o serviço de Transporte em um servidor de Caixa de Correio em um DAG, site do Active Directory ou floresta do Active Directory diferente.
    
      - Para entrega para a Internet por meio de um conector de Envio no mesmo servidor de Caixa de Correio, por meio do serviço de Transporte em um servidor de Caixa de Correio diferente, por meio do serviço de Transporte de front-end em um servidor de Acesso para Cliente ou por meio do serviço de Transporte em um servidor de Transporte de Borda na rede de perímetro.

## Serviço de transporte em servidores de Transporte de Borda

Os componentes do serviço de Transporte em servidores de Transporte de Borda são idênticos aos componentes do serviço de Transporte em servidores de Caixa de Correio. Entretanto, o que realmente acontece durante cada estágio do processamento em servidores de Transporte de Borda é diferente. As diferenças são descritas na lista a seguir.

  - **Recebimento de SMTP**   Quando um servidor de Transporte de borda é inscrito em um site interno do Active Directory, o conector de Recebimento padrão é automaticamente configurado para aceitar emails de servidores de Caixa de Correio internos e da Internet. Quando as mensagens são recebidas no servidor de Transporte de Borda, os agentes antispam e antivírus filtram os conteúdos das conexões e das mensagens e ajudam a identificar o remetente e o destinatário de uma mensagem enquanto esta está sendo aceita na organização. Os agentes antispam são instalados e habilitados por padrão. Estão disponíveis recursos de filtragem de anexo e de filtragem de conexão adicionais, mas a filtragem de malware interna não. Além disso, as regras de transporte são controladas pelo agente de Regra de Borda. Em comparação ao agente de Regra de Transporte em servidores de Caixa de Correio, somente um pequeno subconjunto de condições de regras de transporte está disponível em servidores de Transporte de Borda. Porém, existem ações de regra de transporte exclusivas relacionadas a conexões SMTP disponíveis somente em servidores de Transporte de Borda.

  - **Envio**   Em um servidor de Transporte de Borda, as mensagens geralmente entram na fila de Envio por meio de um conector de Recebimento. Entretanto, o diretório de seleção e o diretório de reprodução também estão disponíveis.

  - **Categorizador**   Em um servidor de Transporte de Borda, a categorização é um processo abreviado no qual a mensagem é colocada diretamente em uma fila de entrega para entrega a destinatários internos ou externos.

  - **Envio de SMTP**   Quando um servidor de Transporte de Borda for inscrito em um site interno do Active Directory, dois conectores de Envio serão automaticamente criados e configurados. Um é responsável pelo envio de emails de saída para destinatários da Internet; o outro, responsável pelo envio de emails de entrada da Internet para destinatários internos. O email de entrada é enviado para o serviço de Transporte em um servidor de Caixa de Correio no site inscrito do Active Directory.

## Documentação de fluxo de emails

A tabela a seguir contém links para tópicos que irão ajudar você a aprender sobre e gerenciar o fluxo de emails no Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tópico</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-routing-exchange-2013-help.md">Roteamento de mensagens</a></p></td>
<td><p>O roteamento de email descreve como as mensagens são transmitidas entre servidores de mensagens.</p></td>
</tr>
<tr class="even">
<td><p><a href="connectors-exchange-2013-help.md">Conectores</a></p></td>
<td><p>Os conectores definem onde e como as mensagens são transmitidas para e dos servidores do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="domains-exchange-2013-help.md">Domínios</a></p></td>
<td><p>Os domínios aceitos definem os espaços de endereçamento SMTP que são usados na organização do Exchange. Os domínios remotos configuram a formatação de mensagens e as configurações de codificação para mensagens enviadas para domínios externos.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-agents-exchange-2013-help.md">Agentes de transporte</a></p></td>
<td><p>Os agentes de transporte agem nas mensagens, conforme elas viajam através do pipeline de transporte do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-high-availability-exchange-2013-help.md">Alta disponibilidade de transporte</a></p></td>
<td><p>A alta disponibilidade de transporte descreve como o Exchange 2013 mantém cópias redundantes das mensagens durante o trânsito e após a entrega.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-logs-exchange-2013-help.md">Logs de transporte</a></p></td>
<td><p>Os logs de transporte gravam o que acontece às mensagens, conforme elas fluem através do pipeline de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-message-approval-exchange-2013-help.md">Gerenciar a aprovação de mensagens</a></p></td>
<td><p>O transporte moderado requer aprovação para mensagens enviadas a destinatários específicos.</p></td>
</tr>
<tr class="even">
<td><p><a href="content-conversion-exchange-2013-help.md">Conversão de conteúdo</a></p></td>
<td><p>A conversão de conteúdo controla as opções de conversão de mensagens no formato de codificação Neutro para Transporte (TNEF) para destinatários externos e as opções de conversão MAPI para destinatários internos.</p></td>
</tr>
<tr class="odd">
<td><p><a href="dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md">DSNs e notificações de falha na entrega no Exchange 2013</a></p></td>
<td><p>As notificações de status de entrega (DSNs) são as mensagens do sistema que são enviados para os remetentes das mensagens, por exemplo, relatórios de falha de entrega (NDRs).</p></td>
</tr>
<tr class="even">
<td><p><a href="track-messages-with-delivery-reports-exchange-2013-help.md">Acompanhar mensagens com notificações de entrega</a></p></td>
<td><p>Notificações de Entrega é uma ferramenta de controle de mensagens que pode ser usada para pesquisar o status de entrega de emails enviados ou recebidos dos usuários do catálogo de endereços compartilhado da organização, com um determinado assunto. É possível acompanhar informações de entrega sobre mensagens enviadas ou recebidas em qualquer caixa de correio específica da organização.</p></td>
</tr>
<tr class="odd">
<td><p><a href="message-size-limits-exchange-2013-help.md">Limites de tamanhos de mensagens</a></p></td>
<td><p>Esse tópico descreve o os limites de tamanho e de componentes individuais que são impostos às mensagens.</p></td>
</tr>
<tr class="even">
<td><p><a href="queue-viewer-exchange-2013-help.md">Visualizador de Filas</a></p></td>
<td><p>Você usa o Visualizador de Filas da Caixa de Ferramentas do Exchange para exibir e agir em relação às filas e às mensagens nas filas.</p></td>
</tr>
<tr class="odd">
<td><p><a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Diretório de retirada e repetição</a></p></td>
<td><p>Os diretórios de retirada e repetição são usados para inserir arquivos de mensagens no pipeline de transporte.</p></td>
</tr>
<tr class="even">
<td><p><a href="use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md">Usar um Exchange 2010 ou o servidor de transporte de borda 2007 no Exchange 2013</a></p></td>
<td><p>Este tópico descreve as considerações para se usar um servidor de Transporte de Borda de versões anteriores do Exchange no Exchange 2013.</p></td>
</tr>
</tbody>
</table>

