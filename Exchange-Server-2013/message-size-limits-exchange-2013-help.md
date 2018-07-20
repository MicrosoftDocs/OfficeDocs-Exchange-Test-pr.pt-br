---
title: 'Limites de tamanhos de mensagens: Exchange 2013 Help'
TOCTitle: Limites de tamanhos de mensagens
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 50486457
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Limites de tamanhos de mensagens

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-08-20_

É possível aplicar limites de tamanho da mensagem a mensagens individuais que passam pela organização do Microsoft Exchange Server 2013. Você pode restringir o tamanho total de uma mensagem ou o tamanho dos componentes individuais da mensagem, como o cabeçalho, os anexos ou o número de destinatários da mensagem. Você pode aplicar limites globalmente para toda a organização do Exchange ou especificamente para um determinado objeto de usuário ou conector.

Ao planejar os limites de tamanho de mensagem para sua organização do Exchange, considere as seguintes questões:

  - Que limites de tamanho devo impor para todas as mensagens de entrada?

  - Que limites de tamanho devo impor para todas as mensagens de saída?

  - Qual é a cota de caixa de correio da minha organização do Exchange?

  - Como os limites de tamanho de mensagens que eu escolhi se relacionam ao tamanho da cota de caixa de correio?

  - Existem usuários em minha organização do Exchange que precisam enviar ou receber mensagens maiores do que o tamanho permitido especificado?

  - Minha topologia de rede do Exchange inclui outros sistemas de mensagens ou unidades comerciais distintamente separadas que possuem limites de tamanho de mensagens diferentes?

Este tópico fornece diretrizes para ajudar a responder essas perguntas.

**Sumário**

Tipos de limites de tamanho de mensagem

Escopo dos limites

Ordem de precedência para limites de tamanho de mensagem

Isenção de mensagem dos limites de tamanho

## Tipos de limites de tamanho de mensagem

A seguir, as categorias básicas dos limites de tamanho disponíveis para mensagens individuais:

  - **Limites de tamanho de cabeçalho de mensagem**   Esses limites se aplicam ao tamanho total de todos os campos de cabeçalho de mensagem presentes na mensagem. O tamanho do corpo ou dos anexos da mensagem não é considerado. Como os campos de cabeçalho são texto não criptografado, o tamanho do cabeçalho é determinado pelo número de caracteres em cada campo de cabeçalho e pelo número total de campos de cabeçalho. Cada caractere de texto consome 1 byte.
    

    > [!TIP]  
    > Alguns servidores proxy ou firewalls de terceiros aplicam seus próprios limites de tamanho de cabeçalho da mensagem. Esses firewalls ou servidores proxy de terceiros podem ter dificuldades para processar mensagens que contenham nomes de arquivos anexos com mais de 50 caracteres ou com caracteres que não sejam US-ASCII.



  - **Limites de tamanho de mensagem**   Esses limites se aplicam ao tamanho total de uma mensagem, que inclui o cabeçalho da mensagem, o corpo da mensagem e todos os anexos. Os limites de tamanho de mensagem podem ser impostos em mensagens de entrada ou de saída. Para o fluxo interno de mensagens, o Exchange usa o cabeçalho de mensagens personalizado do `X-MS-Exchange-Organization-OriginalSize:` para gravar o tamanho original da mensagem quando ela entra na organização do Exchange. Sempre que a mensagem é verificada em relação aos limites de tamanho de mensagem especificados, é usado o menor valor de tamanho de mensagem atual ou o cabeçalho do tamanho de mensagem original. O tamanho da mensagem pode mudar devido à conversão de conteúdo, à codificação e ao processamento do agente.

  - **Limites de tamanho de anexo**   Esses limites se aplicam ao tamanho máximo permitido para um único anexo em uma mensagem. A mensagem pode conter muitos anexos que aumentam muito o tamanho geral da mensagem. Porém, um limite de tamanho do anexo só se aplica ao tamanho de um anexo individual.

  - **Limites de destinatários**   Esses limites se aplicam ao número total de destinatários da mensagem. Na primeira vez que a mensagem é escrita, existem destinatários nos campos de cabeçalho `To:`, `Cc:` e `Bcc:`. Quando a mensagem é enviada para entrega, os destinatários da mensagem são convertidos em entradas `RCPT TO:` no envelope da mensagem. Um grupo de distribuição é contado como um único destinatário durante o envio da mensagem.

