---
title: 'Remover uma política de catálogo de endereços: Exchange 2013 Help'
TOCTitle: Remover uma política de catálogo de endereços
ms:assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh529946(v=EXCHG.150)
ms:contentKeyID: 50486556
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma política de catálogo de endereços

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2014-03-25_

Use este procedimento para remover uma política de catálogo de endereços (ABP).

Para verificar tarefas de gerenciamento adicionais relacionadas a ABPs, consulte [Procedimentos de política de catálogo de endereços](address-book-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de catálogos de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Não é possível remover a ABP se ela ainda estiver atribuída à caixa de correio de um usuário ou à caixa de correio excluída por software. Para determinar se uma ABP está atribuída a um usuário, execute o comando a seguir no Shell:
    
    `Get-Mailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`
    
    Para determinar se uma ABP está atribuída a uma caixa de correio excluída por software, execute o comando a seguir:
    
    `Get-Mailbox -SoftDeletedMailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`

  - Para remover uma ABP de uma caixa de correio de usuário, você pode utilizar a página **Recursos de Caixa de Correio** das propriedade de caixa de correio ou o cmdlet **Set-Mailbox**.

  - Você não pode usar o Centro de Administração do Exchange (EAC) para remover um ABP. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para remover uma ABP

Este exemplo remove a ABP ABP\_TailspinToys.

    Remove-AddressBookPolicy -Identity "ABP_TailspinToys"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Remove-AddressBookPolicy](https://technet.microsoft.com/pt-br/library/hh529929\(v=exchg.150\)).

