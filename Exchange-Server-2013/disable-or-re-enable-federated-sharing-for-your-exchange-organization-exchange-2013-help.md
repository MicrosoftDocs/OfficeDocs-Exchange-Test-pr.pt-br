---
title: 'Desabilitar/reabilitar compartilhamento federado para organização do Exchange'
TOCTitle: Desabilitar ou reabilitar o compartilhamento federado para sua organização do Exchange
ms:assetid: d36490d8-0268-47b9-a6d4-e56427f1b02e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657497(v=EXCHG.150)
ms:contentKeyID: 50486725
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar ou reabilitar o compartilhamento federado para sua organização do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-02-17_

Pode haver situações nas quais você precise desabilitar temporariamente o compartilhamento federado de sua organização. Em vez de excluir a confiança de federação ou excluir os relacionamentos de organização e as políticas de compartilhamento que você pode precisar no futuro, você pode simplesmente desabilitar o identificador de organização (OrgID) para a confiança federada.


> [!CAUTION]
> Para implantações híbridas com o Office 365, desabilitar a confiança de federação de seus servidores locais também desabilitará recursos híbridos, como informações de disponibilidade de calendário compartilhado, Dicas de Email e acompanhamento de mensagens. Entretanto, o transporte de email seguro não será desabilitado na implantação híbrida se a confiança de federação da organização local estiver desabilitada.



Para saber mais sobre relações de confiança de federação, consulte [Federação](federation-exchange-2013-help.md). Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md).

Para outras tarefas de gerenciamento relacionadas a compartilhamento federado, consulte [Procedimentos de Federação](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esse recurso do Exchange Server 2013 não é totalmente compatível com o Office 365 operado pelo 21Vianet na China e pode haver algumas limitações de recurso. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/?linkid=313640">Saiba mais sobre o Office 365 operado pelo 21Vianet</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de permissões de *Federation and certificates* no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Todos os relacionamentos de organização e todas as políticas de compartilhamento existentes para outras organizações do Exchange federadas não serão modificados e não estarão funcionais. As políticas de compartilhamento configuradas para fornecer aos destinatários de Internet acesso a informações de calendário não serão afetadas.

  - O Centro de Administração do Exchange (EAC) não pode ser usado para habilitar ou desabilitar o OrgID de uma confiança federada. É necessário usar o Shell.

## Usar o Shell para desabilitar ou reabilitar o compartilhamento federado

Este exemplo desabilita o OrgID e a federação e o compartilhamento federado da organização do Exchange.

```powershell
Set-FederatedOrganizationIdentifier -Enabled $false
```

Este exemplo habilita o OrgID e reabilita a federação e o compartilhamento federado da organização do Exchange.

```powershell
Set-FederatedOrganizationIdentifier -Enabled $true
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/pt-br/library/dd351037\(v=exchg.150\)).

## Como saber se funcionou?

A conclusão com êxito do cmdlet **Set-OrganizationIdentifier** será a primeira indicação de que o OrgID foi desabilitado ou habilitado.

Para verificar se houve êxito ou não, execute o seguinte comando do Shell e verifique o valor retornado para o parâmetro *Enabled*

```powershell
Get-FederatedOrganizationIdentifier
```


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


