---
title: Solucionando problemas de OWA. Conjunto de integridade de Protocol.Dep
TOCTitle: Solucionando problemas de OWA. Conjunto de integridade de Protocol.Dep
ms:assetid: f39c63d5-f161-4eee-9415-05f3355e7cc7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.owa.protocol.dep(v=EXCHG.150)
ms:contentKeyID: 54652046
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de OWA. Conjunto de integridade de Protocol.Dep

 

_**Aplica-se a:** Exchange Server 2013, Project Server 2013_

_**Tópico modificado em:** 2016-12-09_

O conjunto de integridade **OWA.Protocol.DEP** monitora a integridade geral dos serviços de mensagens instantâneas (IM) de mensagens no Outlook Web App integradas entre Lync 2013 e Exchange 2013. Para obter mais informações sobre como habilitar o recurso de mensagens instantâneas no Outlook Web App, consulte [integrando Microsoft Lync Server 2013 e o Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418).

Se você receber um alerta que indica que o conjunto de integridade **OWA.Protocol.DEP** não está íntegro, isso indica um problema que poderá impedir mensagens instantâneas funcionando corretamente no Outlook Web App.

## Explicação

O serviço **OWA.Protocol.DEP** é monitorado usando as seguintes sondas e monitores.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sonda</th>
<th>Conjunto de integridade</th>
<th>Monitores associados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>OwaIMInitializationFailedMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>OWA.Protocol.DEP</p></td>
<td><p>WacDiscoveryFailureEventMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Ação do usuário

É possível que o serviço recuperados após ele emitiu o alerta. Portanto, quando você recebe um alerta que especifica o conjunto de integridade **OWA.Protocol.DEP** não está íntegro, primeiro verificar se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções a seguir.

## Ações de recuperação para o erro: "InstantMessageOCSProvider.InitializeEndpointManager. Nenhuma configuração do registro para o provedor de IM."

Esse erro indica que uma chave de registro necessária está ausente no servidor de caixa de correio. Essa chave do registro deve ter sido configurada quando o Microsoft Unified Communications Managed API (UCMA) 4.0 foi instalado no servidor. A chave do registro ausente é:

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\MSExchange OWA\InstantMessaging

Essa chave deve conter uma cadeia de caracteres **ImplementationDLLPath** que aponta para o `Microsoft.Rtc.Internal.Ucweb` DLL. O local padrão é `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP\Microsoft.Rtc.Internal.Ucweb.dll`.

