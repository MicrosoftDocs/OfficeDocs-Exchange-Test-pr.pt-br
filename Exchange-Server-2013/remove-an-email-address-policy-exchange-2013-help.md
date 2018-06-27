---
title: 'Remover uma política de endereço de email: Exchange 2013 Help'
TOCTitle: Remover uma política de endereço de email
ms:assetid: f1d05223-7d41-406d-8fae-f4227be1c1c2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125181(v=EXCHG.150)
ms:contentKeyID: 50486981
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma política de endereço de email

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-13_

Por padrão, Exchange contém uma política de endereço de email que especifica o alias do destinatário como parte local do endereço de email e usa o domínio aceito padrão. A parte local de um endereço de email é o nome que aparece antes do sinal "no" (@). Esta diretiva de endereço de email se aplica a todos os usuários na organização. Não é possível remover esta diretiva de endereço de email.

Para tarefas de gerenciamento adicionais relacionadas a diretivas de endereço de email, consulte [Procedimentos de diretiva de endereço de email](email-address-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Se você remover uma política de endereço de email que é usada pelos destinatários como a principal política e outras diretivas não tiverem sido configuradas para destinatários, a política padrão será usada.

  - Você não pode excluir a política padrão. Se você deseja excluir a política padrão, você deve primeiro atribuir uma política diferente como padrão.

  - Se a diretiva de endereço de email que você estiver excluindo contiver mais de 3.000 destinatários, você deve usar o Shell para executar esse procedimento.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de endereço de email" no tópico [Endereços de email e catálogos de endereços](email-addresses-and-address-books-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para remover uma política de endereço de email

1.  Navegue até **fluxo de emails** \> **políticas de endereço de Email**.

2.  Na exibição de lista, selecione a política de endereço de email que você deseja excluir e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

3.  No aviso, clique em **Sim** para remover a diretiva.

## Use o Shell para remover uma política de endereço de email

Este exemplo remove a diretiva de endereço de email South East Offices.

    Remove-EmailAddressPolicy -Identity "South East Offices"

Digite **Y** para confirmar que você deseja remover a diretiva e pressione ENTER.

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Remove-EmailAddressPolicy](https://technet.microsoft.com/pt-br/library/bb124504\(v=exchg.150\)).

