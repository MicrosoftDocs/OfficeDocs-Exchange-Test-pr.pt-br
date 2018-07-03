---
title: 'Configurar o log de conectividade: Exchange 2013 Help'
TOCTitle: Configurar o log de conectividade
ms:assetid: 24e46a79-33ea-44e9-b03c-549db1c86a6f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996827(v=EXCHG.150)
ms:contentKeyID: 50485152
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o log de conectividade

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-18_

O log de conectividade grava a atividade de conexão de saída que é usada para transmitir mensagens de um serviço de transporte em um servidor Exchange. O log de conectividade grava a origem, o destino, o número de mensagens e os bytes transmitidos da conexão, além de informações de falha de conexão.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entradas "Serviço de Transporte", "Servidor de Transporte de Front End" e "Serviço de Transporte de Caixa de Correio", no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você pode usar o Console de administração do Exchange (EAC) para habilitar ou desabilitar o log de conectividade ou definir o caminho do log de conectividade somente para o serviço de Transporte. Para todas as outras opções de log de conectividade em outros serviços de transporte, você precisará usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para configurar a conectividade de log no serviço de Transporte

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Selecione o servidor de Caixa de Correio que deseja configurar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **Logs de Transporte**.

4.  Na seção **Log de conectividade**, altere qualquer um destes itens:
    
      - **Habilitar log de conectividade**   Para desabilitar o log de conectividade no servidor, desmarque a caixa de seleção. Para habilitar o log de conectividade no servidor, marque a caixa de seleção.
    
      - **Caminho do log de conectividade**   O valor que você especificar deve estar no servidor Exchange local. Se a pasta não existir, ela será criada quando você clicar em **Salvar**.
    
    Quando você tiver concluído, clique em **Salvar**.

## Usar o Shell para configurar o log de conectividade

Para configurar o log de conectividade, execute o seguinte comando:

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ConnectivityLogEnabled <$true | $false> -ConnectivityLogMaxAge <dd.hh:mm:ss> -ConnectivityLogMaxDirectorySize <Size> -ConnectivityLogMaxFileSize <Size> -ConnectivityLogPath <LocalFilePath>

Este exemplo define estas configurações de log de conectividade no serviço de Transporte no servidor de Caixa de Correio chamado Mailbox01:

  -  Define o local dos arquivos de log de conectividade para o Log de Conectividade D:\\Hub. Observe que, se a pasta não existir, ela será criada para você.

  -  Define o tamanho máximo de um arquivo de log de conectividade para 20 MB.

  -  Define o tamanho máximo do diretório do log de conectividade para 1,5 GB.

  -  Define a duração máxima de um arquivo de log de conectividade para 45 dias.

<!-- end list -->

    Set-TransportService Mailbox01 -ConnectivityLogPath "D:\Hub Connectivity Log" -ConnectivityLogMaxFileSize 20MB -ConnectivityLogMaxDirectorySize 1.5GB -ConnectivityLogMaxAge 45.00:00:00


> [!TIP]
> <UL>
> <LI>
> <P>Para definir as configurações do log de conectividade no serviço de Transporte de Caixa de Correio em um servidor de Caixa de Correio, use o cmdlet <STRONG>Set-MailboxTransportService</STRONG>. Para definir as configurações do log de conectividade no serviço de Transporte de Front End em um servidor de Acesso para Cliente, use o cmdlet <STRONG>Set-FrontEndTransportService</STRONG>.</P>
> <LI>
> <P>Definir o parâmetro <EM>ConnectivityLogPath</EM> para o valor <CODE>$null</CODE> efetivamente desabilita o log de conectividade. Entretanto, se o valor do parâmetro <EM>ConnectivityLogEnabled</EM> for <CODE>$true</CODE>, os erros de log de evento serão gerados.</P>
> <LI>
> <P>Definir o valor do parâmetro <EM>ConnectivityLogMaxAge</EM> como <CODE>00:00:00</CODE> impede a remoção automática de arquivos de log de conectividade devido à sua idade.</P></LI></UL>



## Como saber se funcionou?

Para verificar se você configurou com êxito o log de conectividade, faça o seguinte:

1.  No Shell, execute o comando a seguir:
    
        <Get-TransportService | Get-FrontEndTransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List ConnectivityLog*

2.  Verifique se os valores exibidos são os valores que você configurou.

