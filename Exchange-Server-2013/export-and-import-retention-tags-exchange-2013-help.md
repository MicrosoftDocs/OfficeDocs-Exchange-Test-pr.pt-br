---
title: 'Exportar e importar marcas de retenção: Exchange 2013 Help'
TOCTitle: Exportar e importar marcas de retenção
ms:assetid: 18405ea2-7ccc-475e-bd84-8b040e17bf44
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ907307(v=EXCHG.150)
ms:contentKeyID: 51407840
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportar e importar marcas de retenção

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2017-11-15_

Há vários cenários nos quais você pode querer exportar ou importar marcas de retenção, incluindo:

  - Aplicando as mesmas políticas de retenção em todos os servidores em uma organização de várias florestas Exchange

  - Aplicação das mesmas políticas de retenção em uma implantação híbrida na qual algumas caixas de correio residem na sua organização local do Exchange e outras residem no Exchange Online.

  - Aplicação de políticas de retenção em um cenário de arquivamento Exchange, quais usuários com caixas de correio posteriores ou de local Exchange 2010 tenham um arquivamento baseado em nuvem.

Nesses cenários, o Assistente de Pasta Gerenciada pode processar corretamente um item que tenha uma marca de retenção aplicada após a movimentação do item ou caixa de correio para outra organização.


> [!CAUTION]
> Para manter as marcas de retenção e as políticas de retenção sincronizadas entre duas organizações, sempre que realizar alterações em uma marca ou política de retenção na organização de origem, você deve realizar esse procedimento para exportar marcas e políticas de retenção da organização de origem e importá-las na organização de destino.<BR>Você não pode selecionar marcas ou políticas de retenção específicas para exportação. O script Export-RetentionTags.ps1 exporta todas as marcas de retenção e políticas de uma organização.



Para conhecer tarefas de gerenciamento adicionais relacionadas ao MRM (Gerenciamento de Registros de Mensagens), consulte [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de registros de mensagens" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Os procedimentos neste tópico dependem esses três arquivos na pasta `%ExchangeInstallPath%Scripts` no seu servidorExchange:
    
      - Export-RetentionTags.ps1
    
      - Import-RetentionTags.ps1
    
      - MigrateRetentionTags.strings.psd1

  - Você não pode selecionar marcas ou políticas de retenção específicas para exportação ou importação. O script Export-RetentionTags.ps1 exporta todas as marcas de retenção e políticas de uma organização. O script Import-RetentionTags.ps1 importa todas as marcas de retenção e políticas no arquivo XML que está sendo importado, substituindo todas as marcas de retenção e políticas existentes em uma organização do Exchange.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Etapa 1: Exportar marcas de retenção de uma organização do Exchange local

1.  Execute este comando Shell de Gerenciamento do Exchange para alterar o diretório para a subpasta de **Scripts** no seu caminho de instalação Exchange.
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  Execute o script Export-RetentionTags.ps1 para exportar as marcas de retenção para um arquivo .xml.
    

    > [!IMPORTANT]
    > Se você estiver importando ou exportando marcas de retenção e políticas de retenção para Exchange Online, será necessário conectar sua sessão do Windows PowerShell para Exchange Online. Para obter detalhes, consulte <A href="https://technet.microsoft.com/pt-br/library/jj984289(v=exchg.150)">Conectar-se ao Exchange Online usando o PowerShell Remoto</A>.

    
        .\Export-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## Como saber se funcionou?

Para confirmar se você exportou as marcas de retenção e as políticas de retenção, faça o seguinte:

1.  Navegue até o caminho especificado no comando de exportação e verifique se o arquivo XML com o nome especificado foi criado.

2.  Como opção, abra o arquivo XML em um editor de texto para revisar seu conteúdo.

## Etapa 2: Importar marcas de retenção para uma organização do Exchange

1.  Execute este comando Shell de Gerenciamento do Exchange para alterar o diretório para a subpasta de **Scripts** no seu caminho de instalação Exchange.
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  Execute o script Import-RetentionTags.ps1 para importar as marcas de retenção de um arquivo .xml exportado anteriormente.
    

    > [!IMPORTANT]
    > Se você estiver importando ou exportando marcas de retenção e políticas de retenção para Exchange Online, será necessário conectar sua sessão do Windows PowerShell para Exchange Online. Para obter detalhes, consulte <A href="https://technet.microsoft.com/pt-br/library/jj984289(v=exchg.150)">Conectar-se ao Exchange Online usando o PowerShell Remoto</A>.

    

    > [!NOTE]
    > Ao executar esse script contra Exchange Online, você pode ser solicitado a confirmar que você deseja executar o software de um editor confiável. Verifique se o nome do Editor aparece como <CODE>CN=Microsoft Corporation, OU=MOPR, O=Microsoft Corporation, L=Redmond, S=Washington, C=US</CODE>e clique em <STRONG>R</STRONG> para permitir que o script a ser executado uma vez ou <STRONG>uma</STRONG> para sempre são executados.

    
        .\Import-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## Como saber se funcionou?

Para confirmar se você importou as marcas de retenção e as políticas de retenção, faça o seguinte:

1.  No EAC, navegue até **Gerenciamento de Conformidade** \> **Marcas de retenção** e verifique se as marcas de retenção foram importadas com êxito. Navegue até **Gerenciamento de Conformidade** \> **Políticas de retenção** e verifique se as políticas de retenção foram importadas com êxito.

2.  Use os cmdlets **Get-RetentionPolicy** e **Get-RetentionPolicyTag** para verificar se as marcas e políticas foi criadas. Para obter um exemplo sobre como recuperar marcas de retenção e políticas de retenção, consulte os exemplos em [Get-RetentionPolicyTag](https://technet.microsoft.com/pt-br/library/dd298009\(v=exchg.150\)) e [Get-RetentionPolicy](https://technet.microsoft.com/pt-br/library/dd298086\(v=exchg.150\)).

