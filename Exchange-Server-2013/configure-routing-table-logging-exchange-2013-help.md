---
title: 'Configurar o log de tabela de roteamento: Exchange 2013 Help'
TOCTitle: Configurar o log de tabela de roteamento
ms:assetid: 7184f8f7-4eb8-468a-aafe-b2d72868f820
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201696(v=EXCHG.150)
ms:contentKeyID: 50485801
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o log de tabela de roteamento

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Tabela de roteamento log periodicamente um instantâneo da tabela de roteamento é usado pelo Microsoft Exchange Server 2013 para rotear mensagens para seus destinos de registros.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Serviço de transporte" e entradas de "Servidor de transporte de borda" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - Você só pode usar o Shell para executar esse procedimento.

  - Para configurar o intervalo de tempo para recálculo automático da tabela de roteamento, você deve modificar o arquivo de configuração de aplicativo XML EdgeTransport.exe.config. Você pode salvar esse arquivo de alterações são aplicadas depois que você reiniciar o serviço de transporte do Microsoft Exchange. Quando você reiniciar esse serviço, o fluxo de emails no servidor é interrompido temporariamente.

  - Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para configurar o log de tabela de roteamento

Execute o seguinte comando:
```powershell
    Set-TransportService <ServerIdentity> -RoutingTableLogMaxAge <dd.hh:mm:ss> -RoutingTableLogMaxDirectorySize <Size>  -RoutingTableLogPath <LocalFilePath>
```

Este exemplo define as seguintes configurações de log de tabela de roteamento no servidor de caixa de correio chamado Mailbox01:

  - Define o local dos arquivos de log de tabela roteamento D:\\Routing log de tabela. Observe que se a pasta não existir, ele será criado para você.

  - Define o tamanho máximo da pasta de log de tabela de roteamento como 70 MB.

  - Define a idade máxima de um arquivo de log de tabela roteamento como 45 dias.

<!-- end list -->
```powershell
    Set-TransportService Mailbox01 -RoutingTableLogPath "D:\Routing Table Log" -RoutingTableLogMaxDirectorySize 70MB -RoutingTableLogMaxAge 45.00:00:00
```


> [!NOTE]
> Definindo o parâmetro <EM>RoutingTableLogMaxAge</EM> como o valor <CODE>00:00:00</CODE> impede a remoção automática de arquivos de log de tabela de roteamento devido à sua idade.



## Como saber se funcionou?

Para verificar se você configurou com êxito log de tabela de roteamento, faça o seguinte:

1.  No Shell, execute o comando a seguir:
```powershell   
        Get-TransportService <ServerIdentity> | Format-List RoutingTableLog*
```

2.  Verifique se os valores exibidos são os valores que você configurou.

## Usar o Prompt de comando para configurar o intervalo de recálculo automático da tabela de roteamento no arquivo EdgeTransport.exe.config

1.  Em uma janela do Prompt de Comando, abra o arquivo de configuração de aplicativo EdgeTransport.exe.config no Bloco de notas executando o seguinte comando:
    
    ```powershell
    Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

2.  Modifica a seguinte chave na seção `<appSettings>` .
    
    ```command line
    <add key="RoutingConfigReloadInterval" value="<hh:mm:ss>" />
    ```
    
    Por exemplo, para alterar o intervalo de recálculo automático da tabela de roteamento para 10 horas, use o seguinte valor:
    
    ```command line
    <add key="RoutingConfigReloadInterval" value="10:00:00" />
    ```

3.  Quando terminar, salve e feche o arquivo EdgeTransport.exe.config.

4.  Reinicie o serviço de Transporte do Microsoft Exchange executando o seguinte comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Como saber se funcionou?

Para verificar se você configurou com êxito o intervalo para o recálculo automático da tabela de roteamento, verifique se que o log de tabela de roteamento é atualizado durante o intervalo de tempo especificado.

Observe que a tabela de roteamento será recalculada e registrada anteriormente que o valor especificado pela chave *RoutingConfigReloadInterval* se qualquer uma das seguintes condições ocorrerem:

  - Uma alteração de configuração de roteamento é detectada. Por exemplo, um conector de envio ou um conector de recebimento é adicionado, removido ou modificado ou a hora de 6 renovação de token Kerberos ocorre.

  - O serviço de transporte do Microsoft Exchange foi iniciado.

