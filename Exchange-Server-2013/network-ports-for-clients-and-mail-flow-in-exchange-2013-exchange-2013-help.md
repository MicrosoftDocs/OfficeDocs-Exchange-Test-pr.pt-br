---
title: 'Portas de rede para clientes e fluxo de emails do Exchange 2013'
TOCTitle: Portas de rede para clientes e fluxo de emails do Exchange 2013
ms:assetid: fec09455-e99e-42eb-8b32-1ddc08d9a19e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb331973(v=EXCHG.150)
ms:contentKeyID: 64126833
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Portas de rede para clientes e fluxo de emails do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico fornece informações sobre a rede de portas que são usadas pelo MicrosoftExchange Server 2013 para a comunicação com clientes de email, servidores de email da Internet e outros serviços externos à sua organização local do Exchange. Antes de falarmos sobre isso, entenda as seguintes regras básicas:

  - Não há suporte para restringir ou alterando o tráfego de rede entre servidores internos do Exchange, entre servidores internos do Exchange e servidores internos do Lync ou do Skype for Business, ou entre servidores internos do Exchange e controladores de domínio do Active Directory em todos os tipos de topologias. Se você tiver firewalls ou dispositivos de rede que poderiam restringir ou alterar esse tipo de tráfego de rede, é preciso configurar regras que permitam a comunicação gratuita e irrestrita entre esses servidores (regras que permitam o tráfego de rede de entrada e saída em qualquer porta, incluindo portas aleatórias RPC, e qualquer protocolo que nunca altere os bits na conexão).

  - Os servidores de Transporte de Borda quase sempre estão localizados em uma rede de perímetro, portanto é esperado que você restrinja o tráfego de rede entre o servidor de transporte de borda e a Internet e entre o servidor de transporte de borda e a organização interna do Exchange. Estas portas de rede são descritas neste tópico.

  - É esperado que você restrinja o tráfego de rede entre clientes e serviços externos e sua organização interna do Exchange. Também não há problema se você decidir restringir o tráfego de rede entre clientes internos e servidores internos do Exchange. Estas portas de rede são descritas neste tópico.

**Sumário**

Portas de rede necessárias para clientes e serviços

Portas de rede necessárias para o fluxo de emails (sem servidores de Transporte de Borda)

Portas de rede necessárias para o fluxo de emails com servidores de Transporte Edge

Portas de rede necessárias para implantações híbridas

Portas de rede necessárias para Unificação de Mensagens

## Portas de rede necessárias para clientes e serviços

As portas de rede necessárias para que os clientes de email acessem caixas de correio e outros serviços na organização do Exchange são descritos na tabela e diagrama a seguir.

**Observações:** 

  - O destino para esses clientes e serviços é um servidor de Acesso para Cliente. Isso poderia ser um servidor de Acesso para Cliente autônomo ou um servidor de Acesso para Cliente e servidor de Caixa de Correio instalados no mesmo computador.

  - Embora o diagrama mostre clientes e serviços da Internet, os conceitos são os mesmos para os clientes internos (por exemplo, os clientes em um floresta de contas acessando servidores do Exchange em uma floresta de recursos). Da mesma forma, a tabela não tem uma coluna de origem porque a origem pode ser qualquer local externo à organização do Exchange (por exemplo, a Internet ou uma floresta de contas).

  - Os servidores de transporte de borda não têm nenhum envolvimento no tráfego de rede associado a esses clientes e serviços.

