---
title: 'Configurar o log de protocolo para POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Configurar o log de protocolo para POP3 e IMAP4
ms:assetid: 451b337b-cb6b-4460-8687-be0b19c469bc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997690(v=EXCHG.150)
ms:contentKeyID: 50556177
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o log de protocolo para POP3 e IMAP4

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-27_

Você pode usar o Shell para habilitar, desabilitar ou modificar as configurações de log de protocolo para POP3 e IMAP4. Por padrão, esse registro em log não está habilitado.

O log de protocolo permite que você analise as conexões POP3 e IMAP4 em seu ambiente do Exchange. Isso pode ser útil se você estiver solucionando problemas relacionados ao desempenho de POP3 ou IMAP4. Para mais informações, consulte [Log de protocolo para POP3 e IMAP4](protocol-logging-for-pop3-and-imap4-exchange-2013-help.md). Para mais informações relacionadas a POP3 e IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "configurações de POP3" e "configurações de IMAP4" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o Shell para habilitar o registro em log de protocolo para POP3 ou IMAP4

Este exemplo habilita o registro em log de protocolo para POP3 ou IMAP4 no servidor de Acesso para Cliente CAS01.

    Set-ImapSettings -Server "CAS01" -ProtocolLogEnabled $true
    Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true


> [!TIP]
> Após alterar as configurações de log de protocolo para POP3 ou IMAP4, será necessário reiniciar o serviço que estiver em uso: POP3 ou IMAP4. Para obter informações sobre como reiniciar os serviços POP3 e IMAP4, consulte <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Iniciar e interromper os serviços POP3</A> e <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Iniciar e interromper os serviços de IMAP4</A>.



Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-ImapSettings](https://technet.microsoft.com/pt-br/library/aa998252\(v=exchg.150\)) e [Set-PopSettings](https://technet.microsoft.com/pt-br/library/aa997154\(v=exchg.150\)).

## Usar o Shell para desabilitar o registro em log de protocolo para POP3 ou IMAP4

Este exemplo desabilita o registro em log de protocolo para POP3 ou IMAP4 no servidor de Acesso para Cliente CAS01.

    Set-ImapSettings -Server "CAS01" -protocolLogEnabled $false
    Set-PopSettings -Server "CAS01" -protocolLogEnabled $false


> [!TIP]
> Após alterar as configurações de log de protocolo para POP3 ou IMAP4, será necessário reiniciar o serviço que estiver em uso: POP3 ou IMAP4. Para obter informações sobre como reiniciar os serviços POP3 e IMAP4, consulte <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Iniciar e interromper os serviços POP3</A> e <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Iniciar e interromper os serviços de IMAP4</A>.



Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-ImapSettings](https://technet.microsoft.com/pt-br/library/aa998252\(v=exchg.150\)) e [Set-PopSettings](https://technet.microsoft.com/pt-br/library/aa997154\(v=exchg.150\)).

## Usar o Shell para modificar o registro em log de protocolo para POP3 ou IMAP4

Para modificar as configurações de registro em log de POP3 ou IMAP4, execute os cmdlets **Set-ImapSettings** ou **Set-PopSettings** com um ou mais dos seguintes parâmetros.

  - *LogFileLocation*   Esse parâmetro especifica o local dos arquivos de log de protocolo POP3 ou IMAP4. Por padrão, os arquivos de log com protocolo POP3 se encontram no diretório C:\\Arquivos de Programas\\Microsoft\\Exchange Server\\V15\\Logging\\Pop3. Esse exemplo ativa o registro em log do protocolo POP3 no servidor de Acesso para Cliente CAS01. Ele também altera o diretório de registro em log de protocolo POP3 para C:\\Pop3Logging.
    
        Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true -LogFileLocation "C:\Pop3Logging"

  - *LogFileRollOverSettings*   Esse parâmetro define com qual frequência o registro em log do protocolo POP3 ou IMAP4 cria um novo arquivo de log. Por padrão, o novo arquivo de log é criado a cada dia. Os valores possíveis são:
    
    Por hora
    
    Diário
    
    Semanal
    
    Mensal
    
    Esta configuração só é aplicável quando o valor do parâmetro *LogPerFileSizeQuota* for definido como . Esse exemplo altera o registro em log do protocolo POP3 no servidor de Acesso para Cliente CAS01 para criar um novo arquivo de log a cada hora.
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 0 -LogFileRollOverSettings Hourly

  - *LogPerFileSizeQuota*   Esse parâmetro define o tamanho máximo de um arquivo de log de protocolo POP3 ou IMAP4 em bytes. Por padrão, esse valor é definido como zero. Quando este valor está definido como zero, um novo arquivo de log de protocolo é criado na frequência especificada pelo parâmetro *LogFileRollOverSettings*.
    
    Esse exemplo altera o registro em log do protocolo POP3 no servidor de Acesso para Cliente CAS01 para criar um novo arquivo de log quando um arquivo de log atingir 2 MB.
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 2000000
    
    Esse exemplo altera o registro em log do protocolo POP3 no servidor de Acesso para Cliente CAS01 para usar o mesmo arquivo de log, independentemente de seu tamanho e sua data de criação.
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota unlimited


> [!TIP]
> Após alterar as configurações de log de protocolo para POP3 ou IMAP4, será necessário reiniciar o serviço que estiver em uso: POP3 ou IMAP4. Para obter informações sobre como reiniciar os serviços POP3 e IMAP4, consulte <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Iniciar e interromper os serviços POP3</A> e <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Iniciar e interromper os serviços de IMAP4</A>.



Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-ImapSettings](https://technet.microsoft.com/pt-br/library/aa998252\(v=exchg.150\)) e [Set-PopSettings](https://technet.microsoft.com/pt-br/library/aa997154\(v=exchg.150\)).

## Como saber se funcionou?

Execute o seguinte comando no Shell para verificar as definições de registro em log de protocolo POP3. Se o registro em log de protocolo POP3 for habilitado, o valor para o parâmetro *ProtocolLogEnabled* será `True`. Se o log de protocolo POP3 estiver desabilitado, o valor será `False`. Você também pode verificar se os valores para os parâmetros *LogFileLocation*, *LogPerFileSizeQuota* e *LogFileRollOverSettings* estão corretos.

    Get-PopSettings | format-list

Execute o seguinte comando no Shell para verificar as definições de registro em log de protocolo IMAP4. Se o registro em log de protocolo IMAP4 for habilitado, o valor para o parâmetro *ProtocolLogEnabled* será `True`. Se o log de protocolo IMAP4 estiver desabilitado, o valor será `False`. Você também pode verificar se os valores para os parâmetros *LogFileLocation*, *LogPerFileSizeQuota* e *LogFileRollOverSettings* estão corretos.

    Get-ImapSettings | format-list

## Para mais informações

Depois de definir as configurações do log de protocolo para POP3 e IMAP4, você pode também:

[Iniciar e interromper os serviços de IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md)

[Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md)

