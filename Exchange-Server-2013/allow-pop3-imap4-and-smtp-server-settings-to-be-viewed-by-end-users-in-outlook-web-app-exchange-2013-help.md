---
title: 'Exibir configurações POP3, IMAP4 e SMTP para usuários no Outlook Web App'
TOCTitle: Permitir que as configurações dos servidores POP3, IMAP4 e SMTP sejam visualizadas pelos usuários finais no Outlook Web App
ms:assetid: bd22bf7e-3bf7-45e6-8790-919b780166f6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg298947(v=EXCHG.150)
ms:contentKeyID: 50556268
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permitir que as configurações dos servidores POP3, IMAP4 e SMTP sejam visualizadas pelos usuários finais no Outlook Web App

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-28_

Se seus usuários utilizarem POP3 ou IMAP4 para se conectarem às suas respectivas caixas de correio do MicrosoftExchange Server 2013, eles precisam conhecer as configurações corretas de servidor para se conectarem. Depois de uma instalação padrão do Exchange 2013, seus usuários não poderão procurar suas próprias configurações de servidor de entrada POP 3 ou IMAP4 ou de servidor de saída SMTP. No entanto, o Exchange pode ser configurado para que seus usuários possam procurar suas próprias configurações usando o MicrosoftOutlook Web App.

Depois que você executar esses procedimentos, seus usuários poderão procurar suas configurações de servidor no Outlook Web App, desta maneira:

1.  No Outlook Web App, clique em **Configurações** \> **Opções**.

2.  Em **Opções**, clique em **Conta** \> **Minha conta** \> **Configurações de acesso POP ou IMAP**.

Para mais informações relacionadas a POP3 e IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o Shell para permitir que usuários POP3 e IMAP4 vejam suas configurações de entrada POP3 e IMAP4 no Outlook Web App

As entradas "configurações POP3" e "configurações IMAP4" do Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Este exemplo permite que as configurações de servidores POP3 externos sejam visualizadas por usuários finais.

```powershell
Set-PopSettings -ExternalConnectionSettings {Dublin01.Contoso.com:995:SSL}
```

Para informações detalhadas sobre sintaxes e parâmetros, confira [Set-PopSettings](https://technet.microsoft.com/pt-br/library/aa997154\(v=exchg.150\)).

Este exemplo permite que as configurações de servidores IMAP4 externos sejam visualizadas por usuários finais.

```powershell
Set-ImapSettings -ExternalConnectionSettings {Dublin01.Contoso.com:993:SSL}
```

Para informações detalhadas sobre sintaxes e parâmetros, confira [Set-ImapSettings](https://technet.microsoft.com/pt-br/library/aa998252\(v=exchg.150\)).

Para aplicar essas alterações, você deve reiniciar o IIS. Você não precisa reiniciar os serviços POP3. Para reiniciar o IIS, em um prompt de comando, digite o seguinte:

```powershell
iisreset
```

## Como saber se funcionou?

Para verificar se você configurou o Exchange para permitir que usuários exibam suas configurações de servidor POP3:

1.  Execute o seguinte comando no Shell.
    
    ```powershell
Get-PopSettings | format-list
```

2.  Verifique se a propriedade *ExternalConnectionSettings* está definida.

Para verificar se você configurou o Exchange para permitir que usuários exibam suas configurações de servidor IMAP4:

1.  Execute o seguinte comando no Shell.
    
    ```powershell
Get-ImapSettings | format-list
```

2.  Verifique se a propriedade *ExternalConnectionSettings* está definida.

## Usar o Shell para permitir que usuários POP3 e IMAP4 vejam suas configurações de saída SMTP no Outlook Web App

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de recebimento" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

Este exemplo permite que as configurações de servidores SMTP internos e externos sejam visualizadas por usuários finais usando o Outlook Web App.

    Get-ReceiveConnector "*Client Frontend*" | Set-ReceiveConnector -Fqdn Server.Contoso.com -AdvertiseClientSettings $true 

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125140\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você configurou o Exchange para permitir que usuários exibam suas configurações de servidor SMTP:

1.  Execute o seguinte comando no Shell.
    
    ```powershell
Get-ReceiveConnector | format-list
```

2.  Se a propriedade *AdvertiseClientSettings* estiver definida como `true`, os usuários poderão ver suas configurações de servidor SMTP no Outlook Web App. Se a propriedade *AdvertiseClientSettings* estiver definida como `false`, os usuários não poderão ver suas configurações de servidor SMTP no Outlook Web App.

## Para saber mais

Depois de permitir que usuários finais visualizem suas respectivas configurações de POP3, IMAP4 e SMTP, você também poderá:

[Habilitar ou desabilitar o acesso POP3 de um usuário](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[Habilitar ou desabilitar o acesso de IMAP4 para um usuário](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

