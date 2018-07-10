---
title: 'Remover uma regra de proteção do Outlook: Exchange 2013 Help'
TOCTitle: Remover uma regra de proteção do Outlook
ms:assetid: 569fc3be-b269-43f5-8797-73ab0691e685
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633467(v=EXCHG.150)
ms:contentKeyID: 50485628
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma regra de proteção do Outlook

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Usando regras de proteção do Microsoft Outlook, você pode proteger mensagens com o gerenciamento de direitos de informação (IRM) aplicando um modelo do [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) no Outlook 2010 antes que as mensagens são enviadas. Para impedir que uma regra de proteção de Outlook está sendo aplicada, é possível desabilitar a regra. Remover uma regra de proteção de Outlook remove Active Directory a definição da regra.

Para tarefas de gerenciamento adicionais relacionadas a IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Proteção por direitos" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - O EAC (Centro de Administração do Exchange) não pode ser usado para remover regras de proteção do Outlook. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para remover uma regra de proteção do Outlook

Este exemplo remove a regra de proteção do Outlook OPR-DG-Finance.

    Remove-OutlookProtectionRule -Identity "OPR-DG-Finance"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Remove-OutlookProtectionRule](https://technet.microsoft.com/pt-br/library/dd297961\(v=exchg.150\)).

## Usar o Shell para remover todas as regras de proteção do Outlook

Este exemplo remova todas as regras de proteção do Outlook na organização do Exchange.

    Get-OutlookProtectionRule | Remove-OutlookProtectionRule

Para obter a sintaxe detalhada e informações sobre o parâmetro, consulte [Get-OutlookProtectionRule](https://technet.microsoft.com/pt-br/library/dd298004\(v=exchg.150\)) e [Remove-OutlookProtectionRule](https://technet.microsoft.com/pt-br/library/dd297961\(v=exchg.150\)).

## Como saber se funcionou?

Para confirmar se você removeu com êxito uma regra de proteção do Outlook, use o cmdlet [Get-OutlookProtectionRule](https://technet.microsoft.com/pt-br/library/dd298004\(v=exchg.150\)) para recuperar as regras de proteção do Outlook. Para obter um exemplo de como recuperar as regras de proteção do Outlook, consulte [Examples](https://technet.microsoft.com/pt-br/dd298004\(exchg.150\)#examples) em **Get-OutlookProtectionRule**.

