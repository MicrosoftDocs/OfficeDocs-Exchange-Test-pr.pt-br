---
title: 'Habilitar ou desabilitar o Exchange ActiveSync para uma caixa de correio: Exchange Online Help'
TOCTitle: Habilitar ou desabilitar o Exchange ActiveSync para uma caixa de correio
ms:assetid: dcf7c05b-b1b9-4b0f-800d-fec9f2ddc9e4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124809(v=EXCHG.150)
ms:contentKeyID: 50556303
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar ou desabilitar o Exchange ActiveSync para uma caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-11-13_

Você pode usar o EAC ou o Shell para habilitar ou desabilitar o Microsoft Exchange ActiveSync para uma caixa de correio de usuário. O Exchange ActiveSync é um protocolo cliente que permite aos usuários sincronizar um dispositivo móvel com a caixa de correio do Exchange. O Exchange ActiveSync é ativado por padrão quando uma caixa de correio de usuário é criada. Para saber mais, confira [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configuração do Exchange ActiveSync" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou desabilitar o Exchange ActiveSync

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuário, clique na caixa de correio para a qual você deseja habilitar ou desabilitar o Exchange ActiveSync e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Recursos da Caixa de Correio**.

4.  Em **Dispositivos Móveis**, siga um destes procedimentos:
    
      - Como desabilitar o Exchange ActiveSync, clique em **Desabilitar o Exchange ActiveSync**.
        
        Um aviso é exibido perguntando se você tem certeza de que deseja desabilitar o Exchange ActiveSync. Clique em **Sim**.
    
      - Para habilitar o Exchange ActiveSync, clique em **Habilitar o Exchange ActiveSync**.

5.  Clique em **Salvar** para salvar a alteração.


> [!TIP]
> Você pode habilitar e desabilitar o Exchange ActiveSync para caixas de correio de vários usuários usando o recurso de edição em massa do EAC. Para saber como fazer isso, confira a seção "Editar caixas de correio de usuários em massa" em <A href="manage-user-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio do usuário</A>.



## Usar o Shell para habilitar ou desabilitar o Exchange ActiveSync

Este exemplo desabilita o Exchange ActiveSync para a caixa de correio de Paulo Araújo.

    Set-CASMailbox -Identity "Yan Li" -ActiveSyncEnabled $false

Este exemplo desabilita o Exchange ActiveSync para a caixa de correio de Laura Cunha.

    Set-CASMailbox -Identity Ellyn@contoso.com -ActiveSyncEnabled $true

Para informações detalhadas sobre sintaxes e parâmetros, confira [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou o Exchange ActiveSync para uma caixa de correio de usuário com êxito, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de Correio**, clique na caixa de correio e em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

  - Na página de propriedades de caixa de correio, clique em **Recursos da Caixa de Correio**.

  - Em **Dispositivos Móveis**, verifique se o Exchange ActiveSync está habilitado ou desabilitado.

Ou

  - Execute o seguinte comando no Shell.
    
        Get-CASMailbox <identity>
    
    Se o Exchange ActiveSync estiver habilitado, o valor da propriedade *ActiveSyncEnabled* será `True`. Se o Exchange ActiveSync estiver desabilitado, o valor será `False`.

