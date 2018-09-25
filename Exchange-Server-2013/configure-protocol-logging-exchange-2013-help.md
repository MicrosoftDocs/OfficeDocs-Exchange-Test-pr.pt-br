---
title: 'Configurar o log de protocolo: Exchange 2013 Help'
TOCTitle: Configurar o log de protocolo
ms:assetid: c81cac9c-b990-492a-b899-5be8d08a6068
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124531(v=EXCHG.150)
ms:contentKeyID: 50486633
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o log de protocolo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-03-15_

Log de protocolo registra as conversas de SMTP que ocorrem em conectores de envio e conectores de recebimento como parte da entrega da mensagem.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Serviço de transporte", "Serviço Front End transporte", "Serviço de transporte de caixa de correio", "Conectores de recebimento" e entradas de "Conectores de envio" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - Você pode usar o Centro de administração do Exchange (EAC) para habilitar ou desabilitar o log de protocolo para conectores de envio e conectores de recebimento no serviço de transporte em servidores de caixa de correio e para conectores de recebimento no serviço Front End Transport em servidores de acesso para cliente. Você também pode usar o EAC para configurar os caminhos de log de protocolo para o serviço de transporte. Para todos os outro protocolo opções de log, você precisará usar o Shell.

  - Log de protocolo está habilitada ou desabilitada em cada conector. Todos os conectores de recebimento no servidor Exchange compartilham os mesmos arquivos de log do protocolo e as opções de log de protocolo. Essas configurações de log do protocolo são separadas dos arquivos de log do protocolo de conector de envio e opções de log de protocolo que estão no mesmo servidor.

  - UNRESOLVED\_TOKENBLOCK\_VAL(ALERT\_Do não realize este no servidor de borda inscrito)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para configurar o log de protocolo

Para usar o EAC para habilitar ou desabilitar o protocolo de registro em log em um conector de envio ou um conector de recebimento no serviço de transporte em um servidor de caixa de correio ou em um conector de recebimento no serviço Front End Transport em um servidor de acesso para cliente, faça o seguinte:

1.  No EAC, navegue até **fluxo de emails** \> **conectores de envio** ou o **fluxo de emails** \> **conectores de recebimento**.

2.  Selecione o conector que você deseja configurar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na guia **Geral**, na seção **nível de log de protocolo**, selecione uma das seguintes opções:
    
      - **Nenhum**   Log de protocolo desabilitado no conector.
    
      - **Verbose**   O log do protocolo é habilitado no conector.
    
    Quando você tiver concluído, clique em **Salvar**.

Para usar o EAC para configurar os caminhos de log de protocolo para os conectores de envio e conectores de recebimento no serviço de transporte em um servidor de caixa de correio, faça o seguinte:

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  Selecione o servidor de Caixa de Correio que você deseja configurar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página Propriedades do servidor, clique em **logs de transporte**.

4.  Na seção **log de protocolo**, altere qualquer uma das seguintes configurações:
    
      - **Enviar o caminho de log do protocolo**   O valor especificado deve ser no servidor Exchange local. Se a pasta não existir, ele será criado para você quando você clicar em **Salvar**.
    
      - **Caminho de log do protocolo de recebimento**   O valor especificado deve ser no servidor Exchange local. Se a pasta não existir, ele será criado para você quando você clicar em **Salvar**.
    
    Quando você tiver concluído, clique em **Salvar**.

## Como saber se funcionou?

Para verificar que você usou com êxito o EAC para definir as configurações de log de protocolo, faça o seguinte:

1.  Navegue até o local especificado para o conector de envio ou logs de protocolo do conector de recebimento.

2.  Se você habilitou o log de protocolo, verifique se que um arquivo de log é criado. Se você tiver desabilitado o log de protocolo, verifique se que o arquivo de log mais recente não está sendo atualizado.

## Usar o Shell para habilitar ou desabilitar o log em um conector de envio ou um conector de recebimento de protocolo

Para habilitar ou desabilitar o log em um conector de envio ou um conector de recebimento de protocolo, execute o seguinte comando:

```powershell
<Set-SendConnector |Set-ReceiveConnector> <ConnectorIdentity> -ProtocolLoggingLevel <Verbose | None>
```

Este exemplo habilita o log para o conector de recebimento chamado conexão de Contoso.com de protocolo.

```powershell
Set-ReceiveConnector "Connection from Contoso.com" -ProtocolLoggingLevel Verbose
```

## Como saber se funcionou?

Para verificar se você habilitou com êxito ou log de protocolo desativado, faça o seguinte:

1.  No Shell, execute o comando a seguir:
    
    ```command line
    <Get-SendConnector |Get-ReceiveConnector> | Format-List Name,ProtocolLoggingLevel
    ```

2.  Verifique se os valores exibidos são os valores que você configurou.

## Usar o Shell para habilitar ou desabilitar o log no conector de envio dentro da organização de protocolo

Para habilitar ou desabilitar o protocolo de logon o conector de envio invisíveis e implícita dentro da organização que existe no serviço de transporte em um servidor de caixa de correio e no serviço Front End Transport em um servidor de acesso para cliente, execute o seguinte comando:

```powershell
<Set-TransportService | Set-FrontEndTransportService> -IntraOrgConnectorProtocolLoggingLevel <Verbose | None>
```

Esse protocolo permite de exemplo logon de dentro da organização de conector de envio no serviço de transporte em um servidor de caixa de correio chamado Mailbox01.