Retornar ao início

## Escopo dos limites

A seguir, as categorias básicas para o escopo dos limites disponíveis para mensagens individuais:

  - **Limites organizacionais**   Esses limites se aplicam a todos os servidores de caixa de correio do Exchange 2013 e servidores de Transporte de Hub do Exchange 2010 e do Exchange 2007 existentes na organização. Caso possua um servidor de Transporte de Borda instalado na rede de perímetro, os limites especificados se aplicam ao servidor específico.

  - **Limites de conector**   Esses limites se aplicam a quaisquer mensagens que usem o conector de Envio, conector de Recebimento, conector do Agente de Entrega ou conector estrangeiro para entrega de mensagens. Os conectores de Envio são definidos no serviço de Transporte nos servidores de Caixa de Correio e nos servidores de Transporte de Borda. Os conectores de Recebimento são definidos no serviço de Transporte nos servidores de Caixa de Correio, no serviço de Transporte de Front-End nos servidores de Acesso para Cliente e nos servidores de Transporte de Borda.

  - **Links do site do Active Directory**   O serviço de Transporte nos servidores de Caixa de Correio utilizam sites do Active Directory, bem como os custos atribuídos aos links do site IP do Active Directory, são fatores determinantes para definir o caminho de roteamento mais econômico entre os servidores de Caixa de Correio na organização. É possível atribuir limites de tamanho de mensagem específicos aos links do site do Active Directory na organização.

  - **Limites de servidor**   Esses limites se aplicam a um servidor de Caixa de Correio ou servidor de Transporte de Borda específico. Você pode configurar os limites de mensagens especificados de forma independente em cada servidor de Caixa de Correio ou de Transporte de Borda.
    
    No Outlook Web App, a configuração de limite máximo de tamanho de solicitação HTTP nos servidores de Acesso para Cliente também controlará o tamanho das mensagens que os usuários do Outlook Web App podem enviar.

  - **Limites de usuário**   Esses limites se aplicam a um objeto de usuário específico, como uma caixa de correio, grupo de distribuição ou pasta pública.

As tabelas a seguir exibem os limites de mensagens, incluindo informações sobre como configurar os limites no Shell de Gerenciamento do Exchange ou no Centro de Administração do Exchange (EAC).

### Limites organizacionais

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Limite de tamanho</th>
<th>Valor padrão</th>
<th>Configuração do Shell</th>
<th>Configuração do EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamanho máximo para mensagens recebidas</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parâmetro: <em>MaxReceiveSize</em></p></td>
<td><p><strong>Fluxo de emails</strong> &gt; <strong>Conectores de Recebimento</strong> &gt; <strong>Mais opções</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Ícone Mais opções" alt="Ícone Mais opções" /> &gt; <strong>Configurações de transporte da organização</strong> &gt; guia <strong>Limites</strong> &gt; <strong>Tamanho máximo de mensagem de recebimento</strong></p></td>
</tr>
<tr class="even">
<td><p>Tamanho máximo para mensagens enviadas</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parâmetro: <em>MaxSendSize</em></p></td>
<td><p><strong>Fluxo de emails</strong> &gt; <strong>Conectores de Recebimento</strong> &gt; <strong>Mais opções</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Ícone Mais opções" alt="Ícone Mais opções" /> &gt; <strong>Configurações de transporte da organização</strong> &gt; guia <strong>Limites</strong> &gt; <strong>Tamanho máximo de mensagem de envio</strong></p></td>
</tr>
<tr class="odd">
<td><p>Número máximo de destinatários por mensagem</p>

> [!Tip]  
> <p></p>

