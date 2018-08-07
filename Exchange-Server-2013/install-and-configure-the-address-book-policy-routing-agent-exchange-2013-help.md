---
title: 'Instalar/configurar agente de roteamento de política de catálogo de endereços'
TOCTitle: Instalar e configurar o agente de roteamento de política de catálogo de endereços
ms:assetid: 20e8a43d-4508-4388-a2c9-aa3073593cc2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ907308(v=EXCHG.150)
ms:contentKeyID: 51407846
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instalar e configurar o agente de roteamento de política de catálogo de endereços

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-01-09_

O agente Roteamento da Política de Catálogo de Endereços (ABP) é um agente de Transporte que executa no servidor de Caixa de Correio e controla como os destinatários são resolvidos em sua organização. Quando o agente de Roteamento ABP é instalado e configurado, os usuários atribuídos a GALs diferentes aparecem como destinatários externos e não podem exibir os cartões de contato dos destinatários externos.

Para conhecer tarefas de gerenciamento adicionais relacionadas a ABPs, consulte [Procedimentos de política de catálogo de endereços](address-book-policy-procedures-exchange-2013-help.md).

Procurando a versão do Exchange Online deste tópico? Consulte [Ativar a política de catálogo de endereços roteamento](https://technet.microsoft.com/pt-br/library/jj891095\(v=exchg.150\)).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 15 minutos.

  - Após a instalação e configuração do agente Roteamento ABP, pode demorar até 30 minutos para que os emails na organização sejam avaliados pelo agente.

  - O EAC não pode ser usado para esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Instalar o agente Roteamento ABP

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Agentes de transporte", no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

Instale o agente Roteamento ABP executando o seguinte comando. Este é o comando e a sintaxe exatos que você precisará usar.

    Install-TransportAgent -Name "ABP Routing Agent" -TransportAgentFactory "Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.AddressBookPolicyRoutingAgentFactory" -AssemblyPath $env:ExchangeInstallPath\TransportRoles\agents\AddressBookPolicyRoutingAgent\Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.dll

Você receberá um aviso de que o serviço Transporte precisa ser reiniciado para que suas alterações entrem em vigor, mas execute a Etapa 2 primeiro, para que reinicie apenas uma vez o serviço Transporte.

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Install-TransportAgent](https://technet.microsoft.com/pt-br/library/aa997998\(v=exchg.150\)).

## Etapa 2: Habilitar o agente Roteamento de Transporte

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Agentes de transporte", no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

Após a instalação do agente Roteamento ABP, é necessário habilitá-lo executando o seguinte comando:

    Enable-TransportAgent "ABP Routing Agent"

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Enable-TransportAgent](https://technet.microsoft.com/pt-br/library/bb124921\(v=exchg.150\)).

## Etapa 3: Reiniciar o serviço de Transporte e verificar se o agente Roteamento ABP está instalado e habilitado

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Agentes de transporte", no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

1.  Reinicie o serviço de Transporte executando o comando a seguir.
    
        Restart-Service MSExchangeTransport

2.  Após a reinicialização do serviço, verifique se o agente Roteamento ABP está instalado e habilitado executando o seguinte cmdlet.
    
        Get-TransportAgent
    
    Se o agente Roteamento ABP estiver listado, ele estará corretamente instalado.

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Get-TransportAgent](https://technet.microsoft.com/pt-br/library/bb123536\(v=exchg.150\)).

## Etapa 4: Habilitar o agente Roteamento ABP

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configuração de transporte", no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

A etapa final nesse processo é habilitar o roteamento ABP para a organização. Execute o seguinte comando.

    Set-TransportConfig -AddressBookPolicyRoutingEnabled $true

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Set-TransportConfig](https://technet.microsoft.com/pt-br/library/bb124151\(v=exchg.150\)).

