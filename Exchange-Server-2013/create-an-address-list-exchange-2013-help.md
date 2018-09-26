---
title: 'Criar uma lista de endereços: Exchange 2013 Help'
TOCTitle: Criar uma lista de endereços
ms:assetid: e86ba1b7-c41c-4050-bc29-13996cf53c59
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125036(v=EXCHG.150)
ms:contentKeyID: 50486918
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewAddressListWizardForm.AddressListIntroductionPage
ms.translationtype: MT
---

# Criar uma lista de endereços

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-12_

Listas de endereços são uma coleção de destinatário e outros objetos do Active Directory. Cada lista de endereços pode conter um ou mais tipos de objetos (por exemplo, usuários, contatos, grupos, pastas públicas, conferência e outros recursos). Listas de endereços também fornecem um mecanismo para particionar objetos habilitados para email no Active Directory em benefício dos grupos de usuários específicos.

Para outras tarefas de gerenciamento relacionadas às listas de endereços, consulte [Procedimentos da lista de endereços](address-list-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Listas de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para criar uma lista de endereços

1.  Navegue até **organização** \> **listas de endereços** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na **Lista de endereços**, digite um nome e especifique os tipos de destinatários para incluir na lista.

3.  Por padrão, o Exchange cria listas de endereços que contém todos os membros da sua organização. Para criar uma lista exclusiva de endereço personalizado, clique em **Adicionar uma regra**.
    

    > [!IMPORTANT]
    > Se você não adicionar uma regra, você criará uma lista de endereços que é redundante com uma das listas de endereços padrão.



4.  Na lista, selecione uma opção de filtragem (por exemplo, **o atributo personalizado 1** ).

5.  Em **Especificar palavras ou frases**, digite palavras ou frases para filtrar por, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")e, em seguida, clique em **Okey**.
    
    Você pode continuar adicionar várias palavras ou frases, repetindo a etapa 4. O filtro é uma instrução booleano **ou**. Por exemplo, você pode criar um filtro que se aplicam a lista de endereços para os usuários cujo atributo personalizado 1 é igual a **Idaho**, **Oregon** ou **Washington**.

6.  (Opcional) Clique em **Adicionar uma regra** novamente para adicionar filtros adicionais. Filtros adicionais criar uma instrução Boolean **e**. Quanto mais filtros você adicionar, o número de menos de usuários se aplica a lista de endereços.

7.  Clique em **Visualizar inclui as listas de endereços de destinatários** para ver os destinatários que esta lista de endereços será a ser aplicado ao.

8.  Clique em **Salvar**.

9.  Você receberá um aviso de que a lista de endereços não será aplicada até que você atualizá-lo. Dependendo do tamanho da organização e os filtros que você adicionou à lista de endereços, algumas listas de endereços podem conter milhares ou dezenas de milhares de destinatários. Atualizar as listas de endereços pode afetar o seus recursos, talvez você queira atualizar o endereço de horário de pico.
    
    Para obter detalhes sobre como atualizar uma lista de endereços, consulte [Atualizar uma lista de endereços](update-an-address-list-exchange-2013-help.md).

## Use o Shell para criar uma lista de endereços

Este exemplo cria a lista de endereços MyAddressList usando o parâmetro *RecipientFilter* e inclui destinatários que são os usuários de caixa de correio e tem `StateOrProvince` definida como `Washington` ou `Oregon`.

```powershell
New-AddressList -Name MyAddressList -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}
```

Este exemplo cria a lista de endereços filhas as salas de reunião do edifício 34 no contêiner todas as salas pai, usando as condições internas.

```powershell
New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-AddressList](https://technet.microsoft.com/pt-br/library/aa996912\(v=exchg.150\)).