</td>
<td><p>5000</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>Parâmetro: <em>MaxRecipientEnvelopeLimit</em></p></td>
<td><p><strong>Fluxo de emails</strong> &gt; <strong>Conectores de Recebimento</strong> &gt; <strong>Mais opções</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Ícone Mais opções" alt="Ícone Mais opções" /> &gt; <strong>Configurações de transporte da organização</strong> &gt; guia <strong>Limites</strong> &gt; <strong>Número máximo de destinatários</strong></p></td>
</tr>
<tr class="even">
<td><p>Tamanho de anexo máximo em regras de Transporte que se aplicam a todos os servidores de Caixa de Correio na organização</p></td>
<td><p>Não configurado</p></td>
<td><p>Cmdlets: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Parâmetro: <em>AttachmentSizeOver</em></p></td>
<td><p><strong>Fluxo de emails</strong> &gt; <strong>Regras</strong> &gt; <strong>Adicionar</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Ícone Adicionar" alt="Ícone Adicionar" /> ou <strong>Editar</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Ícone de edição" alt="Ícone de edição" />.</p>
<p>Use o predicado <strong>Aplicar esta regra se</strong> &gt; <strong>Qualquer anexo</strong> &gt; <strong>for maior do que ou igual a</strong></p>
<p>Use o predicado <strong>Aplicar esta regra se</strong> &gt; <strong>O tamanho</strong> &gt; <strong>da mensagem for maior do que ou igual a</strong></p></td>
</tr>
<tr class="odd">
<td><p>Tamanho de mensagem máximo em regras de Transporte que se aplicam a todos os servidores de Caixa de Correio na organização</p></td>
<td><p></p></td>
<td><p>Cmdlets: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>Parâmetro: <em>MessageSizeOver</em></p></td>
<td><p><strong>Fluxo de emails</strong> &gt; <strong>Regras</strong> &gt; <strong>Adicionar</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Ícone Adicionar" alt="Ícone Adicionar" /> ou <strong>Editar</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Ícone de edição" alt="Ícone de edição" />.</p>
<p>Use o predicado <strong>Aplicar esta regra se</strong> &gt; <strong>O tamanho</strong> &gt; <strong>da mensagem for maior do que ou igual a</strong></p></td>
</tr>
</tbody>
</table>


Retornar ao início

### Limites do conector

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Limite de tamanho</th>
<th>Valor padrão</th>
<th>Configuração do Shell</th>
<th>Configuração do EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamanho de cabeçalho máximo por meio de um conector de recebimento</p></td>
<td><p>128 KB</p></td>
<td><p>Cmdlets: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parâmetro: <em>MaxHeaderSize</em></p></td>
<td><p>N/D</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Tamanho de mensagem máximo por meio de um conector de recebimento</p>

> [!TIP]  
> O tamanho real de mensagem pode ser menor devido à codificação de mensagem e à conversão de conteúdo.


</td>
<td><p><strong>Serviço de transporte em servidores de caixa de correio</strong></p>
<p>35 MB para os conectores Padrão e de Recebimento de Proxy de Cliente</p>
<p><strong>Serviço de Transporte de Front-End nos servidores de Acesso para Cliente</strong></p>
<p>36 MB para os conectores Front-end Padrão e de Recebimento de Front-end de Proxy de Saída.</p>
<p>35 MB para o conector de Recebimento de Front-end de Cliente.</p></td>
<td><p>Cmdlets: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parâmetro: <em>MaxMessageSize</em></p></td>
<td><p><strong>Fluxo de emails</strong> &gt; <strong>Conectores de Recebimento</strong> &gt; <strong>Editar</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Ícone de edição" alt="Ícone de edição" /> &gt; guia <strong>Geral</strong> &gt; <strong>Tamanho máximo da mensagem de recebimento</strong></p></td>
</tr>
<tr class="odd">
<td><p>Número máximo de destinatários por meio de um conector de recebimento</p></td>
<td><p><strong>Serviço de transporte em servidores de caixa de correio</strong></p>
<p>5.000 para o conector de Recebimento Padrão</p>
<p>200 para o conector de Recebimento de Proxy de Cliente</p>
<p><strong>Serviço de Transporte de Front-End nos servidores de Acesso para Cliente</strong></p>
<p>200 para os conectores de Front-end Padrão, Front-end de Cliente e Front-end de Recebimento de Proxy de Cliente.</p>

> [!TIP]  
> Se o número de destinatários for excedido para um remetente anônimo, a mensagem será aceita para os primeiros 200&nbsp;destinatários. A maior parte dos servidores de mensagens SMTP detecta que há um limite de destinatários em vigor. O servidor de mensagens SMTP continua reenviando a mensagem em grupos de 200 destinatários até que a mensagem seja entregue a todos os destinatários.