![Portas de rede necessárias para clientes e serviços](images/Bb331973.f5ba3439-f001-43c8-848e-0e3fd0fce931(EXCHG.150).png "Portas de rede necessárias para clientes e serviços")


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Objetivo</th>
<th>Portas</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>As conexões Web criptografadas são usadas pelos seguintes clientes e serviços:</p>
<ul>
<li><p>Serviço de descoberta automática</p></li>
<li><p>Exchange ActiveSync</p></li>
<li><p>Serviços Web do Exchange (EWS)</p></li>
<li><p>Distribuição do catálogo de endereços offline</p></li>
<li><p>Outlook em Qualquer Lugar (RPC sobre HTTP)</p></li>
<li><p>MAPI sobre HTTP no Outlook</p></li>
<li><p>Outlook Web App</p></li>
</ul></td>
<td><p>443/TCP (HTTPS)</p></td>
<td><p>Para saber mais sobre esses clientes e serviços, consulte os seguintes tópicos:</p>
<ul>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Serviço de descoberta automática</a></p></li>
<li><p><a href="exchange-activesync-exchange-2013-help.md">Exchange ActiveSync</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/?linkid=529544">Referência EWS do Exchange</a></p></li>
<li><p><a href="offline-address-books-exchange-2013-help.md">Catálogos de endereços offline</a></p></li>
<li><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook em Qualquer Lugar</a></p></li>
<li><p><a href="mapi-over-http-exchange-2013-help.md">MAPI sobre HTTP</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Novidades do Outlook Web App no Exchange 2013</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>As conexões Web sem criptografia são usadas pelos seguintes clientes e serviços:</p>
<ul>
<li><p>Publicação de calendários na Internet</p></li>
<li><p>Outlook Web App (redirecionar para 443/TCP)</p></li>
<li><p>Descoberta automática (fallback quando 443/TCP não estiver disponível)</p></li>
</ul></td>
<td><p>80/TCP (HTTP)</p></td>
<td><p>Sempre que possível, recomendamos usar conexões Web criptografadas em 443/TCP para ajudar a proteger os dados e credenciais. No entanto, você pode descobrir que alguns serviços devem ser configurados para usar as conexões Web sem criptografia em 80/TCP com o servidor de Acesso para Cliente.</p>
<p>Para saber mais sobre esses clientes e serviços, consulte os seguintes tópicos:</p>
<ul>
<li><p><a href="enable-internet-calendar-publishing-exchange-2013-help.md">Habilitar a publicação de calendário da Internet</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Novidades do Outlook Web App no Exchange 2013</a></p></li>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Serviço de descoberta automática</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Clientes IMAP4</p></td>
<td><p>143/TCP (IMAP), 993/TCP (IMAP seguro)</p></td>
<td><p>O IMAP4 está desabilitado por padrão. Para saber mais, consulte <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">POP3 e IMAP4 no Exchange Server 2013</a>.</p>
<p>O serviço IMAP4 nas conexões de proxies do servidor de Acesso para Cliente para o serviço de Back-end IMAP4 em um servidor de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>Clientes POP3</p></td>
<td><p>110/TCP (POP3), 995/TCP (POP3 seguro)</p></td>
<td><p>POP3 está desabilitado por padrão. Para saber mais, consulte <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">POP3 e IMAP4 no Exchange Server 2013</a>.</p>
<p>O serviço POP3 nas conexões de proxies do servidor de Acesso para Cliente para o serviço de Back-end POP3 em um servidor de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>Clientes SMTP (autenticados)</p></td>
<td><p>587/TCP (SMTP autenticado)</p></td>
<td><p>O conector de Recebimento padrão chamado &quot;<em>&lt;Server name&gt;</em> de Front-End do Cliente&quot; escuta envios de cliente SMTP autenticados na porta 587 no servidor de Acesso para Cliente.</p>
<p><strong>Observação:</strong></p>
<p>Se tiver clientes de email que possam enviar emails SMTP autenticados somente na porta 25, você pode modificar o valor das associações do adaptador de rede deste conector de Recebimento para também escutar envios de email SMTP autenticados na porta 25.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Portas de rede necessárias para fluxo de emails

O modo como o email é entregue de e para suas organizações do Exchange depende da sua topologia do Exchange. O fator mais importante é ter um servidor de Transporte de Borda inscrito implantado na sua rede de perímetro.

## Portas de rede necessárias para o fluxo de mensagens (sem servidores de Transporte de Borda)

As portas de rede exigidas para fluxo de emails em uma organização do Exchange que só tenha servidores de Acesso para Cliente e servidores de Caixa de Correio são descritos no seguinte diagrama e tabela. Ainda que o diagrama mostre servidores de Caixa de Correio e de Acesso para Cliente separados, os conceitos são os mesmos quer o servidor de Acesso para Cliente e o servidor de Caixa de Correio estejam instalados no mesmo computador ou em computadores separados.

