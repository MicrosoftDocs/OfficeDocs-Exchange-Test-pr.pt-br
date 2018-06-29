---
title: 'Adicionar ou remover usuários de uma política de caixa de correio móvel: Exchange 2013 Help'
TOCTitle: Adicionar ou remover usuários de uma política de caixa de correio móvel
ms:assetid: 4ca8e395-c074-4165-b788-16fae3e2ccab
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997929(v=EXCHG.150)
ms:contentKeyID: 50485532
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar ou remover usuários de uma política de caixa de correio móvel

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-07-16_

Uma política de caixa de correio de dispositivo móvel permite que você aplique um conjunto comum de configurações de segurança e dispositivo móvel para um grupo de usuário. Você pode criar várias políticas de caixa de correio para dispositivos móveis.


> [!WARNING]
> Quando você instalar o Microsoft Exchange Server 2013, uma política de caixa de correio de dispositivo móvel padrão é criada, e todos os usuários recebem automaticamente essa política.



Para outras tarefas de gerenciamento relacionadas a políticas de caixa de correio de dispositivo móvel, consulte [Políticas de caixa de correio para dispositivos móveis](mobile-device-mailbox-policies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Política de caixa de correio de dispositivo móvel", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Você deve ter uma política de caixa de correio de dispositivo móvel disponível no EAC, em **Móvel** \> **Políticas de Caixa de Correio de Dispositivo Móvel**.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Alterar um política de caixa de correio de dispositivo móvel do usuário

Você pode usar o EAC ou o Shell para alterar uma política de caixa de correio de dispositivo móvel de usuário.

## Usar o EAC para alterar a política de caixa de correio de dispositivo móvel do usuário

Você alterar uma política de caixa de correio de dispositivo móvel de um único usuário usando o EAC.

1.  No EAC, clique em **Destinatários** \> **Caixas de correio** e selecione uma caixa de correio.

2.  No painel de Detalhes, role para a tela **Recursos de Telefone e Voz** e selecione **Exibir detalhes**, para mostrar os **Detalhes do Dispositivo Móvel**.

3.  A política de caixa de correio de dispositivo móvel atualmente atribuída é exibida. Para alterar a política de caixa de correio do dispositivo móvel, clique em **Procurar**.

4.  Escolha a política de caixa de correio de dispositivo móvel apropriada, na lista, clique em **OK** e em **Salvar**.

## Usar o Shell para adicionar um usuário a uma política de caixa de correio de dispositivo móvel

Você pode alterar a política de caixa de correio de dispositivo móvel de um único usuário usando o cmdlet **Set-CASMailbox** no Shell.

1.  No Shell, execute o comando a seguir.
    
        Set-CASMailbox -Identity tony@contoso.com -ActiveSyncMailboxPolicy "Sales" 

## Como saber se funcionou?

Para verificar se você alterou com êxito uma política de caixa de correio de dispositivo móvel do usuário, escolha um desses procedimentos:

1.  No EAC, clique em **Destinatários** \> **Caixas de correio** e selecione um destinatário específico. No painel de Detalhes, role para baixo, até **Recursos de telefone e voz**e clique em **Exibir detalhes**.

2.  No Shell, execute o comando a seguir.
    
        Get-CASMailbox -Identity tony@contoso.com 

## Alterar a política de caixa de correio de dispositivo móvel para vários usuários ao mesmo tempo

Se você quiser alterar a política de caixa de correio de dispositivo móvel para vários usuários ao mesmo tempo, você pode usar a funcionalidade de edição em massa, no EAC, ou usar o Shell, para alterar a política de caixa de correio de dispositivo móvel para um conjunto filtrado de usuários.

## Usar a ferramenta de edição em massa no EAC para alterar a política de caixa de correio de dispositivo móvel para vários usuários

Você pode atualizar a política de caixa de correio do dispositivo móvel para vários usuários de uma vez, usando a funcionalidade de Edição em Massa.

1.  Na EAC, clique em **Destinatários** \> **Caixas de correio**.

2.  Selecione vários usuários.

3.  No painel Detalhes, role para **Exchange ActiveSync** e clique em **Atualizar uma política**.

4.  Clique em **Procurar**, para escolher uma política de caixa de correio do dispositivo móvel.

5.  Clique em **OK** e em **Salvar**.

## Usar o Shell para alterar a política de caixa de correio do dispositivo móvel para um conjunto filtrado de usuários

Você pode usar o Shell para alterar a política de caixa de correio do dispositivo móvel para um conjunto filtrado de usuários. Você pode filtrar os usuários usando vários atributos.

1.  No Shell, execute o comando a seguir.
    
        Get-Mailbox | where { $_.CustomAttribute1 -match "Manager"
         } | Set-CASMailbox -activesyncmailboxpolicy(Get-ActiveSyncMailboxPolicy "Contoso").Identity
    

    > [!TIP]
    > Você pode usar <CODE>CustomAttribute1</CODE> em substituição a qualquer das propriedades no objeto de <STRONG>Get-Mailbox</STRONG>. Para exibir a lista completa, digite: <CODE>Get-Mailbox username |fl</CODE>.



## Como saber se funcionou?

Para verificar se você alterou com êxito uma política de caixa de correio de dispositivo móvel do usuário, escolha um desses procedimentos:

1.  No EAC, clique em **Destinatários** \> **Caixas de correio** e selecione um destinatário específico. No painel de Detalhes, role para baixo, até **Recursos de telefone e voz**e clique em **Exibir detalhes**.

2.  No Shell, execute o comando a seguir.
    
        Get-CASMailbox -Identity tony@contoso.com

