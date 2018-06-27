---
title: 'Criar uma política de endereço de email usando filtros de destinatários: Exchange 2013 Help'
TOCTitle: Criar uma política de endereço de email usando filtros de destinatários
ms:assetid: e3f446bd-1511-479c-8d87-2dfce5547c90
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232194(v=EXCHG.150)
ms:contentKeyID: 50486895
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma política de endereço de email usando filtros de destinatários

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-16_

Você pode usar o Shell para criar uma política de endereço de email usando filtros de destinatários. Para saber mais sobre as políticas de endereço de email, consulte [Políticas de endereço de email](email-address-policies-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a políticas de endereço de email, consulte [Procedimentos de diretiva de endereço de email](email-address-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para usar o parâmetro *RecipientFilter* para criar um filtro personalizado, você deve especificar uma cadeia de caracteres para o filtro. O Shell usa OPath para a sintaxe de filtragem. OPath é uma linguagem de consulta projetada para fontes de dados do objeto de consulta.
    

    > [!IMPORTANT]
    > Se você usar um filtro de destinatário para criar ou editar uma política de endereço de email, você não pode usar o Centro de administração do Exchange (EAC) para editar a política de endereço de email. Você deve usar o Shell. Para detalhadas sobre sintaxe e informações de parâmetro, consulte <A href="https://technet.microsoft.com/pt-br/library/bb124517(v=exchg.150)">Set-EmailAddressPolicy</A>.



  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de endereço de email" no tópico [Endereços de email e catálogos de endereços](email-addresses-and-address-books-exchange-2013-help.md) .

  - Antes de um domínio do endereço SMTP pode ser usado em uma política de endereço de email, você deve configurar um domínio aceito. Para obter mais informações, consulte [Domínios aceitos](accepted-domains-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para criar uma política de endereço de email usando filtros de destinatários

Para criar uma política de endereço de email usando filtros de destinatários, use a seguinte sintaxe.

    New-EmailAddressPolicy -Name <String> -RecipientFilter <String>

Este exemplo cria uma política de endereço de email que se aplica a todos os executivos e para que a parte local do endereço de email consiste em duas primeiras letras de seu nome e sobrenome, todo.

    New-EmailAddressPolicy -Name 'Execs' -EnabledEmailAddressTemplates 'SMTP:%2g%s@contoso.com' -RecipientFilter {((RecipientType -eq 'UserMailbox') -and (Title -like 'executive'))}

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-EmailAddressPolicy](https://technet.microsoft.com/pt-br/library/aa996800\(v=exchg.150\)).

