---
title: 'Gerenciar o administrador do log de auditoria: Exchange 2013 Help'
TOCTitle: Gerenciar o administrador do log de auditoria
ms:assetid: 15c284c0-b8e6-42ca-9913-7c59fdb6885d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335109(v=EXCHG.150)
ms:contentKeyID: 50556147
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar o administrador do log de auditoria

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-05-17_

O Log de Auditoria de Administrador do Microsoft Exchange Server 2013 permite a você criar uma entrada de log sempre que um cmdlet especificado é executado. As entradas de log fornecem informações sobre qual cmdlet foi executado, quais parâmetros foram usados, quem executou o cmdlet e quais objetos foram afetados. Para obter mais informações sobre o registro em log de auditoria do administrador, consulte [Log de auditoria de administrador](administrator-audit-logging-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: menos de 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Registro em log de auditoria do administrador" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - O registro em log da auditoria do administrador depende da replicação do Active Directory para replicar as definições de configuração e especificar os controladores de domínio na organização. Dependendo das configurações de replicação, as alterações feitas talvez não sejam aplicadas imediatamente a todos os servidores do Exchange 2013 em sua organização.

  - As alterações feitas na configuração do log de auditoria são atualizadas a cada 60 minutos em computadores que têm o Shell aberto no momento em que é feita uma alteração na configuração. Se você quiser aplicar as alterações imediatamente, feche e reabra o Shell em cada computador.

  - Um comando pode demorar até 15 minutos após sua execução para aparecer nos resultados de pesquisa do log de auditoria. Isso ocorre porque as entradas do log de auditoria precisam ser indexadas antes de serem pesquisáveis. Se um comando não aparecer no log de auditoria do administrador, aguarde alguns minutos e execute a pesquisa novamente.

  - Você deve usar o Shell para executar estes procedimentos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Especificar os cmdlets a serem auditados

Por padrão, o log de auditoria cria uma entrada de log para cada cmdlet executado. Se você estiver habilitando o log de auditoria pela primeira vez e quiser esse comportamento, não será preciso alterar a lista de auditoria de cmdlet. Se já tiver especificado anteriormente os cmdlets para auditar e agora quiser auditar todos os cmdlets, você poderá auditar todos os cmdlets especificando o caractere curinga de asterisco (\*) com o parâmetro *AdminAuditLogCmdlets* no cmdlet **Set-AdminAuditLogConfig**, conforme exibido no comando a seguir:

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets *

É possível especificar quais cmdlets serão auditados fornecendo uma lista de cmdlets usando o parâmetro *AdminAuditLogCmdlets*. Ao fornecer a lista de cmdlets a serem auditados, você pode indicar cmdlets individuais, cmdlets com caracteres curinga de asterisco(\*) ou uma mistura de ambos. As entradas da lista são separadas por vírgulas. Os seguintes valores são válidos:

  - `New-Mailbox`

  - `*TransportRule`

  - `*Management*`

  - `Set-Transport*`

Este exemplo audita os cmdlets especificados na lista anterior.

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets New-Mailbox, *TransportRule, *Management*, Set-Transport*

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-AdminAuditLogConfig](https://technet.microsoft.com/pt-br/library/dd298169\(v=exchg.150\)).

## Especificar os parâmetros a serem auditados

Por padrão, o log de auditoria cria uma entrada de log para cada cmdlet executado, independente dos parâmetros especificados. Se você estiver habilitando o log de auditoria pela primeira vez e quiser esse comportamento, não será preciso alterar a lista de auditoria do parâmetro. Se já tiver especificado anteriormente os parâmetros para auditar e agora quiser auditar todos os parâmetros, você poderá fazer isso especificando o caractere curinga de asterisco (\*) com o parâmetro *AdminAuditLogParameters* no cmdlet **Set-AdminAuditLogConfig**, conforme exibido no comando a seguir:

    Set-AdminAuditLogConfig -AdminAuditLogParameters *

Você pode especificar que parâmetros deseja auditar usando o parâmetro *AdminAuditLogParameters*. Ao fornecer a lista de parâmetros a serem auditados, você pode indicar parâmetros individuais, parâmetros com caracteres curinga de asterisco (\*) ou uma mistura de ambos. As entradas da lista são separadas por vírgulas. Os seguintes valores são válidos:

  - `Database`

  - `*Address*`

  - `Custom*`

  - `*Region`


> [!TIP]
> Para uma entrada de log de auditoria ser criada quando um comando for executado, o comando deve incluir pelo menos um parâmetro que exista em pelo menos um cmdlet especificado com o parâmetro <EM>AdminAuditLogCmdlets</EM>.



Este exemplo audita os parâmetros especificados na lista anterior.

    Set-AdminAuditLogConfig -AdminAuditLogParameters Database, *Address*, Custom*, *Region

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-AdminAuditLogConfig](https://technet.microsoft.com/pt-br/library/dd298169\(v=exchg.150\)).

## Especificar o limite de idade do log de auditoria

O limite de idade de log de auditoria determina por quanto tempo as entradas de log de auditoria serão mantidas. Quando um arquivo de log exceder o limite de idade, ele será excluído. O padrão é 90 dias.

É possível especificar o número de dias, horas, minutos e segundos que as entradas de log de auditoria devem ser mantidas. Para especificar um valor, utilize o formato dd.hh.mm.ss em que o seguinte se aplica:

  - **dd**   O número de dias que a entrada do log de auditoria será mantida

  - **hh**   O número de horas que a entrada do log de auditoria será mantida

  - **mm**   O número de minutos que a entrada do log de auditoria será mantida

  - **ss**   O número de segundos que a entrada do log de auditoria será mantida


> [!WARNING]
> Você pode definir para o limite de idade do log de auditoria um valor menor do que o limite de idade atual. Se isso for feito, todas as entradas do log de auditoria com idade que excede o novo limite de idade são excluídas.<BR>Se você definir o limite de idade para 0, o Exchange&nbsp;exclui todas as entradas no log de auditoria.<BR>Recomendamos que você conceda permissões de configuração do limite de idade do log de auditoria somente a usuários extremamente confiáveis.



Este exemplo especifica um limite de idade de dois anos e seis meses.

    Set-AdminAuditLogConfig -AdminAuditLogAgeLimit 913.00:00:00

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-AdminAuditLogConfig](https://technet.microsoft.com/pt-br/library/dd298169\(v=exchg.150\)).

## Habilitar ou desabilitar o registro em log de cmdlets Teste

Os cmdlets que começam com o verbo **Test** não são registrados em log por padrão. A razão é que os cmdlets **Test** podem gerar uma quantidade significativa de dados em um curto espaço de tempo. Habilite o registro em log de cmdlets **Test** apenas por períodos curtos de tempo.

Este comando habilita o registro em log de cmdlets **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $True

Este comando desabilita o registro em log de cmdlets **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $False

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-AdminAuditLogConfig](https://technet.microsoft.com/pt-br/library/dd298169\(v=exchg.150\)).

## Desabilitar log de auditoria de administrador

Para desabilitar o log de auditoria de administrador, use o comando a seguir.

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $False

## Habilitar log de auditoria de administrador

Para habilitar o log de auditoria de administrador, use o comando a seguir.

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $True

## Exibir as configurações do log de auditoria de administrador

Para exibir as configurações de log de auditoria do administrador configuradas para sua organização, use o comando a seguir.

    Get-AdminAuditLogConfig

