---
title: 'Relatórios de auditoria do Exchange: Exchange Online Help'
TOCTitle: Relatórios de auditoria do Exchange
ms:assetid: 2b3e1529-1677-4564-be0b-ce22757ddc0d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150497(v=EXCHG.150)
ms:contentKeyID: 50484671
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Relatórios de auditoria do Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Use o log de auditoria para solucionar problemas de configuração controlando alterações específicas feitas pelos administradores e para ajudar você a atender aos requisitos normativos, de conformidade e de litígio. O Microsoft Exchange fornece dois tipos de log de auditoria:

  - O *log de auditoria de administrador* grava qualquer ação baseada em um cmdlet do Shell de Gerenciamento do Exchange, executado por um administrador. Isso pode ajudá-lo a solucionar problemas de configuração ou identificar a causa de problemas relacionados a segurança ou conformidade. No Exchange Online, as ações realizadas pelos administradores e administradores delegados da Microsoft também são gravadas.

  - O *log de auditoria de caixas de correio* grava quando uma caixa de correio é acessada por um administrador, um usuário delegado ou pelo proprietário da caixa de correio. Isso pode ajudá-lo a determinar quem acessou a caixa de correio e o que a pessoa fez.

Este tópico explica o seguinte:

  - Exportar logs de auditoria

  - Executar relatórios de auditoria

  - Configurar log de auditoria
    
      - Habilitar log de auditoria de caixas de correio
    
      - Fornecer, aos usuários, acesso aos Relatórios de Auditoria
    
      - Configurar o Outlook Web App para permitir anexos de XML

## Exportar logs de auditoria

