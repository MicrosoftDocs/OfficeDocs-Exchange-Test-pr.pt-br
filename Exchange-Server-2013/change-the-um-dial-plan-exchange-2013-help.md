---
title: 'Alterar UM plano de discagem: Exchange 2013 Help'
TOCTitle: Alterar UM plano de discagem
ms:assetid: 4a6b6b6f-c61c-44e8-91dd-c5d28835f441
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633465(v=EXCHG.150)
ms:contentKeyID: 50485515
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar UM plano de discagem

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-05_

Você pode precisar mover um usuário que está habilitado para Unificação de Mensagens (UM) para um plano de discagem de UM diferente ou para alterar o plano de discagem associado ao usuário. Por exemplo, você pode querer mover um usuário habilitado para Um de um plano de discagem de ‏Ramal Telefônico para um plano de discagem SIP URI.

Para alterar o plano de discagem de UM, você terá que desabilitar o usuário para Unificação de Mensagens e, depois, habilitar o usuário para Unificação de Mensagens, no novo plano de discagem de UM. Isso é porque planos de discagem diferentes podem ter configurações e requisitos variados, como tamanho do ramal e tipo de URI diferentes. Por exemplo, um plano de discagem de SIO URI requer um Identificador de Recursos SIP a ser atribuído a cada caixa de correio habilitada para UM, mas os planos de discagem de Ramal de Telefone, não. Além disso, cada caixa de correio de UM contém referências ao plano de discagem de UM e à política de caixa de correio de UM. A política de caixa de correio de UM, por sua vez, contém referências ao plano de discagem de UM. Se você alterar o endereço proxy principal de um usuário habilitado para UM para apontar para um plano de discagem diferente, a caixa de correio de UM ficará em um estado inconsistente.

Para conhecer tarefas de gerenciamento adicionais relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se uma política de caixa de correio de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de você executar esses procedimentos, verifique se o destinatário do Exchange existente está habilitado para Unificação de Mensagens. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Como fazer isso?

## Etapa 1: Criar o novo plano de discagem de UM


> [!IMPORTANT]
> Se estiver migrando usuários habilitados para UM para o Microsoft Office Communications Server 2007 R2 ou para o Microsoft Lync Server, você deverá primeiro criar um plano de discagem SIP URI.



Para instruções detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

## Etapa 2: Desabilitar o usuário para Unificação de Mensagens

Para instruções detalhadas, consulte [Desabilitar a caixa postal de um usuário](disable-voice-mail-for-a-user-exchange-2013-help.md).

## Etapa 3: Habilitar o usuário para Unificação de Mensagens no novo plano de discagem de UM


> [!IMPORTANT]
> Se você estiver movendo usuários para um ambiente com o Office Communications Server 2007 ou o Lync Server, será preciso também incluir um Identificador de Recursos SIP para o usuário ao habilitar o usuário para UM. Será preciso também selecionar a diretiva de caixa de correio de UM associada a um plano de discagem SIP.



Para instruções detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

