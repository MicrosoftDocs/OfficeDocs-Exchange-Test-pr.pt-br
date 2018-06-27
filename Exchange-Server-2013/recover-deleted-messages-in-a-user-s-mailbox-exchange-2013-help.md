---
title: 'Recuperar mensagens excluídas na caixa de correio de um usuário: Exchange Online Help'
TOCTitle: Recuperar mensagens excluídas na caixa de correio de um usuário
ms:assetid: 9e0e34ce-efc5-454e-8d15-57b4da867f12
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff660637(v=EXCHG.150)
ms:contentKeyID: 50556254
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recuperar mensagens excluídas na caixa de correio de um usuário

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

(Este tópico é destinado a administradores do Exchange.)

Os administradores podem pesquisar e recuperar as mensagens de email excluídas na caixa de correio de um usuário. Isso inclui itens que foram excluídos permanentemente (eliminados) por uma pessoa (usando o recurso Recuperar Itens Excluídos no Outlook ou no Outlook Web App) ou itens excluídos por um processo automático, como a política de retenção atribuída às caixas de correio do usuário. Nessas situações, os itens eliminados não podem ser recuperados por um usuário. Mas os administradores podem recuperar mensagens eliminadas se o período de retenção do item excluído ainda não tiver expirado.


> [!TIP]
> Além de usar este procedimento para procurar e recuperar itens excluídos (que são movidos para a pasta Items Recuperáveis\Limpeza se a recuperação de item individual ou a retenção de litígio estiver habilitada), você também pode usar este procedimento para procurar por itens residir em outras pastas na caixa de correio e excluir itens da caixa de correio de origem (também conhecido como <EM>pesquisar e destruir</EM>).



