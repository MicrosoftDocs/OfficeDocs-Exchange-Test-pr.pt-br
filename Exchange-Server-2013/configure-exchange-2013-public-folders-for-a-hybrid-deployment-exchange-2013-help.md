---
title: 'Configurar pastas públicas do Exchange 2013 para uma implantação híbrida'
TOCTitle: Configurar pastas públicas do Exchange 2013 para uma implantação híbrida
ms:assetid: b828520f-022c-4fcb-ab68-e1c330e87c33
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn986544(v=EXCHG.150)
ms:contentKeyID: 65407509
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar pastas públicas do Exchange 2013 para uma implantação híbrida

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

**Resumo:**  instruções para habilitar os usuários do Exchange Online para acessar pastas públicas do local em seu ambiente do Exchange 2013.

Em uma implantação híbrida, os usuários podem estar em Exchange Online, local ou ambos, e suas pastas públicas são seja no Exchange Online ou local. Em alguns casos, os usuários online, talvez seja necessário acessar pastas públicas em seu ambiente do Exchange Server 2013 local. Da mesma forma, os usuários do Exchange 2013, talvez seja necessário acessar pastas públicas no Office 365 ou Exchange Online.


> [!TIP]
> Se você tiver pastas públicas do Exchange 2010 ou Exchange 2007, consulte <A href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">Configurar pastas públicas locais herdadas para uma implantação híbrida</A>.



Este artigo descreve como permitir que os usuários do Exchange Online/Office 365 acessar pastas públicas no Exchange 2013. Para permitir que usuários do Exchange 2013 local acessar pastas públicas no Exchange Online, consulte [Configurar pastas públicas do Exchange Online para uma implantação híbrida](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md).

