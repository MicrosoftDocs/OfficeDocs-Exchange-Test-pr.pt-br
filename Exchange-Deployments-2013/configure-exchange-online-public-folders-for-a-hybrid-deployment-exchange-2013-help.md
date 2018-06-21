---
title: 'Configurar pastas públicas do Exchange Online para uma implantação híbrida: Exchange 2013 Help'
TOCTitle: Configurar pastas públicas do Exchange Online para uma implantação híbrida
ms:assetid: d979edb3-967b-4431-8beb-0c236bf7f56d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt729076(v=EXCHG.150)
ms:contentKeyID: 72768735
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar pastas públicas do Exchange Online para uma implantação híbrida

 

_<strong>Aplica-se a:</strong>Exchange Server 2013_

_<strong>Tópico modificado em:</strong>2016-12-15_

**Resumo:** instruções para a habilitação de usuários Exchange 2013 para acessar pastas públicas no Exchange Online no local.

Em uma implantação híbrida, os usuários podem estar em Exchange Online, local ou ambos e suas pastas públicas são seja no Exchange Online ou local. Em alguns casos, os usuários online, talvez seja necessário acessar pastas públicas em seu ambiente do Exchange Server 2013 local. Da mesma forma, os usuários do Exchange 2013, talvez seja necessário acessar pastas públicas no Office 365 ou Exchange Online.

Este artigo descreve como permitir que os usuários em seu ambiente do Exchange 2013 local acessar pastas públicas do Exchange Online/Office 365. Para permitir que os usuários do Exchange Online/Office 365 acessar pastas públicas do Exchange 2013 local, consulte [Configurar pastas públicas do Exchange 2013 para uma implantação híbrida](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md).


> [!TIP]
> Se você tiver pastas públicas do Exchange 2010 ou Exchange 2007, consulte <A href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">Configurar pastas públicas locais herdadas para uma implantação híbrida</A>.



## O que você precisa saber antes de começar?

1.  Estas instruções pressupõem que você tenha usado o Assistente de Configuração Híbrida para configurar e sincronizar seus ambientes do Exchange Online e no local e que os registros DNS usados ​​para a Descoberta Automática da maioria dos usuários façam referência a um ponto de extremidade no local. Para obter mais informações, consulte [Assistente de Configuração Híbrida](hybrid-configuration-wizard-exchange-2013-help.md).