![Portas de rede necessárias para o fluxo de mensagens (sem servidores de Transporte de Borda)](images/Bb331973.af54dfd3-fe6b-4b6e-bb8e-b00df94a0be0(EXCHG.150).png "Portas de rede necessárias para o fluxo de mensagens (sem servidores de Transporte de Borda)")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Objetivo</th>
<th>Portas</th>
<th>Origem</th>
<th>Destino</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Email de entrada</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet (qualquer)</p></td>
<td><p>Servidor de Acesso para Cliente</p></td>
<td><p>O conector de Recebimento padrão denominado &quot;<em>&lt;Client Access server name&gt;</em> Padrão de Front-End&quot; no servidor de Acesso para Cliente escuta emails SMTP de entrada anônimos na porta 25.</p>
<p>O email é retransmitido do servidor de Acesso para Cliente para um servidor de Caixa de Correio usando o conector de Envio implícito e invisível intraorganizacional que automaticamente roteia emails entre servidores do Exchange na mesma organização.</p></td>
</tr>
<tr class="even">
<td><p>Email de saída</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidor de Caixa de Correio</p></td>
<td><p>Internet (qualquer)</p></td>
<td><p>Por padrão, o Exchange não cria nenhum conector de Envio que permita enviar emails para a Internet. Você precisa criar conectores de Envio manualmente. Para saber mais, consulte <a href="send-connectors-exchange-2013-help.md">Conectores de envio</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Email de saída (se roteado pelo servidor de Acesso para Cliente)</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidor de Acesso para Cliente</p></td>
<td><p>Internet (qualquer)</p></td>
<td><p>O email de saída é roteado através de um servidor de Acesso para Cliente somente quando um conector de Envio está configurado com um <strong>Proxy através do servidor de Acesso para Cliente</strong> no Centro de administração do Exchange ou em <code>-FrontEndProxyEnabled $true</code> no Shell de Gerenciamento do Exchange.</p>
<p>Nesse caso, o conector de Recebimento padrão denominado &quot;<em>&lt;Client Access server name&gt;</em> do Front-End de Proxy de Saída&quot; no servidor de Acesso para Cliente escuta emails de saída do servidor de Caixa de Correio. Para saber mais, consulte <a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">Criar um conector de envio de email enviado para a Internet</a>.</p></td>
</tr>
<tr class="even">
<td><p>DNS para resolução de nomes do próximo salto de emails (não representado)</p></td>
<td><p>53/UDP,53/TCP (DNS)</p></td>
<td><p>Servidor Exchange para a Internet (servidor de Acesso para Cliente ou servidor de Caixa de Correio)</p></td>
<td><p>Servidor DNS</p></td>
<td><p>Consulte a seção Resolução de nomes.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Portas de rede são necessárias para o fluxo de mensagens com servidores de Transporte Edge

Ter um servidor de Transporte de Borda inscrito instalado na sua rede de perímetro basicamente elimina o fluxo de emails SMTP no servidor de Acesso para Cliente. Especificamente:

  - O email de saída da organização do Exchange nunca flui através de um servidor de Acesso para Cliente. O email flui sempre de email de um servidor de Caixa de Correio no site do Active Directory inscrito para o servidor de Transporte de Borda (independentemente da versão do Exchange no servidor de Transporte de Borda).

  - O email de entrada nunca flui através de um servidor de Acesso para Cliente autônomo. Fluxos de email do servidor de Transporte de Borda para um servidor de caixa de correio no site do Active Directory inscrito. Se o servidor de Caixa de Correio e o servidor de Acesso para Cliente estiverem instalados no mesmo computador, emails de um servidor de Transporte de Borda do Exchange 2013 chegam pela primeira vez ao computador no serviço de Transporte de Front-End (a função de servidor de Acesso para Cliente) antes de fluir para o serviço de Transporte (a função de servidor de Caixa de Correio). Os servidores de Transporte de Borda do Exchange 2007 ou do Exchange 2010 sempre enviam mensagens diretamente para o serviço de Transporte, mesmo quando o servidor de Caixa de Correio e o servidor de Acesso para Cliente são instalados no mesmo computador.

