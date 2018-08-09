---
title: 'Importar entradas de endereço em servidores de Transporte de Borda'
TOCTitle: Entradas em servidores de transporte de borda de reconfiguração de endereço de importação
ms:assetid: bd0942c6-9c66-4b4c-b9bc-2f5f783def76
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb331966(v=EXCHG.150)
ms:contentKeyID: 61060560
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Entradas em servidores de transporte de borda de reconfiguração de endereço de importação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

É possível importar ou criar informações de reconfiguração de endereço em massa para dentro de um servidor de Transporte de Borda usando um arquivo de valores separados por vírgula (CSV). A lista a seguir descreve cenários comuns que exigem esse procedimento:

  - Você está substituindo uma solução de reconfiguração de endereço com um servidor de Transporte de Borda.

  - Você estabelece um acordo com um provedor de soluções terceirizado que exige a reconfiguração dos seus endereços de email.

  - Você adquire outra organização e é necessário reconfigurar temporariamente os endereços de email dessa organização.

É possível usar qualquer editor de texto, como o Bloco de Notas ou um aplicativo como o Microsoft Excel, para criar o arquivo CSV. Formate o arquivo conforme descrito no tópico e salve-o como um arquivo .csv.

A primeira linha, ou *linha de cabeçalho*, do arquivo CSV lista os nomes dos parâmetros. Cada parâmetro é separado por uma vírgula. Os parâmetros obrigatórios e opcionais estão descritos na tabela a seguir.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Obrigatório ou opcional</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Obrigatório</p></td>
<td><p>Um nome exclusivo e descritivo para a entrada de reconfigurações de endereços.</p></td>
</tr>
<tr class="even">
<td><p><em>InternalAddress</em></p></td>
<td><p>Obrigatório</p></td>
<td><p>O endereço que você deseja alterar. É possível usar os seguintes valores:</p>
<ul>
<li><p>Um único endereço de email (chris@contoso.com)</p></li>
<li><p>Um único domínio ou subdomínio (contoso.com ou sales.contoso.com)</p></li>
<li><p>Um domínio e todos os subdomínios (*.contoso.com)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>ExternalAddress</em></p></td>
<td><p>Obrigatório</p></td>
<td><p>O endereço de email final desejado. Use um dos seguintes valores:</p>
<ul>
<li><p>Um único endereço de email se você tiver especificado um único endereço de email para <em>InternalAddress</em></p></li>
<li><p>Um único domínio ou subdomínio para os demais valores de <em>InternalAddress</em></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ExceptionList</em></p></td>
<td><p>Opcional</p></td>
<td><p>Disponível apenas quando você estiver reconfigurando endereços de email em um domínio e todos os subdomínios (*.contoso.com). Especifica um ou mais subdomínios que você deseja excluir da reconfiguração de endereço. Delimite o valor entre aspas duplas e separe vários valores com vírgulas. Por exemplo, <code>&quot;marketing.contoso.com&quot;</code> ou <code>&quot;marketing.contoso.com,legal.contoso.com&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>Opcional</p></td>
<td><p><code>False</code> significa que os endereços são configurados em emails de entrada e saída. <code>True</code> significa que os endereços são reconfigurados apenas em emails de saída e é necessário configurar manualmente o endereço de email reconfigurado como um endereço de proxy para os destinatários afetados.</p>
<p>O valor padrão é <code>False</code>, mas é necessário defini-lo com <code>True</code> se o <em>InternalAddress</em> contiver o caractere curinga (*.contoso.com).</p>
<p>O valor do parâmetro <em>OutboundOnly</em> no arquivo CSV é <code>True</code> ou <code>False</code>, não <code>$True</code> ou <code>$False</code>.</p></td>
</tr>
</tbody>
</table>


