---
title: 'Permitir que os usuários do mesmo plano de discagem recebam faxes'
TOCTitle: Permitir que os usuários no mesmo plano de discagem para receber faxes
ms:assetid: cb245028-0b86-4171-879e-934dd35fa626
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124557(v=EXCHG.150)
ms:contentKeyID: 52058527
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir que os usuários no mesmo plano de discagem para receber faxes

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

É possível habilitar todos os usuários que estão vinculados com um plano de discagem de Unificação de mensagens (UM) para receber mensagens de fax em suas caixas de correio. Por padrão, os usuários que estão habilitados para Unificação de mensagens e vinculados com um plano de discagem de UM podem receber mensagens de fax. Para permitir que os usuários habilitados receber mensagens de fax em suas caixas de correio, o plano de discagem deve ser configurado para aceitar chamadas de fax de entrada. Você também deve habilitar o envio de fax na diretiva de caixa de correio UM e para o usuário. Por padrão, o envio de fax está habilitado em planos de discagem, políticas de caixa de correio de Unificação de MENSAGENS e para usuários. No entanto, pode haver ocasiões nessas configurações padrão foram alteradas e usuários habilitados para Unificação de MENSAGENS não podem receber mensagens de fax.

Se você evitar mensagens de fax sendo recebidos em um plano de discagem, todos os usuários que estão associados ao plano de discagem não será capazes de receber mensagens de fax, mesmo se você configurar propriedades de um usuário individual para que eles possam receber mensagens de fax. Habilitar ou desabilitar o envio de fax em um plano de discagem de UM terá precedência sobre as configurações para envio de fax em uma diretiva de caixa de correio UM ou de um usuário individual de habilitado.


> [!NOTE]
> Você pode usar o EAC para definir configurações de fax em uma política de caixa de correio de UM. Entretanto, você deve utilizar o Shell para fazer as configurações de fax em planos de discagem e para usuários individuais.



Para obter mais informações sobre os parceiros de fax, consulte [Microsoft identifique para parceiros de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para conhecer tarefas de gerenciamento adicionais relacionadas a mensagens de fax, consulte [Procedimentos de envio de fax](faxing-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para permitir que os usuários que estão vinculados a um plano de discagem para receber faxes

Este exemplo permite que os usuários habilitados para Unificação de MENSAGENS que são vinculados com UM plano de discagem chamado `MyUMDialPlan` para receber faxes de entrada.

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $true