Para corrigir esse problema, reinstale o UCMA 4.0 ou criar manualmente a chave do registro. Você pode baixar UCMA 4.0 aqui: [Unified Communications Managed API 4.0 Runtime](https://go.microsoft.com/fwlink/p/?linkid=260990).

## Ações de recuperação para o erro: "InstantMessageOCSProvider.InitializeEndpointManager. IM provider não encontrada."

Esse erro indica que o arquivo DLL `Microsoft.Rtc.Internal.Ucweb` está ausente no servidor de caixa de correio. Este arquivo deve ter sido instalado quando UCMA 4.0 foi instalado no servidor. O local padrão é `C:\Program Files\Microsoft UCMA 4.0\Runtime\SSP`.

Para corrigir esse problema, reinstale o UCMA 4.0. Para obter mais informações, consulte [Unified Communications Managed API 4.0 Runtime](https://go.microsoft.com/fwlink/p/?linkid=260990).

## Ações de recuperação para o erro: "nome do servidor de mensagens instantâneas é definido como nulo ou vazia na Web. config."

Esse erro indica que o servidor de Lync 2013 não está definido no arquivo de configuração (Web. config) do aplicativo Outlook Web App no servidor de caixa de correio. Este arquivo `web.config` está localizado em `%ExchangeInstallPath%ClientAccess\Owa`e deve conter uma chave chamada **IMServerName** que especifica o FQDN do servidor Lync 2013. Para corrigir esse problema, siga estas etapas:

1.  Em uma janela de prompt de comando, abra o arquivo Web. config de Outlook Web App no bloco de notas executando o seguinte comando:
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  Procure uma chave chamada **IMServerName**. Se ele for encontrado, verifique se o FQDN do servidor Lync 2013. Se a chave não for encontrada, você deve adicioná-lo executando as etapas a seguintes.
    
    1.  Encontre a marca denominada **\<appSettings\>**.
    
    2.  No nó da **\<appSettings\>** , adicione a seguinte linha:
        
            <add key="IMServerName" value="Lync Server FQDN" />
        
        Por exemplo:
        
            <add key="IMServerName" value="lync01.contoso.com" />
    
    3.  Para aplicar as alterações no Outlook Web App, execute o seguinte comando:
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## Ações de recuperação para o erro: "A impressão digital do certificado Instant Messaging está nula ou vazia na Web. config".

Esse erro indica que o certificado que é usado para integrar Lync 2013 e Outlook Web App não está definido no arquivo de configuração (Web. config) do aplicativo Outlook Web App no servidor de caixa de correio. Este arquivo `web.config` está localizado em `%ExchangeInstallPath%ClientAccess\Owa`e deve conter uma chave chamada **IMCertificateThumbprint** que especifica o thumbprint do certificado (hash).

Você pode obter o valor da impressão digital do certificado usando o cmdlet **Get-ExchangeCertificate** ou no Centro de administração do Exchange (EAC) em **servidores** \> **certificados**.

Para corrigir esse problema, siga estas etapas:

1.  Em uma janela de prompt de comando, abra o arquivo Web. config de Outlook Web App no bloco de notas executando o seguinte comando:
    
        Notepad %ExchangeInstallPath%ClientAccess\Owa\web.config

2.  Procure uma chave chamada **IMCertificateThumbprint**. Se ele for encontrado, verifique se que o valor de impressão digital está correto. Se a chave não for encontrada, você deve adicioná-lo executando as seguintes etapas:
    
    1.  Encontre a marca denominada **\<appSection\>**.
    
    2.  No nó da **\<appSection\>** , adicione a seguinte linha:
        
            <add key="IMCertificateThumbprint" value="thumbprint"/>
        
        Por exemplo:
        
            <add key="IMCertificateThumbprint" value="35CB4C441D55506C88E59B7946B567A4F45B3B5C" />
    
    3.  Para aplicar as alterações no Outlook Web App, execute o seguinte comando:
        
            %windir%\system32\inetsrv\appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

## Ações de recuperação para o erro: "IM certificado com impressão digital \< valor \> não foi encontrado."

Esse erro indica que o certificado que é usado para integrar Lync 2013 e Outlook Web App não foi encontrado no servidor de caixa de correio. Esse certificado deve ser instalado no servidor caixa de correio e o servidor de Lync 2013 e deve ser confiável para ambos os servidores. Para obter mais informações sobre os requisitos de certificado, consulte Habilitando sistema de mensagens instantâneas, na seção do Outlook Web App [integrando Microsoft Lync Server 2013 e o Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418).

Você pode fazer a correspondência ele valor da impressão digital no erro ao certificado usando o cmdlet **Get-ExchangeCertificate** ou no Exchange admin center (EAC) em **servidores** \> **certificados**.

## Ações de recuperação para o erro: "IM certificado expirou."

Esse erro indica que o certificado usado para integrar Lync 2013 e Outlook Web App expirou. Para resolver esse erro, você precisará renovar o certificado.

Você pode fazer a correspondência ele valor da impressão digital no erro ao certificado usando o cmdlet **Get-ExchangeCertificate** ou no Centro de administração do Exchange (EAC) em **servidores** \> **certificados**.

## Ações de recuperação para o erro: "IM certificado não se tornou válido ainda."

Esse erro indica que o certificado que é usado para integrar o Lync 2013 e Outlook Web App tem datas inválidas. Para resolver esse erro, você precisa configurar um novo certificado e você precisa adicionar o novo valor de impressão digital na chave **IMCertificateThumbprint** no `%ExchangeInstallPath%ClientAccess\Owa\web.config` . Para obter mais informações sobre os requisitos de certificado, consulte Habilitando sistema de mensagens instantâneas, na seção do Outlook Web App [integrando Microsoft Lync Server 2013 e o Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418).

## Ações de recuperação para o erro: "Certificado de mensagens Instantâneas não tem uma chave privada."

Esse erro indica que o certificado que é usado para integrar Lync 2013 e Outlook Web App não tem uma chave privada. Para resolver esse erro, você precisa configurar um novo certificado que tem uma chave privada, e você precisa adicionar o novo valor de impressão digital na chave **IMCertificateThumbprint** no `%ExchangeInstallPath%ClientAccess\Owa\web.config` . Para obter mais informações sobre os requisitos de certificado, consulte Habilitando sistema de mensagens instantâneas, na seção do Outlook Web App [integrando Microsoft Lync Server 2013 e o Microsoft Outlook Web App 2013](https://go.microsoft.com/fwlink/p/?linkid=280418).

