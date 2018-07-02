---
title: 'Criar uma caixa de correio compartilhada: Exchange Online Help'
TOCTitle: Criar uma caixa de correio compartilhada
ms:assetid: d34bc827-1e83-4a7f-a219-8ba9c19fe24b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150570(v=EXCHG.150)
ms:contentKeyID: 50486712
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Criar uma caixa de correio compartilhada

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**Tópico modificado em:** 2016-12-09_

**Tempo estimado para finalização: 5 minutos**

Com as caixas de correio compartilhadas, um grupo de pessoas em sua empresa pode monitorar e enviar emails de uma conta comum com mais facilidade, como info@contoso.com ou suporte@contoso.com. Quando uma pessoa do grupo responde a uma mensagem enviada à caixa de correio compartilhada, o email parece ter sido enviado da caixa de correio compartilhada, e não pelo usuário individual.


> [!IMPORTANT]
> Se estiver usando o Office 365 para empresas, crie uma caixa de correio compartilhada no Centro de administração do Office 365. 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=834766">Criar caixas de correio compartilhadas no Office 365</A></P></LI></UL>



Se sua organização usa um ambiente híbrido do Exchange, você deve usar o Centro de Administração do Exchange local para criar e gerenciar caixas de correio compartilhadas. Para saber mais sobre caixas de correio compartilhadas, confira o tópico [Caixas de correio compartilhadas](shared-mailboxes-exchange-2013-help.md).

## Usar o EAC para criar uma caixa de correio compartilhada

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio do usuário" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

1.  Vá em **Destinatários** \> **Compartilhado** \> **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Preencha os campos necessários:
    
      - **Nome para exibição**
    
      - **Endereço de email**

3.  Para conceder permissões de Acesso Total ou Enviar Como, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), e depois selecione os usuários para os quais você deseja conceder as permissões. Você pode usar a tecla **CTRL** para selecionar vários usuários. Confuso sobre qual permissão usar? Consulte Quais permissões você deve usar? mais à frente neste tópico.
    

    > [!TIP]
    > A permissão de Acesso Total permite ao usuário abrir uma caixa de correio assim como criar e modificar itens na mesma. A permissão de Enviar Como permite que qualquer um que não seja o proprietário da caixa de correio envie email a partir desta caixa de correio compartilhada. Ambas as permissões são necessárias para que a operação da caixa de correio compartilhada seja realizada com sucesso.



4.  Clique em **Salvar** para salvar suas alterações e criar a caixa de correio compartilhada.

## Use o EAC para editar a delegação da caixa de correio compartilhada.

1.  Vá em **Destinatários** \> **Compartilhado** \> **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Clique em **Delegação da caixa de correio**

3.  Para conceder ou remover permissões de Acesso Total ou Enviar Como, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") ou **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover") e depois selecione os usuários para os quais você deseja conceder a permissão.
    

    > [!TIP]
    > A permissão de Acesso Total permite ao usuário abrir uma caixa de correio assim como criar e modificar itens na mesma. A permissão de Enviar Como permite que qualquer um que não seja o proprietário da caixa de correio envie email a partir desta caixa de correio compartilhada. Ambas as permissões são necessárias para que a operação da caixa de correio compartilhada seja realizada com sucesso.



4.  Clique em **Salvar** para salvar as suas alterações.

## Usar uma caixa de correio compartilhada

Para saber como os usuários podem acessar e usar caixas de correio compartilhadas, confira o seguinte:

  - [Abrir e usar uma caixa de correio compartilhada no Outlook 2016 e no Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=834764)

  - [Abra e use uma caixa de correio compartilhada no Outlook na Web para empresas](https://go.microsoft.com/fwlink/p/?linkid=834766)

## Usar o Shell para criar uma caixa de correio compartilhada

Este exemplo cria a caixa de correio compartilhada Departamento de Vendas e concede permissões de Acesso Total e Enviar em Nome de para o MarketingSG do grupo de segurança. Os usuários que são membros do grupo de segurança receberão as permissões para a caixa de correio.


> [!TIP]
> Este exemplo assume que você já criou o grupo de segurança MarketingSG e o que o grupo de segurança está habilitado para email. Consulte <A href="manage-mail-enabled-security-groups-exchange-2013-help.md">Gerenciar grupos de segurança habilitados para email</A>.



    New-Mailbox -Shared -Name "Sales Department" -DisplayName "Sales Department" -Alias Sales | Set-Mailbox -GrantSendOnBehalfTo MarketingSG | Add-MailboxPermission -User MarketingSG -AccessRights FullAccess -InheritanceType All

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-Mailbox](https://technet.microsoft.com/pt-br/library/aa997663\(v=exchg.150\)).

## Quais permissões você deve usar?

Você pode usar as seguintes permissões com uma caixa de correio compartilhada.

  - **Acesso Total**   A permissão Acesso Total permite que um usuário abra a caixa de correio compartilhada e atue como o proprietário dessa caixa de correio. Após acessar a caixa de correio compartilhada, o usuário pode criar itens de calendário; ler, exibir, excluir e alterar mensagens de email; criar tarefas e contatos de calendário. No entanto, um usuário com a permissão Acesso Total não pode enviar email da caixa de correio compartilhada, a menos que também tenha a permissão Enviar Como ou Enviar em Nome de.

  - **Enviar Como**   A permissão Enviar Como permite que um usuário represente a caixa de correio compartilhada ao enviar um email. Por exemplo, se Kweku efetuar login na caixa de correio compartilhada Departamento de Marketing e enviar um email, ele será exibido como se o Departamento de Marketing tivesse enviado o email.

  - **Enviar em Nome de**   A permissão Enviar em Nome de permite que um usuário envie um email em nome da caixa de correio compartilhada. Por exemplo, se John efetuar login na caixa de correio compartilhada Edifício de Recepção 32 e enviar um email, ele será exibido como sendo enviado por "John, em nome do Edifício de Recepção 32". Não é possível usar o EAC para conceder permissões Enviar em nome de, você deve usar o cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) com o parâmetro *GrantSendonBehalf*.

## Mais informações

Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


