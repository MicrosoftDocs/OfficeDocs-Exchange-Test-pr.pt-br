---
title: 'Restaurar pastas públicas e cxs. de corr. de pasta pública de movim. com falha'
TOCTitle: Restaurar pastas públicas e caixas de correio de pasta pública de movimentações com falha
ms:assetid: 2ade83c9-5f9b-4945-bf32-48fa8185b515
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ983802(v=EXCHG.150)
ms:contentKeyID: 52058807
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Restaurar pastas públicas e caixas de correio de pasta pública de movimentações com falha

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-13_

Se uma solicitação de movimentação para uma pasta pública ou caixa de correio de pasta pública falhar, você poderá restaurar a pasta ou caixa de correio contanto que as seguintes condições se apliquem:

  - **Falha na movimentação de pasta pública**   Ainda há uma cópia excluída com possibilidade de reversão da pasta pública na caixa de correio da pasta pública de origem e ainda está dentro do período de retenção.

  - **Falha na movimentação da caixa de correio de pasta pública**   Ainda há uma cópia excluída com possibilidade de reversão da caixa de correio da pasta pública no banco de dados da caixa de correio de origem e ainda está dentro do período de retenção da caixa de correio.

Se o período de retenção da caixa de correio tiver passado, você poderá recuperar uma caixa de correio de pasta pública individual a partir do backup. Em seguida, extraia dados da caixa de correio restaurada e copie-os para uma pasta de destino ou mescle-os com outra caixa de correio. Para obter mais informações, consulte [Restaurar dados usando um banco de dados de recuperação](restore-data-using-a-recovery-database-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Solicitação de restauração de caixa de correio", no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - O EAC não pode ser usado para esse procedimento. É necessário usar o Shell.

  - Para criar uma solicitação de restauração, é necessário fornecer os valores para os parâmetros *DisplayName*, *LegacyDN* ou *MailboxGUID* para exclusão reversível da caixa de correio de pasta púbica.

  - Por padrão, as pastas dumpster serão restauradas junto com as pastas regulares. Isso pode ser impedido usando o parâmetro *ExcludeDumpster*.

  - A restauração das caixas de correio de pasta pública é diferente da restauração das caixas de correio regulares pelo fato de as pastas não serem criadas se não existirem na caixa de correio de destino. As pastas ausentes serão exibidas em uma mensagem de aviso ao final da solicitação de restauração.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Restaurar uma pasta pública excluída de forma reversível

Este exemplo restaura a pasta pública \\Dev\\CustomerEnagagements para a caixa de correio de pasta pública de destino Development01.

  ```powershell
  New-MailboxRestoreRequest -SourceStoreMailbox Development -SourceDatabase MBX_DB01 -TargetMailbox Development01 -AllowLegacyDNMismatch -IncludeFolders \Dev\CustomerEngagements
  ```

Para obter informações detalhadas de sintaxes e parâmetros, consulte [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)).

## Restaurar uma caixa de correio de pasta pública excluída de forma reversível

Este exemplo restaura a caixa de correio de pasta pública PF\_Singapore para a nova caixa de correio de pasta pública PF\_Singapore\_Restore.

  ```powershell
  New-MailboxRestoreRequest -SourceStoreMailbox PF_Singapore -SourceDatabase MBX_DB01 -TargetMailbox PF_Singapore_Restore -AllowLegacyDNMismatch
  ```

Para obter informações detalhadas de sintaxes e parâmetros, consulte [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)).

