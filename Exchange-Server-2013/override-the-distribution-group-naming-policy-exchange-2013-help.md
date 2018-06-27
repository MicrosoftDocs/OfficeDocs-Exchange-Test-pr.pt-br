---
title: 'Substituir o diretiva de nomenclatura de grupo de distribuição: Exchange 2013 Help'
TOCTitle: Substituir o diretiva de nomenclatura de grupo de distribuição
ms:assetid: 9eb23fc9-3f59-4d09-9077-85c89a051ee0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ218685(v=EXCHG.150)
ms:contentKeyID: 50484767
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Substituir o diretiva de nomenclatura de grupo de distribuição

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2012-10-13_

O grupo de diretiva de nomenclatura para grupos de distribuição é aplicado somente aos grupos criados por usuários. Quando você ou outros administradores de usarem o Centro de administração do Exchange (EAC) para criar grupos de distribuição, o diretiva de nomenclatura de grupo é ignorado e não é aplicado ao nome do grupo.

No entanto, se você usar o Shell de gerenciamento do Exchange para criar ou renomear um grupo de distribuição, o diretiva de nomenclatura de grupo é aplicado aos grupos criados por administradores, a menos que você use o parâmetro *IgnoreNamingPolicy* para substituir o diretiva de nomenclatura de grupo.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de distribuição" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o Shell para substituir o grupo de diretiva de nomenclatura quando você cria um novo grupo

Para substituir o diretiva de nomenclatura de grupo, execute o seguinte comando.

    New-DistributionGroup -Name <Group Name> -IgnoreNamingPolicy

Por exemplo, se o grupo de diretiva de nomenclatura para sua organização for **DG\_ \< nome do grupo \> \_Users**, execute o seguinte comando para criar um grupo chamado **Todos os administradores**.

    New-DistributionGroup -Name "All Administrators" -IgnoreNamingPolicy

Quando o Microsoft Exchange cria esse grupo, ele usa **Todos os administradores** para os parâmetros de *Name* e *DisplayName* .

## Use o Shell para substituir o grupo de diretiva de nomenclatura quando você renomeia um grupo

Para substituir o grupo de diretiva de nomenclatura quando você renomeia um grupo existente com o Shell, execute o seguinte comando.

    Set-DistributionGroup -Identity <Old Group Name> -Name <New Group Name> -DisplayName <New Group Name> -IgnoreNamingPolicy

Por exemplo, digamos que você criou um grupo de diretiva de nomenclatura uma noite e da manhã concretizados que você digitou incorretamente a cadeia de caracteres de texto no prefixo. Da manhã, você verá que um novo grupo já foi criado com o prefixo incorreta. Você pode corrigir o política no EAC de nomenclatura de grupo, mas você precisará usar o Shell para renomear o grupo com o nome incorreta. Execute o seguinte comando.

    Set-DistributionGroup -Identity "Goverment_Contracts_NWRegion" -Name "Government_ContractEstimates_NWRegion" -DisplayName "Government_ContractEstimates_NWRegion" -IgnoreNamingPolicy


> [!IMPORTANT]
> Certifique-se de incluir o parâmetro <EM>DisplayName</EM> quando você renomeia um grupo. Se não fizer isso, o nome antigo ainda é exibido no catálogo de endereços compartilhado para:, Cc: e a partir: linhas em mensagens de email.



## Como saber se funcionou?

Para verificar que você tiver criado com êxito ou renomeado um grupo de distribuição que ignora o diretiva de nomenclatura de grupo, execute os seguintes comandos.

    Get-DistributionGroup <Name> | FL DisplayName

    Get-OrganizationConfig | FL DistributionGroupNamingPolicy

Se o formato do nome para exibição para o grupo for diferente daquela imposto pela diretiva de nomenclatura de grupo da sua organização, ele funcionou.