```powershell
Set-TransportService Mailbox01 -IntraOrgConnectorProtocolLoggingLevel Verbose
```

## Como saber se funcionou?

Para verificar que você com êxito habilitada ou desabilitada protocolo logon o conector de envio interna da organização, faça o seguinte:

1.  No Shell, execute o comando a seguir:
    
    ```powershell
    <Get-TransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List IntraOrgConnectorProtocolLoggingLevel
    ```

2.  Verifique se o valor apresentado é o valor que você configurou.

## Usar o Shell para habilitar ou desabilitar o protocolo logon a entrega de caixa de correio conector de envio

Para habilitar ou desabilitar o protocolo de log a entrega de caixa de correio implícita e invisível conector de envio que existe no serviço de transporte de caixa de correio em um servidor de caixa de correio, execute o seguinte comando:

```powershell
Set-MailboxTransportService -MailboxDeliveryConnectorProtocolLoggingLevel <Verbose | None>
```

Este exemplo habilita o protocolo logon o conector de recebimento de entrega de caixa de correio no serviço de transporte de caixa de correio em um servidor de caixa de correio chamado Mailbox01.

```powershell
Set-MailboxTransportService Mailbox01 -MailboxDeliveryConnectorProtocolLoggingLevel Verbose
```

## Como saber se funcionou?

Para verificar que você com êxito habilitada ou desabilitada protocolo logon o conector de entrega de caixa de correio, faça o seguinte:

1.  No Shell, execute o comando a seguir:
    
    ```powershell
    Get-MailboxTransportService <ServerIdentity> | Format-List MailboxDeliveryConnectorProtocolLoggingLevel
    ```

2.  Verifique se o valor apresentado é o valor que você configurou.

## Usar o Shell para configurar definições do log de protocolo

Para definir as configurações de log de protocolo, execute o seguinte comando:

```powershell
<Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ReceiveProtocolLogPath <LocalFilePath> -SendProtocolLogPath <LocalFilePath> -ReceiveProtocolLogMaxFileSize <Size> -SendProtocolLogMaxFileSize <Size> -ReceiveProtocolLogMaxDirectorySize <Size> -SendProtocolLogMaxDirectorySize <Size> -ReceiveProtocolLogMaxAge <dd.hh:mm:ss> -SendProtocolLogMaxAge <dd.hh:mm:ss>
```

Este exemplo define o protocolo de seguir as configurações de log no serviço de transporte no servidor de caixa de correio chamado Mailbox01:

  -  O local do protocolo de conector de recebimento todos os logs D:\\Hub receber SMTP Log e todos os conjuntos de conector de envio logs de protocolo D:\\Hub enviar SMTP log. Observe que se a pasta não existir, ele será criado para você.

  -  Define o tamanho máximo de um conector de recebimento de arquivo de log do protocolo e um arquivo de log de protocolo de conector de envio a 20 MB.

  -  Define o tamanho máximo da pasta de log de protocolo de conector de recebimento e a pasta de log de protocolo de conector de envio para 400 MB.

  -  Define a idade máxima de um conector de recebimento de arquivo de log de protocolo e um arquivo de log de protocolo do conector de envio como 45 dias.

<!-- end list -->

```powershell
Set-TransportService Mailbox01 -ReceiveProtocolLogPath "D:\Hub Receive SMTP Log" -SendProtocolLogPath "D:\Hub Send SMTP Log" -ReceiveProtocolLogMaxFileSize 20MB -SendProtocolLogMaxFileSize 20MB -ReceiveProtocolLogMaxDirectorySize 400MB -SendProtocolLogMaxDirectorySize 400MB -ReceiveProtocolLogMaxAge 45.00:00:00 -SendProtocolLogMaxAge 45.00:00:00
```


> [!NOTE]
> <UL>
> <LI>
> <P>Para configurar as configurações de log do protocolo no serviço de transporte de caixa de correio em um servidor de caixa de correio, use o cmdlet <STRONG>Set-MailboxTransportService</STRONG> . Para configurar as configurações de log do protocolo no serviço Front End Transport em um servidor de acesso para cliente, use o cmdlet <STRONG>Set-FrontEndTransportService</STRONG> .</P>
> <LI>
> <P>Definir os parâmetros <EM>SendProtocolLogPath</EM> ou <EM>ReceiveProtocolLogPath</EM> como o valor <CODE>$null</CODE> efetivamente desabilita o log de protocolo para todos os conectores de envio ou todos os conectores de recebimento no servidor. No entanto, configurar qualquer um desses parâmetros <CODE>$null</CODE> quando o log de protocolo é habilitado para todos os outros conectores no servidor, incluindo o dentro da organização enviar o conector ou o conector de envio de entrega de caixa de correio, os erros de log de eventos são gerados.</P>
> <LI>
> <P>Definindo os parâmetros <EM>ReceiveProtocolLogMaxAge</EM> ou <EM>SendProtocolLogMaxAge</EM> como o valor <CODE>00:00:00</CODE> impede a remoção automática de arquivos de log do protocolo devido à sua idade.</P></LI></UL>



## Como saber se funcionou?

Para verificar se você configurou com êxito as configurações de log do protocolo, faça o seguinte:

1.  No Shell, execute o comando a seguir:
    
    ```powershell
    <Get-TransportService | Get-MailboxTransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List SendConnectorProtocolLog*,ReceiveConnectorProtocolLog*
    ```

2.  Verifique se os valores exibidos são os valores que você configurou.

