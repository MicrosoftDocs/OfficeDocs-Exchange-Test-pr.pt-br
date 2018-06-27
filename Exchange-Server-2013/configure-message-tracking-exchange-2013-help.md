---
title: 'Configurar o rastreamento de mensagem: Exchange 2013 Help'
TOCTitle: Configurar o rastreamento de mensagem
ms:assetid: 50eb5213-cf27-4179-b427-38d751ee4a70
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997984(v=EXCHG.150)
ms:contentKeyID: 51407856
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o rastreamento de mensagem

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2013-02-18_

O acompanhamento de mensagens registra a atividade de transporte de SMTP de todas as mensagens transferidas para e a partir do serviço de Transporte ou caixas de correio em um servidor de Caixa de Correio do Microsoft Exchange Server 2013. É possível usar logs de controle de mensagens para análise forense de mensagens, análise de fluxo de mensagens, criação de relatórios e solução de problemas.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entradas "Serviço de transporte" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) ou entrada "Configuração de servidor de caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Você pode usar o Centro de Administração do Exchange (EAC) para habilitar ou desabilitar o acompanhamento de mensagens, ou definir o caminho do log de acompanhamento de mensagens. Para todas as outras opções de acompanhamento de mensagens, você precisará usar o Shell de Gerenciamento do Exchange.

  - Em um servidor de caixa de correio do Exchange 2013, você pode usar o cmdlet **Set-TransportService** ou **Set-MailboxServer** para configurar as opções de acompanhamento de mensagens. Os procedimentos deste tópico usam o cmdlet **Set-TransportService**.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para configurar o acompanhamento de mensagens em servidores de caixa de correio

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Selecione o servidor de Caixa de Correio que você deseja configurar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **Logs de Transporte**.

4.  Na seção **Log de acompanhamento de mensagens**, altere qualquer um destes itens:
    
      - **Habilitar log de acompanhamento de mensagens**   Para desabilitar o log de acompanhamento de mensagens, desmarque a caixa de seleção. Para habilitar o log de acompanhamento de mensagens, marque a caixa de seleção.
    
      - **Caminho do log de acompanhamento de mensagens**   O valor que você especificar deve estar no servidor Exchange local. Se a pasta não existir, ela será criada quando você clicar em **Salvar**.

5.  Clique em **Salvar**.

## Usar o Shell para configurar o acompanhamento de mensagens

Para configurar o acompanhamento de mensagens, execute o seguinte comando:

    Set-TransportService <ServerIdentity> -MessageTrackingLogEnabled <$true | $false> -MessageTrackingLogMaxAge <dd.hh:mm:ss> -MessageTrackingLogMaxDirectorySize <Size> -MessageTrackingLogMaxFileSize <Size> -MessageTrackingLogPath <LocalFilePath> -MessageTrackingLogSubjectLoggingEnabled <$true|$false>

Este exemplo define as seguintes configurações do log de acompanhamento de mensagens no servidor de Caixa de Correio chamado Mailbox01:

  -  
    Define o local dos arquivos de log de acompanhamento de mensagens em D:\\Log de Acompanhamento de Mensagens. Observe que, se a pasta não existir, ela será criada para você.

  -  
    Define o tamanho máximo de um arquivo de log de acompanhamento de mensagens para 20 MB.

  -  
    Define o tamanho máximo do diretório de log de acompanhamento de mensagens para 1.5 GB.

  -  
    Define a duração máxima de um arquivo de log de acompanhamento de mensagens para 45 dias.

<!-- end list -->

    Set-TransportService Mailbox01 -MessageTrackingLogPath "D:\Hub Message Tracking Log" -MessageTrackingLogMaxFileSize 20MB -MessageTrackingLogMaxDirectorySize 1.5GB -MessageTrackingLogMaxAge 45.00:00:00


> [!TIP]
> <UL>
> <LI>
> <P>Definir o parâmetro <EM>MessageTrackingLogPath</EM> para o valor <CODE>$null</CODE> desabilita efetivamente o acompanhamento de mensagens. Entretanto, se o valor do parâmetro <EM>MessageTrackingLogEnabled</EM> for <CODE>$true</CODE>, os erros de log de evento serão gerados.</P>
> <LI>
> <P>Definir o valor do parâmetro <EM>MessageTrackingLogMaxAge</EM> como <CODE>00:00:00</CODE> impede a remoção automática de arquivos de log de acompanhamento de mensagens devido à sua idade.</P>
> <LI>
> <P>Nos servidores de Caixa de Correio do Exchange 2013, o tamanho máximo do diretório de log de acompanhamento de mensagens é três vezes o valor do parâmetro <EM>MessageTrackingLogMaxDirectorySize</EM>. Embora os arquivos de log de ​​controle de mensagens gerados pelos quatro serviços diferentes tenham quatro prefixos de nomes diferentes, a quantidade e a frequência dos dados gravados nos arquivos de log <STRONG>MSGTRKMA</STRONG> são insignificantes em comparação aos três outros prefixos de arquivo de log. Para obter mais informações, consulte a seção "Estrutura dos arquivos de log de acompanhamento de mensagens" no tópico <A href="message-tracking-exchange-2013-help.md">Controle de mensagens</A>.</P></LI></UL>



Este exemplo desabilita o registro do assunto da mensagem no log de acompanhamento de mensagens no servidor de caixa de correio chamado Mailbox01:

    Set-TransportService Mailbox01 -MessageTrackingLogSubjectLoggingEnabled $false

Este exemplo desabilita o acompanhamento de mensagens no servidor de caixa de correio chamado Mailbox01:

    Set-TransportService Mailbox01 -MessageTrackingLogEnabled $false

## Como saber se funcionou?

Para verificar se você configurou com êxito o acompanhamento de mensagens, faça o seguinte:

1.  No Shell, execute o comando a seguir:
    
        Get-TransportService <ServerIdentity> | Format-List MessageTrackingLog*

2.  Verifique se os valores exibidos são os valores que você configurou.

