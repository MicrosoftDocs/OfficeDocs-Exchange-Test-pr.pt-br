---
title: 'Permitir ou impedir que um servidor de acesso para cliente de atendimento de chamadas: Exchange 2013 Help'
TOCTitle: Permitir ou impedir que um servidor de acesso para cliente de atendimento de chamadas
ms:assetid: 8287bb78-2621-4b80-a128-8f2ccd67923a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123529(v=EXCHG.150)
ms:contentKeyID: 50556217
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir ou impedir que um servidor de acesso para cliente de atendimento de chamadas

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-18_

Você pode permitir que o serviço Microsoft Exchange Unified Messaging roteador de chamadas em um servidor de acesso para cliente para atender chamadas novas ou impedir isso. Por padrão, um servidor de acesso para cliente está em um estado habilitado depois que ele é instalado. Quando você estiver definindo o servidor de acesso para cliente para aceitar entrada chamadas de voz, fax, atendedor automático e Outlook Voice Access, você pode usar o cmdlet **Set-ServerComponentState** .

Configurando o modo de manutenção para um servidor de acesso para cliente permite que você coloque o servidor de serviço. Para um servidor de acesso para cliente, fora de serviço significa que o servidor não aceita qualquer chamadas de entrada de gateways VoIP, IP PBXs, PBXs habilitados para SIP ou controladores de borda de sessão (SBCs).

Em Exchange 2007 e Exchange 2010, houve um parâmetro de status que pode ser usado para controlar o status operacional de um servidor de Unificação de mensagens. Exchange 2013, nenhum parâmetro status está disponível para essa finalidade no cmdlet **Set-UMCallRouterSettings** em um servidor de acesso para cliente.


> [!IMPORTANT]
> Não é necessário que os servidores de Acesso para Cliente e de Caixa de Correio sejam adicionados a um plano de discagem de UM antes de poderem processar chamadas para a Unificação de Mensagens, exceto quando você estiver integrando a UM e o Microsoft Office Communications 2007 R2 ou Microsoft Lync Server. Por padrão, todos os servidores de Acesso para Cliente e de Caixa de Correio em uma organização estão disponíveis para atender chamadas de entrada.



Para tarefas de gerenciamento adicionais relacionadas a servidores acesso para cliente, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configuração do servidor Exchange", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se o servidor de Acesso para Cliente está instalado no mesmo computador que o servidor de Caixa de Correio ou em um computador separado.

  - Se você estiver colocando um servidor de acesso para cliente no modo de manutenção, verifique se há capacidade suficiente íntegra na matriz de acesso para cliente para permitir que o servidor Ir fora de serviço.

  - Antes de retirar um servidor do Modo de Manutenção, verifique a integridade do servidor e certifique-se de que está pronto para o serviço.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para permitir ou impedir que um servidor de acesso para cliente de atendimento de chamadas

Este exemplo habilita um servidor de acesso para cliente `UMCallRouter-05x.contoso.com` para atendimento de voz de entrada, fax, atendedor automático e Outlook Voice Access chama a partir de gateways VoIP, IP PBXs, SBCs e PBXs habilitados para SIP e grava as alterações no registro no UMCallRouter-05 x server.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

Este exemplo impede que um servidor de acesso para cliente `UMCallRouter-05x.contoso.com` de atendimento de voz de entrada, fax, atendedor automático e Outlook Voice Access chamadas de gateways VoIP, IP PBXs, SBCs e PBXs habilitados para SIP e grava as alterações para o Active Directory.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

