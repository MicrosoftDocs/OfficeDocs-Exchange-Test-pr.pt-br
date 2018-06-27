---
title: 'Permitir que o indicador de espera de mensagem: Exchange 2013 Help'
TOCTitle: Permitir que o indicador de espera de mensagem
ms:assetid: 57fb439e-8208-499f-a20b-814677843a8c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298001(v=EXCHG.150)
ms:contentKeyID: 54651966
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir que o indicador de espera de mensagem

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-03-09_

Indicador de Espera da Mensagem (MWI) é um recurso encontrado na maioria dos sistemas de caixa postal herdados. Ele permite que os usuários saibam que têm mensagens de voz novas ou não ouvidas. Na sua forma mais comum, este recurso acende uma lâmpada no telefone de um usuário para indicar a presença de uma mensagem de voz nova ou não ouvida.

**Sumário**

Visão geral

The Mailbox server's role in MWI

MWI SIP NOTIFY messages

MWI resilience

MWI administration

Text message (SMS) notifications for voice mail messages and missed calls

## Visão geral

Notificações de MWI podem incluir qualquer mecanismo que indica a existência de uma mensagem de voz nova ou não ouvida. A mensagem pode estar em uma nova mensagem de email ou uma marcada como não lida. A notificação MWI pode tomar qualquer uma das seguintes formas:

  - Uma nova mensagem de caixa postal, como no Outlook ou no Outlook Web App.

  - Uma mensagem de texto ou SMS enviada para um celular configurado para receber mensagens de texto.

  - Uma chamada de saída feita pela UM do Exchange.

  - Uma lâmpada em um telefone.

  - Um tom de discagem especial.

  - Ícones ou botões na tela do visor de um telefone.

  - Uma notificação realçada em um aplicativo.

Na Unificação de Mensagens, um correio de voz do usuário é armazenado em sua caixa de correio. Ela pode ser acessada de um telefone usando Outlook Voice Access, de um desktop ou um computador portátil usando Outlook ou Outlook Web App e de clientes de celular. Quando um usuário recebe uma nova mensagem de voz, a mensagem aparece na pasta de pesquisa do correio de voz. Se a mensagem de voz for acessada com o uso do Outlook ou do Outlook Web App, uma mensagem de email será incluída na mensagem de voz.

Quando versões anteriores de UM foram implantadas em uma organização, o MWI apoiava-se em um ambiente tradicional de gateway VoIP ou um ambiente de PBX IP usando uma solução ou aplicativo de terceiros, ou foi incluído como parte de UM do Exchange. No Exchange 2010 ou posterior, o MWI também é suportado quando a UM é implantada com o Microsoft Lync Server. O mecanismo de notificação MWI usado pelo Lync Server depende do tipo de telefone baseado em VoIP que é usado pelo Enterprise Voice e usuário habilitado para UM, e pode estar localizado em qualquer um dos seguintes:

  - Um telefone

  - Um visor de telefone

  - Um botão de teclado de discagem

Por padrão, o MWI é ativado para todos os usuários que são habilitados para UM. Ele é controlado por meio de configurações em uma política de caixa de correio de UM ou nos gateways IP de UM que foram criados e vinculados a um plano de discagem de UM. O MWI também funciona com mensagens de voz protegidas.

Para implementar o MWI em um ambiente de telefonia tradicional com gateways VoIP, PBXs IP ou PBXs habilitados para SIP, um servidor de caixa de correio executando o serviço de Unificação de Mensagens do Microsoft Exchange envia uma mensagem de notificação de protocolo SIP do MWI para um *SIP de mesmo nível*, que é um PBX IP, um gateway VoIP usado com um PBX herdado, um PBX habilitado para SIP ou, se você tiver implantado o Lync Server, os servidores do Lync também são considerados SIP de mesmo nível. O PBX IP ou PBX acende a lâmpada no telefone de mesa para notificar o usuário de uma mensagem de voz nova ou não ouvida.

Há duas maneiras pelas quais os chamadores podem deixar mensagens de voz: usando atendimento de chamadas e Outlook Voice Access. Com atendimento de chamadas, um servidor de caixa de correio atende uma chamada e permite que o chamador deixe uma mensagem de voz para um usuário. Com o Outlook Voice Access, quando um chamador ligar para um número do Outlook Voice Access, ele poderá usar o sistema de menus para deixar uma mensagem de voz para um usuário habilitado para UM.

