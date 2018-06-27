---
title: 'Definir o parceiro URI para permitir que o envio de fax do servidor de fax: Exchange 2013 Help'
TOCTitle: Definir o parceiro URI para permitir que o envio de fax do servidor de fax
ms:assetid: 77a9013b-d76b-4af2-8b2c-cef435cf67af
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ650873(v=EXCHG.150)
ms:contentKeyID: 52058441
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir o parceiro URI para permitir que o envio de fax do servidor de fax

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Você pode habilitar e desabilitar os faxes de entrada para os usuários associados a uma diretiva de caixa de correio de Unificação de mensagens (UM). Por padrão, quando você habilita usuários para Unificação de MENSAGENS, os usuários não podem receber mensagens de fax até você habilitar o envio de fax de entrada na diretiva de caixa de correio UM e especifique o URI do servidor de parceiro de fax. Se os URIs são configurados na diretiva de caixa de correio de Unificação de MENSAGENS, mas a opção para permitir que os faxes de entrada está desabilitada em UM plano de discagem ou para um usuário individual, os usuários habilitados para UM vinculadas à política de caixa de correio de Unificação de MENSAGENS ainda não conseguirá receber faxes.

Para obter mais informações sobre os parceiros de fax, consulte [Microsoft identifique para parceiros de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para conhecer tarefas de gerenciamento adicionais relacionadas a mensagens de fax, consulte [Procedimentos de envio de fax](faxing-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para definir o URI do parceiro de fax

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **plano de discagem de UM**, em **Diretivas de caixa de correio de UM**, selecione a política que você deseja modificar e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **política de caixa de correio de Unificação de MENSAGENS** \> **Geral**, na caixa **URI do servidor de fax do parceiro**, insira o TCP ou TLS URI. Por exemplo: *sip:faxserver1.contoso.com:5060;transport=tcp* ou *sip:faxserver2.contoso.com:5061;transport=tls*
    

    > [!TIP]
    > Embora caixa pode conter mais de um URI do servidor de fax, apenas um será usado. Se você inserir dois URIs, somente o primeiro será usado.



4.  Clique em **Salvar** para salvar as suas alterações.

## Use o Shell para definir o URI de parceiro de fax

Este exemplo permite que os usuários que estão vinculados com a Unificação de MENSAGENS da caixa de correio diretiva `UMDialPlan Default Policy` para usar TCP com porta 5060 para o de servidor de fax do parceiro `faxserver1`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver1.contoso.com:5060;transport=tcp

Este exemplo permite que os usuários que estão vinculados com a Unificação de MENSAGENS da caixa de correio diretiva `UMDialPlan Default Policy` para usar o TLS com porta 5061 para o de servidor de fax do parceiro `faxserver2`.

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver2.contoso.com:5061;transport=tls

