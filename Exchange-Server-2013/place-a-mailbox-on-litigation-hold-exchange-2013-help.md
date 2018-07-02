---
title: 'Colocar uma caixa de correio em Retenção de Litígio: Exchange Online Help'
TOCTitle: Colocar uma caixa de correio em Retenção de Litígio
ms:assetid: adee4621-3626-4aec-aa53-00b35ff0d0b0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn743673(v=EXCHG.150)
ms:contentKeyID: 62269012
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Colocar uma caixa de correio em Retenção de Litígio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-10-18_

Colocar uma caixa de correio em Retenção de Litígio também preserva todo o conteúdo da caixa de correio, incluindo itens excluídos e versões originais de itens modificados. Ao colocar a caixa de correio de um usuário em Retenção de Litígio, o conteúdo na caixa de correio de arquivo morto do usuário (se habilitada) também é colocado em retenção. Itens excluídos e modificados são preservados por um determinado período, ou até você remover a caixa de correio da Retenção de Litígio. Todos os itens da caixa de correio são retornados em uma pesquisa de [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md).


> [!IMPORTANT]
> A Retenção de Litígio preserva itens na pasta Itens Recuperáveis na caixa de correio do usuário. Dependendo da quantidade e do tamanho dos itens excluídos ou modificados, o tamanho da pasta Itens Recuperáveis da caixa de correio pode aumentar rapidamente. A pasta Itens Recuperáveis está configurada com uma cota alta por padrão. No Exchange Online, essa cota é aumentada automaticamente quando você coloca uma caixa de correio em Retenção de Litígio. No Exchange Server 2013, recomendamos que você monitore as caixas de correio colocadas em Retenção de Litígio semanalmente para garantir que não atinjam os limites de cotas de Itens Recuperáveis.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - A configuração de Retenção de Litígio pode demorar até 60 minutos para entrar em vigor.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Bloqueio In-loco" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para colocar uma caixa de correio do Exchange Online em Retenção de Litígio, ela deve ter uma licença do Exchange Online (Plano 2). Se uma caixa de correio tiver uma licença do Exchange Online (Plano 1), seria preciso atribuir uma licença separada de arquivamento do Exchange Online para colocá-la em retenção.

  - Conforme explicado anteriormente, ao colocar a caixa de correio de um usuário em Retenção de Litígio, o conteúdo na caixa de correio de arquivo morto do usuário também é colocado em retenção. Se você colocar uma caixa de correio principal local em Retenção de Litígio em uma implantação híbrida do Exchange, a caixa de correio de arquivo morto baseada na nuvem (se estiver habilitada) também será colocada em retenção.

  - No Exchange Online, a cota da pasta Itens recuperáveis é automaticamente aumentada para 100 GB quando você coloca uma caixa de correio em Retenção de Litígio. O tamanho padrão dessa pasta é 30 GB.

  - A Retenção de Litígio preserva os itens excluídos e também versões originais de itens modificados até que a retenção seja removida. Opcionalmente, você pode especificar uma duração da retenção, que preserva um item da caixa de correio pelo período de tempo especificado. Se você especificar um período de duração para a retenção, ele é calculado a partir da data que uma mensagem é recebida ou que um item da caixa de correio é criado. Para preservar os itens que atendem aos critérios especificados, use um Bloqueio In-loco para criar uma retenção *baseada em consulta*. Para saber mais, confira [Criar ou remover um bloqueio In-loco](create-or-remove-an-in-place-hold-exchange-2013-help.md).

  - Para usar o Shell para colocar uma caixa de correio do Exchange Online em retenção, você deve usar o Exchange Online PowerShell. Para saber mais, confira [Conectar-se ao Exchange Online usando o PowerShell Remoto](https://technet.microsoft.com/pt-br/library/jj984289\(v=exchg.150\)).

  - Não há suporte para colocar uma Retenção de Litígio em uma caixa de correio de pasta pública. Você precisa usar o Bloqueio In-loco para colocar uma retenção em pastas públicas.

## Usar o EAC para colocar uma caixa de correio em retenção de litígio

1.  Acesse **Destinatários** \> **Caixas de Correio**.

2.  Na lista de caixas de correio de usuários, clique na caixa de correio para a qual você deseja habilitar ou desabilitar a Retenção de Litígio e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades da caixa de correio, clique em **Recursos da Caixa de Correio**.

4.  Em **Retenção de Litígio: Desativado**, clique em **Habilitar** para colocar a caixa de correio em Retenção de Litígio.

5.  Na página **de Litígio**, insira as seguintes informações opcionais.
    
      - **Duração da retenção de litígio (dias)**   Use esta caixa para especificar por quanto tempo os itens da caixa de correio devem ser mantidos quando esta estiver em Retenção de Litígio. A duração é calculada a partir da data em que um item de caixa de correio é recebido ou criado. Se você deixar esta caixa em branco, os itens serão mantidos indefinidamente ou até que a retenção seja removida. Use dias para especificar a duração.
    
      - **Observação**   Use esta caixa para informar o usuário que sua caixa de correio está em Retenção de Litígio. A nota aparecerá na caixa de correio do usuário se ele estiver usando o Outlook 2010 ou posterior.
    
      - **URL**   Use esta caixa para direcionar o usuário a um site para saber mais sobre a Retenção de Litígio. Esta URL aparece na caixa de correio do usuário se ele estiver usando o Outlook 2010 ou posterior.

6.  Clique em **Salvar** na página **Retenção de Litígio** e, em seguida, clique em **Salvar** na página de propriedades da caixa de correio.

Voltar ao início

## Usar o Shell para colocar uma caixa de correio em Retenção de Litígio indefinidamente

Este exemplo coloca a caixa de correio bsuneja@contoso.com em Retenção de Litígio. Os itens na caixa de correio serão retidos indefinidamente ou até que a retenção seja removida.

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true


> [!TIP]
> Quando você coloca uma caixa de correio em retenção de litígio indefinidamente (ao não especificar um período de duração), o valor da propriedade <EM>LitigationHoldDuration</EM> é definido como <CODE>Unlimited</CODE>.



## Usar o Shell para colocar uma caixa de correio em Retenção de Litígio e preservar itens por um período específico

Este exemplo coloca a caixa de correio bsuneja@contoso.com em Retenção de Litígio e preserva itens por 2555 dias (aproximadamente sete anos).

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true -LitigationHoldDuration 2555

## Usar o Shell para colocar todas as caixas de correio em Retenção de Litígio por um período específico

A sua organização pode exigir que todos os dados de caixas de correio sejam preservados durante um período específico. Antes de colocar todas as caixas de correio de uma organização em Retenção de Litígio, considere o seguinte:

Este exemplo coloca todas as caixas de correio de usuários na organização em Retenção de Litígio por um ano (365 dias).

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 365

O exemplo usa o cmdlet [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\))para recuperar todas as caixas de correio na organização, especifica um filtro de destinatários para incluir todas as caixas de correio de usuários e, então, envia essa lista ao cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) para ativar a Retenção de Litígio e definir a duração da retenção.