Voltar ao início

## Função do servidor de caixa de correio em MWI

Quando um chamador liga para um usuário habilitado para UM e o usuário não atende seu telefone, o serviço de Unificação de Mensagens do Microsoft Exchange em um servidor de caixa de correio recebe informações de alteração de estado do MWI e usa uma mensagem de Notificação SIP para enviar a solicitação de alteração de notificação para um gateway VoIP, PBX IP ou PBX habilitado para SIP. A alteração da notificação inclui as seguintes informações:

  - Indicador de espera de mensagem habilitado (Sim ou Não).

  - Número de mensagens de voz novas ou não ouvidas.

  - Número de mensagens de voz antigas ou ouvidas.

  - Número de mensagens de voz urgentes novas ou não ouvidas.

  - Número de mensagens de voz urgentes antigas ou ouvidas.

  - O número do ramal principal no plano de discagem de UM principal.

  - O endereço IP ou nome de domínio totalmente qualificado (FQDN) do SIP correspondente para ser usado para mensagens de notificação SIP.

  - O tipo de segurança do plano de discagem de UM (Não Protegido, Protegido por SIP ou Protegido). Esta informação será usada para determinar se a conexão com o gateway VoIP ou PBX IP deve ser SIP por TCP ou SIP por TLS. Protocolo TLS com suporte para notificação SIP do MWI.

Um servidor de caixa de correio usa as informações de desvio do cabeçalho de chamada de entrada para determinar o número do ramal ou número de telefone do usuário habilitado para UM. Quando o número de telefone ou ramal é determinado, o servidor de caixa de correio envia a solicitação para o SIP correspondente. O SIP correspondente, em seguida, altera o estado do MWI e ativa a notificação no telefone do usuário.


> [!TIP]
> Embora as paralisações de PBX devam ser raras, a UM atualiza automaticamente o estado do MWI para cada caixa de correio pelo menos uma vez a cada 12 horas. Não há nenhuma maneira para forçar uma atualização, mas se o PBX ou PBX IP estiver desligado e todas as lâmpadas do MWI se apagarem, todas as lâmpadas devem ser restauradas para o estado correto dentro de seis horas.



Voltar ao início

## Mensagens de notificação SIP do MWI

As notificações do MWI usam mensagens de notificação SIP para se comunicar com os SIP correspondentes. Informações de alteração de estado do MWI estão incluídas na mensagem de notificação SIP e indica se as notificações do MWI serão enviadas aos usuários. Sempre que há uma alteração no estado do MWI, o Assistente de Caixa de Correio envia essas informações para o serviço de Unificação de Mensagens do Microsoft Exchange sendo executado em um servidor de caixa de correio. Depois que o serviço de Unificação de Mensagens recebe essas informações, ele analisa a mensagem para obter o SIP correspondente de destino e as informações de alteração de estado do MWI. Ele forma uma mensagem de notificação SIP com as informações de alteração de estado do MWI no corpo da mensagem e envia essas informações para o SIP correspondente.

O MWI baseia-se na RFC 3842. O RFC 3842 afirma que as notificações de eventos do SIP devem ser utilizadas para notificações de mensagens em espera. MWI tem como base o modelo SIP e é direcionada pelos pontos de extremidade encontrados em um sistema de mensagens unificadas. Pontos de extremidade do SIP, também chamados de SIP correspondente, que obtêm informações do MWI devem enviar uma mensagem de inscrição do SIP para o serviço de Unificação de Mensagens. O serviço responde com uma mensagem de notificação que indica que a inscrição foi aceita. Todas as informações de alteração de estado do MWI serão transportadas do sistema de Unificação de Mensagens para um ponto de extremidade do SIP usando mensagens de notificação que são inseridas na inscrição que foi criada anteriormente. A sintaxe exata da mensagem de notificação SIP a ser enviada para o SIP correspondente é baseada no formato descrito no RFC 3842.

Quando o serviço de Unificação de Mensagens em um servidor de caixa de correio envia uma mensagem de notificação do MWI para o SIP correspondente, o cabeçalho do evento é definido como "resumo-mensagem", que indica que se trata de uma mensagem de notificação relacionada ao MWI. O campo do cabeçalho Para indica o ponto de extremidade SIP para o qual o serviço de MWI deve ser fornecido. O cabeçalho Assinatura-Estado deve ser definido como \&quot;finalizado\&quot; em vez de \&quot;ativo\&quot;. As seguintes ações ocorrem em resposta à mensagem de notificação SIP:

