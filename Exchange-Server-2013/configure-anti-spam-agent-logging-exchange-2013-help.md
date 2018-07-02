---
title: 'Configurar o log de agente de antispam: Exchange 2013 Help'
TOCTitle: Configurar o log de agente de antispam
ms:assetid: df157ca3-ad8e-4302-acbc-5fbb8570c21d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb691337(v=EXCHG.150)
ms:contentKeyID: 50486797
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o log de agente de antispam

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Log de agente registra as ações executadas pelos agentes de antispam específicos do Exchange. As informações gravadas no log de agente dependem do agente, o evento SMTP e a ação executada na mensagem.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Serviço de transporte" e entradas de "Servidor de transporte de borda" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - Por padrão, os recursos antispam não estão habilitados no serviço de Transporte em um servidor de Caixa de Correio. Normalmente, você apenas habilita os recursos antispam em um servidor de Caixa de Correio se sua organização do Exchange não realiza nenhuma ação antes da filtragem antispam antes de aceitar mensagens de entrada. Para saber mais, confira [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para configurar o log de agente de antispam

Execute o seguinte comando:

    Set-TransportService <ServerIdentity> -AgentLogEnabled <$true | $false> -AgentLogMaxAge <dd.hh:mm:ss> -AgentLogMaxDirectorySize <Size> -AgentLogMaxFileSize <Size> -AgentLogPath <LocalFilePath>

Este exemplo define o agente de seguir as configurações de log no servidor de caixa de correio chamado Mailbox01:

  -  
    Define o local do agente de arquivos de log D:\\Anti-Spam log de agente. Observe que se a pasta não existir, ele será criado para você.

  -  
    Define o tamanho máximo de um agente do arquivo de log a 20 MB.

  -  
    Define o tamanho máximo do agente do diretório de log para 400 MB.

  -  
    Define a idade máxima de um agente do arquivo de log para 14 dias.

<!-- end list -->

    Set-TransportService Mailbox01 -AgentLogPath "D:\Anti-Spam Agent Log" -AgentLogMaxFileSize 20MB -AgentLogMaxDirectorySize 400MB -AgentLogMaxAge 14.00:00:00


> [!TIP]
> <UL>
> <LI>
> <P>Se você definir o parâmetro <EM>AgentLogPath</EM> como o valor <CODE>$null</CODE>, você efetivamente desabilitar o log de agente. No entanto, se você definir <EM>AgentLogPath</EM> como <CODE>$null</CODE> quando o valor do parâmetro <EM>AgentLogEnabled</EM> é <CODE>$true</CODE>, erros de log de eventos são gerados. O método preferencial para desabilitar o log de agente é definida <EM>AgentLogEnabled</EM> como <CODE>$false</CODE>.</P>
> <LI>
> <P>Definindo o parâmetro <EM>AgentLogMaxAge</EM> como o valor <CODE>00:00:00</CODE> impede a remoção automática de arquivos de log de agente devido à sua idade.</P></LI></UL>



Para detalhadas sobre sintaxe e informações de parâmetro, consulte os parâmetros de *AgentLog* em [Set-TransportService](https://technet.microsoft.com/pt-br/library/jj215682\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você configurou com êxito agente anti-spam log, faça o seguinte:

1.  No Shell, execute o comando a seguir:
    
        Get-TransportService <ServerIdentity> | Format-List AgentLog*

2.  Verifique se os valores exibidos são os valores que você configurou.

