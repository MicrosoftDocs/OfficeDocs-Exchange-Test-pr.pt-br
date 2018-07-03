---
title: 'Usar regras de transporte para inspecionar anexos de mensagens: Exchange 2013 Help'
TOCTitle: Usar regras de transporte para inspecionar anexos de mensagens
ms:assetid: c0de687e-e33c-4e8a-b253-771494678795
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ674307(v=EXCHG.150)
ms:contentKeyID: 50486551
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar regras de transporte para inspecionar anexos de mensagens

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-27_

Você pode inspecionar anexos de email em sua organização configurando regras de transporte. O Exchange oferece regras de transporte que proporcionam a capacidade de examinar anexos de email como parte de suas necessidades de segurança e conformidade de mensagens. Ao inspecionar anexos, é possível realizar ações nas mensagens que foram inspecionadas com base no conteúdo ou nas características desses anexos. Aqui temos algumas tarefas relacionadas a anexos que podem ser realizadas usando as regras de transporte:

  - Procurar arquivos em anexos compactados, como arquivos .zip, .rar e, se houver qualquer texto que corresponda ao padrão especificado, adicionar um aviso de isenção ao final da mensagem.

  - Inspecionar o conteúdo de anexos e, se houver qualquer palavra-chave especificada, redirecionar a mensagem para um moderador para que ela seja aprovada antes de ser entregue.

  - Verificar mensagens com anexos que não podem ser inspecionados e bloquear o envio de toda a mensagem.

  - Verificar anexos que excedam um determinado tamanho e notificar o remetente do problema, caso escolha impedir que a mensagem seja entregue.

  - Criar notificações para alertar os usuários quando eles enviam uma mensagem que corresponda a uma regra de transporte.

  - Bloquear todas as mensagens contendo anexos. Para obter exemplos, consulte [Cenários comuns de bloqueio de anexo](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md).

Os administradores do Exchange podem criar regras de transporte acessando o **Centro de administração do Exchange** \> **Fluxo de email** \> **Regras**. Para executar este procedimento, você precisa de permissões. Depois de começar a criar uma nova regra, você poderá ver a lista completa de condições relacionadas aos anexos clicando em **Mais opções** \> **Qualquer anexo** sob **Aplicar essa regra se**. As opções relacionadas aos anexos são mostradas no seguinte diagrama.

![Caixa de diálogo para selecionar regras sobre anexos](images/JJ674307.2ae4a179-bfd2-4a0e-abe1-53ed4e9e3368(EXCHG.150).jpg "Caixa de diálogo para selecionar regras sobre anexos")

