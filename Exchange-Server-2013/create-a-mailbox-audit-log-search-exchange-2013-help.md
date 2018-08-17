---
title: 'Criar uma pesquisa de log de auditoria de caixas de correio'
TOCTitle: Criar uma pesquisa de log de auditoria de caixas de correio
ms:assetid: 48ba22cf-b1f2-4dbc-98fc-fed22d97db14
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff461929(v=EXCHG.150)
ms:contentKeyID: 50485478
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma pesquisa de log de auditoria de caixas de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-11_

Você pode criar uma pesquisa de log de auditoria de caixa de correio para pesquisar uma ou mais caixas de correio de forma assíncrona e enviar os resultados da busca por email como um arquivo XML para endereços especificados.

Para pesquisar logs de auditoria de caixa de correio em uma única caixa de correio e exibir os resultados no Shell, consulte [Pesquisar o log de auditoria de caixa de correio para uma caixa de correio](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas ao log de auditoria de caixa de correio, consulte [Procedimentos de registro em log de auditoria de caixa de correio](mailbox-audit-logging-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Log de auditoria de caixas de correio" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Por padrão, o registro em log de auditoria de caixa de correio está desabilitado para todas as caixas de correio. Para cada caixa de correio que deseja auditorar, você deve habilitar o registro em log de auditoria e especificar as ações do proprietário, delegado ou administrador da caixa de correio que será auditada. Para obter mais detalhes, consulte [Habilitar ou desabilitar uma caixa de correio do log de auditoria de caixa de correio](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

  - Você não pode usar o EAC para pesquisar os logs de auditoria de caixa de correio para acesso de proprietário. A seção de auditoria no EAC inclui relatórios para acesso à caixa de correio por não proprietários e também permite que você procure por e exporte os eventos de acesso a não proprietários.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para criar uma pesquisa de log de auditoria de caixa de correio

1.  Navegue até **Gerenciamento de conformidade** \> **Auditoria**.

2.  No modo de exibição de lista, selecione **Exportar logs de auditoria de caixa de correio**.

3.  Em **Exportar logs de auditoria de caixa de correio**, preencha os campos a seguir e clique em **Exportar**:
    
      - **Data de início**
    
      - **Data de término**
    
      - **Pesquisar essas caixas de correio ou deixar em banco, para encontrar todas as caixas de correio acessadas por não proprietários**
        

        > [!CAUTION]
        > Dependendo do número de caixas de correio na sua organização e a quantidade de dados de log de auditoria de caixa de correio em cada caixa de correio, pesquisar todas as caixas de correio pode demorar muito.

    
      - **Buscar acesso por**
        
        Selecione os seguintes tipos de eventos de acesso que você deseja pesquisar:
        
          - **Todos os não proprietários**
        
          - **Usuários externos**
        
          - **Administradores e usuários delegados**
        
          - **Administradores**
    
      - **Enviar o relatório de auditoria para**

## Usar o Shell para criar uma pesquisa de log de auditoria de caixa de correio

Para um exemplo de como usar o Shell para criar uma pesquisa de log de auditoria de caixa de correio, consulte o [Example 1](https://technet.microsoft.com/pt-br/95365cab-bbb2-4a64-8e8f-1c89fa9e0352\(exchg.150\)#example1) em **New-MailboxAuditLogSearch**.

