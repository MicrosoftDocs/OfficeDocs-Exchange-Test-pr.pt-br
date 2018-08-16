---
title: 'Usar o Backup do Windows Server para restaurar um backup do Exchange'
TOCTitle: Usar o Backup do Windows Server para restaurar um backup do Exchange
ms:assetid: 2d0f31dc-eb32-451a-8852-591269026506
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876864(v=EXCHG.150)
ms:contentKeyID: 50485252
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar o Backup do Windows Server para restaurar um backup do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-06-18_

Você pode usar o Backup do Windows Server para fazer backup e restaurar os bancos de dados do Exchange. O Exchange inclui um plugin do Backup do Windows Server, que permite criar e restaurar backups dos dados do Exchange com base no VSS (Serviço de Cópias de Sombra de Volume). Para obter mais informações, consulte [Usar o Backup do Windows Server para fazer backup e restaurar dados do Exchange](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto, mais o tempo que leva para restaurar os dados

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recuperação de caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - O recurso de Backup do Windows Server deve ser instalado no computador local.

  - Ao restaurar um banco de dados para sua localização original, o banco de dados pode permanecer em estado de desligamento anormal e ser montável pelo sistema. Ao restaurar para um local alternativo (por exemplo, na preparação para usar uma recuperação de banco de dados), o banco de dados deve ser colocado manualmente em estado de Desligamento Normal usando os utilitários de banco de dados do Exchange Server (Eseutil.exe).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Backup do Windows Server para restaurar um backup do Exchange

1.  Inicie o Backup do Windows Server.

2.  Selecione **Backup Local**.

3.  No painel Ações, clique em **Recuperar...** para iniciar o Assistente de Recuperação.

4.  Na página **Introdução**, execute um dos seguintes procedimentos:
    
      - Se o backup dos dados que estão sendo recuperados foi feito no servidor local, selecione **Esse servidor (NomeDoServidor)** e clique em **Avançar**.
    
      - Se os dados que estão sendo recuperados forem de outro servidor, ou se o backup que estiver sendo recuperado estiver em outro computador, selecione **Outro servidor** e clique em **Avançar**. Na página **Especificar tipo de local**, selecione **Unidades locais** ou **Pasta compartilhada remota** e clique em **Avançar**. Se selecionar **Unidades locais**, selecione a unidade que contém o backup na página **Selecione um local de backup** e clique em **Avançar**. Na página **Pasta compartilhada remota**, digite o caminho UNC dos dados de backup na página **Especificar pasta remota** e clique em **Avançar**.

5.  Na página **Selecionar Data do Backup**, selecione a data e a hora do backup que deseja recuperar e clique em **Avançar**.

6.  Na página **Selecionar Tipo de Recuperação**, selecione **Aplicativos** e clique em **Avançar**.
    

    > [!NOTE]
    > Se a opção <STRONG>Aplicativos</STRONG> não estiver disponível, isso indica que o backup a ser recuperado era um backup no nível de pasta e não no nível de volume. Você deve realizar backups no nível de volume quando estiver fazendo backup de dados do Exchange com o Backup do Windows Server.



7.  Na página **Selecionar Aplicativo**, verifique se o Exchange está selecionado no campo **Aplicativos**. **Clique para exibir detalhes** e visualizar os componentes de aplicativo dos backups. Se o backup que você estiver recuperando for o mais recente, a caixa de seleção **Não executar uma recuperação com "rolagem para frente" do banco de dados do aplicativo** será exibida. Marque essa caixa de seleção para impedir que o Backup do Windows Server realize o roll-forward do banco de dados que está sendo recuperado confirmando todos os logs de transação não confirmados. Clique em **Avançar**.

8.  Na página **Especificar Opções de Recuperação**, selecione onde deseja recuperar os dados e clique em **Avançar**:
    
      - Escolha **Recuperar para o local original** se desejar restaurar os dados do Exchange diretamente para o local original. Caso utilize essa opção, você não poderá escolher quais bancos de dados serão restaurados. Todos os backups de bancos de dados no volume serão restaurados para seus locais originais.
    
      - Escolha **Recuperar para outro local** se quiser restaurar os bancos de dados individuais e seus arquivos para um local especificado. Clique em **Procurar** para especificar o local alternativo. Caso utilize essa opção, você pode escolher quais bancos de dados serão restaurados. Depois de serem restaurados, os arquivos de dados podem ser movidos para um banco de dados de recuperação, movidos manualmente para o local original ou montados em algum lugar na organização do Exchange usando a [Portabilidade do banco de dados](database-portability-exchange-2013-help.md). Ao restaurar um banco de dados para um local alternativo, o banco de dados restaurado estará no estado de Desligamento Anormal. Depois que o processo de restauração estiver completo, você terá que colocar manualmente o banco de dados em estado de Desligamento Normal usando o Eseutil.exe.

9.  Na página **Confirmação**, revise as configuração de recuperação e clique em **Recuperar**.

10. Na página **Andamento da Recuperação**, você pode visualizar o status e o progresso da operação de recuperação.

11. Clique em **Fechar** quando a operação de recuperação for concluída.

## Como saber se funcionou?

A página **Andamento da Recuperação** indicará se o processo de recuperação foi concluído com êxito. Para verificar se você restaurou os dados com êxito, faça o seguinte:

  - Examine o diretório de destino de backup e verifique se os dados restaurados estão lá.

  - No servidor em que o backup do Windows Server foi executado, verifique se o trabalho foi concluído com êxito, exibindo os logs de backup.

  - Abra o visualizador de eventos e verifique se um evento de conclusão de restauração foi registrado no log de eventos do Aplicativo.

