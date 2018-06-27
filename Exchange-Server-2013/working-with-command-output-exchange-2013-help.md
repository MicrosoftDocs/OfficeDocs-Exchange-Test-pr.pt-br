---
title: 'Trabalhando com a saída do comando: Exchange 2013 Help'
TOCTitle: Trabalhando com a saída do comando
ms:assetid: 8320e1a5-d3f5-4615-878d-b23e2aaa6b1e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123533(v=EXCHG.150)
ms:contentKeyID: 50486012
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Trabalhando com a saída do comando

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O Shell de Gerenciamento do Exchange oferece vários métodos de formatação para saída de comando. Este tópico discute os seguintes assuntos:

  - Como formatar dados   Controle o modo de formatação dos dados exibidos usando os cmdlets **Format-List**, **Format-Table** e **Format-Wide**.

  - Como produzir dados   Determine se os dados são produzidos para a janela do console do Shell ou para um arquivo usando os cmdlets **Out-Host** e **Out-File**. Este tópico inclui um exemplo de script para produzir dados para o MicrosoftInternet Explorer.

  - Como filtrar dados   Filtre os dados usando um dos seguintes métodos de filtragem:
    
      - Filtragem no servidor, disponível com determinados cmdlets.
    
      - Filtragem no cliente, disponível em todos os cmdlets pela canalização dos resultados de um comando para o cmdlet **Where-Object**.

