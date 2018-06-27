---
title: 'Impedir que os usuários no mesmo plano de discagem receber faxes: Exchange 2013 Help'
TOCTitle: Impedir que os usuários no mesmo plano de discagem receber faxes
ms:assetid: 4fc66414-c950-4bca-ac20-4e489f288d06
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201688(v=EXCHG.150)
ms:contentKeyID: 52058415
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impedir que os usuários no mesmo plano de discagem receber faxes

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Você pode impedir que usuários habilitados para UM (Unificação de Mensagens) vinculados a um plano de discagem de UM recebam faxes. Por padrão, os usuários que estão habilitados para Unificação de Mensagens e estão vinculados a um plano de discagem de UM podem receber mensagens de fax. No entanto, há ocasiões em que você deseja evitar que usuários que estão associados a um plano de discagem do UM específico recebam fax.

É possível impedir que usuários habilitados para UM recebam faxes configurando o plano de discagem de UM, a política de caixa de correio de UM ou a caixa de correio do usuário habilitada para UM. Se você desabilitar a entrega de mensagens de fax de entrada em um plano de discagem do UM, todos os usuários que estiverem associados ao plano de discagem serão impedidos de receber mensagens de fax. A habilitação ou a desabilitação de fax em um plano de discagem de UM tem precedência sobre as configurações de um usuário individual habilitado para UM.


> [!TIP]
> Você pode usar o EAC para definir configurações de fax em uma política de caixa de correio de UM. Entretanto, você deve utilizar o Shell para fazer as configurações de fax em planos de discagem e para usuários individuais.



Para obter mais informações sobre os parceiros de fax, consulte [Microsoft identifique para parceiros de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para conhecer tarefas de gerenciamento adicionais relacionadas a mensagens de fax, consulte [Procedimentos de envio de fax](faxing-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para impedir que usuários vinculados a um plano de discagem recebam fax

Esse exemplo impede que usuários habilitados para UM associados ao plano de discagem de UM denominado `MyUMDialPlan` recebam faxes.

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $false