1.  O SIP correspondente transmite essas informações ao PBX usando um protocolo de comutação de circuitos, como SMDI.

2.  O PBX envia uma mensagem de sucesso em um protocolo de comutação telefônica.

3.  O SIP correspondente pode responder com qualquer uma das seguintes mensagens: 200 OK (Sucesso) ou 480 (Temporariamente Indisponível). Um servidor de caixa de correio pode tratar estas respostas e respostas adicionais com falha.

## MWI em um ambiente de telefonia tradicional

Em um ambiente de telefonia tradicional, uma chamada é recebida pelo PBX e, em seguida, enviada para o gateway VoIP, ou recebida pelo PBX IP ou PBX habilitado para SIP. O servidor de caixa de correio e o assistente de caixa de correio são usados para determinar o estado do MWI para o usuário habilitado para UM. Eles são responsáveis por entregar a notificação SIP de volta para o gateway VoIP e PBX herdado, PBX IP ou PBX habilitado para SIP.

Em um ambiente de telefonia tradicional, o fluxo de chamadas e a notificação de MWI são conforme segue:

1.  A chamada de entrada é recebida pelo PBX herdado, encaminhada para o gateway VoIP, ou para um PBX IP ou PBX habilitado para SIP, e encaminhada para o ramal do usuário habilitado para UM. O usuário não responde, e o chamador é solicitado a deixar uma mensagem de voz.

2.  O gateway VoIP ou PBX IP envia a chamada para um servidor de caixa de correio que está executando o serviço de Unificação de Mensagens do Microsoft Exchange.

3.  O servidor de caixa de correio executa uma consulta LDAP para localizar informações do usuário habilitado para UM, como o número do ramal do usuário e saudações pessoais. As saudações para o usuário habilitado para UM são reproduzidas.

4.  A mensagem de voz que foi criada pelo serviço de Unificação de Mensagens é enviada para o serviço de transporte do Microsoft Exchange no mesmo servidor de caixa de correio.

5.  O serviço de transporte no servidor de caixa de correio envia a mensagem de voz para o servidor de caixa de correio que contém a caixa de correio do usuário. O Assistente de Caixa de Correio recebe um evento MAPI para uma nova mensagem de voz.

6.  O Assistente de Caixa de Correio lê o plano de discagem de UM e a política de caixa de correio de UM para determinar se as notificações de MWI devem ser enviadas ao usuário habilitado para UM. As consultas do Assistente de Caixa de Correio para todos os servidores de caixa de correio que estão associados ao plano de discagem de UM do usuário habilitado para UM. O Assistente de Caixa de Correio tenta enviar o evento RPC para o primeiro servidor de caixa de correio que é retornado. Se esse falhar, ele tentará enviar o seguinte Vai manter repetindo por cinco minutos ou até que todos os servidores de caixa de correio tenham sido tentados. Se todas as chamadas RPC falharem, o Assistente de Caixa de Correio registrará em log o erro no Visualizador de Eventos. As consultas do servidor de caixa de correio para todos os gateways IP de UM são associadas ao plano de discagem de UM da caixa de correio do usuário habilitado para UM.

7.  A UM envia uma mensagem de notificação SIP para o primeiro gateway VoIP ou PBX IP retornado da consulta. Se isso falhar, o servidor de caixa de correio vai escolher o próximo gateway VoIP ou PBX IP. O servidor de caixa de correio vai continuar tentando um gateway VoIP ou PBX IP por cinco minutos. Se todas as tentativas de encontrar um gateway VoIP ou PBX IP falharem, o servidor de caixa de correio registrará um erro. Se um gateway VoIP ou PBX IP for localizado com sucesso, o gateway VoIP irá enviar a notificação para o PBX, e o PBX enviará uma notificação do evento MWI para o telefone do usuário para acender a lâmpada do telefone. Se um PBX IP for usado, a notificação do MWI será processada pelo PBX IP e, em seguida, a lâmpada do telefone do usuário será acesa. Outros mecanismos de notificação do MWI estão listados na seção Visão geral. O tipo de notificação depende do fornecedor de hardware de PBX ou PBX IP e se o Lync Server está sendo usado. Também depende do tipo de telefone — analógico, digital ou VoIP — que está sendo usado.

Voltar ao início

