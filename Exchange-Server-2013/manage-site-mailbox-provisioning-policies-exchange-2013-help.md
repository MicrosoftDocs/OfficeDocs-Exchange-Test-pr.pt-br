---
title: 'Gerenciar políticas de provisionamento de caixa de correio do site'
TOCTitle: Gerenciar políticas de provisionamento de caixa de correio do site
ms:assetid: 2f160d1a-a031-461f-8d29-c9cd49ca1645
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ710340(v=EXCHG.150)
ms:contentKeyID: 50485253
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar políticas de provisionamento de caixa de correio do site

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-21_

As políticas de provisionamento de caixa de correio de Site se aplicam somente ao email que enviado de e para a caixa de correio de site e o tamanho da caixa de correio de site no servidor do Exchange.

Para saber mais sobre caixas de correio de site, consulte [Caixas de correio locais](site-mailboxes-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o entrada "Caixas de correio do site" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Apesar de você poder criar várias políticas de provisionamento de caixa de correio de site, somente a política de provisionamento padrão será aplicada a todas as caixas de correio de site. Você não pode aplicar várias políticas dentro de sua organização.

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar uma política de provisionamento de caixa de correio de site

Este exemplo cria a política de provisionamento padrão SM\_ProvisioningPolicy com as seguintes configurações:

  - A cota de aviso para as caixas de correio do site é 9 GB.

  - As caixas de correio do site estão proibidas de receber mensagens quando o tamanho da caixa de correio chega a 10 GB.

  - O tamanho máximo das mensagens de email que podem ser enviadas para as caixas de correio do site é de 50 MB.

<!-- end list -->

    New-SiteMailboxProvisioningPolicy -Name SM_ProvisioningPolicy -IsDefault -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB -MaxReceiveSize 50MB

## Exibir as configurações de uma política de provisionamento de caixa de correio de site

Este exemplo retorna informações detalhadas sobre todas as políticas de provisionamento de caixa de correio de site em sua organização.

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List
```

Este exemplo retorna todas as políticas na sua organização, mas mostra apenas as informações de `IsDefault` para identificar que política é a política padrão.

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List IsDefault
```

## Fazer alterações em uma política de provisionamento de caixa de correio local existente

Este exemplo altera a política de provisionamento de caixas de correio locais chamado Padrão para permitir que o tamanho máximo das mensagens de email que podem ser recebidas pela caixa de correio local seja 25 MB. (Quando você instalar o Exchange, uma política de provisionamento chamada **Padrão** será criada.)

```powershell
Set-SiteMailboxProvisioningPolicy -Identity Default -MaxReceiveSize 25MB
```

Este exemplo altera a cota de alerta para 9,5 GB e a proibição da quota de envio e de recebimento para 10 GB.

    Set-SiteMailboxProvisioningPolicy -Identity Default -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB

## Configurar um prefixo de nome de caixa de correio da equipe

Quando uma nova caixa de correio da equipe é criada, por padrão seu endereço de email terá um prefixo. O prefixo de endereço de email permite que você pesquise facilmente e consulte caixas de correio de equipe e também possa ajudar usuários a reconhecê-los. Se quiser, você pode desabilitar o prefixo ou alterá-lo para seu locatário no Office 365 ou para uma determinada floresta em uma implantação local. Com o comportamento de prefixo padrão, se sua caixa de correio da equipe for criada no Office 365, o prefixo padrão será **SMO-**. Como alternativa, se sua caixa de correio da equipe for criada em sua implantação local, o prefixo será **SM-**. O comportamento padrão diferente entre essas premissas de forma que clientes híbridos não experimentem conflitos caso as caixas de correio da equipe sejam criadas em ambos os locais e então sejam sincronizadas entre locais.

Este exemplo desabilita a nomenclatura de prefixo ao configurar o parâmetro *DefaultAliasPrefixEnabled* como $false.

    Set-SiteMailboxProvisioningPolicy -Identity Default -DefaultAliasPrefixEnabled $false -AliasPrefix $null

Este exemplo altera a política de provisionamento padrão e define *AliasPrefix* como FOREST01.


> [!NOTE]
> Para implantações com várias florestas, é recomendável que um prefixo diferente seja usado em cada floresta para impedir conflitos quando objetos sejam sincronizados entre florestas, no caso de que caixas de correio da equipe tiverem sido criadas com o mesmo nome em duas ou mais florestas.



    Set-SiteMailboxProvisioningPolicy -Identity Default -AliasPrefix FOREST01 -DefaultAliasPrefixEnabled $false


> [!NOTE]
> No caso de uma implantação híbrida onde você tiver o Exchange local e no Office 365, todas caixas de correio da equipe baseadas em nuvem serão criadas com o prefixo <STRONG>SMO-</STRONG>. Os prefixos são diferentes no Office 365 e no Exchange local de forma que clientes híbridos não experimentem conflitos caso as caixas de correio da equipe sejam criadas em ambos os locais e então sincronizadas entre locais. O parâmetro AliasPrefix tem precedência sobre o parâmetro DefaultAliasPrefixEnabled; portanto, se o parâmetro <EM>AliasPrefix</EM> for definido como uma cadeia de caracteres válida e não nula, cada nova caixa de correio da equipe terá essa cadeia de caracteres como prefixo do alias.



## Excluir uma política de provisionamento de caixa de correio de site

Este exemplo exclui a política de caixa de correio de site padrão que foi criada durante a Instalação do Setup.

```powershell
Remove-SiteMailboxProvisioningPolicy -Identity Default
```


> [!IMPORTANT]
> Você deve primeiro criar e designar uma política padrão antes de poder remover a política chamada <STRONG>Padrão</STRONG>.



## Para obter mais informações

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

[New-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/pt-br/library/jj218647\(v=exchg.150\))

[Get-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/pt-br/library/jj218617\(v=exchg.150\))

[Set-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/pt-br/library/jj218624\(v=exchg.150\))

[Remove-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/pt-br/library/jj218672\(v=exchg.150\))