</td>
<td><p>Cmdlets: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>Parâmetro: <em>MaxRecipientsPerMessage</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Tamanho de mensagem máximo por meio de um conector de envio</p></td>
<td><p>10 MB</p></td>
<td><p>Cmdlets: <strong>New-SendConnector</strong>, <strong>Set-SendConnector</strong></p>
<p>Parâmetro: <em>MaxMessageSize</em></p></td>
<td><p><strong>Fluxo de emails</strong> &gt; <strong>Conectores de Envio</strong> &gt; <strong>Editar</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Ícone de edição" alt="Ícone de edição" /> &gt; guia <strong>Geral</strong> &gt; <strong>Tamanho máximo da mensagem de envio</strong></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Tamanho de mensagem máximo por meio de um link de site do Active Directory</p></td>
<td><p>Ilimitado</p></td>
<td><p>Cmdlet: <strong>Set-AdSiteLink</strong></p>
<p>Parâmetro: <em>MaxMessageSize</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Tamanho de mensagem máximo por meio de um conector do agente de entrega</p></td>
<td><p>Ilimitado</p></td>
<td><p>Cmdlets: <strong>New-DeliveryAgentConnector</strong>, <strong>Set-DeliveryAgentConnector</strong></p>
<p>Parâmetro: <em>MaxMessageSize</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Tamanho de mensagem máximo por meio de um conector estrangeiro</p></td>
<td><p>Ilimitado</p></td>
<td><p><strong>Cmdlet: Set-ForeignConnector</strong> Parâmetro: <em>MaxMessageSize</em></p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


Retornar ao início

### Limites do servidor

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Limite de tamanho</th>
<th>Valor padrão</th>
<th>Configuração do Shell</th>
<th>Configuração do EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamanho de cabeçalho máximo para mensagens no diretório de retirada</p></td>
<td><p>64 KB</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>Parâmetro: <em>PickupDirectoryMaxHeaderSize</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>Número máximo de destinatários por mensagem para mensagens no diretório de retirada</p></td>
<td><p>100</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>Parâmetro: <em>PickupDirectoryMaxRecipientsPerMessage</em></p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>Limites máximos de tamanho das mensagens específicas do cliente do Outlook Web App, Exchange ActiveSync e do Exchange Web Services</p></td>
<td><p>Outlook Web App   35 MB</p>
<p>Exchange ActiveSync   10 MB</p>
<p>Serviços Web do Exchange   64 MB</p>

> [!TIP]  
> Esses valores são aproximadamente 33% maiores que o tamanho máximo de mensagem utilizável real por causa da sobrecarga associada à codificação Base64.


</td>
<td><p>Você configura esses valores no arquivo XML de configuração de aplicativo web.config apropriado em servidores de Acesso para Cliente. Para saber mais, consulte <a href="configure-client-specific-message-size-limits-exchange-2013-help.md">Configurar limites de tamanho de mensagem específicos para o cliente</a>.</p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


Retornar ao início

### Limites do usuário

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Limite de tamanho</th>
<th>Valor padrão</th>
<th>Configuração do Shell</th>
<th>Configuração do EAC</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tamanho de mensagem máximo que possa ser enviado pelo destinatário</p></td>
<td><p>Ilimitado</p></td>
<td><p>Cmdlets:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-RemoteMailbox</strong></p>
<p>Parâmetro: <em>MaxSendSize</em></p></td>
<td><p>Para caixas de correio:</p>
<p><strong>Destinatários</strong> &gt; <strong>Caixas de Correio</strong> &gt; <strong>Editar</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Ícone de edição" alt="Ícone de edição" /> &gt; <strong>Recursos de caixa de correio</strong> &gt; <strong>Fluxo de emails</strong> &gt; <strong>Restrições de tamanho de mensagem</strong> &gt; <strong>Exibir detalhes</strong> &gt; <strong>Mensagens enviadas</strong></p>

> [!TIP]  
> Esta definição não é configurável usando o EAC para outros tipos de destinatário.


