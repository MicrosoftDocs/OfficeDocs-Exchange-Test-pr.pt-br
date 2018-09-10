---
title: 'Configurar a UM para funcionar com o Lync Server: Exchange 2013 Help'
TOCTitle: Configurar a Unificação de mensagens para funcionar com o Lync Server
ms:assetid: 29bdddbf-75d5-4c92-988e-c8506ecc7a1c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ966276(v=EXCHG.150)
ms:contentKeyID: 52058805
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a Unificação de mensagens para funcionar com o Lync Server

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-06-11_

Ao integrar o Microsoft Lync Server com a Unificação de Mensagens do Exchange (UM), você deve executar o script ExchUcUtil.ps1 no Shell. O script ExchUcUtil.ps1 faz o seguinte:

  - Cria um gateway IP de UM para cada pool do Lync Server.
    

    > [!IMPORTANT]
    > O script ExchUcUtil.ps1 cria um ou mais gateways IP de UM. Você deve desativar as chamadas de saída em todos os gateways IP de UM com exceção o gateway criado pelo script. Isto inclui a desativação de chamadas de saída em gateways IP de UM que foram criados antes de você executar o script. Para desativar as chamadas de saída em um gateway IP de UM, consulte <A href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/disable-outgoing-calls-on-um-ip-gateways">Desabilitar as chamadas de saída nos gateways IP de UM</A>.



  - Crie um grupo de busca de UM para cada gateway IP de UM. O identificador piloto de cada grupo de busca especifica o plano de discagem URI do SIP de UM usado pelo servidor Standard Edition ou pool do Lync Server Front End associado com o gateway IP de UM.

  - Concede permissão ao Lync Server para leitura dos objetos do contêiner de UM do Active Directory tais como planos de discagem de UM, atendentes automáticos, gateways IP de UM e grupos de busca de UM.


> [!IMPORTANT]
> Cada floresta de UM deve ser configurada para confiar na floresta na qual o Lync Server 2013 é implantado e a floresta na qual o Lync Server 2013 é implantado deve ser configurada para confiar em cada floresta de UM. Se a UM do Exchange for instalada em várias florestas, as etapas de integração do Exchange Server devem ser realizadas para cada floresta de UM ou você deverá especificar o domínio do Lync Server. Por exemplo, <EM>ExchUcUtil.ps1 –Forest:&lt;lync-domain-controller-fqdn&gt;</EM>.



Para mais tarefas de gerenciamento relacionadas à integração do Lync Server e da Unificação de Mensagens, consulte [Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalização: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada sobre "Cmdlets de Permissões\&quot; no tópico [Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\)).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o Shell para executar o script ExchUcUtil.ps1

Execute o script ExchUcUtil.ps1 em qualquer servidor Exchange na sua organização que esteja na mesma topologia que o Microsoft Lync Server. Você pode executar o script a partir de um servidor de Caixa de Correio usando o Shell ou você pode executar o script usando o Windows PowerShell Remoto em um servidor de Acesso do Cliente. Se você executar o script em um servidor de Acesso do Cliente na sua organização, o servidor de Acesso do Cliente irá usar um proxy da sessão do Windows PowerShell Remoto para um servidor de Caixa de Correio na organização.


> [!IMPORTANT]
> O script ExchUcUtil.ps1 cria um ou mais gateways IP de UM. Você deve desativar as chamadas de saída em todos os gateways IP de UM com exceção o gateway criado pelo script. Isto inclui a desativação de chamadas de saída em gateways IP de UM que foram criados antes de você executar o script. Para desativar as chamadas de saída em um gateway IP de UM, consulte <A href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/disable-outgoing-calls-on-um-ip-gateways">Desabilitar as chamadas de saída nos gateways IP de UM</A>.




> [!IMPORTANT]
> Você deve possuir as permissões da função de Gerenciamento da Organização do Exchange ou ser um membro do grupo de segurança dos Administradores da Organização do Exchange para executar o script.



1.  Abra o Shell de Gerenciamento do Exchange Management Shell.

2.  No prompt do `C:\Windows\System32`, digite **cd \&quot;\<letra do drive\>\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts\>.ExchUcUtil.ps1\&quot;**, e depois aperte Enter.

## Como saber se funcionou?

Para verificar se o script ExchUcUtul.ps1 foi finalizado com sucesso, faça o seguinte:

  - Use o cmdlet **Get-UMIPGateway** ou o EAC para exibir o gateway de IP de UM ou os gateways que foram criados.

  - Use o cmdlet **Get-UMHuntGroup** ou o EAC para exibir o novo grupo ou os novos grupos de busca de UM que foram criados.

