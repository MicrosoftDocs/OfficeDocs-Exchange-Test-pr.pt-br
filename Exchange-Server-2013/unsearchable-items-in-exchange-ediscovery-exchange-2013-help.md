---
title: 'Itens não pesquisáveis na Descoberta Eletrônica do Exchange'
TOCTitle: Itens não pesquisáveis na descoberta eletrônica do Exchange
ms:assetid: 32550081-9af9-474b-ae7b-28f1e68cad41
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn602498(v=EXCHG.150)
ms:contentKeyID: 61071990
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Itens não pesquisáveis na descoberta eletrônica do Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Em In-Place eDiscovery para Exchange Server 2013 e Exchange Online, itens não pesquisáveis são itens de caixa de correio que não podem ser indexados pela pesquisa do Exchange ou que foram indexados apenas parcialmente. Um item não pesquisável normalmente contém um arquivo, que não pode ser indexado, anexado a uma mensagem de email. Aqui estão alguns motivos por que os arquivos não podem ser indexados para pesquisa e são retornados como um item não pesquisável quando anexado a uma mensagem de email:

  - O tipo de arquivo é incompatível com a indexação porque não há um filtro de pesquisa (também conhecido como *IFilter*) instalado para indexar o formato de arquivo.

  - O tipo de arquivo está desabilitado para indexação.

  - O tipo de arquivo é compatível com a indexação, mas ocorreu um erro de indexação com um arquivo específico.

  - Um arquivo foi criptografado com tecnologias que não são da Microsoft.

  - Um arquivo está protegido por senha.

Para realizar uma pesquisa de Descoberta eletrônica com êxito, pode ser necessário que sua organização revise itens não pesquisáveis. Você pode especificar se incluirá itens não pesquisáveis ao copiar resultados da pesquisa da Descoberta eletrônica para uma caixa de correio de descoberta ou exportar resultados para um arquivo PST.

## Tipos de arquivo incompatíveis com a pesquisa

Certos tipos de arquivos, como um Bitmap ou arquivos MP3, não contêm o conteúdo que pode ser indexado. Como resultado, pesquisa do Exchange não realiza a indexação de texto completo sobre esses tipos de arquivos. Esses tipos de arquivos são considerados como tipos de arquivo incompatíveis. Também há tipos de arquivo para o qual a indexação de texto completo foi desabilitada, por padrão, ou por um administrador. Os tipos de arquivo não suportado, mas desabilitado são considerados itens não pesquisáveis nas pesquisas de descoberta eletrônica. Esses tipos de arquivos, que geralmente são anexados a uma mensagem de email, estão incluídos no conjunto quando você inclui itens não pesquisáveis ao copiar ou exportar os resultados da pesquisa de resultados. Para obter uma lista dos formatos de arquivo com suporte, mas desabilitado, consulte [Formatos de arquivo indexados pela pesquisa do Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md). Em Exchange Server 2013, os administradores podem desabilitar indexing para um formato de arquivo com suporte usando o cmdlet [Set-SearchDocumentFormat](https://technet.microsoft.com/pt-br/library/jj873756\(v=exchg.150\)) . Este cmdlet não está disponível em Exchange Online.

Para identificar os itens não pesquisáveis em uma caixa de correio específica, você poderá executar o cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/pt-br/library/dd351154\(v=exchg.150\)) para obter uma lista de itens que podem ser copiados ou exportados ao optar por incluir itens não pesquisáveis nos resultados da pesquisa.

## Mensagens com tipos de arquivo incompatíveis retornados nos resultados da pesquisa

Nem todas as mensagens com um anexo de arquivo incompatível são automaticamente retornadas como um item não pesquisável. Isso acontece porque outras propriedades do arquivo, como o nome de arquivo, são indexadas e estão disponíveis para serem pesquisadas. Por exemplo, uma pesquisa pela palavra-chave "financeiro" retornará uma mensagem com um anexo de arquivo incompatível caso a palavra-chave apareça no nome do arquivo. Se a palavra-chave só aparece no corpo do arquivo anexado, a mensagem retorna como um item não pesquisável.

De forma semelhante, as mensagens com os anexos de arquivo incompatível são incluídas nos resultados da pesquisa quando outras propriedades de um item de caixa de correio, que são indexadas e pesquisáveis, atendem aos critérios da pesquisa. As propriedades de mensagem indexadas pela pesquisa incluem datas de envio e de recepção, remetente e destinatário, o nome de arquivo de um anexo e o texto no corpo da mensagem. Dessa forma, mesmo que um anexo de mensagem não seja pesquisável, a mensagem será incluída nos resultados normais da pesquisa caso o valor das propriedades corresponda aos critérios da pesquisa. Na verdade, é comum que mensagens com anexos não pesquisáveis sejam incluídos nos resultados normais da pesquisa.

Para obter uma lista de propriedades da mensagem de email indexadas pela pesquisa, consulte [Propriedades de mensagem indexadas pela pesquisa do Exchange](message-properties-indexed-by-exchange-search-exchange-2013-help.md).

## Incluindo itens não pesquisáveis nos resultados da pesquisa

Sua organização pode ter de identificar e executar processamento adicional em itens não pesquisáveis para determinar o que eles são, o que contêm e se são relevantes. Para incluir itens não pesquisáveis nos resultados da pesquisa da Descoberta eletrônica, você pode usar os itens não pesquisáveis ao copiar ou exportar resultados da pesquisa. Para incluir itens não pesquisáveis usando a Descoberta eletrônica in-loco no Exchange ou no Exchange Online, selecione a opção **Incluir itens não pesquisáveis** ao copiar resultados da pesquisa para uma caixa de correio de descoberta ou exportá-los para um arquivo PST. Para incluir itens não pesquisáveis ao usar o Centro de Descoberta eletrônica no SharePoint ou no SharePoint Online, selecione a opção **Incluir itens criptografados ou com um formato não reconhecido**.

