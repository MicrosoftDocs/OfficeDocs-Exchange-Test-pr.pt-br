---
title: 'Exibir membros de um grupo dinâmico de distribuição: Exchange 2013 Help'
TOCTitle: Exibir membros de um grupo dinâmico de distribuição
ms:assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232019(v=EXCHG.150)
ms:contentKeyID: 50484688
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir membros de um grupo dinâmico de distribuição

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2018-03-02_

Os grupos dinâmicos de distribuição são grupos de distribuição cuja associação é aceita com base em filtros específicos de destinatários em vez de um conjunto definido de destinatários. O MicrosoftExchange fornece filtros predefinidos para facilitar a criação de filtros de destinatários para grupos dinâmicos de distribuição. Um *filtro predefinido* é um filtro normalmente usado para atender a diversos critérios de filtragem de destinatários. É possível especificar os tipos de destinatários que você deseja incluir no grupo dinâmico de distribuição. Além disso, você também pode especificar uma lista de condições que os destinatários devem atender. É possível usar o Shell para visualizar a lista de destinatários de um grupo dinâmico de distribuição que usa filtros predefinidos.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos dinâmicos de distribuição" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o Shell para visualizar a lista de membros de um grupo de distribuição dinâmico

Este exemplo retorna a lista de membros para o grupo dinâmico de distribuição chamado funcionários em tempo integral. O primeiro comando armazena o objeto de grupo dinâmico de distribuição na variável `$FTE`. O segundo comando usa o cmdlet **Get-Recipient** para listar os destinatários que correspondem aos critérios definidos para o grupo dinâmico de distribuição.

    $FTE = Get-DynamicDistributionGroup "Full Time Employees"

    Get-Recipient -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer

Para a sintaxe detalhada e informações sobre o parâmetro, consulte [Get-DynamicDistributionGroup](https://technet.microsoft.com/pt-br/library/bb124762\(v=exchg.150\)) e [Get-Recipient](https://technet.microsoft.com/pt-br/library/aa996921\(v=exchg.150\)).


> [!TIP]
> Você não pode exibir membros de um grupo dinâmico de distribuição usando o EAC.



## Como saber se funcionou?

Para verificar se você tiver exibido com êxito os membros de um grupo dinâmico de distribuição, faça o seguinte:

  - No Shell, uma lista de membros é retornada após você executar o comando anterior, para exibir uma lista de membros do grupo dinâmico de distribuição. Por exemplo, se você tiver criado uma caixa de correio para um novo usuário com propriedades que correspondam ao filtro do destinatário do grupo dinâmico de distribuição, esse novo usuário deverá ser exibido na lista de membros do grupo.