## O que você precisa saber antes de começar?

  - Tempo estimado de conclusão: 15 a 30 minutos.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - A recuperação de item individual deve estar habilitada para uma caixa de correio para que o item que deseja recuperar seja excluído. No Exchange Online, a recuperação de item individual é habilitada por padrão ao criar uma nova caixa de correio. No Exchange 2013, a recuperação de item individual fica desabilitada ao criar uma nova caixa de correio. Para saber mais, confira [Habilitar ou desabilitar a recuperação de item único para uma caixa de correio](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md).

  - Para pesquisar e recuperar itens, você deve ter as seguintes informações:
    
      - **Caixa de correio de origem**   Esta é a caixa de correio a ser pesquisada.
    
      - **Caixa de correio de destino**   Esta é a caixa de correio de descoberta para a qual as mensagens serão recuperadas. A configuração do Exchange cria uma caixa de correio de descoberta padrão. No Exchange Online, uma caixa de correio de descoberta também é criada por padrão. Se necessário, você pode criar caixas de correio de descoberta adicionais. Para saber mais, confira [Criar uma caixa de correio de descoberta](create-a-discovery-mailbox-exchange-2013-help.md).
        

        > [!TIP]
        > Ao usar o cmdlet <STRONG>Search-Mailbox</STRONG>, também é possível especificar uma caixa de correio de destino que não seja de descoberta. No entanto, não é possível especificar a mesma caixa de correio como a caixa correio de origem e de destino.

    
      - **Critérios de pesquisa**   Os critérios incluem o remetente ou destinatário, ou palavras chave (palavras ou frases) na mensagem.

  - Esse tópico se concentra no uso do PowerShell para recuperar itens excluídos da caixa de correio de um usuário. Você também pode usar a ferramenta de Descoberta Eletrônica In-Loco baseada em GUI para localizar e exportar os itens excluídos para um arquivo PST. O usuário utilizará esse arquivo PST para restaurar as mensagens excluídas em sua caixa de correio. Para saber mais, confira [Recuperar itens excluídos na caixa de correio de um usuário – Ajuda para Administradores](https://go.microsoft.com/fwlink/p/?linkid=722928).

## (Opcional) Etapa 1: conecte-se ao Exchange Online usando o PowerShell remoto

Você só precisa realizar esta etapa se tiver uma organização do Exchange Online ou do Office 365. Se tiver uma organização do Exchange 2013, vá para a próxima etapa e execute o comando no Shell de Gerenciamento do Exchange.

1.  Em seu computador local, abra o Windows PowerShell e execute o comando a seguir.
    
        $UserCredential = Get-Credential
    
    Na caixa de diálogo **Solicitação de Credenciais do Windows PowerShell**, digite o nome de usuário e a senha de sua conta de administrador global do Office 365 e clique em **OK**.

2.  Execute o seguinte comando.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  Execute o seguinte comando.
    
        Import-PSSession $Session

4.  Para verificar se você está conectado à sua organização do Exchange Online, execute o comando a seguir para obter uma lista de todas as caixas de correio de sua organização.
    
        Get-Mailbox

Para saber mais, ou se você tiver problemas para se conectar à sua organização do Exchange Online, confira [Conectar-se ao Exchange Online usando o PowerShell remoto](http://go.microsoft.com/fwlink/p/?linkid=517283).

## Etapa 2: pesquisar e recuperar itens perdidos

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Descoberta" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!TIP]
> Você pode usar a Descoberta Eletrônica In-loco no Centro de administração do Exchange (EAC) para pesquisar itens perdidos. Entretanto, ao usar o EAC, você não pode restringir a pesquisa à pasta Itens Recuperáveis. As mensagens correspondentes aos seus parâmetros de pesquisa serão retornadas, mesmo se elas não foram excluídas. Após serem recuperadas para a caixa de correio de descoberta especificada, talvez seja preciso analisar os resultados da pesquisa e remover as mensagens desnecessárias antes de recuperar as mensagens remanescentes para a caixa de correio do usuário ou exportá-las para um arquivo .pst.<BR>Para saber mais sobre como usar o EAC para realizar uma pesquisa de Descoberta Eletrônica In-loco, confira <A href="create-an-in-place-ediscovery-search-exchange-2013-help.md">Criar uma pesquisa de Descoberta Eletrônica In-loco</A>.



A primeira etapa do processo de recuperação é pesquisar as mensagens na caixa de correio de origem. Use um dos métodos a seguir para buscar em uma caixa de correio de usuário e copiar mensagens para uma caixa de correio de descoberta.

Este exemplo pesquisa mensagens na caixa de correio de April Stewart que atendam aos seguintes critérios:

  - Remetente: Ken Kwok

  - Palavra-chave: Seattle

<!-- end list -->

    Search-Mailbox "April Stewart" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "Discovery Search Mailbox" -TargetFolder "April Stewart Recovery" -LogLevel Full


> [!TIP]
> Ao usar o cmdlet <STRONG>Search-Mailbox</STRONG>, é possível definir o escopo da pesquisa usando o parâmetro <EM>SearchQuery</EM> para especificar uma consulta formatada usando KQL (Keyword Query Language, Linguagem de Consulta de Palavra-Chave). Você também pode usar a opção <EM>SearchDumpsterOnly</EM> para pesquisar apenas os itens na pasta Itens Recuperáveis.



Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Search-Mailbox](https://technet.microsoft.com/pt-br/library/dd298173\(v=exchg.150\)).

**Como saber se funcionou?**

Para verificar se pesquisou as mensagens que deseja recuperar com êxito, faça logon na caixa de correio de descoberta selecionada como a caixa de correio de destino e analise os resultados da pesquisa.

## Etapa 3: restaurar itens recuperados

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Descoberta" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!TIP]
> O EAC não pode ser usado para restaurar itens recuperados.



Após as mensagens terem sido recuperadas para uma caixa de correio de descoberta, é possível restaurá-las para a caixa de correio do usuário com o cmdlet **Search-Mailbox**. No Exchange 2013, também é possível usar os cmdlets **New-MailboxExportRequest** e **New-MailboxImportRequest** para exportar ou importar as mensagens de um arquivo .pst.

## Usar o Shell para restaurar mensagens

Este exemplo restaura as mensagens para a caixa de correio de April Stewart e as exclui da caixa de correio de pesquisa de descoberta.

    Search-Mailbox "Discovery Search Mailbox" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "April Stewart" -TargetFolder "Recovered Messages" -LogLevel Full -DeleteContent

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Search-Mailbox](https://technet.microsoft.com/pt-br/library/dd298173\(v=exchg.150\)).

**Como saber se funcionou?**

Para verificar se recuperou mensagens com êxito para a caixa de correio do usuário, solicite que o usuário analise as mensagens na pasta de destino especificada no comando anterior.

## (Exchange 2013) Usar o Shell para exportar e importar mensagens de um arquivo .pst

No Exchange 2013, é possível exportar o conteúdo de uma caixa de correio para um arquivo .pst e importar esse arquivo em uma caixa de correio. Para saber mais sobre como importar e exportar de uma caixa de correio, confira [Solicitações de importação e exportação da caixa de correio](mailbox-import-and-export-requests-exchange-2013-help.md). Não é possível executar esta tarefa no Exchange Online.

Este exemplo usa as configurações a seguir para exportar mensagens da pasta April Stewart Recovery na caixa de correio de pesquisa de descoberta para um arquivo .pst:

  - **Mailbox**   Discovery Search Mailbox

  - **Source folder**   April Stewart Recovery

  - **ContentFilter**   April travel plans

  - **PST file path**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxExportRequest -Mailbox "Discovery Search Mailbox" -SourceRootFolder "April Stewart Recovery" -ContentFilter {Subject -eq "April travel plans"} -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [New-MailboxExportRequest](https://technet.microsoft.com/pt-br/library/ff607299\(v=exchg.150\)).

Este exemplo usa as configurações a seguir para importar mensagens a partir de um arquivo .pst para a pasta Recovered By HelpDesk na caixa de correio de April Stewart:

  - **Mailbox**   April Stewart

  - **Target folder**   Recovered By Helpdesk

  - **PST file path**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxImportRequest -Mailbox "April Stewart" -TargetRootFolder "Recovered By Helpdesk" -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst 

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [New-MailboxImportRequest](https://technet.microsoft.com/pt-br/library/ff607310\(v=exchg.150\)).

**Como saber se funcionou?**

Para verificar se exportou as mensagens com êxito para um arquivo .pst, use o Outlook para abrir o arquivo .pst e inspecione seu conteúdo. Para verificar se importou as mensagens importadas com êxito do arquivo .pst, solicite que o usuário inspecione o conteúdo da pasta de destino especificada no comando anterior.

## Mais informações

  - A capacidade de recuperar itens excluídos é habilitada na *recuperação de item individual*, que possibilita que o administrador recupere uma mensagem que foi eliminada por um usuário ou política de retenção, desde que o período de retenção do item excluído não tenha expirado. Para saber mais sobre a recuperação de item individual, confira [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

  - Uma caixa de correio do Exchange Online é configurada, por padrão, para manter itens excluídos por 14 dias. Você pode alterar essa configuração para até 30 dias. No Exchange 2013, um banco de dados de caixa de correio é configurado, por padrão, para manter os itens excluídos por 14 dias. Você pode definir as configurações de itens excluídos para uma caixa de correio ou um banco de dados de caixa de correio. Para saber mais, confira:
    
      - [Alterar quanto tempo os itens permanentemente excluídos são mantidos em uma caixa de correio do Exchange Online](https://technet.microsoft.com/pt-br/library/dn163584\(v=exchg.150\))
    
      - [Configurar cotas de itens recuperáveis e retenção de Item excluído](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)

  - Conforme explicado anteriormente, também é possível usar a ferramenta Descoberta Eletrônica In-Loco para localizar e exportar itens excluídos para um arquivo PST. O usuário utilizará esse arquivo PST para restaurar as mensagens excluídas em sua caixa de correio. Para saber mais, confira [Recuperar itens excluídos na caixa de correio de um usuário – Ajuda para Administradores](http://go.microsoft.com/fwlink/p/?linkid=722928).

  - Os usuários podem recuperar um item excluído se ele não tiver sido eliminado e se seu período de retenção não estiver expirado. Caso os usuários precisem recuperar itens excluídos da pasta Itens Recuperáveis, direcione-os para os seguintes tópicos:
    
      - [Recuperar itens excluídos no Outlook 2010](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Recuperar itens excluídos no Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=624829)
    
      - [Recuperar itens ou emails excluídos no Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

  - Este tópico mostra como usar o cmdlet **Search-Mailbox** para pesquisar por e recuperar itens perdidos. Ao usar este cdmlet, só é possível pesquisar em uma caixa de correio por vez. Se quiser pesquisar em várias caixas de correio ao mesmo tempo, use o [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md) no Centro de administração do Exchange (EAC) ou o cmdlet [New-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd298064\(v=exchg.150\)) no Windows PowerShell.

  - Além de usar este procedimento para procurar e recuperar itens excluídos, você também pode usar um procedimento semelhante para pesquisar itens em caixas de correio de usuários e, em seguida, excluir esses itens da caixa de correio de origem. Para saber mais, confira [Pesquisar e excluir mensagens - ajuda de Admin](search-for-and-delete-messages-admin-help-exchange-2013-help.md).

