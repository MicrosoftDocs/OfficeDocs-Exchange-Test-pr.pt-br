---
title: 'Desabilitar os padrões comuns de PIN para caixa postal: Exchange 2013 Help'
TOCTitle: Desabilitar os padrões comuns de PIN para caixa postal
ms:assetid: eecc40ae-fac7-41e4-a1e1-16330f4462a3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125160(v=EXCHG.150)
ms:contentKeyID: 50556311
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar os padrões comuns de PIN para caixa postal

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode habilitar ou desabilitar os padrões comuns de PIN de Unificação de mensagens (UM) para usuários do Outlook Voice Access. Se você habilitar ou desabilitar os padrões comuns de PIN configuração em uma diretiva de caixa de correio UM, a configuração se aplicará a todos os usuários habilitados para UM associados com a diretiva de caixa de correio de Unificação de mensagens. Por padrão, os usuários habilitados para Unificação de mensagens não podem usar padrões comuns quando eles criam um PIN.

Você pode configurar várias configurações relacionadas ao PIN em uma diretiva de caixa de correio de UM. A configuração **Permitir padrões comuns do PIN** é usada para permitir ou impedir o uso de padrões de número comuns quando os usuários criarem um PIN. Por padrão, essa configuração é desabilitada e evita que usuários usem os seguintes padrões de número:

  - **Números sequenciais**   Estes são os valores PIN que incluem somente números consecutivos. Exemplos de números consecutivos um PIN são 1234 e 65432.

  - **Números de repetida**   Estes são os valores PIN que incluem somente números repetidos. Exemplos de números repetidos são 11111 e 22222.

  - **Sufixo da extensão de caixa de correio**   Estes são os valores PIN que incluem o sufixo da extensão de caixa de correio do usuário. Por exemplo, se a extensão de caixa de correio de um usuário for 36697, o PIN do usuário não pode ser 3669712.


> [!TIP]
> Se a configuração <STRONG>Permitir padrões comuns do PIN</STRONG> é habilitada, será rejeitado apenas o sufixo da extensão de caixa de correio.



Para tarefas adicionais relacionadas à segurança do PIN do Outlook Voice Access, consulte [Procedimentos de segurança PIN](pin-security-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para desabilitar os padrões comuns de PIN

1.  No EAC, navegue até **Unificação de mensagens** \> **planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de Unificação de mensagens que você deseja modificar e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Diretivas de caixa de correio de UM**, selecione a política de caixa de correio de Unificação de mensagens que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição")na barra de ferramentas.

3.  Na página **Diretiva de caixa de correio de UM**, em **políticas de PIN**, desmarque a caixa de seleção ao lado de **Permitir padrões comuns de PIN**.

4.  Clique em **Salvar**.

## Use o Shell para desabilitar os padrões comuns de PIN

Este exemplo impede que os usuários associados a diretiva de caixa de correio de Unificação de mensagens denominada `MyUMMailboxPolicy` utilizem PINs que contêm padrões comuns.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowCommonPatterns $false