## MWI em um ambiente do Lync Server

Em ambientes de telefonia que incluem Lync Server, uma chamada de entrada pode ser enviada de um telefone externo para um servidor de mediação, enviada de um cliente do Lync ou enviada de comunicações unificadas (UC) ou outro telefone baseado em VoIP. Depois que a chamada é recebida, ela é enviada para o pool do servidor front-end do Lync Server. O servidor de caixa de correio e o Assistente de Caixa de Correio são usados para determinar o estado do MWI para o usuário habilitado para UM e entregar essa notificação para o cliente do Lync, analógico, digital ou UC ou telefone baseado em VoIP.

Em um ambiente de telefonia com Lync Server, o fluxo de chamadas e a notificação do MWI são os seguintes:

1.  A chamada é enviada de um dos seguintes:
    
      - Um telefone externo à organização (enviado para um servidor de mediação)
    
      - Um cliente baseado no Lync
    
      - UC ou outro telefone baseado em VoIP

2.  A chamada de entrada é recebida pelo pool de servidor front-end do Lync Server e enviada para o telefone ou o ponto de extremidade SIP do usuário habilitado para UM. O usuário não responde, e o chamador é solicitado a deixar uma mensagem de voz.

3.  O pool do servidor front-end do Lync Server envia a chamada para um servidor de caixa de correio dentro da rede local e a caixa de correio do usuário é encontrada.

4.  O servidor de caixa de correio executa uma consulta LDAP para localizar informações para o usuário habilitado para UM, como seu número de ramal e saudações. As saudações são reproduzidas, e o chamador é solicitado a deixar uma mensagem de voz.

5.  A mensagem de voz que foi criada pelo serviço de Unificação de Mensagens é enviada para o serviço de transporte no mesmo servidor de caixa de correio no mesmo site.

6.  O serviço de transporte envia a mensagem de voz para o servidor de caixa de correio que contém a caixa de correio do usuário. O Assistente de Caixa de Correio recebe um evento MAPI para a nova mensagem de voz.

7.  O Assistente de Caixa de Correio lê o plano de discagem de UM e a política de caixa de correio de UM para decidir se as notificações de MWI devem ser enviadas ao usuário habilitado para UM. As consultas do Assistente de Caixa de Correio para todos os servidores de caixa de correio que estão associados ao plano de discagem do usuário. O Assistente de Caixa de Correio tenta enviar o evento RPC para o primeiro servidor de caixa de correio que é retornado. Se essa tentativa falhar, ele tentará o seguinte. Vou continuar tentando encontrar um servidor de caixa de correio por cinco minutos ou até que todos os servidores tenham sido tentados. Se todas as chamadas RPC falharem, o Assistente de Caixa de Correio registrará em log um erro no Visualizador de Eventos. O servidor de caixa de correio consulta o Active Directory para todos os gateways IP de UM associados ao plano de discagem de UM do usuário habilitado para UM.

8.  A UM envia uma mensagem de notificação SIP para o primeiro gateway VoIP ou PBX IP retornado da consulta. Se isso falhar, o servidor de caixa de correio vai escolher o próximo gateway VoIP ou PBX IP. O servidor de caixa de correio vai continuar tentando encontrar um gateway VoIP ou PBX IP por cinco minutos. Se todas as tentativas de contatar o gateway VoIP ou PBX IP falharem, o servidor de caixa de correio registrará um erro. Se for bem-sucedida, o gateway VoIP ou PBX IP enviará a notificação para o pool de servidor front-end do Lync Server que, por sua vez, enviará uma notificação do evento MWI para um ponto de extremidade SIP usado pelo usuário, o telefone do usuário ou um cliente do Lync.

Voltar ao início

## Resiliência de MWI

Quando você está implantando servidores de Caixa de Correio e Acesso para Cliente, planos de discagem de UM e gateways IP de UM, e está usando MWI para usuários habilitados para UM, é melhor implantar servidores múltiplos de Caixa de Correio e Acesso para Cliente, bem como vários gateways VoIP e PBXs IP para criar resiliência e tolerância a falhas. Isso também cria resiliência do MWI porque ele fornece várias maneiras para enviar notificações do MWI, conforme descrito na seção anterior.