2.  Estas instruções pressupõem que Outlook Anywhere está habilitado e funcional em todos os servidores do Exchange local. Para obter informações sobre como habilitar o Outlook em qualquer lugar, consulte [Outlook em Qualquer Lugar](https://technet.microsoft.com/pt-br/library/bb123741\(v=exchg.150\)).

3.  Implementando a coexistência de pasta pública para uma implantação híbrida do Exchange com Office 365 pode exigir a corrigir conflitos durante o procedimento de importação. Conflitos podem acontecer devido ao endereço de email não roteáveis atribuído ao email habilitadas pastas públicas, está em conflito com outros usuários e grupos no Office 365 e outros atributos.

4.  Para acessar as pastas públicas entre locais, os usuários devem atualizar seus clientes do Outlook para a atualização pública de novembro de 2012 do Outlook ou posterior.
    
    1.  Baixar o novembro de 2012 atualização Outlook para o Outlook 2010, consulte [atualizar para Microsoft Outlook 2010 (kb2687623 edição) 32-Bit Edition](https://www.microsoft.com/en-us/download/details.aspx?id=35702).
    
    2.  Para baixar o novembro de 2012 atualização do Outlook para o Outlook 2007, consulte [atualização do Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/en-us/download/details.aspx?id=35718).

5.  Outlook 2011 para Mac e o Outlook para Mac para o Office 365, não há suporte para as pastas públicas entre locais. Os usuários devem estar no mesmo local em que as pastas públicas para acessá-los com o Outlook 2011 para Mac ou o Outlook para Mac para o Office 365. Além disso, os usuários cujas caixas de correio estão no Exchange Online não conseguirá acessar pastas públicas no local, usando o Outlook Web App.
    

    > [!TIP]
    > 2016 do Outlook para Mac é suportado para as pastas públicas entre locais. Se os clientes na sua organização usarem 2016 do Outlook para Mac, certifique-se de que eles tenham instalado a atualização de abril de 2016. Do contrário, os usuários não poderão acessar pastas públicas em uma coexistência ou uma topologia híbrida. Para obter mais informações, consulte <A href="https://technet.microsoft.com/pt-br/library/mt788631(v=exchg.150)">Acesso a pastas públicas com 2016 do Outlook para Mac</A>.



## Etapa 1: Baixar os scripts

1.  Baixe os seguintes arquivos de [Habilitados para email pastas públicas - sincronização de diretório do EXO para script no prem](https://go.microsoft.com/fwlink/p/?linkid=797795).
    
      - `Import-PublicFolderMailboxes.ps1`
    
      - `ImportPublicFolderMailboxes.strings.psd1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.ps1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.strings.psd1`

2.  Salve os arquivos no computador local em que você executará o PowerShell. Por exemplo, C:\\PFScripts.

## Etapa 2: Configurar a sincronização do diretório

Executar o script `Sync-MailPublicFoldersCloudToOnprem.ps1` sincronizará as pastas públicas habilitadas para email entre o Exchange Online e o seu ambiente do Exchange 2013 local. Permissões especiais atribuídas a pastas públicas habilitadas para email precisará ser recriados na nuvem, desde que o local entre permissões não são suportadas nos cenários de implantação híbrida. Para obter mais informações, consulte [Implantação híbrida do Exchange Server 2013](exchange-server-hybrid-deployments-exchange-2013-help.md).


> [!TIP]
> Pastas públicas habilitadas para email sincronizadas aparecerá como fins de fluxo de emails de objetos de contato para email e não serão visíveis no Centro de administração do Exchange. Consulte o comando Get-MailPublicFolder. Para recriar as permissões SendAs na nuvem, use o comando Add-RecipientPermission.



1.  No servidor Exchange 2013, execute o seguinte comando para sincronizar habilitados para email a pastas públicas do Exchange Online/Office 365 para o seu local local Active Directory.
    
        Sync-MailPublicFoldersCloudToOnprem.ps1 -Credential (Get-Credential)
    
    Onde `Credential` é o seu nome de usuário do Office 365 e senha.


> [!TIP]
> Recomendamos que você execute esse script diariamente para sincronizar suas pastas públicas habilitadas para email.



## Etapa 3: Configurar os usuários no local para acessar pastas públicas do Exchange Online

A etapa final deste procedimento é configurar a Exchange 2013 na organização local para permitir o acesso às pastas públicas Exchange Online.

Executar o script `Import-PublicFolderMailboxes.ps1` importará objetos de caixa de correio de pasta pública da nuvem como usuários habilitados para email ao seu ambiente local. O script também configurar os objetos importados como caixas de correio de pasta pública remoto.

1.  No servidor Exchange 2013, execute o seguinte comando para importar objetos de caixa de correio de pasta pública da nuvem para seu local Active Directory.
    
        Import-PublicFolderMailboxes.ps1 -Credential (Get-Credential)
    
    Onde `Credential` é o seu nome de usuário do Office 365 e senha.
    

    > [!TIP]
    > Recomendamos que você execute esse script diariamente para importar os objetos de caixa de correio de pasta pública porque sempre que caixas de correio de pasta pública atingem sua capacidade de limite, eles divididas automaticamente em várias caixas de correio novas. Portanto, você sempre deseja Certifique-se de que ter importado as caixas de correio de pasta pública mais recentes da nuvem.



2.  Habilite a Exchange 2013 na organização local acessar as pastas públicas Exchange Online.
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote


> [!TIP]
> Você deve aguardar até que a sincronização do ActiveDirectory concluiu para ver as alterações. Esse processo pode levar até 3 horas para ser concluída. Se você não quiser aguarde as sincronizações recorrentes que ocorrem a cada três horas, você pode forçar sincronização de diretórios, a qualquer momento. Para obter etapas detalhadas para forçar a sincronização de diretórios, consulte <A href="http://technet.microsoft.com/en-us/library/jj151771.aspx">Forçar sincronização de diretórios</A>.



## Como saber se funcionou?

1.  Faça logon no Outlook para um usuário que esteja no Exchange Online e execute os seguintes testes de pasta pública:
    
      - Visualize a hierarquia.
    
      - Verifique as permissões
    
      - Crie e exclua pastas públicas.
    
      - Publique conteúdo e exclua conteúdo de uma pasta pública.