Na página **Gerenciamento de Conformidade** \> **Auditoria** do Centro de Administração do Exchange (EAC), você pode procurar e exportar entradas do log de auditoria de administrador e do log de auditoria de caixas de correio.

  - **Exportar o log de auditoria de administrador**   Qualquer ação executada por um administrador que seja baseada em um cmdlet do Shell e não começa com os verbos **Get**, **Search** ou **Test** é registrada no log de auditoria de administrador. As entradas do log de auditoria incluem o cmdlet que foi executado, o parâmetro e os valores usados com o cmdlet e quando a operação foi bem-sucedida. Você pode procurar e exportar entradas do log de auditoria de administrador. Quando você exporta os resultados da pesquisa, o Microsoft Exchange os salva em um arquivo XML e os anexa a uma mensagem de email. Para saber mais, confira:
    
      - [Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)
    
      - [Exibir e exportar o log de auditoria do administrador externo](https://technet.microsoft.com/pt-br/library/dn505728\(v=exchg.150\))
    

    > [!TIP]
    > Por padrão, as entradas do log de auditoria são mantidas por 90 dias. Quando uma entrada ultrapassa esses 90 dias, ela é excluída. Essa configuração não pode ser alterada em uma organização baseada em nuvem. Entretanto, ela pode ser alterada em uma organização do Exchange local usando-se o cmdlet <STRONG>Set-AdminAuditLog</STRONG>.



  - **Exportar logs de auditoria de caixa de correio**   Quando o log de auditoria de caixas de correio é habilitado para uma caixa de correio, o Microsoft Exchange armazena um registro de ações executadas nos dados da caixa de correio por não proprietários no log de auditoria de caixas de correio, que é armazenado em uma pasta oculta da caixa de correio que está sendo auditada. O log de auditoria de caixas de correio também pode ser configurado para registrar ações do proprietário. As entradas desse log indicam quem acessou a caixa de correio e quando, as ações executadas e se a ação foi bem-sucedida. Quando você procura entradas no log de auditoria de caixas de correio e as exporta, o Microsoft Exchange salva os resultados da pesquisa em um arquivo XML e o anexa a uma mensagem de email. Para saber mais, configura [Exportar logs de auditoria de caixas de correio](export-mailbox-audit-logs-exchange-2013-help.md).

## Executar relatórios de auditoria

Quando você executa qualquer um dos relatórios a seguir na página **Auditoria**, no EAC, os resultados são exibidos no painel de detalhes do relatório.

  - **Executar um relatório de acesso à caixa de correio de não proprietário**   Utilize este relatório para encontrar caixas de correio que foram acessadas por alguém que não era o proprietário da caixa de correio. Para saber mais, confira [Executar um relatório de acesso não proprietário da caixa de correio](run-a-non-owner-mailbox-access-report-exchange-online-help.md).

  - **Executar um relatório do grupo de funções do administrador:**  Utilize esse relatório para procurar alterações feitas nos grupos de funções do administrador. Para mais informações, consulte [Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

  - **Executar uma descoberta in-loco e relatório de suspensão:**  Utilize este relatório para encontrar caixas de correio que tenham sido colocadas em, ou removidas de, Suspensão no Local. Para mais informações, consulte:
    
      - [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md)
    
      - [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md)

  - **Executar um relatório de suspensão de litigação por caixa de correio**   Utilize este relatório para encontrar caixas de correio que tenham sido colocadas em, ou removidas de, suspensão de litigação. Para saber mais, confira.
    
      - [Executar um relatório de suspensão de litígio por caixa de correio](run-a-per-mailbox-litigation-hold-report-exchange-2013-help.md)
    
      - [Colocar uma caixa de correio em Retenção de Litígio](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - **Executar o relatório de log de auditoria do administrador**   Use este relatório para exibir entradas do log de auditoria do administrador. Em vez de exportar o log de auditoria do administrador, cujo recebimento via mensagem de email pode demorar até 24 horas, você pode executar este relatório no EAC. Este relatório registra as alterações de configuração feitas por administradores em sua organização. Serão exibidas até 5 mil entradas em várias páginas. Para restringir a pesquisa, especifique um intervalo de datas. Para saber mais, confira:
    
      - [Exibir o log de auditoria do administrador](view-the-administrator-audit-log-exchange-2013-help.md)
    
      - [Log de auditoria de administrador](administrator-audit-logging-exchange-2013-help.md)

  - **Executar o relatório de log de auditoria do administrador externo**   Esse relatório só está disponível no Exchange Online e no Proteção do Exchange Online. As ações realizadas pelos administradores e administradores delegados da Microsoft são registradas no log de auditoria do administrador. Use o relatório do log de auditoria do administrador externo para pesquisar e exibir as ações que os administradores de fora de sua organização realizaram na configuração de sua organização do Exchange Online. Para saber mais, confira [Exibir e exportar o log de auditoria do administrador externo](https://technet.microsoft.com/pt-br/library/dn505728\(v=exchg.150\)).

## Configurar log de auditoria

Para poder executar relatórios de auditoria e exportar logs de auditoria, você precisa configurar o log de auditoria para sua organização.

## Habilitar log de auditoria de caixas de correio

Você precisa habilitar o log de auditoria de caixas de correio em cada caixa de correio para a qual desejar executar um relatório de acesso não proprietário. Se o log de auditoria de caixas de correio não for habilitado para uma caixa de correio, você não obterá nenhum resultado ao executar um relatório ou ao exportar o log de auditoria de caixas de correio.

Para habilitar o log de auditoria de caixas de correio para uma única caixa de correio, execute o seguinte comando do Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Para habilitar a auditoria de caixas de correio para todas as caixas de correio de usuário da sua organização, execute os seguintes comandos:

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

Para saber mais sobre como configurar quais ações são registradas em log, confira:

  - **Exchange 2013** [Habilitar ou desabilitar uma caixa de correio do log de auditoria de caixa de correio](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)

  - **Exchange Online**   [Habilitar a auditoria de caixa de correio no Office 365](http://go.microsoft.com/fwlink/p/?linkid=626109)

## Fornecer, aos usuários, acesso aos Relatórios de Auditoria

Por padrão, os administradores podem acessar e executar todos os relatórios da página Auditoria do EAC. No entanto, outros usuários, como o gerente de documentação administrativa ou a equipe jurídica, precisam receber as permissões necessárias.

A maneira mais fácil de fornecer acesso aos usuários é adicioná-los ao grupo de funções Gerenciamento de Registros. Também é possível usar o Shell para fornecer ao usuário o acesso à página **Auditoria** no EAC, atribuindo-lhe a função Logs de Auditoria.

## Adicionar um usuário ao grupo de funções Gerenciamento de Registros

1.  Acesse **Permissões** \> **Funções Administrativas**.

2.  Na lista de grupos de funções, clique em **Gerenciamento de Registros** e em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **Membros**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Na caixa de diálogo **Selecionar Membros**, selecione o usuário. Você pode procurar um usuário digitando todo ou parte do nome de exibição e clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar"). Você também pode classificar a lista clicando nos títulos de coluna **Nome** ou **Nome de Exibição**.

5.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e em **OK** para voltar à página do grupo de funções.

6.  Clique em **Salvar** para salvar as alterações feitas no grupo de funções.

No painel Detalhes, o usuário é listado em **Membros** e pode acessar a página Auditoria no EAC, executar relatórios de auditoria e exportar logs de auditoria.

## Atribuir a função Logs de Auditoria a um usuário

Execute o comando a seguir para atribuir a função Logs de Auditoria a um usuário:

    New-ManagementRoleAssignment -Role "Audit Logs" -User <Identity>

Isso habilita o usuário a selecionar **Gerenciamento de Conformidade** \> **Auditoria** no EAC, para executar qualquer um dos relatórios. O usuário também pode exportar o log de auditoria de caixa de correio e exportar e exibir o log de auditoria do administrador.


> [!TIP]
> Para permitir que um usuário execute relatórios de auditoria, mas não exporte logs de auditoria, use o comando anterior para atribuir a função Logs de Auditoria Somente para Exibição.



## Configurar o Outlook Web App para permitir anexos de XML

Quando você exporta o log de auditoria de caixas de correio ou o log de auditoria de administrador, o Microsoft Exchange anexa o log de auditoria, que é um arquivo XML, a um email. No entanto, o Outlook Web App bloqueia anexos XML por padrão. Se você quiser usar o Outlook Web App para acessar esses logs de auditoria, você terá que configurar o Outlook Web App para permitir anexos em XML.

Execute o comando a seguir para permitir anexos XML no Outlook Web App.

    Set-OwaMailboxPolicy -Identity Default -AllowedFileTypes '.rpmsg','.xlsx','.xlsm','.xlsb','.tiff','.pptx','.pptm','.ppsx','.ppsm','.docx','.docm','.zip','.xls','.wmv','.wma','.wav','.vsd','.txt','.tif','.rtf','.pub','.ppt','.png','.pdf','.one','.mp3','.jpg','.gif','.doc','.bmp','.avi','.xml'