Lembre-se do seguinte ao copiar ou exportar itens não pesquisáveis:

  - Quando você copia itens não pesquisáveis para uma caixa de correio de descoberta, todos os itens não pesquisáveis são copiados para uma pasta separada chamada **Unsearchable**, que está localizada sob a pasta que contém os resultados da pesquisa. Quando você exporta resultados da pesquisa e inclui itens não pesquisáveis, os itens não pesquisáveis são exportados para um arquivo PST separado.

  - Quando você inclui itens não pesquisáveis nos resultados da pesquisa, todos os itens não pesquisáveis nas caixas de correio pesquisadas serão retornados, independentemente dos critérios da pesquisa.

  - Se você optar por incluir todos os itens de caixa de correio nos resultados da pesquisa ou se uma consulta de pesquisa não especificar qualquer palavra-chave ou só especificar um intervalo de datas, é possível que os itens não pesquisáveis não sejam copiados para a pasta **Unsearchable** se você selecionar a opção para incluir itens não pesquisáveis. Isso ocorre porque todos os itens, incluindo qualquer item não pesquisável, serão automaticamente incluídos nos resultados normais da pesquisa.

  - Como declarado anteriormente, como as propriedades e os metadados da mensagem são indexados, uma pesquisa de palavra-chave pode retornar resultados caso essa palavra-chave apareça nas propriedades ou nos metadados de uma mensagem com um um arquivo não pesquisável anexado a ela. Neste caso, duas cópias do mesmo item de caixa de correio também serão incluídas nos resultados da pesquisa. Para impedir este tipo de duplicação e só incluir uma cópia do item nos resultados normais da pesquisa, você poderá selecionar a opção **Habilitar deduplicação** ao copiar ou exportar os resultados da pesquisa.

  - A inclusão dos itens não pesquisáveis nos resultados da pesquisa também pode afetar os resultados da pesquisa estimados que são exibidos. Se você incluir itens não pesquisáveis ao copiar resultados da pesquisa, a contagem total de itens estimados e o tamanho total estimado incluirão os itens não pesquisáveis.

Para obter mais informações sobre a inclusão de itens não pesquisáveis nos resultados da pesquisa, consulte:

  - [Criar uma pesquisa de Descoberta Eletrônica In-loco](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-ediscovery/create-in-place-ediscovery-search)

  - [Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-ediscovery/export-search-results)

  - [SharePoint: Exportar conteúdo do eDiscovery e criar relatórios](https://go.microsoft.com/fwlink/p/?linkid=324757)

## Mais informações sobre itens não pesquisáveis

  - Embora um tipo de arquivo compatível da Pesquisa do Exchange seja indexado com texto completo, pode haver erros de indexação ou de pesquisa que farão com que um arquivo seja retornado como um item não pesquisável. Por exemplo, pesquisar um arquivo do Excel muito grande pode ser parcialmente bem-sucedido, mas então falhará, pois o limite de tamanho será excedido. Neste caso, é possível que o mesmo arquivo seja retornado com os resultados da pesquisa e como um item não pesquisável.

  - Arquivos anexados criptografados com tecnologias da Microsoft são indexados pela Pesquisa do Exchange e serão pesquisados. Os arquivos criptografados com tecnologias que não sejam da Microsoft são retornados como não pesquisáveis.

  - Mensagens de email criptografadas com S/MIME não são indexadas e são consideradas como itens não pesquisáveis. Isso inclui mensagens criptografadas com ou sem anexos de arquivo.

  - As mensagens protegidas usando o Gerenciamento de Direitos de Informações (IRM) são indexadas pela Pesquisa do Exchange e, portanto, incluídas nos resultados da pesquisa se corresponderem aos parâmetros de consulta. Para obter mais informações sobre o IRM, consulte [Gerenciamento de Direitos de Informação](information-rights-management-exchange-2013-help.md).

  - Como declarado anteriormente, como propriedades e metadados de mensagem são indexados, uma pesquisa de palavra-chave poderá retornar resultados caso essa palavra-chave apareça nos metadados indexados. Entretanto, essa mesma pesquisa de palavra-chave poderá não retornar o mesmo item caso a palavra-chave só apareça no conteúdo de um item anexado com um tipo de arquivo incompatível. Nesse caso, o item só pode retornar como um item não pesquisável.

  - Na Descoberta eletrônica do Exchange 2010, há um conceito de uma *lista de segurança*. Esses são os tipos de arquivo que têm conteúdo que não é pesquisável e, portanto, não são indexados pela Pesquisa do Exchange; por exemplo, arquivos Windows Media Video (.wmv) e Waveform Audio (.wav). Como esses tipos de arquivos não têm conteúdo pesquisável, não são considerados como itens não pesquisáveis no Exchange 2010. Os itens de caixa de correio com esses tipos de arquivo não eram retornados como itens não pesquisáveis e não eram copiados para uma caixa de correio de descoberta.
    
    Não existe mais uma lista de segurança no Exchange 2013 ou no Exchange Online. Os tipos de arquivo são habilitados ou desabilitados para indexação ou são incompatíveis. Os tipos de arquivo incompatíveis e desabilitados são considerados itens não pesquisáveis.

