---
title: 'Remover uma confiança de Federação: Exchange 2013 Help'
TOCTitle: Remover uma confiança de Federação
ms:assetid: dc4d126d-b567-470d-a5d0-e1402bf8f369
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657500(v=EXCHG.150)
ms:contentKeyID: 50486782
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma confiança de Federação

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-01-04_

Uma relação de confiança de Federação estabelece uma relação de confiança entre uma organização do Microsoft Exchange 2013 e o sistema de autenticação Azure Active Directory e oferece suporte a compartilhamento com outras organizações federadas do Exchange. Remover uma confiança de federação de seu local a organização do Exchange desabilitará o compartilhamento federado com outras organizações federadas do Exchange e com organizações do Office 365 conectadas à sua organização como parte de uma implantação híbrida. Considere com cuidado o impacto geral à sua organização antes de remover uma confiança de Federação.

Para tarefas de gerenciamento adicionais relacionadas às confianças de federação, consulte [Procedimentos de Federação](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esse recurso do Exchange Server 2013 não é totalmente compatível com o Office 365 operado pelo 21Vianet na China e pode haver algumas limitações de recurso. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/?linkid=313640">Saiba mais sobre o Office 365 operado pelo 21Vianet</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Permissões de certificados e federação" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Depois de remover a confiança de federação, você poderá remover os registros TXT do seu servidor DNS público para cada domínio federado. Reveja os requisitos para remover um registro TXT com a organização que hospeda seus registros DNS públicos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para remover uma confiança de federação

1.  Em um servidor do Exchange 2013 na organização local, navegue até **organização** \> **compartilhamento**.

2.  Na seção **Confiança de federação**, clique em **Remover**.

3.  No aviso, clique em **sim** para confirmar se deseja remover a confiança de federação.

4.  Depois que a confiança de federação for removida, clique em **Fechar**.

## Usar o Shell para remover uma confiança de federação

Este exemplo remove a confiança de federação.

    Remove-FederationTrust

Para informações detalhadas de sintaxes e de parâmetros, consulte [Remove-FederationTrust](https://technet.microsoft.com/pt-br/library/dd351153\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você removeu com êxito a confiança de federação, faça um dos seguintes:

  - No EAC, navegue até **organização** \> **compartilhamento**. Se tiver removido com êxito a confiança de federação, somente o botão **Habilitar** ficará disponível em **Confiança de Federação**.

  - No Shell, execute o seguinte comando para verificar se informações da confiança de federação não são retornadas para a sua organização do Exchange.
    
        Get-FederationTrust
    
    Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-FederationTrust](https://technet.microsoft.com/pt-br/library/dd351262\(v=exchg.150\)).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

