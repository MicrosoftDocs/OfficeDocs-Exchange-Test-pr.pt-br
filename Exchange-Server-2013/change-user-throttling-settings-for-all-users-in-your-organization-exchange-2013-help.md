---
title: 'Alterar as configurações para todos os usuários em sua organização de limitação de usuário: Exchange 2013 Help'
TOCTitle: Alterar as configurações para todos os usuários em sua organização de limitação de usuário
ms:assetid: c45cacfc-768d-4605-9bb0-53e30273fe4d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ863578(v=EXCHG.150)
ms:contentKeyID: 50556278
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar as configurações para todos os usuários em sua organização de limitação de usuário

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-08-05_

Você pode controlar como os recursos são consumidos por usuários individuais em sua organização do Exchange, alterando as configurações de limitação padrão.

Controlar como os recursos são consumidos por usuários individuais que era possível nos Exchange Server 2010 e esse recurso foi expandido para Exchange Server 2013. A política de chamada GlobalThrottlingPolicy define o padrão de limitação de configurações para cada usuário nova e existente em sua organização, a menos que você personalizou as políticas de limitação. Em muitos cenários típicos de implantação do Exchange, a política chamada GlobalThrottlingPolicy é adequada para gerenciar usuários.

Para personalizar as configurações de limitação que se aplicam a todos os usuários em sua organização, crie uma nova política de limitação com a organização de atribuição de escopo. Você só pode alterar o padrão de configurações de limitação usando o Shell.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Limitação do usuário" no tópico [Permissões de integridade e desempenho do servidor](server-health-and-performance-permissions-exchange-2013-help.md) .

  - Em novas políticas de escopo da organização, você deve definir somente as configurações de limitação que serão diferentes na política denominada GlobalThrottlingPolicy e quaisquer outras diretivas da organização. Dessa forma, o restante das configurações de diretiva da política denominada GlobalThrottlingPolicy será herdado, assim como quaisquer atualizações para limitação políticas que são adicionadas no futuro que atualizações do Exchange. É recomendável que você examine a seção "Gerenciar limitação usando escopos de políticas" no tópico [Gerenciamento de carga de trabalho do Exchange](exchange-workload-management-exchange-2013-help.md) antes de seguir esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o Shell para alterar os recursos de maneira pode ser usado por todos os usuários em toda sua organização

Este exemplo cria uma política de limitação que se aplica a todos os usuários em sua organização. Quaisquer parâmetros que você omitir herdem a diretiva padrão de limitação GlobalThrottlingPolicy os valores.

    New-ThrottlingPolicy -Name AllUsersEWSPolicy EwsMaxConcurrency 4 -ThrottlingPolicyScope Organization

Para obter mais informações sobre sintaxe e parâmetros, consulte [New-ThrottlingPolicy](https://technet.microsoft.com/pt-br/library/dd351045\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou a política de limitação de organização com êxito, faça o seguinte:

1.  Execute o seguinte comando.
    
        Get-ThrottlingPolicy | Format-List

2.  Verifique se a organização limitação política que você acabou de criar está listada na coluna que mostra o objeto GlobalThrottlingPolicy.

3.  Execute o seguinte comando.
    
        Get-ThrottlingPolicy | Format-List

4.  Verifique se as propriedades para a nova política de organização correspondem o valor ou valores que você configurou.