</td>
</tr>
<tr class="even">
<td><p>Tamanho de mensagem máximo que possa ser enviado para o destinatário</p></td>
<td><p>Ilimitado</p>
<p>Políticas de provisionamento de caixas de correio de site: 36 MB</p></td>
<td><p>Cmdlets:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>New-SiteMailboxProvisioningPolicy</strong></p>
<p><strong>Set-SiteMailboxProvisioningPolicy</strong></p>
<p>Parâmetro: <em>MaxReceiveSize</em></p></td>
<td><p>Para caixas de correio:</p>
<p><strong>Destinatários</strong> &gt; <strong>Caixas de Correio</strong> &gt; <strong>Editar</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Ícone de edição" alt="Ícone de edição" /> &gt; <strong>Recursos de caixa de correio</strong> &gt; <strong>Fluxo de emails</strong> &gt; <strong>Restrições de tamanho de mensagem</strong> &gt; <strong>Exibir detalhes</strong> &gt; <strong>Mensagens recebidas</strong></p>

> [!TIP]  
> Esta definição não é configurável usando o EAC para outros tipos de destinatário.


</td>
</tr>
<tr class="odd">
<td><p>Número máximo de destinatários por mensagem enviada pelo destinatário</p></td>
<td><p>Ilimitado</p></td>
<td><p>Cmdlets:</p>
<p><strong>Set-Mailbox</strong>, <strong>Set-MailUser</strong></p>
<p>Parâmetro: <em>RecipientLimits</em></p>
<p></p></td>
<td><p>N/D</p></td>
</tr>
</tbody>
</table>


Retornar ao início

## Ordem de precedência para limites de tamanho de mensagem

É possível definir limites de tamanho de mensagem diferentes na organização do Exchange. Como uma mensagem é roteada pela infraestrutura de Transporte, ela pode estar sujeita a várias restrições de tamanho de mensagem diferentes. Você deve planejar restrições de tamanho de mensagem de maneira a garantir que as mensagens no pipeline de transporte sejam rejeitadas assim que possível caso violem os limites de tamanho de mensagem. Em geral, você deve definir limites mais restritivos nos pontos em que as mensagens entram na infraestrutura. Por exemplo, qualquer restrição de tamanho de mensagem em conectores de Recebimento que recebam mensagens da Internet deve ser menor que ou igual às restrições de tamanho de mensagem configuradas para a organização interna do Exchange. Seria uma perda de recursos do sistema o servidor do Exchange aceitar e processar uma mensagem da Internet que seria rejeitada pelo serviço de Transporte nos servidores de Caixa de Correio. Verifique se a organização, o servidor e os limites de conector estão configurados de maneira a minimizar todo o processamento desnecessário de mensagens.

Uma exceção a essa abordagem está nos limites de usuário. Os limites de nível de usuário têm precedência sobre outras restrições de tamanho de mensagem. Por isso, é possível configurar um usuário para exceder os limites de tamanho de mensagem para a organização. Por exemplo, é possível permitir que um grupo específico de caixas de correio de usuário envie mensagens maiores do que o restante da organização configurando limites de envio e recebimento personalizados para essas caixas de correio.

As exceções para os limites do usuário se aplicam somente para troca de mensagens entre usuários autenticados. Se uma mensagem for enviada ou recebida por um destinatário na Internet, os limites organizacionais serão aplicados. Por exemplo, suponha que você tenha uma restrição organizacional de tamanho de mensagem de 10 MB, mas você configurou os usuários do departamento de finanças para enviar e receber mensagens de até 50 MB. Estes usuários serão capazes de trocar mensagens grandes uns com os outros, mas ainda não serão capazes de receber mensagens grandes de usuários da Internet, pois tais mensagens serão provenientes de remetentes não autenticados.

Retornar ao início

## Mensagens isentas de limites de tamanho

A lista a seguir mostra os tipos de mensagens geradas por um servidor de Caixa de Correio ou de Transporte de Borda isentos de todos os limites de tamanho de mensagens:

  - Mensagens do sistema

  - Mensagens geradas por agente

  - Mensagens de notificação de status de entrega (DSN)

  - Mensagens de relatório de diário

  - Mensagens em quarentena

No entanto, essas mensagens continuam sujeitas ao valor organizacional para o número máximo de destinatários em uma mensagem.

Retornar ao início

