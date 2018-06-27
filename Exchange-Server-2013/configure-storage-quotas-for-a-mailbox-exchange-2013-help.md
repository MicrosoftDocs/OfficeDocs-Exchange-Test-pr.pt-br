---
title: 'Configurar cotas de armazenamento para uma caixa de correio: Exchange 2013 Help'
TOCTitle: Configurar cotas de armazenamento para uma caixa de correio
ms:assetid: 5f5fe292-c80e-4a0b-b3e6-e193ea5171d0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998353(v=EXCHG.150)
ms:contentKeyID: 50556198
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar cotas de armazenamento para uma caixa de correio

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-07-07_

**Resumo:** Use o EAC ou Shell para definir as cotas de armazenamento de caixas de correio específicas.

As cotas de armazenamento permitem que os administradores controlem o tamanho de caixas de correio e gerenciem o crescimento de bancos de dados de caixa de correio. Quando uma caixa de correio atinge ou excede uma cota de armazenamento especificada, o Exchange envia uma notificação descritiva ao proprietário da caixa de correio.


> [!TIP]
> As cotas de armazenamento são aplicadas em relação ao tamanho de uma determinada caixa de correio conforme definido pela propriedade <CODE>TotalItemSize</CODE> ao executar o cmdlet <CODE>Get-MailboxStatistics</CODE>. Saiba mais em <A href="https://technet.microsoft.com/pt-br/library/bb124612(v=exchg.150)">Get-MailboxStatistics</A>.



As cotas de armazenamento são geralmente configuradas para cada banco de dados. Isso significa que as cotas configuradas para um banco de dados de caixa de correio se aplicam a todas as caixas de correio nesse banco de dados. Para obter mais informações sobre como gerenciar configurações de caixa de correio por banco de dados, consulte [Gerenciar bancos de dados de caixa de correio no Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

Este tópico mostra como personalizar as configurações de armazenamento de uma caixa de correio específica em vez de usar as configurações de armazenamento a partir do banco de dados de caixa de correio. Para tarefas de gerenciamento adicionais relacionadas a caixas de correio de usuário, consulte [Gerenciar caixas de correio do usuário](manage-user-mailboxes-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar cotas de armazenamento para uma caixa de correio

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuários, clique na caixa de correio cujas cotas de armazenamento deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Uso de Caixa de Correio** e clique em **Mais opções**.

4.  Clique em **Personalizar as configurações desta caixa de correio** e configure as seguintes caixas. O intervalo de valores para qualquer configuração de cota de armazenamento vai de 0 a 2.047 gigabytes (GB).
    
      - **Emitir aviso em (GB)**   Essa caixa mostra o limite máximo de armazenamento antes de um aviso ser emitido para o usuário. Se o tamanho da caixa de correio atingir ou exceder o valor especificado, o Exchange enviará uma mensagem de aviso para o usuário.
        

        > [!IMPORTANT]
        > A mensagem associada à cota de <STRONG>Aviso de problema</STRONG> não será enviada ao usuário, a menos que o valor dessa configuração seja superior a 50% do valor especificado na cota <STRONG>Proibir envio</STRONG>. Por exemplo, se você definir a cota de <STRONG>Proibir envio</STRONG> para 8 Mb, você deve definir o <STRONG>Aviso de problema</STRONG> da cota para pelo menos 4 MB. Se você não fizer isso, o <STRONG>Aviso de problema</STRONG> mensagem de cota não será enviada.

    
      - **Proibir envio em (GB)**   Essa caixa mostra o limite para *proibir envio* para a caixa de correio. Se o tamanho da caixa de correio atingir ou exceder o limite especificado, o Exchange impedirá que o usuário da caixa de correio envie novas mensagens e exibirá uma mensagem de erro descritiva.
    
      - **Proibir envio e recebimento em (GB)**   Essa caixa mostra o limite para *proibir envio e recebimento* para a caixa de correio. Se o tamanho da caixa de correio atingir ou exceder o limite especificado, o Exchange impedirá que o usuário da caixa de correio envie novas mensagens e não entregará nenhuma mensagem nova para a caixa de correio. Todas as mensagens enviadas para a caixa de correio são devolvidas ao remetente com uma mensagem de erro descritiva.

5.  Clique em **Salvar** para salvar as alterações.

## Usar o Shell para configurar cotas de armazenamento para uma caixa de correio

Este exemplo define as cotas de aviso de problema, proibição de envio e proibição de envio e recebimento para a caixa de correio de Joe Healy em 24,5 GB, 24,75 GB e 25 GB respectivamente.


> [!TIP]
> Para garantir que as configurações personalizadas da caixa de correio sejam usadas em lugar dos padrões de banco de dados da caixa de correio, você deve definir o parâmetro <EM>UseDatabaseQuotaDefaults</EM> como <CODE>$false</CODE>.



    Set-Mailbox -Identity "Joe Healy" -IssueWarningQuota 24.5gb -ProhibitSendQuota 24.75gb -ProhibitSendReceiveQuota 25gb -UseDatabaseQuotaDefaults $false

Este exemplo define as cotas de aviso de problema, proibição de envio e proibição de envio e recebimento para a caixa de correio de Ayla Kol em 900 MB, 950 MB e 1 GB respectivamente e configura a caixa de correio para utilizar configurações personalizadas.

    Set-Mailbox -Identity "Ayla Kol" -IssueWarningQuota 900mb -ProhibitSendQuota 950mb -ProhibitSendReceiveQuota 1gb -UseDatabaseQuotaDefaults $false

Para informações detalhadas sobre sintaxes e parâmetros, confira [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Como saber se funcionou?

Para confirmar se você definiu com êxito as cotas de armazenamento de uma caixa de correio, siga um destes procedimentos:

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuários, clique na caixa de correio cujas cotas de armazenamento deseja verificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Uso de Caixa de Correio** e clique em **Mais opções**.

4.  Verifique se **Personalizar as configurações para esta caixa de correio** está selecionada.

5.  Verifique as configurações de cota de armazenamento.

Ou

Execute o seguinte comando no Shell.

    Get-Mailbox <identity> | fl IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

