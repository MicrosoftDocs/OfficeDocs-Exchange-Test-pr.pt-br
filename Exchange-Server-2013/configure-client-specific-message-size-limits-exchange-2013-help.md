---
title: 'Configurar limites de tamanho de mensagem para o cliente: Exchange 2013 Help'
TOCTitle: Configurar limites de tamanho de mensagem específicos para o cliente
ms:assetid: fef9ca78-b68f-4342-ada0-881ab985ce3c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh529949(v=EXCHG.150)
ms:contentKeyID: 52058897
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar limites de tamanho de mensagem específicos para o cliente

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-01-26_

No Microsoft Exchange Server 2013, há vários limites de tamanho de mensagem diferente que se aplicam às mensagens conforme elas passam pela sua organização do Exchange. Para obter mais informações, consulte [Limites de tamanhos de mensagens](message-size-limits-exchange-2013-help.md).

No entanto, há limites de tamanho de mensagem específicos para o cliente, que você pode definir para Outlook Web App e clientes de email que usam ActiveSync ou Serviços Web do Exchange (EWS). Se você alterar os limites de tamanho de mensagem em toda a organização do Exchange, você precisará verificar se o tamanho da mensagem limites para Outlook Web App, ActiveSync, e serviços Web do Exchange estão definidos de acordo. Você pode configurar esses valores nos arquivos Web. config nos servidores de acesso para cliente e caixa de correio. Esses limites são descritas nas tabelas a seguir.

### ActiveSync

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Função do servidor</th>
<th>Arquivo de configuração</th>
<th>Chaves e valores padrão</th>
<th>Tamanho</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acesso do cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   Não está presente por padrão (consulte comentários).</p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Acesso do cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>quilobytes</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de Correio</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   Não está presente por padrão (consulte comentários).</p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Caixa de Correio</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>quilobytes</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de Correio</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>&lt;add key=&quot;MaxDocumentDataSize&quot; value=&quot;10240000&quot;&gt;</code></p></td>
<td><p>bytes</p></td>
</tr>
</tbody>
</table>


**Comentários sobre os limites de ActiveSync**

Por padrão, há sem tecla *maxAllowedContentLength* nos arquivos `web.config` para ActiveSync. No entanto, o tamanho máximo da mensagem para ActiveSync é afetado pelo valor **maxAllowedContentLength** que é aplicado a todos os sites da web no servidor. O valor padrão é 30000000 bytes (30 MB). Para ver esses valores para ActiveSync em servidores de caixa de correio no Gerenciador do IIS e servidores de acesso para cliente, execute as seguintes etapas:

1.  Execute uma das seguintes etapas:
    
      - Nos servidores de acesso para cliente, abra **O Gerenciador do IIS**, navegue em **Sites** \> **Default Web Site** e selecione **Microsoft-Server-ActiveSync**.
    
      - Nos servidores de correio, abra **O Gerenciador do IIS**, navegue em **Sites** \> **Exchange Back-End** e selecione **Microsoft-Server-ActiveSync**.

2.  Verifique se o **Modo de exibição de recursos** está marcada e clique duas vezes em **Editor de configuração**, na seção **gerenciamento** de.

3.  Clique na seta suspensa no campo de **seção**, navegue até **System. webServer** \> **segurança** e selecione **requestFiltering**.

4.  Nos resultados da, expanda **requestLimits** e você verá **maxAllowedContentLength** e o valor padrão 30000000 (bytes).

Para alterar o valor de **maxAllowedContentLength** , insira um novo valor em bytes e clique em **Aplicar**. Você precisa alterar o valor nos servidores de acesso para cliente e nos servidores de caixa de correio. Depois de alterar o valor no Gerenciador do IIS, uma nova chave de *maxAllowedContentLength* é gravada no arquivo de `web.config` correspondente (`%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config` nos servidores de acesso para cliente) e `%ExchangeInstallPath%ClientAccess\Sync\web.config` nos servidores de caixa de correio.

Para alterar o tamanho máximo da mensagem para clientes de ActiveSync, você precisará alterar o valor de *maxRequestLength* no arquivo `web.config` nos servidores de acesso para cliente e caixa de correio, *MaxDocumentDataSize* no arquivo `web.config` nos servidores de correio e *maxAllowedContentLength* no Gerenciador do IIS nos servidores de acesso para cliente e caixa de correio.

### Serviços Web do Exchange

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atender a função</th>
<th>Arquivo de configuração</th>
<th>Chaves e valores padrão</th>
<th>Tamanho</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acesso do cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Caixa de Correio</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de Correio</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p>14 instâncias do <code>maxReceivedMessageSize=&quot;67108864&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
</tbody>
</table>


**Comentários sobre os limites de serviços Web do Exchange**

  - Há 14 instâncias separadas do valor `maxReceivedMessageSize="67108864"` que correspondem aos diferentes combinações das ligações (http e https) e os métodos de autenticação.

  - Para alterar o tamanho máximo da mensagem para clientes de serviços Web do Exchange, você precisará alterar o valor de *maxAllowedContentLength* em arquivos de `web.config` e todas as instâncias de 14 de `maxReceivedMessageSize="67108864"` no arquivo `web.config` nos servidores de caixa de correio.

  - No arquivo `web.config` nos servidores de caixa de correio, há também duas instâncias do valor `maxReceivedMessageSize="1048576"` para ligações **UMLegacyMessageEncoderSoap11Element** que você não precisa modificar.

  - *maxRequestLength* é uma configuração do ASP.NET que está presente em ambos os arquivos Web. config, mas não é usada pelos serviços Web do Exchange, portanto você não precisa modificá-lo.