Para obter mais informações sobre regras de transporte, incluindo a variedade completa de condições e ações que você pode escolher, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md). O Proteção do Exchange Online (EOP) e clientes híbridos podem se beneficiar das práticas recomendadas para regras de transporte fornecidas em [Práticas recomendadas para a configuração do EOP](https://technet.microsoft.com/pt-br/library/jj723164\(v=exchg.150\)). Se você estiver pronto para começar a criar regras, consulte [Gerenciar regras de fluxo de emails](manage-mail-flow-rules-exchange-2013-help.md).

## Inspecione o conteúdo em anexos

É possível usar as condições de regra de transporte na tabela a seguir para examinar o conteúdo de anexos em mensagens. Para estas condições, apenas os primeiros 150 KB de um anexo são inspecionados. Para começar a usar essas condições ao inspecionar mensagens, você precisa adicioná-las a uma regra de transporte. Saiba mais sobre a criação ou a alteração de regras em [Gerenciar regras de fluxo de emails](manage-mail-flow-rules-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome da condição no EAC</th>
<th>Nome da condição no Shell</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>O conteúdo de qualquer anexo inclui qualquer uma dessas palavras</strong></p></td>
<td><p><code>AttachmentContainsWords</code></p></td>
<td><p>Esta condição corresponde a mensagens com anexos de tipos de arquivos suportados que contêm uma sequência ou grupo de caracteres especificados.</p></td>
</tr>
<tr class="even">
<td><p><strong>O conteúdo de qualquer anexo corresponde a esses padrões de texto</strong></p></td>
<td><p><code>AttachmentMatchesPatterns</code></p></td>
<td><p>Esta condição corresponde a mensagens com anexos de tipos de arquivos suportados que contêm um padrão de texto que corresponde a uma expressão regular especificada.</p></td>
</tr>
</tbody>
</table>


Os nomes do Shell de Gerenciamento do Exchange para as condições listadas aqui são parâmetros que exigem o cmdlet `TransportRule`.

  -  Saiba mais sobre o cmdlet em [New-TransportRule](https://technet.microsoft.com/pt-br/library/bb125138\(v=exchg.150\)).

  -  Saiba mais sobre tipos de propriedade para essas condições em [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Regras de transporte podem inspecionar apenas o conteúdo de tipos de arquivos compatíveis. Se o agente de regras de transporte encontrar um anexo que não está relacionado na lista de tipos de arquivos compatíveis, a condição `AttachmentIsUnsupported` será acionada. Os tipos de arquivos suportados estão listados na seção a seguir. Qualquer arquivo não listado acionará a condição `AttachmentIsUnsupported`.

## Arquivos compactados

Se houver um arquivo compactado na mensagem, como .zip ou .cab, o agente de regras de transporte inspecionará os arquivos contidos no anexo. Essas mensagens são processadas de maneira semelhante às mensagens que contêm vários anexos. As propriedades dos arquivos compactados não são inspecionadas. Por exemplo, se o tipo de arquivo contiver comentários, esse campo não será verificado.

## Tipos de arquivo compatíveis para inspeção de conteúdo de regra de transporte

A tabela a seguir lista os tipos de arquivo compatíveis com as regras de transporte. O sistema usa a detecção automática de tipos de arquivos por meio da inspeção das propriedades do arquivo, em vez de examinar a extensão de nome do arquivo real. Dessa forma, o sistema impede que os hackers maliciosos consigam se evitar a filtragem de regra de transporte via renomeação da extensão de um arquivo. Uma lista de tipos de arquivo com código executável que pode ser verificado dentro do contexto de regras de transporte é apresentada posteriormente neste tópico.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Categoria</th>
<th>Extensão de arquivo</th>
<th>Observações</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Office 2013, Office 2010 e Office 2007</p></td>
<td><p>.docm, .docx, .pptm, .pptx, .pub, .one, .xlsb, .xlsm, .xlsx</p></td>
<td><p>Arquivos de Microsoft OneNote e Microsoft Publisher não são suportados por padrão. Você pode habilitar o suporte para esses tipos de arquivos usando a integração com o IFilter. Para mais informações, consulte <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Registrar IFilters do Filter Pack com o Exchange 2013</a>.</p>
<p>O conteúdo de quaisquer partes incorporadas contidas nesses tipos de arquivos também será inspecionado. Entretanto, quaisquer objetos que não estejam incorporados, como documentos vinculados, não serão inspecionados.</p></td>
</tr>
<tr class="even">
<td><p>Office 2003</p></td>
<td><p>.doc, .ppt, .xls</p></td>
<td><p>Nenhum</p></td>
</tr>
<tr class="odd">
<td><p>Arquivos adicionais do Office</p></td>
<td><p>.rtf, .vdw, .vsd, .vss, .vst</p></td>
<td><p>Nenhum</p></td>
</tr>
<tr class="even">
<td><p>Adobe PDF</p></td>
<td><p>.pdf</p></td>
<td><p>Nenhum</p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p>.html</p></td>
<td><p>Nenhum</p></td>
</tr>
<tr class="even">
<td><p>XML</p></td>
<td><p>.xml, .odp, .ods, .odt</p></td>
<td><p>Nenhum</p></td>
</tr>
<tr class="odd">
<td><p>Texto</p></td>
<td><p>.txt, .asm, .bat, .c, .cmd, .cpp, .cxx, .def, .dic, .h, .hpp, .hxx, .ibq, .idl, .inc, inf, .ini, inx, .js, .log, .m3u, .pl, .rc, .reg, .txt, .vbs, .wtx</p></td>
<td><p>Nenhum</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument</p></td>
<td><p>.odp, .ods, .odt</p></td>
<td><p>Nenhuma parte de arquivos .odf será processada. Por exemplo, se o arquivo .odf contiver um documento incorporado, o conteúdo desse documento incorporado não será verificado.</p></td>
</tr>
<tr class="odd">
<td><p>Desenho em AutoCAD</p></td>
<td><p>.dxf</p></td>
<td><p>Arquivos em AutoCAD 2013 não são suportados.</p></td>
</tr>
<tr class="even">
<td><p>Imagem</p></td>
<td><p>.jpg, .tiff</p></td>
<td><p>Apenas o texto de metadados associado a esses arquivos de imagem é inspecionado. Não há reconhecimento óptico de caracteres.</p></td>
</tr>
</tbody>
</table>


## Inspecionar as propriedades de arquivo dos anexos

As condições de regra de transporte a seguir inspecionam as propriedades de um arquivo que está anexado a uma mensagem. Para começar a usar essas condições ao inspecionar mensagens, você precisa adicioná-las a uma regra de transporte. Uma lista de tipos de arquivo com código executável que pode ser verificado dentro do contexto de regras de transporte é apresentada aqui. Para obter mais informações sobre a criação ou a alteração de regras, consulte [Gerenciar regras de fluxo de emails](manage-mail-flow-rules-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome da condição no EAC</th>
<th>Nome da condição no Shell</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Qualquer nome de arquivo de anexo corresponde a esses padrões de texto</strong></p></td>
<td><p><code>AttachmentNameMatchesPatterns</code></p></td>
<td><p>Esta condição faz a correspondência de mensagens com anexos de tipos de arquivos compatíveis quando estes anexos têm um nome que contém os caracteres especificados.</p></td>
</tr>
<tr class="even">
<td><p><strong>Qualquer extensão de arquivo de anexo inclui essas palavras</strong></p></td>
<td><p><code>AttachmentExtensionMatchesWords</code></p></td>
<td><p>Esta condição faz a correspondência de mensagens com anexos de tipos de arquivos compatíveis quando a extensão de nome de arquivo corresponde ao que foi especificado.</p></td>
</tr>
<tr class="odd">
<td><p><strong>O tamanho de qualquer anexo é maior ou igual a</strong></p></td>
<td><p><code>AttachmentSizeOver</code></p></td>
<td><p>Esta condição faz a correspondência de mensagens com anexos de tipos de arquivos compatíveis quando estes anexos são maiores do que o tamanho especificado.</p></td>
</tr>
<tr class="even">
<td><p><strong>Um anexo não concluiu a verificação</strong></p></td>
<td><p><code>AttachmentProcessingLimitExceeded</code></p></td>
<td><p>Esta condição faz a correspondência de mensagens quando um anexo não é inspecionado pelos agentes de regras de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Qualquer anexo inclui conteúdo executável</strong></p></td>
<td><p><code>AttachmentHasExecutableContent</code></p></td>
<td><p>Esta condição corresponde a mensagens que contêm arquivos executáveis como anexos. Os tipos de arquivo suportados são listados aqui.</p></td>
</tr>
<tr class="even">
<td><p><strong>Algum anexo está protegido por senha</strong></p></td>
<td><p><code>AttachmentIsPasswordProtected</code></p></td>
<td><p>Esta condição faz a correspondência de mensagens com tipos de arquivos de anexos compatíveis quando estes anexos são protegidos por senha.</p></td>
</tr>
</tbody>
</table>


Os nomes do Shell de Gerenciamento do Exchange para as condições listadas aqui são parâmetros que exigem o cmdlet `TransportRule`.

  -  Saiba mais sobre o cmdlet em [New-TransportRule](https://technet.microsoft.com/pt-br/library/bb125138\(v=exchg.150\)).

  -  Saiba mais sobre tipos de propriedade para essas condições em [Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

## Tipos de arquivo executáveis compatíveis para inspeção de regra de transporte

O agente de transporte usa a detecção de tipo verdadeiro inspecionando as propriedades do arquivo, em vez de analisar apenas as extensões de arquivo. Isso ajuda a impedir que hackers mal-intencionados possam ignorar essa regra usando a renomeação de extensão de arquivo. A tabela a seguir lista os tipos de arquivos executáveis aceitos por essas condições. Se um arquivo encontrado não estiver listado aqui, a condição `AttachmentIsUnsupported` será acionada.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de arquivo</th>
<th>Extensão nativa</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Arquivo de autoextração criado com o arquivador WinRAR.</p></td>
<td><p>.rar</p></td>
</tr>
<tr class="even">
<td><p>Arquivo executável do Windows de 32 bits com extensão de biblioteca de vínculo dinâmico.</p></td>
<td><p>.dll</p></td>
</tr>
<tr class="odd">
<td><p>Arquivo de programa executável de autoação.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Arquivo Java.</p></td>
<td><p>.jar</p></td>
</tr>
<tr class="odd">
<td><p>Arquivo executável de desinstalação</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Arquivo de atalho de programa.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Arquivo de código-fonte compilado, arquivo de objeto 3D ou arquivo de sequência.</p></td>
<td><p>.obj</p></td>
</tr>
<tr class="even">
<td><p>Arquivo executável do Windows de 32 bits.</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Arquivo de desenho XML do Microsoft Visio.</p></td>
<td><p>.vxd</p></td>
</tr>
<tr class="even">
<td><p>Arquivo de sistema operacional OS/2.</p></td>
<td><p>.os2</p></td>
</tr>
<tr class="odd">
<td><p>Arquivo executável do Windows de 16 bits.</p></td>
<td><p>.w16</p></td>
</tr>
<tr class="even">
<td><p>Arquivo de sistema operacional em disco.</p></td>
<td><p>.dos</p></td>
</tr>
<tr class="odd">
<td><p>Arquivo padrão de teste antivírus do Instituto Europeu para Pesquisa de Antivírus de Computador.</p></td>
<td><p>.com</p></td>
</tr>
<tr class="even">
<td><p>Arquivo de informações de programa do Windows.</p></td>
<td><p>.pif</p></td>
</tr>
<tr class="odd">
<td><p>Arquivo de programa executável do Windows.</p></td>
<td><p>.exe</p></td>
</tr>
</tbody>
</table>


## Ampliando o número de tipos de arquivos suportados

Os tipos de arquivos suportados listados neste tópico podem ser revisados a qualquer momento usando a integração de IFilter. Para mais informações, consulte [Registrar IFilters do Filter Pack com o Exchange 2013](register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md).

Os tipos de arquivos adicionados por meio desse processo tornam-se tipos de arquivos compatíveis e não mais acionam a condição `AttachmentIsUnsupported`.

## Políticas de prevenção contra perda de dados e regras de transporte de anexos

Para ajudá-lo a gerenciar informações comerciais importantes em emails, você pode incluir qualquer uma das condições relacionadas a anexos com as regras de uma política de prevenção contra perda de dados (DLP). Por exemplo, você pode optar por permitir que mensagens com números de passaporte sejam enviadas, mas somente se os números estiverem em um anexo protegido por senha. Para fazer isso, execute o seguinte procedimento:

  - Crie uma política de DLP que inspecione emails para informações confidenciais relacionadas ao passaporte. Saiba mais em [Procedimentos DLP](dlp-procedures-exchange-2013-help.md).

  - Adicione a exceção **Qualquer anexo é protegido por senha** na área de regra de transporte em **Exceto se…**.

  - Defina uma ação a ser executada em emails que contenham números de passaporte que não estão no arquivo protegido.

Políticas de DLP e condições relacionadas a anexos podem ajudá-lo a impor as suas necessidades comerciais definindo estas necessidades como condições, exceções e ações de regra de transporte. Quando você inclui a inspeção de informações confidenciais em uma política de DLP, qualquer anexo de mensagem é verificado por essa informação apenas. Entretanto, as condições relacionadas ao anexo, como tamanho ou tipo de arquivo, não são incluídas até que você adicione as condições listadas neste tópico. A DLP não está disponível com todas as versões do Exchange. Saiba mais em [Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md).

## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Usar regras de fluxo de email para inspecionar anexos de mensagens no Office 365](https://technet.microsoft.com/pt-br/library/jj919236\(v=exchg.150\)) em Exchange Online

