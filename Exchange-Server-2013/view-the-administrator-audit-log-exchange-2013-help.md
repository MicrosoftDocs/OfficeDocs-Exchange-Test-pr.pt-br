---
title: 'Exibir o log de auditoria do administrador: Exchange Online Protection Help'
TOCTitle: Exibir o log de auditoria do administrador
ms:assetid: 5c62072a-556d-4fea-9973-d668c6b9fd57
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn342832(v=EXCHG.150)
ms:contentKeyID: 56270406
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir o log de auditoria do administrador

 

_**Aplica-se a:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Tópico modificado em:**2016-05-03_

No Microsoft Proteção do Exchange Online (EOP), Microsoft Exchange Online e Microsoft Exchange 2013, você pode usar o Centro de administração do Exchange (EAC) para pesquisar e exibir entradas no *log de auditoria do administrador*. As ações específicas dos registros do log de auditoria do administrador, com base no cmdlet Shell de Gerenciamento do Exchange, realizadas por administradores e usuários aos quais tenham sido atribuídos privilégios administrativos. Entradas no log de auditoria do administrador fornecem informações sobre qual cmdlet foi executado, quais parâmetros foram usados, quem executou o cmdlet e quais objetos foram afetados.


> [!TIP]
> <UL>
> <LI>
> <P>O log de auditoria do administrador está habilitado por padrão.</P>
> <LI>
> <P>O log de auditoria do administrador não registra qualquer ação baseada em um cmdlet Shell de Gerenciamento do Exchange que comece com os verbos <STRONG>Get</STRONG>, <STRONG>Search</STRONG> ou <STRONG>Test</STRONG>.</P>
> <LI>
> <P>As entradas do log de auditoria são mantidas por 90 dias. Quando uma entrada ultrapassa os 90 dias, ela é excluída.</P></LI></UL>



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Exibir relatórios" no tópico [Permissões de recurso no EOP](https://technet.microsoft.com/pt-br/library/jj723125\(v=exchg.150\)).

  - Como foi mencionado anteriormente, o log de auditoria do administrador está habilitado por padrão. Para verificar se ele está habilitado, você pode executar o comando a seguir.
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    No Exchange 2013, você pode habilitar o log de auditoria do administrador se não estiver desabilitado executando o comando a seguir.
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
    
    No Proteção do Exchange Online e no Exchange Online, o log de auditoria do administrador está sempre habilitado. Ele não pode ser desabilitado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para exibir o log de auditoria do administrador

1.  No EAC, vá até **Gerenciamento de Conformidade** \> **Auditoria** e selecione **Executar o registro do log de auditoria do administrador**.

2.  Escolha uma **Data de início** e uma **Data de término** e então selecione **Pesquisar**. Todas as alterações de configuração feitas durante o período especificado são exibidas e podem ser classificadas com as seguintes informações:
    
      - **Data**   A data e a hora da alteração da configuração. A data e a hora são armazenadas no formato UTC (Tempo Universal Coordenado).
    
      - **Cmdlet** O nome do cmdlet que foi usado para alterar a configuração.
    
      - **Usuário**   O nome da conta do usuário que fez a alteração de configuração.
    
    Serão exibidas até 5.000 entradas em várias páginas. Especifique um intervalo de datas menor se precisar restringir os resultados. Se você selecionar um resultado de pesquisa individual, as informações a seguir serão exibidas no painel de detalhes:
    
      - **Objeto modificado** O objeto que foi modificado pelo cmdlet.
    
      - **Parâmetros (Parameter:Value)**   Os parâmetros de cmdlet que foram usados e qualquer valor especificado com o parâmetro.

3.  Se quiser imprimir uma determinada entrada do log de auditoria, selecione o botão **Imprimir** no painel de detalhes.

## Como verifico se isso funcionou?

Se tiver executado com êxito um relatório de log de auditoria do administrador, as alterações de configuração feitas durante o intervalo de datas especificado serão mostradas no painel de resultados de pesquisa. Se não houver resultados, altere o intervalo de datas e execute o relatório outra vez.


> [!TIP]
> Quando uma alteração é feita na sua organização, pode demorar até 15 minutos para que ela apareça nos resultados de pesquisa do log de auditoria. Se uma alteração não aparecer no log de auditoria do administrador, espere alguns minutos e execute a pesquisa novamente.


