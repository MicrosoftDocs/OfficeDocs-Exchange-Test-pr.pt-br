---
title: 'Usar o Backup do Windows Server para fazer o backup do Exchange: Exchange 2013 Help'
TOCTitle: Usar o Backup do Windows Server para fazer o backup do Exchange
ms:assetid: 188a8291-0a41-4ca2-b6d2-94242e2b1ffc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876854(v=EXCHG.150)
ms:contentKeyID: 50485025
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar o Backup do Windows Server para fazer o backup do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-06-18_

Você pode usar o Backup do Windows Server para fazer backup e restaurar os bancos de dados do Exchange. O Exchange inclui um plugin para o Backup do Windows Server que permite fazer backups dos dados do Exchange com base no VSS (Serviço de Cópias de Sombra de Volume).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto, mais o tempo que leva para fazer backup dos dados

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recuperação da caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - O recurso de Backup do Windows Server deve ser instalado no computador local.

  - Durante a operação de backup, uma verificação de consistência dos arquivos de dados do Exchange é executada para se ter certeza de que os arquivos estejam em bom estado e possam ser usados para recuperação. Se a verificação de consistência for feita com êxito, os dados do Exchange estarão disponíveis para recuperação a partir do backup. Se a verificação de consistência falhar, os dados do Exchange não estarão disponíveis para recuperação. O Backup do Windows Server realiza a verificação de consistência no instantâneo capturado para o backup. Como resultado, antes de copiar arquivos do instantâneo para a mídia de backup, a consistência do backup é conhecida, e o usuário é notificado dos resultados da verificação de consistência.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Backup do Windows Server para fazer o backup do Exchange

1.  Inicie o Backup do Windows Server.

2.  Selecione **Backup Local**.

3.  No painel Ações, clique em **Backup Único...** para iniciar o Assistente de Backup Único.

4.  Na página **Opções de Backup**, selecione **Opções diferentes** e clique em **Avançar**.

5.  Na página **Selecionar Configuração de Backup**, selecione **Personalizado** e clique em **Avançar**.

6.  Na página **Selecionar Itens para Backup**, clique em **Adicionar Itens** para selecionar o(s) volume(s) em que será feito o backup e clique em **OK**.
    

    > [!TIP]
    > Escolha os volumes e não pastas individuais. A única maneira de realizar um backup ou uma restauração no nível de aplicativo é selecionando um volume inteiro.



7.  Clique em **Configurações Avançadas**. Na guia **Exclusões**, clique em **Adicionar Exclusão** para adicionar arquivos ou tipos de arquivos que você deseja excluir do backup.
    

    > [!TIP]
    > Por padrão, os volumes que contêm componentes ou aplicativos do sistema operacional são incluídos no backup e não podem ser excluídos.



8.  Na guia **Configurações de VSS**, selecione **Backup completo VSS**, clique em **OK** e em **Avançar**.

9.  Na página **Especificar Tipo de Destino**, selecione o local em que deseja armazenar o backup e clique em **Avançar**.
    
      - Se você escolher **Unidades locais**, a página **Selecionar Destino do Backup** será exibida. Selecione uma opção na lista suspensa **Destino de Backup** e clique em **Avançar**.
    
      - Se você escolher **Pasta compartilhada remota**, a página **Especificar Pasta Remota** será exibida. Especifique um caminho UNC para os arquivos de backup, defina as configurações de controle de acesso. Escolha **Não herdar** se quiser que o backup esteja acessível somente através de uma conta específica. Forneça um nome de usuário e uma senha para uma conta que tenha permissões para gravação no computador que hospeda a pasta remota e clique em **OK**. Como alternativa, escolha **Herdar** se quiser que o backup esteja acessível para todos que tenham acesso à pasta remota. Clique em **Avançar**.

10. Na página **Confirmação**, verifique as configurações de backup e clique em **Backup**.

11. Na página **Progresso do Backup**, você pode visualizar o status e o progresso da operação de backup.

12. Clique em **Fechar** para sair da página **Progresso do Backup** a qualquer momento. Qualquer backup em andamento continuará a ser executado em segundo plano.

## Como saber se funcionou?

Para verificar se você fez o backup dos dados com êxito, faça o seguinte:

  - No servidor em que estava sendo executado o Backup do Windows Server, o último status de backup será exibido e deve mostrar a mensagem Êxito. Você também pode verificar se o backup foi concluído com êxito visualizando os logs do Backup do Windows Server.

  - Abra o Visualizador de Eventos e verifique se um evento de conclusão de backup foi registrado no log de eventos do Aplicativo.

  - Execute o seguinte comando no Shell de Gerenciamento do Exchange para verificar se cada banco de dados no volume selecionado teve o backup realizado com êxito:
    
        Get-MailboxDatabase -Server <ServerName> -Status | fl Name,*FullBackup
    
    As propriedades *SnapshotLastFullBackup* e *LastFullBackup* do banco de dados indicam quando o último backup bem-sucedido foi feito e se foi um backup VSS completo.

