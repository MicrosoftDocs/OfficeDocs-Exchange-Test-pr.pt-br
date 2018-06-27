---
title: 'Habilitar ou desabilitar a reprodução de multimídia mensagens de voz protegido: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar a reprodução de multimídia mensagens de voz protegido
ms:assetid: 3c33370c-4262-42b1-8d83-d61fc7c426cd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423543(v=EXCHG.150)
ms:contentKeyID: 52058398
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar a reprodução de multimídia mensagens de voz protegido

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode impor que usuários que recebam mensagens de caixa postal protegidas usem o recurso Tocar no Telefone para ouvir as mensagens. Se o software cliente não oferecer suporte para gerenciamento de direitos, os usuários deverão usar o Outlook Voice Access para ouvir as mensagens.

Para ouvirem mensagens de voz, os usuários habilitados para Unificação de Mensagens (UM) poderão usar o recurso Tocar no Telefone ou usar software multimídia em um computador ou dispositivo móvel. A reprodução de multimídia permite que um usuário habilitado para UM use um media player com alto-falantes de computador ou use um media player em um dispositivo móvel para ouvir a mensagem de voz.


> [!TIP]
> A caixa postal protegida só estará disponível em clientes que estejam usando uma versão do Outlook com suporte ao gerenciamento de direitos. Se o software cliente não oferecer suporte para gerenciamento de direitos, os usuários deverão usar o Outlook Voice Access para ouvir as chamadas.



Por padrão, o valor da propriedade **RequireProtectedPlayOnPhone** em uma política de caixa de correio da UM é definido como false. Isso significa que usuários habilitados para UM associados a essa política de caixa de correio da UM podem ouvir mensagens de voz protegidas:

  - Usando o Outlook Voice Access.

  - Usando o media player interno ou o botão Tocar no Telefone no Outlook 2010 ou em uma versão posterior.

  - Usando o media player interno ou o botão Tocar no Telefone no Outlook Web App.

Se o valor estiver definido como true, a reprodução multimídia de caixa postal protegida não será permitida. Usuários habilitados para UM associados a uma política de caixa de correio da UM na qual esse valor é definido como true só poderão ouvir mensagens de voz protegidas:

  - Usando o Outlook Voice Access.

  - Usando o botão Tocar no Telefone no Outlook 2010 ou em uma versão posterior.

  - Usando o botão Tocar no Telefone no Outlook Web App.

Essa configuração é especialmente útil quando os usuários habilitados para UM utilizam computadores públicos, laptops em lugares comuns ou reprodutores de mídia de telefones celulares para ouvir a mensagem de voz protegida com informações particulares.

Para conhecer tarefas de gerenciamento adicionais relacionadas a procedimentos de Caixa Postal Protegida, consulte [Procedimentos de caixa postal protegidos](protected-voice-mail-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou desabilitar a reprodução multimídia de mensagens de voz protegidas

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Política de Caixa de Correio da UM** \> **Caixa postal protegida**, marque a caixa de seleção ao lado de **Exigir Tocar no Telefone para mensagens de voz protegidas** para habilitar essa configuração. Desmarque a caixa de seleção para desabilitar a configuração.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar ou desabilitar a reprodução de multimídia de mensagens de voz protegidas

Este exemplo permite que usuários que estejam associados à política de caixa de correio da UM chamada `MyUMMailboxPolicy` reproduzam mensagens de voz protegidas usando um media player.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $false

Este exemplo impede que usuários que estejam associados à política de caixa de correio da UM chamada `MyUMMailboxPolicy` reproduzam mensagens de voz protegidas usando um media player.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $true