Um usuário do Exchange Online/Office 365 deve ser representado por um objeto MailUser no ambiente Exchange local para acessar pastas públicas do Exchange 2013. Este objeto MailUser também deve ser local para o destino de hierarquia de pastas públicas do Exchange 2013. Se você tiver usuários do Office 365 que não estão atualmente representado local pelos objetos MailUser, consulte o artigo da Base de Conhecimento Microsoft 3106618 ["usuários do Exchange Online não podem acessar as pastas públicas locais herdadas"](https://go.microsoft.com/fwlink/p/?linkid=699451) para criar entidades correspondentes do local.

## O que você precisa saber antes de começar?

1.  Estas instruções pressupõem que você tenha usado o Assistente de Configuração Híbrida para configurar e sincronizar seus ambientes do Exchange Online e no local e que os registros DNS usados ​​para a Descoberta Automática da maioria dos usuários façam referência a um ponto de extremidade no local. Para obter mais informações, consulte [Assistente de Configuração Híbrida](https://technet.microsoft.com/pt-br/library/hh529921\(v=exchg.150\)).

2.  Estas instruções pressupõem que Outlook Anywhere está habilitado e funcional em todos os servidores do Exchange local. Para obter informações sobre como habilitar o Outlook em qualquer lugar, consulte [Outlook em Qualquer Lugar](outlook-anywhere-exchange-2013-help.md).

3.  Implementação da coexistência de pasta pública para uma implantação híbrida do Exchange com o Office 365 pode exigir a corrigir conflitos durante o procedimento de importação. Conflitos podem acontecer devido ao endereço de email não roteáveis atribuído ao email habilitadas pastas públicas, está em conflito com outros usuários e grupos no Office 365 e outros atributos.

4.  Para acessar as pastas públicas entre locais, os usuários devem atualizar seus clientes do Outlook para a atualização pública de novembro de 2012 do Outlook ou posterior.
    
    1.  Para baixar o novembro de 2012 atualização do Outlook para o Outlook 2010, consulte [Update para edição de 32 bits do Microsoft Outlook 2010 (kb2687623 edição)](https://www.microsoft.com/en-us/download/details.aspx?id=35702).
    
    2.  Para baixar o novembro de 2012 atualização do Outlook para o Outlook 2007, consulte [atualização do Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/en-us/download/details.aspx?id=35718).

5.  Outlook 2011 para Mac e o Outlook para Mac para o Office 365, não há suporte para as pastas públicas entre locais. Os usuários devem estar no mesmo local em que as pastas públicas para acessá-los com o Outlook 2011 para Mac ou o Outlook para Mac para o Office 365. Além disso, os usuários cujas caixas de correio estão no Exchange Online não conseguirá acessar pastas públicas do local usando Outlook Web App.
    

    > [!TIP]
    > 2016 do Outlook para Mac é suportado para as pastas públicas entre locais. Se os clientes na sua organização usarem 2016 do Outlook para Mac, certifique-se de que eles tenham instalado a atualização de abril de 2016. Caso contrário, os usuários não poderão acessar pastas públicas em uma topologia híbrida. Para obter mais informações, consulte <A href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Acesso a pastas públicas com 2016 do Outlook para Mac</A>.



## Etapa 1: Baixar os scripts

1.  Baixe os seguintes arquivos de [Habilitados para email pastas públicas - script de sincronização de diretório](https://www.microsoft.com/en-us/download/details.aspx?id=46381):
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  Salve os arquivos no computador local em que você executará o PowerShell. Por exemplo, C:\\PFScripts.

## Etapa 2: Configurar a sincronização de diretórios

O serviço de sincronização de diretório não sincronizar pastas públicas habilitadas para email. Executando o seguinte script sincronizará as pastas públicas habilitadas para email entre locais e Office 365. Permissões especiais atribuídas a pastas públicas habilitadas para email precisará ser recriados na nuvem, desde que a permissão de cruz local não são suportados nos cenários de implantação híbrida. Para obter mais informações, consulte [Implantação híbrida do Exchange Server 2013](https://technet.microsoft.com/pt-br/59e32000-4fcf-417f-a491-f1d8f9aeef9b\(exchg.150\)#doc).


> [!TIP]
> Pastas públicas habilitadas para email sincronizadas aparecerá como fins de fluxo de emails de objetos de contato para email e não será visível na fCentro de administração do Exchange. Consulte o comando Get-MailPublicFolder. Para recriar as permissões SendAs na nuvem, use o comando Add-RecipientPermission.



1.  No servidor Exchange 2013, execute o seguinte comando para sincronizar habilitados para email a pastas públicas do seu local local Active Directory para o O365.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    Onde `Credential` é o seu nome de usuário do Office 365 e senha e `CsvSummaryFile` é o caminho para onde você gostaria de operações de sincronização de log e de erros, no formato. csv.


> [!TIP]
> Antes de executar o script, é recomendável que você primeiro simular as ações que o script percorreria em seu ambiente executando conforme descrito acima com o parâmetro <CODE>-WhatIf</CODE> .<BR>Também recomendamos que você execute esse script diariamente para sincronizar suas pastas públicas habilitadas para email.



## Etapa 3: Configurar usuários do Exchange Online para acessar pastas públicas do Exchange 2013 no local

A etapa final deste procedimento é configurar a organização do Exchange online e deseja permitir acesso a pastas públicas do Exchange 2013.

Habilite a organização do exchange online acessar as pastas públicas do local. Você irá apontar para todas as caixas de correio pasta pública no local.

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3


> [!TIP]
> Você deve aguardar até que a sincronização do ActiveDirectory concluiu para ver as alterações. Esse processo pode levar até 3 horas para ser concluída. Se você não quiser aguarde as sincronizações recorrentes que ocorrem a cada três horas, você pode forçar sincronização de diretórios, a qualquer momento. Para obter etapas detalhadas para forçar a sincronização de diretórios, consulte <A href="http://technet.microsoft.com/en-us/library/jj151771.aspx">Forçar sincronização de diretórios</A>.



## Como saber se funcionou?

1.  Faça logon no Outlook para um usuário que esteja no Exchange Online e execute os seguintes testes de pasta pública:
    
      - Visualize a hierarquia.
    
      - Verifique as permissões
    
      - Crie e exclua pastas públicas.
    
      - Publique conteúdo e exclua conteúdo de uma pasta pública.