Para usar a funcionalidade descrita neste tópico, você deve estar familiarizado com os seguintes conceitos:

  - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))

  - [Variáveis do shell](https://technet.microsoft.com/pt-br/library/bb124036\(v=exchg.150\))

  - [Operadores de comparação](https://technet.microsoft.com/pt-br/library/bb125229\(v=exchg.150\))

## Como formatar dados

Se você chamar os cmdlets de formatação no final da pipeline, poderá substituir a formatação padrão para controlar quais dados serão exibidos e como esses dados aparecerão. Os cmdlets de formatação são **Format-List**, **Format-Table** e **Format-Wide**. Cada um deles tem um estilo de saída distinta, diferente dos outros cmdlets de formatação.

## Format-List

O cmdlet **Format-List** recebe a entrada de pipeline e produz uma lista em colunas verticais de todas as propriedades especificadas de cada objeto. Use o parâmetro *Property* para especificar as propriedades que deseja exibir. Quando o cmdlet **Format-List** é chamado sem nenhum parâmetro especificado, todas as propriedades são produzidas na saída. O cmdlet **Format-List** quebra as linhas em vez de truncá-las. Uma das melhores utilizações para o cmdlet **Format-List** é substituir a saída padrão de um cmdlet, para que você possa recuperar as informações adicionais ou mais destacadas.

Por exemplo, quando você chama o cmdlet **Get-Mailbox**, vê apenas uma quantidade limitada de informações no formato da tabela. Se direcionar a saída do cmdlet **Get-Mailbox** para o cmdlet **Format-List** e adicionar parâmetros para as informações destacadas ou adicionais que deseja exibir, você poderá recuperar a saída desejada.

É possível também especificar um caractere curinga "\*" com um nome de propriedade parcial. Se você incluir um caractere-curinga, poderá corresponder várias propriedades sem precisar digitar o nome de cada uma delas individualmente. Por exemplo, `Get-Mailbox | Format-List -Property Email* ` retorna todas as propriedades que começam com `Email`.

Os exemplos a seguir mostram as diferentes maneiras de exibir os mesmos dados retornados pelo cmdlet **Get-Mailbox**.

    Get-Mailbox TestUser1
    
    Name                      Alias                ServerName       ProhibitSendQuo
                                                                    ta
    ----                      -----                ----------       ---------------
    TestUser1                 TestUser1            mbx              unlimited

No primeiro exemplo, o cmdlet **Get-Mailbox** é chamado sem formatação específica, portanto, a saída padrão está no formato de tabela e contém um conjunto pré-determinado de propriedades.

    Get-Mailbox TestUser1 | Format-List -Property Name,Alias,EmailAddresses
    
    Name           : TestUser1
    Alias          : TestUser1
    EmailAddresses : {SMTP:TestUser1@contoso.com}

No segundo exemplo, a saída do cmdlet **Get-Mailbox** é direcionada para o cmdlet **Format-List**, juntamente com propriedades específicas. Como você pode ver, o formato e o conteúdo da saída são significativamente diferentes.

    Get-Mailbox TestUser1 | Format-List -Property Name, Alias, Email*
    Name                      : Test User
    Alias                     : TestUser1
    EmailAddresses            : {SMTP:TestUser1@contoso.com}
    EmailAddressPolicyEnabled : True

No último exemplo, a saída do cmdlet **Get-Mailbox** é direcionada para o cmdlet **Format-List**, como no segundo exemplo. No entanto, no último exemplo, usamos um caractere curinga para corresponder todas as propriedades iniciadas com `Email`.

Se passar mais de um objeto para o cmdlet **Format-List**, todas as propriedades especificadas de um objeto são exibidas e agrupadas por objeto. A ordem de exibição depende do parâmetro padrão do cmdlet. O parâmetro padrão mais frequente é o *Name* ou o *Identity*. Por exemplo, quando o cmdlet **Get-Childitem** é chamado, a ordem de exibição padrão mostra os nomes de arquivo em ordem alfabética. Para alterar esse comportamento, você deve chamar o cmdlet **Format-List**, junto com o parâmetro *GroupBy* e o nome de um valor da propriedade pela qual deseja agrupar a saída. Por exemplo, o comando a seguir lista todos os arquivos em um diretório e os agrupa por extensão.

    Get-Childitem | Format-List Name,Length -GroupBy Extension
    
        Extension: .xml
    
    Name   : Config_01.xml
    Length : 5627
    
    Name   : Config_02.xml
    Length : 3901
    
    
        Extension: .bmp
    
    Name   : Image_01.bmp
    Length : 746550
    
    Name   : Image_02.bmp
    Length : 746550
    
    
        Extension: .txt
    
    Name   : Text_01.txt
    Length : 16822
    
    Name   : Text_02.txt
    Length : 9835

Neste exemplo, o cmdlet **Format-List** agrupou os itens pela propriedade *Extension*, que é especificada pelo parâmetro *GroupBy*. Você pode usar o parâmetro *GroupBy* com qualquer propriedade válida para os objetos no fluxo de pipeline.

## Format-Table

O cmdlet **Format-Table** permite exibir itens em um formato de tabela com cabeçalhos de rótulo e colunas de dados de propriedade. Por padrão, muitos cmdlets, como **Get-Process** e **Get-Service**, usam o formato de tabela como saída. Os parâmetros para o cmdlet **Format-Table** incluem os parâmetros *Properties* e *GroupBy*. Esses parâmetros funcionam exatamente como no cmdlet **Format-List**.

O cmdlet **Format-Table** também usa o parâmetro *Wrap*. Esse parâmetro permite a exibição completa de longas linhas de informações da propriedade em vez de haver dados truncados no final das linhas. Para ver como o parâmetro *Wrap* é usado para exibir as informações retornadas, compare a saída do comando **Get-Command** nos dois exemplos a seguir.

No primeiro exemplo, quando o cmdlet **Get-Command** é usado para exibir as informações de comando sobre o cmdlet **Get-Process**, as informações para a propriedade *Definition* estão truncadas.

    Get-Command Get-Process | Format-Table Name,Definition
    
    Name                                    Definition
    ----                                    ----------
    get-process                             get-process [[-ProcessName] String[]...

No segundo exemplo, o parâmetro *Wrap* é adicionado ao comando para impor a exibição do conteúdo completo da propriedade *Definition*.

    Get-Command Get-Process | Format-Table Name,Definition -Wrap
    
    Get-Process                             Get-Process [[-Name] <String[]>] [-Comp
                                            uterName <String[]>] [-Module] [-FileVe
                                            rsionInfo] [-Verbose] [-Debug] [-ErrorA
                                            ction <ActionPreference>] [-WarningActi
                                            on <ActionPreference>] [-ErrorVariable
                                            <String>] [-WarningVariable <String>] [
                                            -OutVariable <String>] [-OutBuffer <Int
                                            32>]
                                            Get-Process -Id <Int32[]> [-ComputerNam
                                            e <String[]>] [-Module] [-FileVersionIn
                                            fo] [-Verbose] [-Debug] [-ErrorAction <
                                            ActionPreference>] [-WarningAction <Act
                                            ionPreference>] [-ErrorVariable <String
                                            >] [-WarningVariable <String>] [-OutVar
                                            iable <String>] [-OutBuffer <Int32>]
                                            Get-Process [-ComputerName <String[]>]
                                            [-Module] [-FileVersionInfo] -InputObje
                                            ct <Process[]> [-Verbose] [-Debug] [-Er
                                            rorAction <ActionPreference>] [-Warning
                                            Action <ActionPreference>] [-ErrorVaria
                                            ble <String>] [-WarningVariable <String
                                            >] [-OutVariable <String>] [-OutBuffer
                                            <Int32>]

Assim como no cmdlet **Format-List**, você pode também especificar um caractere curinga "`*`" com um nome de propriedade parcial. Ao incluir um caractere curinga, você pode corresponder várias propriedades sem digitar cada nome de propriedade individualmente.

## Format-Wide

O cmdlet **Format-Wide** fornece um controle de saída mais simples do que os outros cmdlets de formatação. Por padrão, o cmdlet **Format-Wide** tenta exibir o máximo possível de colunas referentes aos valores de propriedade em uma linha de saída. Adicionando parâmetros, você pode controlar o número de colunas e como o espaço de saída será usado.

Na utilização mais básica, chamar o cmdlet **Format-Wide** sem nenhum parâmetro organiza a saída em colunas, tantas quantas couberem na página. Por exemplo, quando você executar o cmdlet **Get-Childitem** e canaliza sua saída para o cmdlet **Format-Wide**, verá a seguinte exibição de informações:

    Get-ChildItem | Format-Wide
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml                           Config_02.xml
    Config_03.xml                           Config_04.xml
    Config_05.xml                           Config_06.xml
    Config_07.xml                           Config_08.xml
    Config_09.xml                           Image_01.bmp
    Image_02.bmp                            Image_03.bmp
    Image_04.bmp                            Image_05.bmp
    Image_06.bmp                            Text_01.txt
    Text_02.txt                             Text_03.txt
    Text_04.txt                             Text_05.txt
    Text_06.txt                             Text_07.txt
    Text_08.txt                             Text_09.txt
    Text_10.txt                             Text_11.txt
    Text_12.txt

Em geral, chamar o cmdlet **Get-Childitem** sem nenhum parâmetro exibe os nomes de todos os arquivos no diretório em uma tabela de propriedades. Neste exemplo, ao canalizar a saída do cmdlet **Get-Childitem** para o cmdlet **Format-Wide**, a saída foi exibida em duas colunas de nomes. Observe que apenas um tipo de propriedade pode ser exibido de cada vez, especificado por um nome de propriedade que segue o cmdlet **Format-Wide**. Se você adicionar o parâmetro *Autosize*, a saída será alterada de duas colunas para o número de colunas possíveis de serem ajustadas na largura da tela.

    Get-ChildItem | Format-Wide -AutoSize
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml   Config_02.xml   Config_03.xml   Config_04.xml   Config_05.xml
    Config_06.xml   Config_07.xml   Config_08.xml   Config_09.xml   Image_01.bmp
    Image_02.bmp    Image_03.bmp    Image_04.bmp    Image_05.bmp    Image_06.bmp
    Text_01.txt     Text_02.txt     Text_03.txt     Text_04.txt     Text_05.txt
    Text_06.txt     Text_07.txt     Text_08.txt     Text_09.txt     Text_10.txt
    Text_11.txt     Text_12.txt

Neste exemplo, a tabela é organizada em cinco colunas, em vez de duas. O parâmetro *Column* oferece mais controle, permitindo que você especifique o número máximo de colunas para exibir as informações, como a seguir:

    Get-ChildItem | Format-Wide -Column 4
    
        Directory: FileSystem::C:\WorkingFolder
    
    Config_01.xml       Config_02.xml       Config_03.xml       Config_04.xml
    Config_05.xml       Config_06.xml       Config_07.xml       Config_08.xml
    Config_09.xml       Image_01.bmp        Image_02.bmp        Image_03.bmp
    Image_04.bmp        Image_05.bmp        Image_06.bmp        Text_01.txt
    Text_02.txt         Text_03.txt         Text_04.txt         Text_05.txt
    Text_06.txt         Text_07.txt         Text_08.txt         Text_09.txt
    Text_10.txt         Text_11.txt         Text_12.txt

Neste exemplo, o número de colunas é restrito a quatro com o parâmetro *Column*.

## Como produzir dados

## Cmdlets Out-Host e Out-File

O cmdlet **Out-Host** é um cmdlet padrão invisível no final da pipeline. Depois que toda a formatação é aplicada, o cmdlet **Out-Host** envia a saída final para a janela do console, para exibição. Você não precisa chamar expressamente o cmdlet **Out-Host**, porque ele é a saída padrão. É possível substituir o envio da saída para a janela do console, chamando o cmdlet **Out-File** como o último cmdlet no comando. O cmdlet **Out-File** então grava a saída no arquivo especificado no comando, como no exemplo a seguir:

    Get-ChildItem | Format-Wide -Column 4 | Out-File c:\OutputFile.txt

Neste exemplo, o cmdlet **Out-File** grava as informações exibidas no comando **Get-ChildItem | Format-Wide -Column 4** em um arquivo chamado `OutputFile.txt`. Você pode também redirecionar a saída da pipeline para um arquivo com o operador de redirecionamento, que é o sinal de maior que ( `>` ). Para anexar a saída da pipeline de um comando para um arquivo existente sem substituir o arquivo original, use o caractere de sinal de maior que duplo (`>>` ), como no exemplo a seguir:

    Get-ChildItem | Format-Wide -Column 4 >> C:\OutputFile.txt

Neste exemplo, a saída do cmdlet **Get-Childitem** está canalizada para o cmdlet **Format-Wide** para formatação e, em seguida, é gravada no final do arquivo `OutputFile.txt`. Observe que, se o arquivo `OutputFile.txt` não existisse, o uso do sinal de maior do que duplo ( `>>` ) criaria o arquivo.

Para saber mais sobre pipelines, confira [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\)).

Para saber mais sobre a sintaxe usada nos exemplos anteriores, confira [Sintaxe](https://technet.microsoft.com/pt-br/library/bb123552\(v=exchg.150\)).

## Visualizando dados no Internet Explorer

Devido à flexibilidade e facilidade de script do Shell de Gerenciamento do Exchange, você pode receber os dados retornados pelos comandos, formatá-los e produzi-los de formas quase ilimitadas.

O exemplo a seguir mostra como você pode usar um script simples para produzir os dados retornados por um comando e exibi-los no Internet Explorer. Esse script recebe os objetos passados pela pipeline, abre uma janela do Internet Explorer e exibe os dados no Internet Explorer:

    $Ie = New-Object -Com InternetExplorer.Application
    $Ie.Navigate("about:blank")
    While ($Ie.Busy) { Sleep 1 }
    $Ie.Visible = $True
    $Ie.Document.Write("$Input")
    # If the previous line doesn't work on your system, uncomment the line below.
    # $Ie.Document.IHtmlDocument2_Write(\"$Input\")
    $Ie

Para usar esse script, salve-o no diretório `C:\Program Files\Microsoft\Exchange Server\V15\Scripts` no computador em que o script será executado. Nomeie o arquivo como `Out-Ie.ps1`. Depois de salvá-lo, você poderá usá-lo como um cmdlet comum.


> [!TIP]
> Para executar scripts no Exchange 2013, eles devem ser adicionados a uma função de gerenciamento sem escopo e você deve ter a função de gerenciamento atribuída diretamente ou por meio de um grupo de funções de gerenciamento. Para saber mais, confira <A href="understanding-management-roles-exchange-2013-help.md">Noções básicas sobre funções de gerenciamento</A>.



O script `Out-Ie` presume que os dados recebidos são HTML válido. Para converter os dados que deseja exibir em HTML, canalize os resultados do comando para o cmdlet **ConvertTo-Html**. Em seguida, canalize os resultados desse comando para o script `Out-Ie`. O exemplo a seguir mostra como exibir uma listagem de diretório em uma janela do Internet Explorer:

    Get-ChildItem | Select Name,Length | ConvertTo-Html | Out-Ie

## Como filtrar os dados

O Shell dá acesso a uma grande quantidade de informações sobre os servidores, caixas de correio, Active Directory e outros objetos da organização. Embora o acesso a essas informações ajude a entender melhor seu ambiente, essa grande quantidade de informações pode sobrecarregá-lo. O Shell permite controlar essas informações e usar a filtragem para retornar apenas os dados que deseja ver. Os dois tipos de filtragem a seguir estão disponíveis:

  - **Filtragem no servidor**   A filtragem no servidor pega o filtro que você especifica na linha de comando e o envia ao servidor do Exchange consultado. Esse servidor processa a consulta e retorna apenas os dados que correspondem ao filtro especificado.
    
    A filtragem no servidor é executada apenas nos objetos onde dezenas ou centenas de milhares de resultados podem ser retornados. Portanto, apenas os cmdlets de gerenciamento de destinatário, como o cmdlet **Get-Mailbox** e os cmdlets de gerenciamento de fila, como o cmdlet **Get-Queue**, suportam a filtragem no servidor. Esses cmdlets suportam o parâmetro *Filter*. Esse parâmetro recebe a expressão de filtro que você especifica e o envia para processamento no servidor.

  - **Filtragem no cliente**   A filtragem no cliente é executada nos objetos na janela do console local no qual você está trabalhando no momento. Quando você usa a filtragem no cliente, o cmdlet recupera todos os objetos que correspondem à tarefa que você está executando na janela do console local. O Shell recebe todos os resultados retornados, aplica o filtro no cliente nesses resultados e retorna apenas os resultados correspondentes ao seu filtro. Todos os cmdlets aceitam filtragem no cliente. Ele é invocado através da canalização dos resultados de um comando para o cmdlet **Where-Object**.

## Filtragem no servidor

A implementação da filtragem no servidor é específica para o cmdlet que oferece suporte para essa filtragem. A filtragem no servidor está habilitada apenas para propriedades específicas nos objetos que são retornados. Para obter mais informações, confira a Ajuda dos seguintes cmdlets:


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-ActiveSyncDevice</p></td>
<td><p>Get-ActiveSyncDeviceClass</p></td>
<td><p>Get-CASMailbox</p></td>
<td><p>Get-Contact</p></td>
<td><p>Get-DistributionGroup</p></td>
</tr>
<tr class="even">
<td><p>Get-DynamicDistributionGroup</p></td>
<td><p>Get-Group</p></td>
<td><p>Get-Mailbox</p></td>
<td><p>Get-MailboxStatistics</p></td>
<td><p>Get-MailContact</p></td>
</tr>
<tr class="odd">
<td><p>Get-MailPublicFolder</p></td>
<td><p>Get-MailUser</p></td>
<td><p>Get-Message</p></td>
<td><p>Get-MobileDevice</p></td>
<td><p>Get-Queue</p></td>
</tr>
<tr class="even">
<td><p>Get-QueueDigest</p></td>
<td><p>Get-Recipient</p></td>
<td><p>Get-RemoteMailbox</p></td>
<td><p>Get-RoleGroup</p></td>
<td><p>Get-SecurityPrincipal</p></td>
</tr>
<tr class="odd">
<td><p>Get-StoreUsageStatistics</p></td>
<td><p>Get-UMMailbox</p></td>
<td><p>Get-User</p></td>
<td><p>Get-UserPhoto</p></td>
<td><p>Remove-Message</p></td>
</tr>
<tr class="even">
<td><p>Resume-Message</p></td>
<td><p>Resume-Queue</p></td>
<td><p>Retry-Queue</p></td>
<td><p>Suspend-Message</p></td>
<td><p>Suspend-Queue</p></td>
</tr>
</tbody>
</table>


## Filtragem no cliente

A filtragem de cliente pode ser usada com qualquer cmdlet. Esse recurso inclui os cmdlets que também oferecem suporte para filtragem no servidor. Conforme descrito anteriormente neste tópico, a filtragem no cliente aceita todos os dados retornados por um comando anterior na pipeline e, por sua vez, retorna apenas os resultados que correspondem ao filtro que você especificar. O cmdlet **Where-Object** executa essa filtragem. Ele pode ser reduzido para **Where**.

Conforme os dados passam pela pipeline, o cmdlet **Where** recebe os dados do objeto anterior e, em seguida, filtra os dados antes de passá-los ao próximo objeto. A filtragem é baseada em um bloco de script definido no comando **Where**. O bloco de script filtra os dados com base nas propriedades e valores do objeto.

O cmdlet **Clear-Host** é usado para limpar a janela do console. Neste exemplo, você pode encontrar todos os aliases definidos para o cmdlet **Clear-Host**, quando executa o seguinte comando:

    Get-Alias | Where {$_.Definition -eq "Clear-Host"}
    
    CommandType     Name                            Definition
    -----------     ----                            ----------
    Alias           clear                           clear-host
    Alias           cls                             clear-host

O cmdlet **Get-Alias** e o comando **Where** funcionam juntos para retornar a lista de aliases definida para o cmdlet **Clear-Host** e nenhum outro cmdlet. A tabela a seguir destaca cada elemento do comando **Where** usado no exemplo.

### Elementos do comando Where

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>{ }</code></p></td>
<td><p>As chaves envolvem o bloco de script que define o filtro.</p></td>
</tr>
<tr class="even">
<td><p><code>$_</code></p></td>
<td><p>Essa variável especial inicia e se vincula automaticamente aos objetos na canalização.</p></td>
</tr>
<tr class="odd">
<td><p><code>Definition</code></p></td>
<td><p>A propriedade <code>Definition</code> é a propriedade dos objetos de pipeline atuais que armazena o nome da definição do alias. Quando <code>Definition</code> é usada com a variável <code>$_</code>, um ponto (.) vem antes do nome da propriedade.</p></td>
</tr>
<tr class="even">
<td><p><code>-eq</code></p></td>
<td><p>Esse operador de comparação para &quot;igual a&quot; é usado para especificar que os resultados devem corresponder exatamente ao valor da propriedade que é fornecido na expressão.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;<strong>Clear-Host</strong>&quot;</p></td>
<td><p>Neste exemplo, &quot;<strong>Clear-Host</strong>&quot; é o valor pelo qual o comando está analisando.</p></td>
</tr>
</tbody>
</table>


No exemplo, os objetos retornados pelo cmdlet **Get-Alias** representam todos os aliases definidos no sistema. Embora você não os veja na linha de comando, os aliases são coletados e passados para o cmdlet **Where** através da pipeline. O cmdlet **Where** usa as informações do bloco de script para aplicar um filtro aos objetos do alias.

A variável especial `$`\_representa os objetos que estão sendo passados. A variável`$_` é inicializada automaticamente pelo Shell e ligada ao objeto pipeline atual. Para saber mais sobre essa variável especial, confira o artigo [Variáveis do shell](https://technet.microsoft.com/pt-br/library/bb124036\(v=exchg.150\)).

Usando a notação "ponto" padrão (object.property), a propriedade `Definition` é adicionada para definir a propriedade exata do objeto a ser avaliado. O operador de comparação `-eq` então compara o valor dessa propriedade com `"Clear-Host"`. Apenas os objetos com a propriedade `Definition` que correspondem a esse critério são passados para a janela do console para saída. Para saber mais sobre operadores de comparação, confira o artigo [Operadores de comparação](https://technet.microsoft.com/pt-br/library/bb125229\(v=exchg.150\)).

Após o comando **Where** filtrar os objetos retornados pelo cmdlet **Get-Alias**, você pode direcionar os objetos filtrados para outro comando. O próximo comando processa apenas os objetos filtrados retornados pelo comando Where.

