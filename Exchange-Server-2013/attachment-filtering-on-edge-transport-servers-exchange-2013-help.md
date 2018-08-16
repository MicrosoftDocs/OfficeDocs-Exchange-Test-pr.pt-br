---
title: 'Filtragem de anexos nos servidores de transporte de borda: Exchange 2013 Help'
TOCTitle: Filtragem de anexos nos servidores de transporte de borda
ms:assetid: be39a181-c82e-41f5-8846-085bf1f84164
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124399(v=EXCHG.150)
ms:contentKeyID: 60829938
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtragem de anexos nos servidores de transporte de borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-02-10_

No Microsoft Exchange Server 2013, é possível usar a filtragem de anexos nos servidores de Transporte de Borda para controlar os anexos que os usuários recebem nas mensagens de email. A filtragem de anexos é realizada pelo agente de Filtragem de anexos, que só está disponível em servidores de Transporte de Borda.

## Tipos de filtragem de anexos

Você pode usar os seguintes tipos de filtragem de anexos para controlar anexos que chegam ou saem da sua organização pelo servidor de Transporte de Borda:

  - **Filtragem baseada no nome de arquivo ou na extensão do nome de arquivo**   Você especifica o nome de arquivo ou a extensão do nome de arquivo exatamente como deseja filtrar. Um exemplo de filtro de nome de arquivo é `BadFileName.exe`. Um exemplo de filtro de extensão de nome de arquivo é `*.exe`.

  - **Filtragem baseada no tipo de conteúdo MIME do arquivo**   Você especifica o valor do tipo de conteúdo MIME que deseja filtrar. O valor do tipo de conteúdo MIME indica o que o anexo é, por exemplo, uma imagem JPEG, um arquivo executável ou um arquivo do Microsoft Excel. Os tipos de conteúdo são expressos como `type/subtype`. Por exemplo, o arquivo de imagem JPEG é expressado como `image/jpeg`.
    
    Para ver a lista completa de extensões de nomes de arquivos e tipos de conteúdo que a filtragem de anexos pode detectar, execute o seguinte comando no servidor de Transporte de Borda:
    
        Get-AttachmentFilterEntry | Format-List

Depois de definir quais arquivos procurar, configure a ação a ser realizada nas mensagens com esses anexos. Não é possível especificar ações diferentes para tipos de anexos diferentes. Configure uma das ações a seguir para todas as mensagens que correspondam aos filtros de anexos:

  - **Rejeitar (bloquear) a mensagem**   A mensagem é bloqueada. O remetente recebe uma notificação de falha na entrega (NDR) explicando que a mensagem não foi entregue por conter um anexo inaceitável. É possível personalizar o texto da NDR. O texto padrão é: `Message rejected due to unacceptable attachments`.

  - **Retirar o anexo, mas permitir que a mensagem seja enviada**   O anexo é removido da mensagem. No entanto, a mensagem em si e os demais anexos que não correspondem ao filtro são enviados. Se um anexo for removido, será substituído por um arquivo de texto que explica por quê o anexo foi removido. Esta é a ação padrão.

  - **Excluir a mensagem silenciosamente**   A mensagem é excluída. O remetente e o destinatário não recebem a notificação.

Para obter mais informações, consulte [Gerenciar filtragem de anexos nos servidores de transporte de borda](manage-attachment-filtering-on-edge-transport-servers-exchange-2013-help.md).


> [!NOTE]
> Não é possível recuperar mensagens bloqueadas ou anexos retirados. Ao configurar filtros de anexo, examine com cuidado todas as possíveis correspondências de nomes de arquivos e verifique se os anexos legítimos não serão afetados pelo filtro.<BR>Além disso, não remova anexos de mensagens de email assinadas digitalmente, criptografadas ou com proteção de direitos. Se os anexos dessas mensagens forem removidos, as mensagens assinadas digitalmente serão invalidadas e as mensagens criptografadas e com proteção de direitos ficarão ilegíveis.


