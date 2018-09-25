---
title: 'Editar uma política de endereço de email: Exchange 2013 Help'
TOCTitle: Editar uma política de endereço de email
ms:assetid: cc8b36a0-95f4-43e9-bc64-87646d2e14e4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124580(v=EXCHG.150)
ms:contentKeyID: 50486666
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.EditEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# Editar uma política de endereço de email

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-12-10_

Políticas de endereço de email geram os endereços de email primários e secundários para seus destinatários (que incluem usuários, contatos e grupos) para que possam receber e enviar email.

Para tarefas de gerenciamento adicionais relacionadas a políticas de endereço de email, consulte [Procedimentos de diretiva de endereço de email](email-address-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Você não pode usar o Centro de administração do Exchange (EAC) para editar uma política de endereço de email se a política foi criada usando o Shell.

  - Se a diretiva de endereço de email foi criada usando um filtro de destinatário, você deve usar o Shell para editar a política de endereço de email. Para obter mais informações, consulte [Criar uma política de endereço de email usando filtros de destinatários](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md).

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de endereço de email" no tópico [Endereços de email e catálogos de endereços](email-addresses-and-address-books-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]  
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para alterar os destinatários aos quais a política se aplica

1.  Navegue até **fluxo de emails** \> **políticas de endereço de Email**.

2.  Na exibição de lista, selecione a política de endereço de email que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na **Diretiva de endereço de Email**, clique em **Aplicar para** e modifique as configurações.

## Usar o EAC para alterar a prioridade da política de endereço de email

Um usuário pode ter vários endereços de email de proxy para a mesma conta de email (por exemplo, ayla@exchange.mail.contoso.com ou ayla@contoso.com). Essas can endereços de email e ser aplicadas por prioridade. Por exemplo, considere este cenário: você tem duas políticas de endereço de email e atribuí-las prioridades de 1 e 2. Se você criar outra política, ela será automaticamente atribuída uma prioridade de 3. No entanto, vamos supor que você tem duas políticas, e você especificar que uma delas seja prioridade 1, mas a outra política foi atribuída uma prioridade padrão de 2 quando ele foi criado. Nesse caso, a próxima diretiva que você crie, por padrão, se tornará a política de prioridade 2. Prioridade de 3 será atribuída a diretiva de prioridade 2 anterior.

1.  Navegue até **fluxo de emails** \> **políticas de endereço de Email**.

2.  Selecione a política de endereço de email para o qual você deseja alterar a prioridade e clique em![Ícone Seta para cima](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Ícone Seta para cima") de **prioridade de aumentar** ou **diminuir a prioridade**![Ícone Seta para baixo](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Ícone Seta para baixo").

## Use o Shell para editar uma política de endereço de email

Este exemplo edita a política de endereço de email South East Offices que atualmente inclui destinatários na Geórgia, Alabama e Louisiana a incluir também destinatários no Texas.

```powershell
Set-EmailAddressPolicy -Identity "South East Offices" -ConditionalStateorProvince "Georgia","Alabama","Louisiana","Texas"
```

> [!NOTE]  
> Embora a política de endereço de email já é aplicada aos destinatários na Geórgia, Alabama e Louisiana, você deve inclui-los no parâmetro porque o parâmetro substitui os valores; ele não acrescente valores já existentes.


Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-EmailAddressPolicy](https://technet.microsoft.com/pt-br/library/bb124517\(v=exchg.150\)).