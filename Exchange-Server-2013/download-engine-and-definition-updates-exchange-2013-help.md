---
title: 'Baixar atualizações de mecanismo e definições: Exchange 2013 Help'
TOCTitle: Baixar atualizações de mecanismo e definições
ms:assetid: 8f2ca383-e463-4df0-aa5d-29afe2f81aaf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657471(v=EXCHG.150)
ms:contentKeyID: 50486144
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Baixar atualizações de mecanismo e definições

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Microsoft os administradores Exchange Server 2013 podem baixar manualmente mecanismo antimalware e atualizações de definições (assinatura). É altamente recomendável que você baixe as atualizações de mecanismo e definições em seu servidor Exchange antes de colocá-lo em produção.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Você só pode usar o Shell para executar esse procedimento. Para saber como abrir o Shell de Gerenciamento do Exchange em sua organização Exchange local, confira [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)).

  - Para baixar atualizações, seu computador deve ser capaz de acessar a Internet e ser capaz de estabelecer uma conexão na porta TCP 80 (HTTP). Se sua organização usa um servidor proxy para acessar a Internet, consulte a seção de usar o Shell para configurar definições de servidor proxy para atualizações de antimalware neste tópico.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Anti-malware? entrada no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para baixar manualmente as atualizações de mecanismos e definições

Para baixar atualizações de mecanismo e definições, execute o seguinte comando:

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity <FQDN of server>

Este exemplo baixa manualmente as atualizações de mecanismo e definições no servidor Exchange chamado mailbox01. contoso.com:

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com

Opcionalmente, você pode usar o parâmetro *EngineUpdatePath* para baixar atualizações em outro lugar que o local padrão do `http://forefrontdl.microsoft.com/server/scanengineupdate`. Você pode usar esse parâmetro para especificar um endereço HTTP alternativo ou um caminho UNC. Se você especificar um caminho UNC, o serviço de rede deve ter acesso ao caminho.

Este exemplo baixa manualmente as atualizações de mecanismo e definições no servidor Exchange chamado mailbox01. contoso.com a partir o do caminho UNC `\\FileServer01\Data\MalwareUpdates`:

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com -EngineUpdatePath \\FileServer01\Data\MalwareUpdates

## Como saber se funcionou?

Para verificar se as atualizações foram baixadas com êxito, acesse o Visualizador de Eventos e exiba o log de eventos. Recomendamos que você filtre somente os eventos FIPFS, conforme descrito no procedimento a seguir.

1.  No menu **Iniciar**, clique em **Todos os programas** \> **Ferramentas Administrativas** \> **Visualizador de Eventos**.

2.  No Visualizador de Eventos, expanda a pasta **Logs de Eventos** e clique em **Aplicativo**.

3.  No menu **Ações**, clique em **Filtrar Log Atual**.

4.  Na caixa de diálogo **Filtrar Log Atual**, na lista suspensa **Fontes de evento**, marque a caixa de seleção **FIPFS** e clique em **OK**.

Se as atualizações de mecanismo forem baixadas com êxito, você verá a ID de Evento 6033, que será parecida com:

`MS Filtering Engine Update process performed a successful scan engine update.`

`Scan Engine: Microsoft`

`Update Path: http://forefrontdl.microsoft.com/server/scanengineupdate`

`Last Update time: ‎2012‎-‎08‎-‎16T13:22:17.000Z`

`Engine Version: 1.1.8601.0`

`Signature Version: 1.131.2169.0`

## Usar o Shell para configurar definições de servidor proxy para atualizações de antimalware

Se sua organização usa um servidor proxy para controlar o acesso à Internet, será necessário identificar o servidor proxy para que o mecanismo antimalware e atualizações de definições podem ser baixadas com êxito. Configurações do servidor proxy que estão disponíveis usando a ferramenta de **Netsh.exe** , Internet Explorer as configurações de conexão e o parâmetro *InternetWebProxy* no cmdlet **Set-ExchangeServer** não afetam como antimalware atualizações são baixadas.

Para configurar as configurações do servidor proxy para atualizações de antimalware, execute as etapas a seguir.

1.  Execute o seguinte comando:
    
        Add-PsSnapin Microsoft.Forefront.Filtering.Management.Powershell

2.  Use os cmdlets **Get-ProxySettings** e **Set-ProxySettings** para exibir e configurar as definições de servidor de proxy que são usadas para baixar atualizações de antimalware. O cmdlet **Set-ProxySettings** usa a seguinte sintaxe:
    
        Set-ProxySettings -Enabled <$true | $false> -Server <Name or IP address of proxy server> -Port <TCP port of proxy server>
    
    Por exemplo, para configurar atualizações de antimalware para usar o servidor proxy no endereço 172.17.17.10 na porta TCP 80, execute o seguinte comando.
    
        Set-ProxySettings -Enabled $true -Server 172.17.17.10 -Port 80
    
    Para verificar as configurações do servidor proxy, execute o cmdlet **Get-ProxySettings** .

## Para obter mais informações

[Configurar políticas antimalware](configure-anti-malware-policies-exchange-2013-help.md)

