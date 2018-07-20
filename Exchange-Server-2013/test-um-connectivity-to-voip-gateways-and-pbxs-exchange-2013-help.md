---
title: 'Teste a conectividade UM com gateways VoIP e PBXs: Exchange 2013 Help'
TOCTitle: Teste a conectividade UM com gateways VoIP e PBXs
ms:assetid: 2aca8631-a99a-4e29-aff0-e462385f03b2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996906(v=EXCHG.150)
ms:contentKeyID: 56270505
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Teste a conectividade UM com gateways VoIP e PBXs

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2014-09-17_

Você pode testar a operação da Unificação de Mensagens (UM) e o equipamento de telefonia ao qual ela está conectada. Ao realizar o procedimento a seguir, o servidor de Caixa de Correio e de Acesso para Cliente testam a operação completa ponta a ponta do sistema de correio de voz. Isso inclui os componentes de telefonia conectados aos servidores de Caixa de Correio e de Acesso para Cliente, incluindo gateways VoIP, PBXs (Centrais Privadas de Comutação Telefônica), PBXs IP e cabeamento.

Para tarefas de gerenciamento adicionais relacionadas à solução de Unificação de mensagens, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalização: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entradas sobre "Servidor de caixa de correio (serviço de UM)" e \&quot;Servidor de Acesso para Cliente (serviço de roteador de chamadas de UM)\&quot;, no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Para realizar os procedimentos a seguir, você deve fazer logon no servidor de Caixa de Correio usando uma conta que seja membro do grupo de Administradores locais.

  - Verifique se o servidor de Caixa de Correio está instalado no mesmo computador que o servidor de Acesso para Cliente ou em um computador separado.

  - Verifique se o servidor de Acesso para Cliente está instalado no mesmo computador que o servidor de Caixa de Correio ou em um computador separado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o Shell para testar a operação da Unificação de Mensagens os componentes de telefonia

Este exemplo testa a capacidade do gateway IP da UM de escutar por solicitações SIP de entrada na porta TCP 5060.

    Test-UMConnectivity -ListenPort 5060 -UMIPGateway MyIPGateway

Este exemplo testa a capacidade do servidor de Caixa de Correio Local de usar uma conexão TCP não segura ao invés de uma conexão TLS mútua segura para fazer uma chamada através de um gateway IP de UM denominado `MyUMIPGateway` com o uso do número de telefone 56780.

    Test-UMConnectivity -UMIPGateway MyUMIPGateway -Phone 56780 -Secured $false

Este exemplo testa o número do Outlook Voice Access em um plano de discagem usando uma URI de SIP. Este exemplo pode ser usado em um ambiente que inclui o Lync Server.

    Test-UMConnectivity -UMIPGateway OCSGateway1 -Phone "sip:SIPdialplan.contoso.com@contoso.com"


> [!TIP]
> Você pode definir o parâmetro <CODE>-Timeout</CODE> com um valor inferior a 5 segundos. No entanto, recomendamos que você sempre configure esse parâmetro com um valor de 5 segundos ou mais. Use o modo 2 quando o parâmetro <CODE>&shy;UMIPGateway</CODE> for especificado na sintaxe de linha de comando.


