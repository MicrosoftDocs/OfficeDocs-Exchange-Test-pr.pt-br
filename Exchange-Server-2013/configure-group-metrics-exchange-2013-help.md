---
title: 'Configurar as métricas de grupo: Exchange 2013 Help'
TOCTitle: Configurar as métricas de grupo
ms:assetid: 76ccd6a7-e2ec-42f4-9ab3-e8cc257ac896
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ649327(v=EXCHG.150)
ms:contentKeyID: 50485946
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar as métricas de grupo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Dicas de email que fornecem informações sobre o tamanho de grupos de distribuição e grupos dinâmicos de distribuição se baseiam em dados de métricas de grupo. Dados de métricas de grupo são gerados em servidores de caixa de correio designadas. Para obter mais informações sobre as métricas de grupo, consulte [Métricas de grupo e as dicas de email](group-metrics-and-https://docs.microsoft.com/pt-br/exchange/clients-and-mobile-in-exchange-online/mailtips/mailtips).

Você pode habilitar ou desabilitar a geração de métricas de grupo em um servidor de caixa de correio.

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Métricas de grupo" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Dados de métricas de grupo são usados somente para as dicas de email. Certifique-se que métricas de grupo que dicas de email estão habilitadas em sua organização. Para obter etapas detalhadas, consulte [Gerenciar dicas de email para relacionamentos da organização](https://docs.microsoft.com/pt-br/exchange/clients-and-mobile-in-exchange-online/mailtips/manage-mailtips-for-organization-relationships).

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para habilitar ou desabilitar a geração de métricas de grupo


> [!NOTE]
> Por padrão, os dados de métricas de grupo são gerados em qualquer servidor responsável por gerar o catálogo de endereços offline (OAB). Estes exemplos somente são necessários para organizações que não usam OABs.



Para ativar ou desativar a geração de métricas de grupo em um servidor de caixa de correio, execute o seguinte comando:

```powershell
Set-MailboxServer <ServerIdentity> -ForceGroupMetricsGeneration <$true | $false>
```

Este exemplo habilita a geração de métricas de grupo em um servidor de caixa de correio chamado MBX1.

```powershell
Set-MailboxServer MBX1 -ForceGroupMetricsGeneration $true
```

## Como saber se funcionou?

Para verificar que você com êxito habilitada ou desabilitada geração de métricas de grupo em uma organização que não usa OABs, faça o seguinte:

1.  Execute o seguinte comando:
    
    ```powershell
    Get-MailboxServer <ServerIdentity> | Format-List ForceGroupMetricsGeneration
    ```

2.  Verifique se a configuração exibida é a configuração que você configurou.

