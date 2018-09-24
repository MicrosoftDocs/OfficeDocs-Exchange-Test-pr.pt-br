---
title: 'Definir Configurações Anti-Spam em Caixas de Correio: Exchange 2013 Help'
TOCTitle: Definir Configurações Anti-Spam em Caixas de Correio
ms:assetid: 868d7fd8-e817-46ba-9b67-edf2f50b9494
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123559(v=EXCHG.150)
ms:contentKeyID: 50486074
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir Configurações Anti-Spam em Caixas de Correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-11-17_

Você pode definir configurações antispam específicas em caixas de correio individuais que sejam diferentes das configurações antispam aplicadas ao resto das caixas de correio na sua organização Exchange. Ao definir uma configuração antispam em uma caixa de correio, essa configuração substitui a filtragem de conteúdo correspondente na organização ou a configuração antispam padrão da organização.


> [!TIP]
> Em 1 de novembro de 2016, o Microsoft interrompeu a produção de atualizações de definição de spam para os Filtros SmartScreen, no Exchange e no Outlook. As definições de spam existentes para SmartScreen permanecerão inalteradas, mas a respectiva eficácia provavelmente diminuirá ao longo do tempo. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Substituição do suporte para SmartScreen no Outlook e no Exchange</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recursos antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) e entrada "Antispam" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Por padrão, os recursos antispam não estão habilitados no serviço de Transporte em um servidor de Caixa de Correio. Normalmente, você apenas habilita os recursos antispam em um servidor de Caixa de Correio se sua organização do Exchange não realiza nenhuma ação antes da filtragem antispam antes de aceitar mensagens de entrada. Para saber mais, confira [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - O valor do limite de SCL da pasta Lixo Eletrônico tem um comportamento diferente dos valores de exclusão, rejeição e quarentena de SCL. Para saber mais, confira [Limite do Nível de Confiança de Spam](spam-confidence-level-threshold-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para configurar recursos antispam em uma única caixa de correio

Para definir as configurações antispam em uma única caixa de correio, use a seguinte sintaxe.

    Set-Mailbox <MailboxIdentity> -AntispamBypassEnabled <$true | $false> -RequireSenderAuthenticationEnabled <$true | $false> -SCLDeleteEnabled <$true | $false | $null> -SCLDeleteThreshold <0-9 | $null> -SCLJunkEnabled <$true | $false | $null > -SCLJunkThreshold <0-9 | $null> -SCLQuarantineEnabled <$true | $false | $null > -SCLQuarantineThreshold <0-9 | $null> -SCLRejectEnabled <$true | $false | $null > -SCLRejectThreshold <0-9 | $null>

Este exemplo configura a caixa de correio de um usuário chamado Pedro Gonçalves de modo que ela ignore todos os filtros antispam e receba na pasta Lixo Eletrônico do Microsoft Outlook mensagens que estão de acordo ou excedam o limite SCL de 5 da pasta Lixo Eletrônico.

```powershell
Set-Mailbox "Jeff Phillips" -AntispamBypassEnabled $true -SCLJunkEnabled $true -SCLJunkThreshold 4
```

## Como saber se funcionou?

Para verificar se os recursos antispam foram configurados com êxito em uma única caixa de correio, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-Mailbox <MailboxIdentity> | Format-List SCL*,Bypass*,*SenderAuth*

2.  Verifique se o valor apresentado é o valor que você configurou.

## Usar o Shell para configurar recursos antispam em múltiplas caixas de correio

Para definir todas as configurações antispam em várias caixas de correio, use a seguinte sintaxe.

    Get-Mailbox [<Filter>]| Set-Mailbox <Anti-Spam Settings>

Este exemplo habilita o limite de quarentena do SCL com um valor 7 em todas as caixas de correio no contêiner Usuários no domínio Contoso.com.

    Get-Mailbox -OrganizationalUnit Contoso.com/Users | Set-Mailbox -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## Como saber se funcionou?

Para verificar se os recursos antispam foram configurados com êxito em várias caixas de correio, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-Mailbox [<Filter>] | Format-List Name,SCL*,*SenderAuth*

2.  Verifique se os valores exibidos são os valores que você configurou.

## Usar o Shell para configurar limites de lixo eletrônico para todas as caixas de correio da sua organização

Execute o seguinte comando:

```powershell
Set-OrganizationConfig -SCLJunkThreshold <Integer>
```

Este exemplo define o limite de lixo eletrônico da organização como 5.

```powershell
Set-OrganizationConfig -SCLJunkThreshold 5
```

## Como saber se funcionou?

Para verificar se os limites de lixo eletrônico foram configurados com êxito para todas as caixas de correio na sua organização, faça o seguinte:

1.  Execute o seguinte comando:
    
    ```powershell
Get-OrganizationConfig | Format-List SCLJunkThreshold
```

2.  Verifique se o valor apresentado é o valor que você configurou.