Para habilitar a tolerância a falhas para MWI na UM, você deverá criar e configurar um ou mais dos seguintes:

  - Um plano de discagem de UM vinculado com o usuário habilitado para UM que receberá as notificações do MWI.

  - Uma política de caixa de correio de UM vinculada com o usuário habilitado para UM que receberá as notificações do MWI.

  - Um gateway IP de UM vinculado com o plano de discagem que está vinculado com o usuário habilitado para UM que receberá as notificações do MWI.

  - Se o Lync Server for usado, todos os servidores de Caixa de Correio e Acesso para Cliente devem ser adicionados ao plano de discagem de URI do SIP vinculado com o usuário habilitado para UM que receberá as notificações do MWI.

## Administração do MWI

O MWI pode ser administrado pelas definições de configuração em dois componentes de UM: políticas de caixa de correio de UM e gateways IP de UM. Para ambos os componentes de UM, você pode habilitar ou desabilitar as notificações do MWI usando o cmdlet **Set-UMMailboxPolicy** ou o cmdlet **Set-UMIPgateway** no Shell de Gerenciamento do Exchange. Você também pode configurar as definições usando o Centro de Administração do Exchange (EAC). Você pode exibir o status de notificações do MWI usando o cmdlet **Get-UMMailboxPolicy** e o cmdlet **Get-UMIPgateway** no Shell ou exibindo as configurações no EAC.

## Políticas de caixa de correio de UM e MWI

Você pode criar uma política de caixa de correio de UM para aplicar um conjunto comum de configurações de política de UM a uma coleção de caixas de correio habilitadas para UM. Por exemplo, você pode usar uma política de caixa de correio de UM para aplicar as configurações de política de PIN, restrições de discagem e configurações de notificações do MWI. Se você habilitar ou desabilitar o MWI em uma política de caixa de correio de UM, ele vai ser ativado ou desativado para todos os usuários habilitados para UM vinculados a essa política de caixa de correio de UM. A configuração do MWI também pode ser aplicada a um subconjunto de usuários vinculados a um plano de discagem de UM. Para saber mais sobre as políticas de caixa de correio de UM, incluindo como habilitar ou desabilitar o MWI para um grupo de usuários habilitados para UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

Você pode usar o EAC ou o cmdlet **Set-UMMailboxPolicy** no Shell para definir a configuração do MWI, como mostra a tabela a seguir.

