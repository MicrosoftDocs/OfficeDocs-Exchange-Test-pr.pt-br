---
title: 'Pesquisa do Exchange: Exchange 2013 Help'
TOCTitle: Pesquisa do Exchange
ms:assetid: 967e2a13-4e54-486a-ac22-08768674abbb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232132(v=EXCHG.150)
ms:contentKeyID: 52058845
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pesquisa do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-09-17_

Com o aumento dos tamanhos das caixas postais e da quantidade de dados sendo armazenados nelas na forma de mensagens e anexos, é crucial que os usuários possam pesquisar e localizar rapidamente as mensagens de que precisam. O [Arquivamento In-loco do Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) ajuda a reduzir ou eliminar o uso de arquivos .pst, movendo para o arquivo morto itens antigos e acessados com pouca frequência. Isso resulta em mais dados de caixa de correio sendo armazenados por um usuário e faz com que a pesquisa nas caixas de correio principal e de arquivo morto do usuário seja uma importante ferramenta de produtividade. A [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md) permite que usuários autorizados pesquisem o conteúdo de caixas de correio em organizações do Exchange locais e na nuvem, a fim de atender às solicitações de descoberta eletrônica, auditorias regulatórias ou investigações internas. A Descoberta Eletrônica In-loco usa os índices de conteúdo criados pela Pesquisa do Exchange.

A Pesquisa do Exchange é diferente da indexação de texto completo disponível no Exchange Server 2003. Houve melhorias no desempenho, na indexação do conteúdo e na pesquisa. Os novos itens são indexados no pipeline de transporte ou quase que imediatamente depois de serem criados ou entregues à caixa de correio, oferecendo aos usuários uma forma rápida, estável e mais confiável de pesquisar dados em caixas de correio. A indexação de conteúdo é habilitada por padrão e não há necessidade de instalação inicial ou configuração.

Para obter mais informações sobre Exchange pesquisa, consulte:

  - [Formatos de arquivo indexados pela pesquisa do Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Propriedades de mensagem indexadas pela pesquisa do Exchange](message-properties-indexed-by-exchange-search-exchange-2013-help.md)

Procurando tarefas de gerenciamento relacionadas à Pesquisa do Exchange? Consulte [Procedimentos de pesquisa do Exchange](exchange-search-procedures-exchange-2013-help.md).

## Novidades

O Exchange 2013 introduz as seguintes alterações na Pesquisa do Exchange:

  - O mecanismo subjacente de indexação de conteúdo foi substituído pelo Microsoft Search Foundation, que oferece aprimoramentos de desempenho e funcionalidade, e serve de mecanismo de indexação de conteúdo subjacente comum no Exchange e no SharePoint. A interface de gerenciamento, porém, permanece a mesma.

  - Por padrão, o Search Foundation é compatível com os formatos de arquivo mais comuns em anexos de email. Você não precisa mais instalar Pacotes de Filtro do Microsoft Office para a Pesquisa do Exchange. Para ver uma lista dos formatos de arquivo compatíveis com a Pesquisa do Exchange, consulte [Formatos de arquivo indexados pela pesquisa do Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md).
    
    Você pode adicionar suporte para qualquer formatos de arquivo adicional instalando IFilters, como nas versões anteriores do Exchange.

  - A indexação de conteúdo é mais eficiente porque agora ela processa as mensagens no pipeline de transporte. Consequentemente, as mensagens endereçadas a vários destinatários ou grupos de distribuição são processadas uma única vez. Um fluxo de anotação é anexado à mensagem, acelerando significativamente a indexação de conteúdo e, ao mesmo tempo, consumindo menos recursos.