Para saber mais, consulte [Fluxo de mensagens](mail-flow-exchange-2013-help.md).

As portas de rede necessárias para fluxo de emails em organizações do Exchange que têm servidores de Transporte de Borda são descritas na tabela e diagrama a seguir. A menos que expresso em contrário, os conceitos são os mesmos independentemente do servidor de Acesso para Cliente e o servidor de Caixa de Correio estarem instalados no mesmo computador ou em computadores distintos.

![Portas de rede são necessárias para o fluxo de mensagens com servidores de Transporte Edge](images/Bb331973.110c79b3-dbd9-4cb5-bba1-02048363ee1c(EXCHG.150).png "Portas de rede são necessárias para o fluxo de mensagens com servidores de Transporte Edge")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Objetivo</th>
<th>Portas</th>
<th>Origem</th>
<th>Destino</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Email de entrada - da Internet para o servidor de Transporte de Borda</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet (qualquer)</p></td>
<td><p>Servidor de Transporte de Borda</p></td>
<td><p>O conector de Recebimento padrão denominado &quot;<em>&lt;Edge Transport server name&gt;</em> Padrão Interno do Conector de Recebimento&quot; no servidor de Acesso para Cliente escuta emails SMTP anônimos na porta 25.</p></td>
</tr>
<tr class="even">
<td><p>Email de entrada - do Servidor de Transporte de Borda para a organização interna do Exchange</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidor de Transporte de Borda</p></td>
<td><p>Servidores de caixa de correio no site Active Directory inscrito</p></td>
<td><p>O conector de Envio padrão denominado &quot;EdgeSync - Entrada para <em>&lt;Active Directory site name&gt;</em>&quot; retransmite mensagens de entrada na porta 25 para qualquer servidor de Caixa de Correio do site do Active Directory inscrito. Para saber mais, consulte a seção “Conectores de Envio criados durante o processo de Inscrição de Borda” no tópico <a href="edge-subscriptions-exchange-2013-help.md">Inscrições de Borda</a>.</p>
<p>O serviço que realmente recebe email depende de se o servidor de Caixa de Correio e o servidor de Acesso para Cliente são instalados no mesmo computador ou em computadores distintos.</p>
<ul>
<li><p><strong>Servidor de Caixa de Correio Autônomo</strong>   O conector de Recebimento padrão denominado &quot;<em>&lt;Mailbox server name&gt;</em> Padrão&quot; escuta emails de entrada (incluindo emails de servidores de Transporte de Borda) na porta 25.</p></li>
<li><p><strong>Servidor de Caixa de Correio e servidor de Acesso para Cliente instalados no mesmo computador</strong>   O conector de Recebimento padrão denominado &quot;<em>&lt;Server name&gt;</em> de Front-End Padrão&quot; no serviço de Transporte de Front-End (a função de Servidor de Acesso para Cliente) escuta emails de entrada (incluindo emails de servidores de Transporte de Borda do Exchange 2013) na porta 25.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Email de saída - da organização interna do Exchange para o Servidor de Transporte de Borda</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidores de caixa de correio no site Active Directory inscrito</p></td>
<td><p>Servidores de Transporte de Borda</p></td>
<td><p>O email de saída sempre ignora o servidor de Acesso para Cliente.</p>
<p>O email é retransmitido de qualquer servidor de Caixa de Correio no site do Active Directory inscrito para um servidor de Transporte de Borda utilizando o conector de Envio intraorganizacional implícito e invisível que roteia correio entre servidores do Exchange automaticamente na mesma organização.</p>
<p>O conector de Recebimento padrão denominado &quot;<em>&lt;Edge Transport server name&gt;</em> do conector de Recebimento Interno Padrão&quot; no servidor de Transporte de Borda escuta emails SMTP na porta 25 de qualquer servidor de Caixa de Correio no site do Active Directory inscrito.</p></td>
</tr>
<tr class="even">
<td><p>Email de saída - Do servidor de Transporte de Borda para a Internet</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Servidor de Transporte de Borda</p></td>
<td><p>Internet (qualquer)</p></td>
<td><p>O conector de Envio padrão denominado &quot;EdgeSync - <em>&lt;Active Directory site name&gt;</em> para a Internet&quot; retransmite emails de saída na porta 25 do servidor de Transporte de Borda para a Internet.</p></td>
</tr>
<tr class="odd">
<td><p>Sincronização EdgeSync</p></td>
<td><p>50636/TCP (LDAP seguro)</p></td>
<td><p>Servidores de caixa de correio no site do Active Directory inscrito para participar da sincronização EdgeSync</p></td>
<td><p>Servidores de Transporte de Borda</p></td>
<td><p>Quando o servidor de Transporte de Borda assinou o site do Active Directory, todos os servidores de Caixa de Correio existentes no site no momento participam da sincronização EdgeSync. No entanto, os servidores de Caixa de Correio adicionados posteriormente não participam automaticamente da sincronização EdgeSync.</p></td>
</tr>
<tr class="even">
<td><p>DNS para resolução de nomes do próximo salto de emails (não representado)</p></td>
<td><p>53/UDP,53/TCP (DNS)</p></td>
<td><p>Servidor de Transporte de Borda</p></td>
<td><p>Servidor DNS</p></td>
<td><p>Consulte a seção Resolução de nomes.</p></td>
</tr>
<tr class="odd">
<td><p>Definição de servidor proxy de reputação do remetente (não representada)</p></td>
<td><p>definido pelo usuário</p></td>
<td><p>Servidores de Transporte de Borda</p></td>
<td><p>Internet</p></td>
<td><p>A reputação do remetente (o agente de análise de protocolo) analisa os caminhos de mensagem de entrada em um esforço para reduzir o spam. Se a sua organização usa um servidor proxy para controlar o acesso à Internet, você precisa definir detalhes sobre o servidor proxy para que a reputação do remetente possa funcionar corretamente (em específico, a detecção de proxy aberto e bloqueio de remetente). Você pode usar os parâmetros <em>ProxyServerName</em>, <em>ProxyServerPort</em> e <em>ProxyServerType</em> no cmdlet <strong>Set-SenderReputationConfig</strong> para definir o servidor proxy da sua organização para que a reputação do remetente possa ser conectada à Internet com êxito. Para saber mais, consulte <a href="manage-sender-reputation-exchange-2013-help.md">Gerenciar reputação do remetente</a>.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Resolução do nome