Para aplicar uma retenção indefinida a todas as caixas de correio de usuários, execute o comando anterior, mas não inclua o parâmetro *LitigationHoldDuration*.

Consulte a seção Mais informações para obter exemplos de como usar outras propriedades de destinatários em um filtro para incluir ou excluir uma ou mais caixas de correio.

## Usar o Shell para remover a Retenção de Litígio de uma caixa de correio

Este exemplo remove a Retenção de Litígio da caixa de correio bsuneja@contoso.com.

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $false

Voltar ao início

## Como saber se funcionou?

Para verificar se você aplicou com sucesso a Retenção de Litígio em uma caixa de correio, faça um dos seguintes:

  - No EAC:
    
    1.  Acesse **Destinatários** \> **Caixas de Correio**.
    
    2.  Na lista de caixas de correio de usuários, clique na caixa de correio para a qual deseja verificar as configurações de Retenção de Litígio e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    
    3.  Na página de propriedades da caixa de correio, clique em **Recursos da Caixa de Correio**.
    
    4.  Em **Retenção de Litígio**, verifique se a retenção está habilitada.
    
    5.  Clique em **Exibir detalhes** para verificar quando a caixa de correio foi colocada em retenção de litígio e por quem. Você também pode verificar ou alterar os valores nas caixas opcionais **Duração da retenção de litígio (dias)**, **Observação** e **URL**.

  - No Shell, execute um destes comandos:
    
        Get-Mailbox <name of mailbox> | FL LitigationHold*
    
    ou
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | FL Name,LitigationHold*
    
    Se uma caixa de correio é colocada em Retenção de Litígio indefinidamente, o valor da propriedade *LitigationHoldDuration* é definido como `Unlimited`.

## Mais informações

  - Se sua organização exige que todos os dados da caixa de correio sejam preservados por um período específico de tempo, considere o seguinte antes de colocar todas as caixas de correio da organização em retenção de litígio.
    
      - Quando você usa o comando anterior para colocar uma retenção em todas as caixas de correio em uma organização (ou um subconjunto de caixas de correio que correspondem a um filtro de destinatário especificado) somente caixas de correio que existem no momento em que você executar o comando são colocadas em retenção. Se você criar novas caixas de correio posteriormente, execute o comando mais uma vez para colocá-las em retenção. Caso crie novas caixas de correio com frequência, você pode executar o comando como uma tarefa agendada com a frequência necessária.
    
      - Colocar todas as caixas de correio em Retenção de Litígio pode impactar significativamente os tamanhos das caixas de correio. Em uma organização do Exchange Server 2013, planeje o armazenamento adequado para atender aos requisitos de preservação da sua organização.
    
      - A pasta Itens Recuperáveis tem seu próprio limite de armazenamento para que itens na pasta não contem para o limite de armazenamento da caixa de correio. Conforme explicado anteriormente, preservar dados de caixa de correio por um longo período resultará no crescimento da pasta Itens Recuperáveis na caixa de correio e no arquivo morto do usuário. Para acomodar esse aumento no Exchange Online, a cota da pasta Itens recuperáveis é automaticamente aumentada de 30 GB para 100 GB quando você coloca uma caixa de correio em Retenção de Litígio.
        
        No Exchange Server 2013, o limite de armazenamento padrão da pasta Itens Recuperáveis também é de 30 GB. Recomendamos que monitore periodicamente o tamanho desta pasta para garantir que não atinja o limite. Para saber mais, confira [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

  - O comando anterior coloca uma retenção em todas as caixas de correio usando um filtro de destinatário que retorna todas as caixas de correio. Você pode usar outras propriedades de destinatário para obter uma lista de caixas de correio específicas, que você pode, então, enviar ao cmdlet **Set-Mailbox** para colocar uma Retenção de Litígio nessas caixas de correio.
    
    Eis alguns exemplos de usar os cmdlets **Get-Mailbox** e **Get-Recipient** para obter um subconjunto de caixas de correio com base em propriedades de usuário ou de caixa de correio comuns. Esses exemplos supõem que as propriedades de caixa de correio relevantes (como *CustomAttributeN* ou *Department*) foram preenchidas.
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    
    Você pode usar outras propriedades de caixa de correio em um filtro para incluir ou excluir caixas de correio. Para saber mais, confira [Propriedades filtráveis para o parâmetro -Filter](https://technet.microsoft.com/pt-br/library/bb738155\(v=exchg.150\)).

Voltar ao início

