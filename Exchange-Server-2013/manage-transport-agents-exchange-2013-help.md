---
title: 'Gerenciar agentes de transporte: Exchange 2013 Help'
TOCTitle: Gerenciar agentes de transporte
ms:assetid: f15ab7e4-015d-45b1-9c10-f733d7cd2a36
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125175(v=EXCHG.150)
ms:contentKeyID: 50486975
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar agentes de transporte

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-08_

Agentes de transporte utilize os eventos de SMTP para operar em mensagens à medida que as mensagens move através do pipeline de transporte. A maioria dos agentes de transporte interno que estão incluídos no Microsoft Exchange Server 2013 são invisíveis e difíceis de gerenciar. No entanto, você pode instalar e configurar os agentes de transporte de terceiros em servidores do Exchange em sua organização. Para obter mais informações sobre agentes de transporte, consulte [Agentes de transporte](transport-agents-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Agentes de transporte" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - Você só pode usar o Shell para executar esse procedimento.

  - Suporte para agentes de transporte herdado não está habilitado por padrão, mas você pode ativá-lo. Para obter instruções, consulte [Habilitar o suporte para agentes de transporte de legado](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Sobre os procedimentos de agente de transporte no serviço Front End Transport em servidores de acesso para cliente

Você não pode usar o Shell de gerenciamento do Exchange para gerenciar o agente de transporte no serviço Front End Transport em um servidor de acesso para cliente. Em vez disso, você precisará abrir o Windows PowerShell no servidor de acesso para cliente e, em seguida, importe os cmdlets do Exchange para a sessão do Windows PowerShell.


> [!WARNING]
> Cmdlets do Exchange em execução no Windows PowerShell para tarefas que não seja o gerenciamento de agentes de transporte no serviço Front End Transport não é suportado. Há sérias conseqüências que podem resultar se ignorar o Shell de gerenciamento do Exchange e controle de acesso baseado em função (RBAC) executando os cmdlets do Exchange no Windows PowerShell. Você sempre deve executar os cmdlets do Exchange no Shell de gerenciamento do Exchange. Para obter mais informações, consulte <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de versão do Exchange 2013</A>.



Para executar qualquer um dos procedimentos de agente de transporte descritos neste tópico no serviço Front End Transport, você precisa executar as seguintes etapas adicionais:

1.  No servidor de acesso para cliente, abra o Windows PowerShell e execute o seguinte comando:
    
        Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn

2.  Execute o comando conforme descrito, mas, adicione o seguinte valor ao comando: `-TransportService FrontEnd`.
    
    Por exemplo, para exibir os agentes de transporte no serviço Front End Transport em um servidor de acesso para cliente, execute o seguinte comando:
    
        Get-TransportAgent -TransportService FrontEnd

## Use o Shell para instalar um agente de transporte

Quando você instala um agente de transporte, o Exchange registra apenas DLLs associadas o agente de transporte. Você precisará certificar-se de que todos os arquivos, chaves do registro e outros objetos que depende do agente de transporte instalados corretamente e configurados. Depois que o Exchange carrega as DLLs, ele continua fazer referência as DLLs após a conclusão do comando.

Agentes de transporte têm acesso total a todas as mensagens de email que eles encontrem. Exchange coloca sem restrições no comportamento de um agente de transporte. Agentes de transporte que estão instáveis ou contêm falhas de segurança podem afetar a estabilidade e a segurança do Exchange. Portanto, você deve instalar somente os agentes de transporte que você confia totalmente e que foram testados totalmente em um ambiente de teste.

Agentes de transporte são instalados em um estado desabilitado para certificar-se de que o fluxo de email não é afetado por agentes de transporte que ainda não tenham sido configurados. Portanto, depois que um agente de transporte foi configurado corretamente, você precisa habilitar o agente de transporte.

Use a sintaxe a seguir para instalar um agente de transporte.

    Install-TransportAgent -Name <TransportAgentIdentity> -TransportAgentFactory <"TransportAgentFactory"> -AssemblyPath <"FilePath">

Este exemplo instala um agente de transporte fictício chamado Contoso agente de transporte no serviço de transporte em um servidor de caixa de correio.

    Install-TransportAgent -Name "Contoso Transport Agent" -TransportAgentFactory "vendor.exchange.ContosoTransportAgentfactory" -AssemblyPath "C:\Program Files\Vendor\TransportAgent\ContosoTransportAgentFactory.dll"

## Como saber se funcionou?

Para verificar que você instalou o agente de transporte com êxito, execute o comando `Get-TransportAgent` e verifique se que o agente de transporte está listado.

## Use o Shell para habilitar um agente de transporte

Use a sintaxe a seguir para habilitar um agente de transporte.

    Enable-TransportAgent <TransportAgentIdentity>

Este exemplo habilita o agente de transporte chamado Contoso agente de transporte no serviço de transporte em um servidor de caixa de correio.

    Enable-TransportAgent "Contoso Transport Agent"

## Como saber se funcionou?

Para verificar se você habilitou com êxito um agente de transporte, execute o comando `Get-TransportAgent | Format-List Name,Enabled` e verifique se que o agente de transporte está habilitado.

## Use o Shell para desabilitar um agente de transporte

Use a seguinte sintaxe para desabilitar um agente de transporte:

    Disable-TransportAgent <TransportAgentIdentity>

Este exemplo desativa o agente de transporte chamado Fabrikam agente de transporte no serviço de transporte em um servidor de caixa de correio.

    Disable-TransportAgent "Fabrikam Transport Agent"

## Como saber se funcionou?

Para verificar se você desabilitou com êxito um agente de transporte, execute o comando `Get-TransportAgent | Format-List Name,Enabled` e verifique se que o agente de transporte está desabilitado.

## Use o Shell para exibir os agentes de transporte

Para exibir uma lista resumida de agentes de transporte, execute o seguinte comando:

    Get-TransportAgent

Para exibir a configuração detalhada de um agente de transporte específica, execute o seguinte comando:

    Get-TransportAgent <TransportAgentIdentity> | Format-List

Este exemplo fornece uma configuração detalhada do agente de transporte chamado agente de regras de transporte.

    Get-TransportAgent "Transport Rule Agent" | Format-List

## Use o Shell para configurar a prioridade de um agente de transporte

Agentes com uma prioridade mais próximo ao 0 mensagens de email do processo de transporte pela primeira vez. No entanto, o evento SMTP no pipeline de transporte em que o agente de transporte está registrado pode causar um agente de prioridade mais baixo agir na mensagem antes de um agente de prioridade mais alta.

Para modificar a prioridade de um agente de transporte existentes, execute o seguinte comando:

    Set-TransportAgent <TransportAgentIdentity> -Priority <Integer>

Este exemplo define o valor da prioridade do agente de 3 para o agente de transporte existente chamado Contoso agente de transporte no serviço de transporte em um servidor de caixa de correio.

    Set-TransportAgent "Contoso Transport Agent" -Priority 3

## Como saber se funcionou?

Para verificar se você configurou com êxito a prioridade de um agente de transporte, execute o comando `Get-TransportAgent | Format-List Name,Priority` e verifique se o valor da prioridade do agente de transporte.

## Use o Shell para desinstalar um agente de transporte

Quando o agente de transporte é desinstalado, Exchange cancela o registro os arquivos DLL usados com o agente. Exchange não remove quaisquer arquivos, chaves do registro ou outros objetos adicionados pela instalação do agente de transporte.

Para desinstalar um agente de transporte, execute o seguinte comando:

    Uninstall-TransportAgent <TransportAgentIdentity>

Este exemplo desinstala o agente de transporte chamado Fabrikam agente de transporte do serviço de transporte em um servidor de caixa de correio.

    Uninstall-TransportAgent "Fabrikam Transport Agent"

## Como saber se funcionou?

Para verificar se você tiver desinstalado o o agente de transporte com êxito, execute o comando `Get-TransportAgent` e verifique se que o agente de transporte não está listado.