### Configuração de Indicador de espera de mensagem (MWI) em uma política de caixa de correio de UM

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro Shell</th>
<th>Configuração disponível no EAC?</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowMessageWaitingIndicator</em></p></td>
<td><p>Sim</p></td>
<td><p>O parâmetro <em>AllowMessageWaitingIndicator</em> especifica se os usuários vinculados a uma política de caixa de correio de UM podem receber notificações do MWI quando receberem uma nova mensagem de voz. O valor padrão é <code>$true</code>.</p>
<p>Quando essa configuração está habilitada, as notificações do MWI são enviadas aos usuários vinculados a uma única política de caixa de correio de UM para chamadas feitas por um gateway IP de UM. Essa configuração permite que o gateway IP de UM receba e envie mensagens de notificação SIP para telefones de usuários habilitados para UM ou pontos de extremidade de SIP.</p>
<p></p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre como gerenciar configurações do MWI em uma política de caixa de correio de UM, consulte os seguintes tópicos:

  - [Gerenciar uma política de caixa de correio de Unificação de mensagens](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [Habilitar o indicador de espera de mensagem (MWI) para usuários](enable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [Desabilitar o indicador de espera de mensagem (MWI) para usuários](disable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/pt-br/library/bb124903\(v=exchg.150\))

## Gateways IP de UM e MWI

Se você desabilitar o MWI em um gateway IP de UM, vai desabilitar notificações do MWI para todos os usuários que se conectam ao gateway VoIP ou o PBX IP que é representado pelo gateway IP de UM. Desabilitar o MWI em um único gateway IP de UM vinculado a um plano de discagem de UM pode desabilitar as notificações do MWI para todos os usuários habilitados para UM associados a um único ou vários planos de discagem de UM ou uma ou várias políticas de caixa de correio de UM. Para saber mais sobre as políticas de caixa de correio de UM, incluindo como habilitar ou desabilitar o MWI para um grupo de usuários habilitados para UM, consulte [Gerenciar uma política de caixa de correio de Unificação de mensagens](manage-a-um-mailbox-policy-exchange-2013-help.md).

Você pode usar o EAC ou o cmdlet **Set-UMMailboxPolicy** no Shell para definir a configuração do MWI, como mostra a tabela a seguir.

### Configuração de Indicador de espera de mensagem (MWI) em um gateway IP de UM

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro Shell</th>
<th>Configuração disponível no EAC?</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>MessageWaitingIndicatorAllowed</em></p></td>
<td><p>Sim</p></td>
<td><p>O parâmetro <em>MessageWaitingIndicatorAllowed</em> especifica se o gateway IP da UM deve ser habilitado para permitir que mensagens de Notificação SIP sejam enviadas aos usuários associados a um plano de discagem da UM. O valor padrão é <code>$true</code>.</p>
<p>Quando essa configuração está habilitada, as notificações de caixa postal podem ser enviadas aos usuários para chamadas recebidas pelo gateway IP de UM. Essa configuração permite que o gateway IP de UM envie notificações de espera de mensagem a usuários habilitados para UM.</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre como gerenciar configurações de MWI, consulte estes tópicos:

  - [Gerenciar um gateway IP de UM](manage-a-um-ip-gateway-exchange-2013-help.md)

  - [Permitir o indicador de espera de mensagem (MWI) em um gateway IP de UM](allow-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [Impedir que o indicador de espera de mensagem (MWI) em um gateway IP de UM](prevent-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [Set-UMIPGateway](https://technet.microsoft.com/pt-br/library/aa996577\(v=exchg.150\))

Voltar ao início

## Notificações de mensagem de texto (SMS) para mensagens de voz e chamadas não atendidas

Como mencionado anteriormente, uma notificação do MWI é qualquer mecanismo que indica a existência de uma nova mensagem de voz. Além dos mecanismos já discutidos, os usuários podem ser notificados de que eles têm uma mensagem de voz aguardando via mensagem de texto, também chamada de mensagem SMS (Short Message Service). Este é um tipo diferente de notificação do MWI para novas mensagens de voz do que a luz tradicional ou outros mecanismos.

Uma mensagem de texto é enviada para o telefone celular de um usuário quando um chamador deixa uma nova mensagem de voz. Os usuários também podem receber uma mensagem de texto notificando quando eles perdem uma chamada telefônica e uma mensagem de voz não é deixada. A mensagem de texto de notificação de chamada não atendida pode ser enviada para o usuário junto com a nova notificação de correio de voz.


> [!TIP]
> A mensagem de texto que é enviada a um usuário inclui visualização da caixa postal.



Notificações de mensagem de texto usam configurações diferentes das configurações do MWI no gateway IP de UM ou a política de caixa de correio de UM. Notificações de mensagem de texto para novo correio de voz e chamadas não atendidas são configuradas em caixas de correio de UM e políticas de caixa de correio de UM. Você pode habilitar ou desabilitar notificações de mensagem de texto usando o cmdlet **Set-UMMailboxPolicy** e o cmdlet **Set-UMMailbox** no Shell. Você pode exibir o status de notificações de mensagem de texto usando o cmdlet **Get-UMMailboxPolicy** e o cmdlet **Get-UMMailbox**. Não é possível configurar notificações de mensagem de texto no EAC.

A tabela a seguir mostra o parâmetro em uma caixa de correio de UM que deve ser configurada para um usuário receber mensagens de texto para as notificações de caixa postal e chamadas perdidas:

### Configurações de notificação de mensagem de texto na caixa de correio de um usuário

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>UMSMSNotificationOption</em></p></td>
<td><p>Não</p></td>
<td><p>O parâmetro <em>UMSMSNotificationOption</em> especifica se um usuário habilitado para UM pode receber notificações de mensagens de texto somente para caixa postal, para caixa postal e chamadas perdidas ou não pode receber nenhuma notificação. Os valores para esse parâmetro são: <code>VoiceMail</code>, <code>VoiceMailAndMissedCalls</code> e <code>None</code>. O valor padrão é <code>None</code>.</p>
<p></p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre como gerenciar configurações de notificação de mensagem de texto na caixa de correio de um usuário, consulte os seguintes tópicos:

  - [Gerenciar configurações de caixa postal de um usuário](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/pt-br/library/bb124893\(v=exchg.150\))

A tabela a seguir mostra o parâmetro em uma política de caixa de correio de UM que deve ser configurada para um usuário para receber mensagens de texto para notificações de caixa postal e chamadas perdidas:

### Configurações de notificação de mensagem de texto e chamada perdida em uma política de caixa de correio de UM

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro Shell</th>
<th>Configuração disponível no EAC?</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowSMSNotification</em></p></td>
<td><p>Não</p></td>
<td><p>O parâmetro <em>AllowSMSNotification</em> especifica se usuários habilitados para UM, cujas caixas de correio estejam associadas à política de caixa de correio de UM, têm permissão para receber notificações de mensagem de texto em seus celulares. Se este parâmetro estiver definido como <code>$true</code>, você deverá também usar o cmdlet <strong>Set-UMMailbox</strong> e definir o parâmetro <em>UMSMSNotificationOption</em> do usuário habilitado para UM como <code>voicemail</code> ou <code>VoiceMailAndMissedCalls</code>. O valor padrão é <code>$true</code>.</p>
<p></p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre como gerenciar configurações de notificação de mensagem de texto, consulte os seguintes tópicos:

  - [Gerenciar uma política de caixa de correio de Unificação de mensagens](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/pt-br/library/bb124903\(v=exchg.150\))

Para as notificações de mensagem de texto para caixa postal e chamadas perdidas funcionarem corretamente, você deve executar as seguintes tarefas:

1.  Use o EAC ou Shell para habilitar o usuário para UM e vinculá-lo à política de caixa de correio UM correta.

2.  Na política de caixa de correio de UM vinculada ao usuário, verifique se o parâmetro *AllowSMSNotification* está definido como `$true`. Para definir o parâmetro como `$true`, execute o seguinte comando: `Set-UMMailboxPolicy -id MyUMMailboxPolicy - AllowSMSNotification $true`.

3.  Na caixa de correio do usuário, habilite as notificações de mensagem de texto definindo o parâmetro *UMSMSNotificationOption* como `VoiceMailAndMissedCalls` ou `VoiceMail`.

4.  Como a configuração padrão é `None`, você deve executar o seguinte comando no Shell e definir a opção de notificação de mensagem de texto como `VoiceMailAndMissedCalls` ou `VoiceMail`. Por exemplo: `Set-UMMailbox- -id MyUMMailbox -UMSMSNotificationOption VoiceMailAndMissedCalls`.
    

    > [!IMPORTANT]
    > O parâmetro <EM>AllowSMSNotification</EM> na política de caixa de correio de UM e o parâmetro <EM>UMSMSNotificationOption</EM> na caixa de correio do usuário devem ser definidos como <CODE>$true</CODE> para as notificações de SMS funcionarem.



Além da configuração da política de caixa de correio de UM e da caixa de correio do usuário para habilitar as notificações de mensagem de texto para novo correio de voz e chamadas perdidas, o usuário deve habilitar e configurar as notificações de mensagem de texto quando entrarem no Outlook Web App. Para instalar e configurar as notificações de mensagem de texto, o usuário deve:

1.  Entre no Outlook Web App e vá em **Opções** \> **Telefone** \> **Caixa Postal**.

2.  Na página **Caixa Postal**, em **Notificações**, clique em **Configurar notificações**.

3.  Na página **Mensagens de texto**, clique no botão **Ativar notificações**.
    

    > [!WARNING]
    > Não clique em <STRONG>Notificações de caixa postal</STRONG> ou você voltará para a página <STRONG>Caixa postal</STRONG>.



4.  Na página **Mensagens de texto**, em **Localidade**, use a lista suspensa para selecionar a localidade ou local da operadora móvel de mensagens de texto.

5.  Na página **Mensagens de texto**, em **Operadora móvel**, use a lista suspensa para selecionar a operadora móvel de mensagens de texto e clique em **Avançar**.

6.  Na página de **Mensagens de texto**, na caixa **Insira o número de telefone e clique em Avançar**, digite o número do celular que é usado para notificações de mensagem de texto e clique em **Avançar**. Será enviada uma senha de seis dígitos para o celular. Se você não recebeu uma senha, clique em **Não recebi uma senha e preciso que ela seja enviada novamente**.

7.  Insira a senha na caixa **Senha** e, em seguida, clique em **Concluir**.

8.  Depois que o usuário habilitar notificações de mensagem de texto, ele poderá clicar em **Configurar notificações por caixa postal** na página **Mensagens de texto**. Ele será levado de volta para a página de caixa postal, onde pode rolar para baixo até a seção **Notificações** e configurar opções de notificação de mensagem de texto para chamadas perdidas e caixa postal.

Voltar ao início