### Outlook Web App

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Função do servidor</th>
<th>Arquivo de configuração</th>
<th>Chaves e valores padrão</th>
<th>Tamanho</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acesso do cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Acesso do cliente</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>quilobytes</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de Correio</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Caixa de Correio</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>quilobytes</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de Correio</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 instâncias do <code>maxReceivedMessageSize=&quot;35000000&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
<tr class="even">
<td><p>Caixa de Correio</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 instâncias do <code>maxStringContentLength=&quot;35000000&quot;</code></p></td>
<td><p>bytes</p></td>
</tr>
</tbody>
</table>


**Comentários sobre os limites de Outlook Web App**

  - No arquivo `web.config` nos servidores de caixa de correio, há duas instâncias separadas dos valores `maxReceivedMessageSize="35000000"` e `maxStringContentLength="35000000"` que correspondem a ligações http e https.

  - Para alterar o tamanho máximo da mensagem para clientes Outlook Web App, você precisará alterar todos esses valores em ambos os arquivos, incluindo ambas as instâncias de *maxReceivedMessageSize* e *maxStringContentLength* no arquivo `web.config` nos servidores de caixa de correio.

  - No arquivo `web.config` nos servidores de correio, há também uma instância do valor `maxStringContentLength="102400"` para a ligação **MsOnlineShellService** que não será necessário modificar.

Para todos os limites de tamanho de mensagem, você precisa definir valores que sejam maiores que os tamanhos reais que deseja aplicar. Este aumento é necessário para lidar com o inevitável aumento no tamanho das mensagens que ocorre após os anexos e outros dados binários serem codificados como Base64. A codificação Base64 aumenta o tamanho da mensagem em aproximadamente 33%, então os valores que você especificar para qualquer limite de tamanho de mensagem são aproximadamente 33% maiores que os tamanhos reais utilizados. Por exemplo, se você especificar um valor de tamanho de mensagem máximo de 64 MB, pode esperar um tamanho realista de aproximadamente 48 MB.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Permissões do Exchange não se aplicam aos procedimentos neste tópico. Esses procedimentos são realizados no sistema operacional do Exchange Server.

  - As alterações salvas no arquivo de configuração Web.config são aplicadas após a reinicialização do IIS.

  - Para permitir um aumento de 33% no tamanho devido à codificação Base64, multiplique o novo valor máximo desejado em megabytes por 4/3. Para converter o valor em kilobytes, multiplique por 1024. Para converter o valor em bytes, multiplique por 1048756 (1024\*1024). Observe que o aumento de tamanho causado pela codificação Base64 pode ser maior que 33% e depende de vários fatores, por exemplo, o tamanho do anexo, o tipo, a compressão e o cliente de email usado para compor e enviar a mensagem.

  - Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o bloco de notas para definir um limite de tamanho de mensagem específicos para o cliente

1.  Abra os arquivos Web. config apropriados no bloco de notas. Por exemplo, para abrir os arquivos Web. config para os clientes Serviços Web do Exchange, execute os seguintes comandos:
    
    ```powershell
        Notepad %ExchangeInstallPath%ClientAccess\exchweb\ews\web.config
        Notepad %ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config
    ```

2.  Encontre as chaves relevantes nos arquivos Web. config apropriado conforme descrito nas tabelas anteriormente no tópico. Por exemplo, para clientes Serviços Web do Exchange, encontre a chave *maxAllowedContentLength* nos arquivos e todas as instâncias de 14 do valor `maxReceivedMessageSize="67108864"` no arquivo de `web.config` nos servidores de caixa de correio.
    
    ```powershell
        <requestLimits maxAllowedContentLength="67108864" />
        ...maxReceivedMessageSize="67108864"...
    ```

    Por exemplo, para permitir um tamanho máximo de mensagem com codificação Base64 de aproximadamente 64 MB, altere todas as instâncias de `67108864` para `89478486` (64\*4/3\*1048756):
    
    ```powershell
        <requestLimits maxAllowedContentLength="89478486" />
        ...maxReceivedMessageSize="89478486"...
    ```

3.  Quando tiver terminado, salve e feche os arquivos Web. config.

4.  Reinicie o IIS executando o seguinte comando:
    
    ```powershell
    IISReset /noforce
    ```

## Configurar os limites de tamanho de mensagem específicos para o cliente da linha de comando

Em vez de usar o bloco de notas, você também pode configurar os limites de tamanho de mensagem específicos para o cliente da linha de comando. Abra um prompt de comando elevado no servidor Exchange (uma janela de Prompt de comando para abrir, selecione **Executar como administrador** ) e execute os comandos apropriados para os limites que você deseja configurar.

**Observações**:

  - Os valores de tamanho nos comandos são os valores padrão, portanto você precisará alterá-los.

  - Preste atenção se o valor é em bytes ou quilobytes.

**ActiveSync**

```powershell
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:appSettings /[key='MaxDocumentDataSize'].value:10240000
```

**Serviços Web do Exchange**

```powershell
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpsBinding'].maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpBinding'].maxReceivedMessageSize:67108864
```

**Outlook Web App**

```powershell
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].readerQuotas.maxStringContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].readerQuotas.maxStringContentLength:35000000
```

## Como saber se funcionou?

Para verificar se você configurou com êxito o limite de tamanho de mensagem específicos para o cliente, você precisa enviar uma mensagem de teste de e para uma caixa de correio que está sendo acessada pelo cliente afetado. Você pode tentar alguns anexos menores ou um anexo grande, portanto, as mensagens de teste são aproximadamente 33% menor que o valor que você configurou. Por exemplo, um valor configurado de 85 MB resulta em um tamanho de mensagem máximo realista de aproximadamente 64 MB.

