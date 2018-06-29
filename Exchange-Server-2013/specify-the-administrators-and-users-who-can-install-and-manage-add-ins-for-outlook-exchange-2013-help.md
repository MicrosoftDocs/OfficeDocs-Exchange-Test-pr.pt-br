---
title: 'Especificar os administradores e usuários que podem instalar e gerenciar suplementos do Outlook: Exchange 2013 Help'
TOCTitle: Especificar os administradores e usuários que podem instalar e gerenciar suplementos do Outlook
ms:assetid: 7ee4302d-b8bb-40a0-9810-10d3a0271bcb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ943754(v=EXCHG.150)
ms:contentKeyID: 52058834
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Especificar os administradores e usuários que podem instalar e gerenciar suplementos do Outlook

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2017-02-08_

Você pode especificar que os administradores em sua organização tem permissões para instalar e gerenciar suplementos do Outlook. Você também pode especificar quais usuários em sua organização têm permissão para instalar e gerenciar suplementos para seu próprio uso.

Isso é feito como atribuir ou remover funções de gerenciamento específicas de suplementos. Há cinco funções internas que você pode usar.

Funções administrativas

  - **Aplicativos do Marketplace org**   Habilita um administrador, instalar e gerenciar suplementos que estão disponíveis no Office Store para sua organização.

  - **Aplicativos personalizados org**   Permite que um administrador instalar e gerenciar suplementos personalizados para sua organização.

Funções de usuário

  - **Meus aplicativos do Marketplace**   Permite que um usuário instalar e gerenciar suplementos do Office Store para seu próprio uso.

  - **Meus aplicativos personalizados**   Permite que um usuário instalar e gerenciar suplementos personalizados para seu próprio uso.

  - **Meus aplicativos ReadWriteMailbox**   Permite que um usuário instalar e gerenciar suplementos que solicitar o nível de permissão ReadWriteMailbox no seu manifesto.

Por padrão, todos os administradores que têm o grupo de funções de **Gerenciamento da organização** têm ambas as funções administrativas acima habilitadas. Também por padrão, os usuários finais têm funções de usuário acima habilitadas.

Para obter informações sobre cada uma dessas funções, consulte [Função de aplicativos do Marketplace org](org-marketplace-apps-role-exchange-2013-help.md), [Função org personalizado Apps](org-custom-apps-role-exchange-2013-help.md), [Minha função de aplicativos do Marketplace](my-marketplace-apps-role-exchange-2013-help.md), [Minha função personalizada Apps](my-custom-apps-role-exchange-2013-help.md)e [Minha função ReadWriteMailbox Apps](my-readwritemailbox-apps-role-exchange-2013-help.md).

Para obter informações sobre suplementos, consulte [Aplicativos para Outlook](add-ins-for-outlook-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar esse cmdlet, você precisa ter permissões. Embora todos os parâmetros para este cmdlet estejam listados neste tópico, talvez você não tenha acesso a alguns parâmetros, caso eles não estejam incluídos nas permissões atribuídas a você. Para ver de que permissões você precisa, consulte o Entrada "Atribuições de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

  - Acesso ao armazenamento do Office não é compatível com caixas de correio ou organizações em regiões específicas. Se você não vir **Adicionar da Office Store** como uma opção no **Centro de administração do Exchange** em **organização** \> **suplementos** \> ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), você poderá instalar um suplemento para Outlook a partir de um local de arquivo ou URL. Para obter mais informações, contate o provedor de serviço.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Atribuir administradores as permissões necessárias para instalar e gerenciar suplementos para sua organização

## Usar o EAC para atribuir permissões a administradores

Você pode usar o EAC para atribuir administradores as permissões necessárias para instalar e gerenciar suplementos disponíveis ou da Office Store para sua organização. Para obter informações detalhadas sobre como fazer isso, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

## Atribuir as permissões necessárias para instalar e gerenciar suplementos para seu próprio uso de usuários

## Usar o EAC para atribuir permissões aos usuários

Você pode usar o EAC para atribuir aos usuários as permissões necessárias para visualizar e modificar suplementos personalizados para seu próprio uso. Para obter informações detalhadas sobre como fazer isso, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

## Como saber se funcionou?

Para verificar que você atribuiu permissões para um usuário com êxito, execute um comando do Shell usando o formato `Get-ManagementRoleAssignment -Role <Role Name> -GetEffectiveUsers`, onde `Role Name` é a função para a qual você deseja verificar permissões atribuídas.

Este exemplo mostra como verificar a quem você atribuiu permissões para instalar suplementos da Office Store para a organização.

1.  Execute `Get-ManagementRoleAssignment -Role "Org Marketplace Apps" -GetEffectiveUsers`.

2.  Nos resultados, analise as entradas na coluna **Efetivo de usuários**.

Para obter mais informações sobre sintaxe e parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

