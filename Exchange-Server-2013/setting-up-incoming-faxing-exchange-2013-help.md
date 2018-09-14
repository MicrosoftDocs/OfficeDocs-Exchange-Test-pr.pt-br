---
title: 'Configurando o envio de fax de entrada: Exchange 2013 Help'
TOCTitle: Configurando o envio de fax de entrada
ms:assetid: 5d3cae58-1690-424d-9bef-011911d0b608
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633468(v=EXCHG.150)
ms:contentKeyID: 52058423
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurando o envio de fax de entrada

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

A Unificação de Mensagens (UM) do Exchange do Microsoft conta com soluções de fax de parceiros certificadas para recursos de fax aprimorados, como encaminhamento de fax ou fax de saída. Por padrão, servidores Exchange não estão configurados para permitir que os faxes de entrada sejam entregues a um usuário habilitado para UM. Em vez disso, o servidor do Exchange redireciona as chamadas de fax de entrada para uma solução de parceiro de fax certificada. O servidor de fax do parceiro recebe os dados do fax e os envia à caixa de correio do usuário em uma mensagem de email com o fax incluído como anexo .tif.

Para obter mais informações sobre os parceiros de fax, consulte [Microsoft identifique para parceiros de Fax](https://go.microsoft.com/fwlink/?linkid=190238)

## Implantando e configurando fax

A UM encaminha chamadas de fax de entrada a uma solução parceira de fax dedicada, que estabelece a chamada de fax com o remetente e o recebe em nome do usuário habilitado para UM. No entanto, para permitir que usuários habilitados para UM recebam mensagens de fax em suas caixas de correio, você deve primeiro habilitar o recebimento de faxes e definir o URI do parceiro de fax na política de caixa de correio da UM que está vinculada ao usuário habilitado para UM. Você pode permitir ou impedir o recebimento de faxes em planos de discagem de UM, políticas de caixa de correio de UM e na caixa de correio para um usuário habilitado para UM. Para obter informações detalhadas, consulte os seguintes tópicos:

  - [Permitir que os usuários no mesmo plano de discagem para receber faxes](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-users-in-the-same-dial-plan-to-receive-faxes)

  - [Impedir que os usuários no mesmo plano de discagem receber faxes](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/prevent-users-in-the-same-dial-plan-from-receiving-faxes)

  - [Habilitar o envio de fax para um grupo de usuários](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/enable-faxing-for-a-group-of-users)

  - [Desabilitar o envio de fax para um grupo de usuários](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/disable-faxing-for-a-group-of-users)

  - [Habilitar um usuário receber faxes](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/enable-a-user-to-receive-faxes)

  - [Impedir que um usuário receba faxes](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/prevent-a-user-from-receiving-faxes)

## Etapa 1: Implantar Unificação de Mensagens

Para poder configurar o envio de faxes para sua organização local ou híbrida, você precisará implantar com sucesso servidores de Acesso para Cliente e Caixa de Correio e configurar seus gateways VoIP com suporte para permitir o envio de faxes. Para obter detalhes sobre como implantar a UM, consulte [Implementar o UM do Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md). Para obter detalhes sobre como implantar gateways VoIP e PBXs IP, consulte [Conectar UM ao seu sistema telefônico](connect-um-to-your-telephone-system-exchange-2013-help.md).


> [!IMPORTANT]
> O envio e o recebimento de fax usando-se T.38 ou G.711 não são compatíveis em um ambiente no qual a Unificação de Mensagens e o MicrosoftOffice Communications Server 2007 R2 ou Microsoft Lync Server estão integrados.



## Etapa 2: Configurar servidores de parceiro de fax

Em seguida, você precisa habilitar o envio de fax de entrada e configurar o URI do parceiro de fax em cada política de caixa de correio de Unificação de MENSAGENS que você precisa em sua organização. Para implantar com êxito a faxes de entrada, você deve integrar uma solução de parceiro de fax certificados com a Unificação de mensagens do Exchange. Para obter detalhes, consulte [Supervisor de fax para UM do Exchange](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/fax-advisor-for-exchange-um). Para obter uma lista de parceiros certificados de fax, consulte [Microsoft identifique para parceiros de Fax](https://go.microsoft.com/fwlink/?linkid=190238)


> [!TIP]
> Como o servidor do parceiro de fax é externo à sua organização, as portas do firewall devem ser configuradas para permitir as portas do protocolo T.38 que permitem o envio de fax em uma rede baseada em IP. Por padrão, o protocolo T.38 usa porta TCP 6004. Ele também pode usar a porta 6044 do protocolo UDP, mas isso será definido pelo fabricante do hardware. As portas do firewall devem ser configuradas para permitir que dados de fax usem as portas TCP ou UDP ou intervalos de portas definidos pelo fabricante.



## Etapa 3: Habilitar fax em Unificação de Mensagens

Três componentes precisam ser configurados corretamente para que os usuários possam receber faxes usando a Unificação de Mensagens:

  - Planos de discagem da UM

  - políticas de caixa de correio de UM

  - Caixas de correio da UM

O fax pode ser habilitado ou desabilitado nos planos de discagem da UM, nas políticas de caixa de correio da UM ou em uma caixa de correio individual do usuário habilitado para UM. Políticas de caixa de correio da UM podem ser habilitadas ou desabilitadas para envio de fax usando o Centro de Administração do Exchange (EAC) ou o Shell de Gerenciamento do Exchange. A habilitação e desabilitação dos planos de discagem e usuários individuais habilitados para UM precisam ser efetuadas usando o Shell de Gerenciamento do Exchange. A tabela a seguir mostra as opções que estão disponíveis e os cmdlets e parâmetros usados para habilitar e desabilitar o fax.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente de UM</th>
<th>Habilitar/desabilitar usando o EAC?</th>
<th>Exemplo de Shell para habilitar o envio de faxes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Plano de discagem</p></td>
<td><p>Não</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -faxenabled $true</code></p></td>
</tr>
<tr class="even">
<td><p>Política de caixa de correio de UM</p></td>
<td><p>Sim</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyPolicy -AllowFax $true</code></p></td>
</tr>
<tr class="odd">
<td><p>Usuário habilitado para UM</p></td>
<td><p>Não</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -faxenabled $true</code></p></td>
</tr>
</tbody>
</table>


Por padrão, embora o plano de discagem de UM e a caixa de correio do usuário permitam o recebimento de faxes, você deve primeiro habilitar o recebimento de faxes na política de caixa de correio da UM atribuída ao usuário habilitado para UM e inserir o URI do servidor do parceiro de fax.

Para possibilitar que usuários habilitados para UM recebam faxes, você deve fazer o seguinte:

  - Verificar se cada plano de discagem de UM permite que os usuários a ele associados recebam faxes. Por padrão, todos os usuários associados a um plano de discagem podem receber faxes. Para os usuários habilitados para UM receberem mensagens de fax em suas caixas de correio, cada gateway VoIP ou PBX IP deve ser configurado para aceitar chamadas de fax de entrada. Habilite também as mensagens de fax a serem recebidas pelos usuários vinculados ao plano de discagem. Para obter mais informações sobre como permitir ou impedir que usuários vinculados a um plano de discagem recebam mensagens de fax, consulte [Habilitar um usuário receber faxes](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/enable-a-user-to-receive-faxes).
    

    > [!TIP]
    > Se você impedir que mensagens de fax sejam recebidas em um plano de discagem, todos os usuários que estiverem associados ao plano de discagem poderão receber mensagens de fax, mesmo que você configure as propriedades de um usuário individual para permitir que eles recebam mensagens de fax. A habilitação ou a desabilitação de fax em um plano de discagem de UM tem precedência sobre as configurações de um usuário individual habilitado para UM.



  - Configure a política de caixa de correio da UM associada ao usuário habilitado para UM. A política de caixa de correio da UM deve ser configurada para permitir faxes de entrada, inclusive o URI do parceiro de fax e o nome do servidor do parceiro de fax. O parâmetro *FaxServerURI* deve usar a seguinte forma: sip:\<*URI do servidor de fax*\>:\<*porta*\>;\<*transporte*\>, onde \&quot;URI do servidor de fax\&quot; é um FQDN ou um endereço IP do servidor de fax do parceiro. "Porta" é a porta na qual o servidor de fax escuta chamadas de fax recebidas e "transporte" é o protocolo de transporte usado para o fax de entrada (UDP, TCP ou TLS). Por exemplo, você pode configurar uma política de caixa de correio de UM para receber um fax da seguinte maneira.
    
        Set-UMMailboxPolicy MyUMMailboxPolicy -AllowFax $true -FaxServerURI "sip:faxserver.abc.com:5060;transport=tcp"

  - Para obter detalhes, consulte [Definir o parceiro URI para permitir que o envio de fax do servidor de fax](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-the-partner-fax-server-uri-to-allow-faxing).
    

    > [!WARNING]
    > Embora você possa incluir múltiplas entradas no formato para o <EM>FaxServerURI</EM> separando-as com um ponto-e-vírgula, só uma entrada será usada. Este parâmetro permite que apenas uma entrada seja usada, e a adição de várias entradas não permite carregar solicitações de fax de saldo.



  - Verifique se a caixa de correio habilitada para UM pode receber mensagens de fax. Por padrão, todos os usuários associados a um plano de discagem podem receber faxes. No entanto, talvez haja situações nas quais um usuário não pode receber faxes porque a possibilidade de receber faxes foi desabilitada na caixa de correio. Para obter mais informações sobre como possibilitar que um usuário habilitado para UM receba faxes, consulte [Habilitar um usuário receber faxes](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/enable-a-user-to-receive-faxes).
    
    Você pode impedir que um usuário individual associado a um plano de discagem receba faxes. Para fazer isso, configure as propriedades para o usuário, usando o cmdlet **Set-UMMailbox** no Shell. Você pode usar também o cmdlet **Set-UMMailboxPolicy** para evitar que vários usuários recebam mensagens de fax. Para obter mais informações sobre como evitar que um ou vários usuários recebem mensagens de fax, consulte [Impedir que um usuário receba faxes](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/prevent-a-user-from-receiving-faxes).

## Etapa 4: Configurar autenticação

Além de configurar seus planos de discagem de UM, as políticas de caixa de correio de UM e usuários habilitados para UM, você deve configurar a autenticação entre servidores Exchange e o servidor do parceiro de fax. Os servidores do Exchange devem ser capazes de autenticar a origem das mensagens provenientes do servidor do parceiro de fax. As mensagens não autenticadas provenientes de um servidor do parceiro de fax não serão processadas por um servidor Exchange.

Para autenticar a conexão do servidor do parceiro de fax com os servidores do Exchange, você pode usar:

  - TLS mútuo

  - Validação da ID de remetente

  - Um conector de recebimento dedicado

Um conector de recebimento deve ser suficiente para autenticar os servidores do parceiro de fax implantados em sua organização. O conector de recebimento irá garantir que os servidores Exchange tratam de todo o tráfego vindo do servidor do parceiro de fax como autenticado.

O conector de recebimento será configurado no servidor Exchange usado pelo servidor do parceiro de fax para enviar mensagens de fax SMTP e deve estar configurado com os seguintes valores:

  - *AuthMechanism: ExternalAuthoritative*

  - *PermissionGroups: ExchangeServers, PartnersFax*

  - *RemoteIPRanges: {the fax server's IP address}*

  - *RequireTLS: False*

  - *EnableAuthGSSAPI: False*

  - *LiveCredentialEnabled: False*

Para obter detalhes, consulte [Conectores](connectors-exchange-2013-help.md).

Se o servidor do parceiro de fax enviar tráfego de rede para um servidor Exchange em uma rede pública, por exemplo, um servidor do parceiro de fax baseado em serviços hospedado na nuvem, é uma boa ideia autenticar o servidor do parceiro de fax usando uma verificação de ID de remetente. Este tipo de autenticação garante que o endereço IP do qual a mensagem de fax veio está autorizado a enviar mensagens de email em nome do domínio do parceiro de fax do qual as mensagens vieram. O DNS é usado para armazenar os registros de ID de remetente (ou registros de SPF (estrutura de política de remetente) e parceiros de fax devem publicar seus registros SPF na zona de pesquisa direta DNS. O Exchange irá validar os endereços IP por meio de consultas DNS. No entanto, o agente de ID de remetente deve estar sendo executado em um servidor de caixa de correio para ser capaz de realizar a consulta DNS.

Você também pode usar TLS para criptografar o tráfego de rede, ou TLS mútuo para criptografia e autenticação entre o servidor do parceiro de fax e servidores Exchange.

