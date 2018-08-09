---
title: 'Alterar as configurações para usuários específicos de limitação de usuário'
TOCTitle: Alterar as configurações para usuários específicos de limitação de usuário
ms:assetid: c5f834d6-189d-485e-9800-5e0066815ecf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ863577(v=EXCHG.150)
ms:contentKeyID: 50556283
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar as configurações para usuários específicos de limitação de usuário

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-08-05_

Você pode controlar como os recursos são consumidos por usuários individuais em sua organização do Exchange, alterando as configurações de limitação padrão.

Controlar como os recursos são consumidos por usuários individuais que era possível nos Exchange Server 2010 e esse recurso foi expandido para Exchange Server 2013. A política de chamada GlobalThrottlingPolicy define o padrão de limitação de configurações para cada usuário nova e existente em sua organização, a menos que você personalizou as políticas de limitação. Em muitos cenários típicos de implantação do Exchange, a política chamada GlobalThrottlingPolicy é adequada para gerenciar usuários.

Para personalizar as configurações de limitação para aplicar somente a usuários específicos na sua organização, crie uma nova política de limitação com a atribuição de escopo Regular. Você só pode alterar o padrão de configurações de limitação usando o Shell.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Limitação do usuário" no tópico [Permissões de integridade e desempenho do servidor](server-health-and-performance-permissions-exchange-2013-help.md) .

  - Em novas políticas de escopo de regulares, você deve definir somente as configurações de limitação que serão diferentes na política denominada GlobalThrottlingPolicy e quaisquer outras diretivas da organização. Dessa forma, o restante das configurações de diretiva da política denominada GlobalThrottlingPolicy será herdado, assim como quaisquer atualizações para limitação políticas que são adicionadas no futuro que atualizações do Exchange. É recomendável que você examine a seção "Gerenciar limitação usando escopos de políticas" no tópico [Gerenciamento de carga de trabalho do Exchange](exchange-workload-management-exchange-2013-help.md) antes de seguir esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o Shell para alterar os recursos de maneira pode ser usado por usuários específicos em toda sua organização

Este exemplo cria um política denominada ITStaffPolicy que pode ser associado aos usuários específicos de limitação de usuário não-padrão. Quaisquer parâmetros que você omitir herdem a diretiva padrão de limitação GlobalThrottlingPolicy os valores. Depois de criar essa diretiva, você deve associá-lo a usuários específicos.

    New-ThrottlingPolicy -Name ITStaffPolicy -EwsMaxConcurrency 4 -ThrottlingPolicyScope Regular

Este exemplo associa um usuário de tonysmith de nome de usuário com a diretiva de limitação ITStaffPolicy (que possui limites mais altos).

    Set-ThrottlingPolicyAssociation -Identity tonysmith -ThrottlingPolicy ITStaffPolicy

Você não precisa usar o cmdlet **Set-ThrottlingPolicyAssociation** para associar um usuário uma política. Os comandos a seguir mostram outra maneira para associar a diretiva de limitação ITStaffPolicy de tonysmith.

``` 
    $b = Get-ThrottlingPolicy ITStaffPolicy
``` 
``` 
    Set-Mailbox -Identity tonysmith -ThrottlingPolicy $b
``` 

Para obter mais informações sobre sintaxe e parâmetros, consulte [New-ThrottlingPolicy](https://technet.microsoft.com/pt-br/library/dd351045\(v=exchg.150\)) e [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/pt-br/library/ff459231\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito a política de limitação de regulares, faça o seguinte:

1.  Execute o seguinte comando.
    
        Get-ThrottlingPolicy | Format-List

2.  Verifique se o regulares limitação política que você acabou de criar está listado na coluna que mostra o objeto GlobalThrottlingPolicy.

3.  Execute o seguinte comando.
    
        Get-ThrottlingPolicy | Format-List

4.  Verifique se as propriedades para a nova política Regular correspondem o valor ou valores que você configurou.

5.  Execute o seguinte comando.
    
        Get-ThrottlingPolicyAssociation

6.  Verifique se a nova política Regular está associada com o usuário ou usuários você associados a ele.

