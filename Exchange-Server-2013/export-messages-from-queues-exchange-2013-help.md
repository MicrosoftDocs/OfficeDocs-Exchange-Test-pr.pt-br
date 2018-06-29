---
title: 'Exportar mensagens de filas: Exchange 2013 Help'
TOCTitle: Exportar mensagens de filas
ms:assetid: 688b342c-f380-4fe0-afce-7e38cf490627
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998625(v=EXCHG.150)
ms:contentKeyID: 51407880
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportar mensagens de filas

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-05-05_

Quando você exporta uma mensagem de uma fila para um arquivo, a mensagem não é removida da fila. Uma cópia da mensagem é feita como arquivo de texto simples no local especificado. O arquivo resultante pode ser exibido em uma aplicativo, como um editor de texto ou um cliente de email, ou o arquivo de mensagem pode ser reenviado usando o diretório de Repetição ou qualquer outro servidor de Caixa de Correio ou servidor de Transporte de Borda dentro ou fora da organização do Exchange.

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 15 minutos

  - Entrada de "Filas" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - As mensagens devem estar com estado de Suspensa para que o processo de exportação seja realizado com sucesso. Você pode exportar mensagens a partir de filas de entrega, a fila Não Localizável ou a fila de mensagem suspeita. As mensagens na fila de mensagem suspeita já estão no estado de Suspensa. Você não pode suspender ou exportar mensagens que estão na fila de Envio.

  - Você não pode usar o Visualizador de fila na Caixa de Ferramentas do Exchange para exportar mensagens. Entretanto, você pode usar o Visualizador de Fila para localizar, identificar e suspender as mensagens antes de exportá-las usando o Shell.

  - Verifique as seguintes informações sobre a localização do diretório alvo para os arquivos de mensagem:
    
      - O diretório de destino deve existir para que você exporte mensagens. O diretório não será criado para você. Se um caminho absoluto não for especificado, o diretório de trabalho atual do Shell de Gerenciamento do Exchange é usado.
    
      - O caminho pode ser local para o servidor do Exchange ou pode ser um caminho de Convenção Universal de Nomenclatura (UNC) para um compartlhamento em um servidor remoto.
    
      - A sua conta deve possuir permissão de **Escrita** para o diretório alvo.
    
      - Ao especificar um nome de arquivo para as mensagens exportadas, certifique-se de inclui a extensão do nome do arquivo .eml para que os arquivos sejam abertos facilmente pelas aplicações do cliente de email ou processadas corretamente pelo diretório Replay.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para exportar uma mensagem específica de uma fila específica

Para exportar uma mensagem a partir de um fila específica, execute o seguinte comando:

    Export-Message -Identity <MessageIdentity> | AssembleMessage -Path <FilePath>\<FileName>.eml

Este exemplo exporta uma cópia da mensagem que possui o valor de **InternalMessageID** 1234 que está localizada no servidor chamado Mailbox01 para o arquivo nomeado export.eml in no caminho D:\\Contoso Export.

    Export-Message -Identity Exchange01\Contoso.com\1234 | AssembleMessage -Path "D:\Contoso Export\export.eml"

## Usar o Shell para exportar todas as mensagens de uma fila específica

Para exportar todas as mensagens a partir de uma fila específica e usar o valor de **InternetMessageID** de cada mensagem como o nome do arquivo, use a sintaxe a seguir.

    Get-Message -Queue <QueueIdentity> | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

Observe que o valor de **InternetMessageID** contém parênteses (\> e \<), que precisam ser removidos por não serem permitidos nos nomes do arquivo.

Este exemplo exporta uma cópia de todas as mensagens da fila de entrega do contoso.com no servidor de nome Mailbox01 para o diretório local de nome D:\\Contoso Export.

    Get-Message -Queue Mailbox01\Contoso.com | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

## Usar o Shell para exportar mensagens específicas de todas as filas de um servidor

Para exportar mensagens específicas de todas as filas em um servidor e usar o valor de **InternetMessageID** de cada mensagem como o nome de arquivo, use a sintaxe a seguir.

    Get-Message -Filter {<MessageFilter>} [-Server <ServerIdentity>] | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

Observe que o valor de **InternetMessageID** contém parênteses (\> e \<), que precisam ser removidos por não serem permitidos nos nomes do arquivo.

Este exemplo exporta uma cópia de todas as mensagens dos remetentes no domínio contoso.com a partir de todas as filas no servidor de nome Mailbox01 para o diretório local de nome D:\\Contoso Export.

    Get-Message -Filter {FromAddress -like "*@contoso.com"} -Server Mailbox01 | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}


> [!TIP]
> se você omitir o parâmetro <EM>Server</EM> , o comando opera no servidor local.


