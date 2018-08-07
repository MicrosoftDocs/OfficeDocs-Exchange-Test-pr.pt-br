---
title: 'Configurar diretório de retirada e diretório de repetição: Exchange 2013 Help'
TOCTitle: Configurar o diretório de retirada e o diretório de repetição
ms:assetid: c9ca7358-9a08-4f57-89d0-910e4438df8a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124549(v=EXCHG.150)
ms:contentKeyID: 50486647
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o diretório de retirada e o diretório de repetição

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Os diretórios de Retirada e Reprodução são utilizados pelo serviço de Transporte em servidores de Caixa de Correio e servidores de Transporte de Borda para inserir arquivos de mensagens diretamente no pipeline de transporte. Os arquivos de mensagens de email formatados corretamente que você copia para o Diretório de Retirada e Reprodução são enviados para entrega. O diretório de Retirada é usado por administradores para testes de fluxo de mensagens ou por aplicativos que devem criar e enviar suas próprias mensagens. O Diretório de repetição recebe mensagens de servidores de gateway externos não SMTP e reenvia mensagens que você exportou das filas de servidores do Microsoft Exchange.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Serviço de transporte" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - O valor do parâmetro *PickupDirectoryMaxMessagesPerMinute* no cmdlet **Set-TransportService** é usado pelos diretórios de Retirada e Reprodução.

  - Alterar o local dos diretórios de Retirada e Reprodução não copia nenhum arquivo de mensagem existente do antigo para o novo local. O novo local de diretório Retirada e Reprodução é ativado quase imediatamente após a alteração da configuração, mas todos os arquivos de mensagem existentes são deixados no antigo local.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O Que Você Deseja Fazer?

## Usar o Shell para configurar o diretório de Retirada

Para configurar o diretório de Retirada, use a seguinte sintaxe.

    Set-TransportService <ServerIdentity> -PickupDirectoryPath <LocalFilePath> -PickupDirectoryMaxHeaderSize <Size> -PickupDirectoryMaxRecipientsPerMessage <Integer> -PickupDirectoryMaxMessagesPerMinute <Integer>

Este exemplo faz as seguintes alterações para o diretório de Retirada no servidor de Caixa de Correio chamado Exchange01:

  - O local do diretório de recebimento é definido como o diretório D:\\Pickup.

  - O tamanho máximo permitido para cabeçalhos de mensagens em um arquivo de mensagem é aumentado para 96 KB.

  - O número máximo de destinatários permitido em um arquivo de mensagens é aumentado para 250.

  - A taxa máxima de processamento de mensagens para os diretórios de Retirada e Reprodução é aumentada para 200 mensagens por minuto.

<!-- end list -->

    Set-TransportService Exchange01 -PickupDirectoryPath "D:\Pickup Directory" -PickupDirectoryMaxHeaderSize 96KB -PickupDirectoryMaxRecipientsPerMessage 250 -PickupDirectoryMaxMessagesPerMinute 200


> [!TIP]
> <UL>
> <LI>
> <P>Configurar o parâmetro <EM>PickupDirectoryPath</EM> para o valor <CODE>$null</CODE> desativa o diretório de Retirada.</P>
> <LI>
> <P>O diretório especificado pelos parâmetros <EM>PickupDirectoryPath</EM> e <EM>ReplayDirectoryPath</EM> não pode ser o mesmo.</P></LI></UL>



## Usar o Shell para configurar o diretório de Reprodução

Para configurar o diretório de repetição, use a seguinte sintaxe.

    Set-TransportService <ServerIdentity> -ReplayDirectoryPath "C:\Replay Directory" <LocalFilePath> -PickupDirectoryMaxMessagesPerMinute <Integer>

Este exemplo faz as seguintes alterações para o diretório de Reprodução no servidor de Caixa de Correio chamado Exchange01:

  - O local do diretório de repetição é definido como o diretório D:\\Replay.

  - A taxa máxima de processamento de mensagens para os diretórios de Retirada e Reprodução é aumentada para 200 mensagens por minuto.

<!-- end list -->

    Set-TransportService Exchange01 -ReplayDirectoryPath "D:\Replay Directory" -PickupDirectoryMaxMessagesPerMinute 200


> [!TIP]
> <UL>
> <LI>
> <P>Configurar o parâmetro <EM>ReplayDirectoryPath</EM> para o valor <CODE>$null</CODE> desativa o diretório de Reprodução.</P>
> <LI>
> <P>O diretório especificado pelos parâmetros <EM>PickupDirectoryPath</EM> e <EM>ReplayDirectoryPath</EM> não pode ser o mesmo.</P></LI></UL>



## Como saber se funcionou?

Para verificar se você configurou com sucesso os diretórios de Retirada e Reprodução, faça o seguinte:

1.  Execute o seguinte comando:
    
        Get-TransportService <ServerIdentity> | Format-List Pickup*,Replay*

2.  Verifique se os valores exibidos são os valores que você configurou.

