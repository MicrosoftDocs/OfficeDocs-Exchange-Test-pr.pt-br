---
title: 'Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador: Exchange 2013 Help'
TOCTitle: Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador
ms:assetid: c7188d53-e672-492b-b57d-cd711379ddb3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff459262(v=EXCHG.150)
ms:contentKeyID: 50556118
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2013-12-02_

Você pode pesquisar os logs de auditoria do administrador para descobrir quem efetuou alterações na organização, no servidor e na configuração de destinatário. Isso pode ser útil quando se tenta acompanhar a causa do comportamento inesperado, para identificar um administrador malicioso ou verificar se os requisitos de conformidade estão sendo atendidos. Para obter mais informações sobre o registro em log de auditoria do administrador, consulte [Log de auditoria de administrador](administrator-audit-logging-exchange-2013-help.md).

Se quiser pesquisar no log de auditoria de caixa de correio, consulte [Registro em log de auditoria da caixa de correio](mailbox-audit-logging-exchange-2013-help.md).


> [!TIP]
> No Exchange Online, você pode usar o EAC para ver as entradas no log de ​​auditoria do administrador. Para obter mais informações, consulte <A href="view-the-administrator-audit-log-exchange-2013-help.md">Exibir o log de auditoria do administrador</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: menos de 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Registro em log de auditoria do administrador somente leitura" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - O log de auditoria do administrador vem habilitado por padrão. Para verificar se ele está habilitado, execute o seguinte comando:
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    O valor `True` indica que o log de auditoria de administrador está habilitado. O valor `False` indica que ele está desabilitado. Se precisar habilitar o log de auditoria de administrador para uma organização Exchange local, execute este comando:
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $true
    

    > [!TIP]
    > O cmdlet <STRONG>Set-AdminAuditLogConfig</STRONG> não está disponível no Exchange Online.

    
    Para obter mais informações, consulte [Gerenciar o administrador do log de auditoria](manage-administrator-audit-logging-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para executar o relatório de alterações de grupo de função de gerenciamento

Se quiser saber quais alterações a associação do grupo de funções de gerenciamento efetuou nos grupos de funções em sua organização, você poderá usar o relatório Alterações de Função do Administrador no Centro de Administração do Exchange (EAC). Usando o relatório de Grupo de Função do Administrador, você pode exibir uma lista de grupos de funções que sofreram alterações durante um intervalo de datas específico. Também é possível selecionar os grupos de funções específicos dos quais deseja exibir as alterações.

1.  No EAC, selecione **Gerenciamento de conformidade** \> **Auditoria** e clique em **Executar o Relatório do Grupo de Funções do Administrador**.

2.  Selecione um intervalo de datas usando os campos **Data de Início** e **Data de Término**.

3.  Clique em **Selecionar grupos de função** e selecione os grupos de função para os quais você deseja mostrar as alterações ou deixe esse campo em branco, para pesquisar alterações em todos os grupos de funções.

4.  Clique em **Pesquisar**.

Se alguma alteração for encontrada com o uso dos critérios especificados, uma lista de alterações será exibida no painel de resultados. Clicar em um grupo de funções exibe as alterações efetuadas no grupo de funções no painel de detalhes.

## Usar o EAC para exportar o log de auditoria de administrador

Se quiser criar um arquivo XML que contenha as alterações efetuadas em sua organização, você poderá usar o relatório Exportar Log de Auditoria de Administrador, no EAC. Usando o relatório Exportar Log de Auditoria de Administrador, você pode especificar um intervalo de datas para pesquisar entradas de log de auditoria que contenham as alterações efetuadas pelos usuários especificados. O arquivo XML é enviado a um destinatário como anexo de email. O tamanho máximo do arquivo XML é de 10 MB.


> [!TIP]
> O Outlook Web App não permite que você abra anexos XML por padrão. O Exchange pode ser configurado para permitir que os anexos XML sejam visualizados usando o Outlook Web App, ou você pode usar outro cliente de email, como o Microsoft Outlook, para exibir o anexo. Para saber mais sobre como configurar o Outlook Web App para permitir a exibição de um anexo XML, confira <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Exibir ou configurar diretórios virtuais do Outlook Web App</A>.



1.  No EAC, selecione **Gerenciamento de conformidade** \> **Auditoria** e clique em **Exportar o log de auditoria do administrador**.

2.  Selecione um intervalo de datas usando os campos **Data de Início** e **Data de Término**.

3.  No campo **Enviar o relatório de auditoria para**, clique em **Selecionar usuários** e selecione o destinatário para o qual você deseja enviar o relatório.

4.  Clique em **Exportar**.

Se alguma entrada de log for encontrada com o uso dos critérios especificados, um arquivo XML será criado e enviado como anexo de email ao destinatário especificado.

## Usar o Shell para pesquisar entradas de log de auditoria

Não é possível usar o Shell para pesquisar entradas de log de auditoria que atendam aos critérios especificados. Para obter uma lista de critérios de pesquisa, consulte [Log de auditoria de administrador](administrator-audit-logging-exchange-2013-help.md). Esse procedimento usa o cmdlet **Search-AdminAuditLog** e exibe os resultados da pesquisa no Shell. Ele pode ser usado quando você precisa retornar um conjunto de resultados que exceda os limites definidos no cmdlet **New-AdminAuditLogSearch** ou nos Relatórios de Auditoria do EAC.

Se quiser enviar resultados da pesquisa de log de auditoria em um anexo de email a um destinatário, consulte Use the Shell to search for audit log entries and send results to a recipient mais adiante neste tópico.

Para pesquisar no log de auditoria pelos critérios especificados, use a sintaxe a seguir.

    Search-AdminAuditLog - Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False >


> [!TIP]
> O cmdlet <STRONG>Search-AdminAuditLog</STRONG> retorna um máximo de 1.000 entradas de log por padrão. Use o parâmetro <EM>ResultSize</EM> para especificar até 250.000 entradas de log. Ou use o valor <CODE>Unlimited</CODE> para retornar todas as entradas.



Esse exemplo realiza uma pesquisa em todas as entradas de log de auditoria com os seguintes critérios:

  - **Data de início**   04.08.12

  - **Data de término**   03.10.12

  - **IDs de Usuário**   davids, chrisd, kima

  - **Cmdlets**   **Set-Mailbox**

  - **Parâmetros**   *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

<!-- end list -->

    Search-AdminAuditLog -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima

Este exemplo pesquisa alterações efetuadas em uma caixa de correio específica. Isso será útil se você estiver solucionando problemas ou precisar fornecer informações para uma investigação. Os seguintes critérios são usados:

  - **Data de início**   01.05.12

  - **Data de término**   03.10.12

  - **ID de Objeto**   contoso.com/Users/DavidS

<!-- end list -->

    Search-AdminAuditLog -StartDate 05/01/2012 -EndDate 10/03/2012 -ObjectID contoso.com/Users/DavidS

Caso as suas pesquisas retornem muitas entradas de log, recomendamos usar o procedimento fornecido em Use the Shell to search for audit log entries and send results to a recipient mais adiante neste tópico. O procedimento dessa seção envia um arquivo XML como anexo de email aos destinatários especificados, permitindo que você extraia com mais facilidade os dados em que está interessado.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Search-AdminAuditLog](https://technet.microsoft.com/pt-br/library/ff459250\(v=exchg.150\)).

## Exibir detalhes de entradas de log de auditoria

O cmdlet **Search-AdminAuditLog** retorna os campos descritos na seção "Conteúdo do log de auditoria" de [Log de auditoria de administrador](administrator-audit-logging-exchange-2013-help.md). Desses campos retornados pelo cmdlet, dois campos, **CmdletParameters** e **ModifiedProperties**, contêm informações adicionais que não podem ser exibidas por padrão.

Para exibir o conteúdo dos campos **CmdletParameters** e **ModifiedProperties**, siga as etapas na sequência. Ou use o procedimento descrito em Use the Shell to search for audit log entries and send results to a recipient mais adiante neste tópico para criar um arquivo XML.

Esse procedimento usa os seguintes conceitos:

  - [Matrizes](https://technet.microsoft.com/pt-br/library/aa998267\(v=exchg.150\))

  - [Variáveis definidas pelo usuário](https://technet.microsoft.com/pt-br/library/bb123690\(v=exchg.150\))

<!-- end list -->

1.  Decida quais critérios deseja pesquisa, execute o cmdlet **Search-AdminAuditLog** e armazene os resultados em uma variável usando o seguinte comando.
    
        $Results = Search-AdminAuditLog <search criteria>

2.  Cada entrada de log de auditoria é armazenada como um elemento de matriz na variável `$Results`. Você pode selecionar um elemento de matriz especificando seu índice de elemento de matriz. Os índices de elemento de matriz começam em zero (0) para o primeiro elemento da matriz. Por exemplo, para recuperar o elemento da quinta matriz, que tem um índice de 4, use o comando a seguir.
    
        $Results[4]

3.  O comando anterior retorna a entrada de log armazenada no elemento de matriz 4. Para ver o conteúdo dos campos **CmdletParameters** e **ModifiedProperties** referentes a essa entrada de log, use os seguintes comandos.
    
        $Results[4].CmdletParameters
        $Results[4].ModifiedProperties

4.  Para exibir o conteúdo dos campos **CmdletParameters** ou **ModifiedParameters** em outra entrada de log, altere o índice do elemento de matriz.

## Usar o Shell para pesquisar entradas de log de auditoria e enviar resultados a um destinatário

Não é possível usar o Shell para pesquisar entradas de log de auditoria que atendam aos critérios especificados e depois enviar os resultados a um destinatário que você especifica como um anexo de arquivo XML. Os resultados são enviados ao destinatário em 15 minutos. Para obter uma lista de critérios de pesquisa, consulte [Log de auditoria de administrador](administrator-audit-logging-exchange-2013-help.md).


> [!TIP]
> O Outlook Web App não permite que você abra anexos XML por padrão. O Exchange pode ser configurado para permitir que os anexos XML sejam visualizados usando o Outlook Web App, ou você pode usar outro cliente de email, como o Microsoft Outlook, para exibir o anexo. Para saber mais sobre como configurar o Outlook Web App para permitir a exibição de um anexo XML, confira <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Exibir ou configurar diretórios virtuais do Outlook Web App</A>.



Para pesquisar no log de auditoria pelos critérios especificados, use a sintaxe a seguir.

    New-AdminAuditLogSearch -Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False > -StatusMailRecipients <recipient 1, recipient 2, ...> -Name <string to include in subject>

Esse exemplo realiza uma pesquisa em todas as entradas de log de auditoria com os seguintes critérios:

  - **Data de início**   04.08.12

  - **Data de término**   03.10.12

  - **IDs de Usuário**   davids, chrisd, kima

  - **Cmdlets**   **Set-Mailbox**

  - **Parâmetros**   *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

O comando envia os resultados para o endereço SMTP davids@contoso.com, com "Alterações de limite da caixa de correio" incluso na linha de assunto da mensagem.

    New-AdminAuditLogSearch -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima -StatusMailRecipients davids@contoso.com -Name "Mailbox limit changes"


> [!TIP]
> O relatório que o cmdlet <STRONG>New-AdminAuditLogSearch</STRONG> gera pode ter tamanho máximo de 10 MB. Se a pesquisa feita retornar um relatório maior do que 10 MB, altere os critérios de pesquisa especificados. Por exemplo, reduza o tamanho do intervalo de datas e execute vários relatórios, cada um com uma parte do intervalo de datas original.



Para mais informações sobre o formato do arquivo XML, consulte [Estrutura de log de auditoria do administrador](administrator-audit-log-structure-exchange-2013-help.md).

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-AdminAuditLogSearch](https://technet.microsoft.com/pt-br/library/ff459243\(v=exchg.150\)).