A resolução de DNS do próximo salto de email é uma parte fundamental do fluxo de emails em qualquer organização do Exchange. Os servidores Exchange responsáveis por receber emails de entrada ou entregar emails de saída devem ser capazes de resolver os nomes de host internos e externos para um roteamento de emails adequado. E todos os servidores internos do Exchange devem ser capazes de resolver nomes de host internos para rotear emails corretamente. Há muitas maneiras diferentes de criar uma infraestrutura DNS, mas o resultado importante é garantir que a resolução de nomes para o próximo salto está funcionando corretamente para todos os seus servidores Exchange.

## Portas de rede necessárias para implantações híbridas

As portas de rede necessárias para uma organização que usa tanto Exchange 2013 quanto MicrosoftOffice 365 são descritas na seção "Protocolos de implantação híbrida, porta e pontos de extremidade" em [Pré-requisitos de implantação híbrida](https://technet.microsoft.com/pt-br/library/hh534377\(v=exchg.150\)).

## Portas de rede necessárias para Unificação de Mensagens

As portas de rede que são necessárias para a Unificação de Mensagens são descritas nos seguintes tópicos:

  - [Serviços, portas e protocolos de Unificação de mensagens](um-protocols-ports-and-services-exchange-2013-help.md)

  - [Cartaz da arquitetura do Exchange Server 2013 SP1](https://go.microsoft.com/fwlink/p/?linkid=518646)

Voltar ao início

