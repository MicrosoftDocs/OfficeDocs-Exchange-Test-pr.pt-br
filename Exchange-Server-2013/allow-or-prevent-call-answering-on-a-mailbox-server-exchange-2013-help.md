---
title: 'Permitir ou impedir atendimento de chamadas em um servidor de Caixa de Correio'
TOCTitle: Permitir ou impedir que um servidor de caixa de correio de atendimento de chamadas
ms:assetid: 4b860c09-6669-4e3d-b3dc-17b8018b3860
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997908(v=EXCHG.150)
ms:contentKeyID: 50556181
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir ou impedir que um servidor de caixa de correio de atendimento de chamadas

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-18_

Você pode permitir que o serviço de Unificação de Mensagens do Microsoft Exchange em um servidor de Caixa de Correio atenda a novas chamadas ou evitar que isso aconteça. Por padrão, o servidor de Caixa de Correio está no estado habilitado após ser instalado. Quando estiver configurando o servidor de Caixa de Correio para aceitar chamadas de voz de entrada, fax, chamadas do atendedor automático e do Outlook Voice Access, use o cmdlet **Set-ServerComponentState**.

A configuração do Modo de Manutenção para um servidor de Caixa de Correio permite que você coloque o servidor fora de serviço. Para um servidor de Caixa de Correio, fora de serviço significa que o servidor não hospedará nenhum banco de dados ativo, todas as filas de transporte estão vazias e o servidor não aceitará nenhuma chamada de entrada de servidores de Acesso para Cliente, gateways VoIP, PBXs IP, PBXs habilitados para SIP ou controladores de borda de sessão (SBCs).

No Exchange 2007 e no Exchange 2010, há um parâmetro de status que pode ser usado para controlar o status operacional de um servidor de Unificação de Mensagens. No Exchange 2013, nenhum parâmetro de status está disponível para essa finalidade no cmdlet **Set-UMService** para um servidor de Caixa de Correio.


> [!IMPORTANT]
> Não é necessário que os servidores de Acesso para Cliente e de Caixa de Correio sejam adicionados a um plano de discagem de UM antes de poderem processar chamadas para a Unificação de Mensagens, exceto quando você estiver integrando a UM e o Microsoft Office Communications 2007 R2 ou Microsoft Lync Server. Por padrão, todos os servidores de Acesso para Cliente e de Caixa de Correio em uma organização estão disponíveis para atender chamadas de entrada.



Para conhecer tarefas de gerenciamento adicionais relacionadas a servidores de Caixa de Correio, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configuração do servidor Exchange", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se o servidor de Caixa de Correio está instalado no mesmo computador que um servidor de Acesso para Cliente ou em um computador separado.

  - Se estiver colocando um servidor de Caixa de Correio no Modo de Manutenção, verifique se há redundância suficiente de todas as cópias de bancos de dados para permitir que o servidor fique fora de serviço.

  - Antes de retirar um servidor do Modo de Manutenção, verifique a integridade do servidor e certifique-se de que está pronto para o serviço.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para permitir ou impedir o atendimento de chamadas em um servidor de Caixa de Correio

Este exemplo permite que um servidor de Caixa de Correio `UMMBXr-05x.contoso.com` atenda sua chamada de voz, fax, chamadas de atendedor automático e do Outlook Voice Access a partir de gateways VoIP, PBXs IP, PBXs habilitados para SIP e SBCs, além de gravar a alteração no registro no servidor UMMBX-05x .

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

Este exemplo evita que um servidor de Caixa de Correio `UMMBX-05x.contoso.com` atenda sua chamada de voz, fax, chamadas de atendedor automático e do Outlook Voice Access a partir de gateways VoIP, PBXs IP, PBXs habilitados para SIP e SBCs, além de gravar a alteração apenas no Active Directory.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

