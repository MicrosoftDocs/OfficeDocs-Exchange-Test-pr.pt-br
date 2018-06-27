---
title: 'Definir o tempo de vida do PIN de caixa postal: Exchange 2013 Help'
TOCTitle: Definir o tempo de vida do PIN de caixa postal
ms:assetid: d17f0bf6-0ad6-40a4-bdd5-f7098f39250d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124712(v=EXCHG.150)
ms:contentKeyID: 50556296
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir o tempo de vida do PIN de caixa postal

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode configurar a vida útil do PIN para usuários habilitados para Unificação de mensagens (UM). A vida útil do PIN é o tempo máximo que uma Outlook PIN Voice Access será válida para destinatários habilitados. A configuração de vida útil do PIN é configurada em uma diretiva de caixa de correio UM e se aplica a todos os usuários habilitados para UM associados com a diretiva de caixa de correio de Unificação de mensagens.

Várias configurações relacionadas ao PIN podem ser configuradas em uma diretiva de caixa de correio de UM. A vida útil do PIN configurando controles o intervalo de tempo, em dias, data Outlook Voice Access usuários última alteraram seu PIN para a data em que eles serão forçados a alterar seu PIN novamente. O intervalo é de 0 a 999, e o padrão é 60 dias. Se você digitar 0, o PIN do usuário não expirará. Recomendamos que você não definir essa configuração como 0, porque, por isso você reduz significativamente a segurança da sua rede.


> [!IMPORTANT]
> A Unificação de mensagens não notifica os usuários quando o PIN está prestes a expirar.



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

## Usar o EAC para configurar a vida útil do PIN

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Clique em Avançar para e **diretivas de PINvida útil do PIN impor (dias)**, insira um valor entre 0 e 999.

5.  Clique em **Salvar**.

## Use o Shell para configurar a vida útil do PIN

Este exemplo define o número de dias que um PIN pode ser usado para os usuários do Outlook Voice Access que estão associados a uma diretiva de caixa de correio UM chamado `MyUMMailboxPolicy` como 30.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINLifetime 30

Este exemplo configura as seguintes configurações de PIN para usuários de Outlook Voice Access, que estão associados a uma diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`:

  - Define o número de falhas de logon antes do PIN do usuário é redefinido como 3.

  - Define o número máximo de tentativas de logon como 5.

  - Define o tamanho mínimo do PIN para 9 dígitos.

  - Define o PIN expirará em 40 dias.

<!-- end list -->

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9 -PINLifetime 40