Cada linha abaixo da linha de cabeçalho representa uma entrada de reconfiguração de endereço. Os valores em cada linha devem estar na mesma ordem dos nomes dos parâmetros na linha de cabeçalho. Cada valor é separado por uma vírgula.

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão desta tarefa: 30 minutos

  - Certifique-se de que entendeu as ramificações da reconfiguração de endereço. Por exemplo, o endereço de email reconfigurado deve ser exclusivo na sua organização do Exchange e talvez seja necessário configurar endereços de proxy nos destinatários afetados. Para obter mais informações, veja [Reconfiguração nos servidores de transporte de borda de endereço](address-rewriting-on-edge-transport-servers-exchange-2013-help.md) e [Gerenciar a reconfiguração de endereço em servidores de transporte de borda](manage-address-rewriting-on-edge-transport-servers-exchange-2013-help.md).

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Agente de Reconfiguração de Endereço" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Se você tiver mais de um servidor de Transporte de Borda, recomendamos usar os procedimentos neste tópico para importar as entradas de reconfiguração de endereço para um único servidor de Transporte de Borda e, em seguida, clonar a configuração desse servidor de Transporte de Borda para os demais servidores de Transporte de Borda da organização. Para obter mais informações sobre como clonar um servidor de Transporte de Borda, consulte [Configuração clonada do servidor de transporte de borda](edge-transport-server-cloned-configuration-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como isso é feito?

## Etapa 1: Criar o arquivo CSV

Ao criar o arquivo CSV, leve os seguintes itens em consideração:

  - Se você especificar valores para parâmetros opcionais no arquivo CSV, cada linha deverá incluir um valor naquela coluna. Se você quiser criar várias entradas de reconfiguração de endereço em um local onde algumas entradas possuem parâmetros opcionais e outras não, será preciso separar essas entradas de reconfiguração de endereço em dois arquivos CSV distintos e, em seguida, importar cada arquivo CSV separadamente.

  - Se o arquivo CSV contiver caracteres não-ASCII, salve o arquivo CSV com codificação UTF-8 ou outra codificação Unicode. Dependendo do aplicativo, é provável que seja mais fácil salvar o arquivo CSV com codificação UTF-8 ou outra codificação Unicode quando localidade do sistema corresponder ao idioma usado no arquivo CSV.

O exemplo a seguir mostra como um arquivo CSV pode ser preenchido com os parâmetros opcionais *ExceptionList* e *OutboundOnly* incluídos:

    Name,InternalAddress,ExternalAddress,ExceptionList,OutboundOnly
    "Wingtip UK",*.wingtiptoys.co.uk,tailspintoys.com,"legal.wingtiptoys.co.uk,finance.wingtiptoys.co.uk,support.wingtiptoys.co.uk",True
    "Wingtip USA",*.wingtiptoys.com,tailspintoys.com,"legal.wingtiptoys.com,finance.wingtiptoys.com,support.wingtiptoys.com,corp.wingtiptoys.com",True
    "Wingtip Canada",*.wingtiptoys.ca,tailspintoys.com,"legal.wingtiptoys.ca,finance.wingtiptoys.ca,support.wingtiptoys.ca",True

## Etapa 2: Importar o arquivo CSV

Para importar o arquivo CSV, use a sintaxe a seguir:

    Import-Csv <FileNameAndPath> | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

Este exemplo importa as entradas de reconfiguração de endereço de C:\\My Documents\\ImportAddressRewriteEntries.csv.

    Import-Csv "C:\My Documents\ImportAddressRewriteEntries.csv" | ForEach {New-AddressRewriteEntry -Name $_.Name -InternalAddress $_.InternalAddress -ExternalAddress $_.ExternalAddress -OutboundOnly ([Bool]::Parse($_.OutboundOnly)) -ExceptionList $_.ExceptionList}

## Como saber se essa etapa funcionou?

Para verificar se as entradas de reconfiguração de endereço foram importadas com êxito de um arquivo CSV, execute a ação a seguir:

1.  Para ver todas as entradas de reconfiguração de endereço, execute o comando `Get-AddressRewriteEntry`.

2.  Para ver detalhes específicos sobre uma entrada de reconfiguração de endereço específica, execute o comando `Get-AddressRewriteEntry <AddressRewriteIdentity> | Format-List`

