---
title: 'Métodos e técnicas para pacotes de regras correspondentes: Exchange 2013 Help'
TOCTitle: Métodos e técnicas para pacotes de regras correspondentes
ms:assetid: 09fe9278-d077-452c-b7e5-729b3dc70b1b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ674702(v=EXCHG.150)
ms:contentKeyID: 50484925
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Métodos e técnicas para pacotes de regras correspondentes

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-07-28_

Este tópico descreve técnicas para correspondência de padrões e elementos de evidência dentro de um arquivo XML de prevenção de perda de dados (DLP) que foi feito para conter seu próprio pacote de regra de tipo de informação confidencial. Depois de ter criado um arquivo XML no formato correto, você poderá importar o arquivo, usando o Centro de administração do Exchange (EAC) ou o Shell de Gerenciamento do Exchange, para ajudar a criar sua solução DLP do Microsoft Exchange Server 2013. Antes de você poder fazer uso dos métodos de correspondência descritos aqui, você já deve ter um arquivo XML de DLP iniciado. Para mais informações sobre definir seus próprios modelos DLP e arquivos XML, consulte [Definir seus próprios modelos de DLP e tipos de informações](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

## O elemento Match

O elemento `Match` é usado dentro dos elementos `Pattern` e `Evidence` para representar a palavra-chave, expressão regular ou função que deve corresponder. A definição da correspondência em si é armazenada fora do elemento `Rule` e é referenciada através do atributo exigido `idRef`. Vários elementos `Match` podem ser incluídos em uma definição de Padrão que pode ser incluída diretamente no elemento `Pattern` ou combinado usando-se o elemento `Any` para definir a semântica de correspondência.

    <?xml version="1.0" encoding="utf-8"?>
    <Rules packageId="...">
            ...
    <Entity id="...">
      <Pattern confidenceLevel="85">
                 <IdMatch idRef="FormattedSSN" />
                 <Match idRef="USDate" />
                 <Match idRef="USAddress" />
      </Pattern>
    </Entity>
            ...
             <Keyword id="FormattedSSN "> ... </Keyword>
             <Regex id=" USDate "> ... </Regex>
             <Regex id="USAddress"> ... </Regex>
            ...
    
    </Rules>

## Definir correspondências baseadas em palavras-chave

Um requisito de Regra comum é fazer a correspondência com base em expressões de cadeia de caracteres de palavra-chave bem conhecidas. Isso é feito usando-se o cmdlet `Keyword`. O elemento Keyword tem um atributo "id" que é usado como uma referência para as regras de Entidade ou Afinidade correspondentes. Um único elemento Keyword pode ser referenciado em várias regras de Entidade e Afinidade.

A correspondência pode ser executada usando uma correspondência exata ou algoritmos de correspondência com base do word. Correspondência exata usa um algoritmo de maiúsculas e minúsculas que pesquisa para o texto no idioma especificado. Correspondência de Word aplica um algoritmo de correspondência com base nos limites do word. Os termos a serem comparadas com podem ser embutida incluída na definição de palavra-chave usando o elemento de subsites do termo.


> [!TIP]
> Use o estilo de correspondência baseada em constantes sobre regex para uma melhor eficiência e desempenho. Use a correspondência de regex somente em casos onde as correspondências baseadas em constantes não são suficientes e a flexibilidade de expressões regulares é necessária.



    <Keyword id="Word_Example">
        <Group matchStyle="word">
           <Term>card verification</Term>
           <Term>cvn</Term>
           <Term>cid</Term>
           <Term>cvc2</Term>
           <Term>cvv2</Term>
           <Term>pin block</Term>
           <Term>security code</Term>
        </Group>
    </Keyword>
    ...
    <Keyword id="String_Example">
        <Group matchStyle="string">
           <Term>card</Term>
           <Term>pin</Term>
           <Term>security</Term>
        </Group>
    </Keyword>

## Definir de expressão regular com base em correspondência

Um outro método comum de correspondência é baseado em expressões regulares. A flexibilidade da correspondência de expressão regular faz dessa uma escolha comum para implementar a correspondência para dados como números de carteira de motorista, endereços. A sintaxe de expressão regular comum é usada para definir os padrões de expressão regular. A tabela a seguir contém exemplos de algumas das mais comuns tokens de expressões regulares disponíveis.


> [!TIP]
> Use o estilo de correspondência baseada em constantes sobre regex para uma melhor eficiência e desempenho. Use a correspondência de regex somente em casos onde as correspondências baseadas em constantes não são suficientes e a flexibilidade de expressões regulares é necessária.




<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Símbolo</th>
<th>Significado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>c</p></td>
<td><p>Compara o caractere literal c uma vez, a menos que seja um dos caracteres especiais.</p></td>
</tr>
<tr class="even">
<td><p>^</p></td>
<td><p>Comparar com o início de uma linha.</p></td>
</tr>
<tr class="odd">
<td><p>.</p></td>
<td><p>Compara a qualquer caractere que não seja uma nova linha.</p></td>
</tr>
<tr class="even">
<td><p>$</p></td>
<td><p>Comparar com o fim de uma linha.</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>Lógica OU entre expressões.</p></td>
</tr>
<tr class="even">
<td><p>()</p></td>
<td><p>Agrupar subexpressões.</p></td>
</tr>
<tr class="odd">
<td><p>[]</p></td>
<td><p>Definir uma classe de caractere.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>Corresponder à expressão anterior zero ou mais vezes.</p></td>
</tr>
<tr class="odd">
<td><p>+</p></td>
<td><p>Corresponder à expressão anterior uma ou mais vezes.</p></td>
</tr>
<tr class="even">
<td><p>?</p></td>
<td><p>Corresponder à expressão anterior zero ou uma vez.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n</em>}</p></td>
<td><p>Corresponder à expressão anterior <em>n</em> vezes.</p></td>
</tr>
<tr class="even">
<td><p>{<em>n,</em>}</p></td>
<td><p>Corresponder à expressão anterior pelo menos <em>n</em> vezes.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n, m</em>}</p></td>
<td><p>Corresponder à expressão anterior pelo menos <em>n</em> vezes e no máximo <em>m</em> vezes.</p></td>
</tr>
<tr class="even">
<td><p>\d</p></td>
<td><p>Corresponder a um dígito.</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>Corresponder a um caractere que não é um dígito.</p></td>
</tr>
<tr class="even">
<td><p>\w</p></td>
<td><p>Corresponder a um caractere alfa, incluindo sublinhado.</p></td>
</tr>
<tr class="odd">
<td><p>\W</p></td>
<td><p>Corresponder a um caractere que não é um caractere alfa.</p></td>
</tr>
<tr class="even">
<td><p>\s</p></td>
<td><p>Corresponder a um caractere de espaço em branco (qualquer um dentre \t, \n, \r ou \f).</p></td>
</tr>
<tr class="odd">
<td><p>\S</p></td>
<td><p>Corresponder a um caractere diferente de espaço.</p></td>
</tr>
<tr class="even">
<td><p>\t</p></td>
<td><p>Tab.</p></td>
</tr>
<tr class="odd">
<td><p>\n</p></td>
<td><p>Nova linha.</p></td>
</tr>
<tr class="even">
<td><p>\r</p></td>
<td><p>Retorno de carro.</p></td>
</tr>
<tr class="odd">
<td><p>\f</p></td>
<td><p>Alimentação de formulário.</p></td>
</tr>
<tr class="even">
<td><p>\<em>m</em></p></td>
<td><p><em>m</em> de escape, em que <em>m</em> é um dos metacaracteres descritos acima: ^, ., $, |, (), [], *, +, ?, \, ou /.</p></td>
</tr>
</tbody>
</table>


O elemento Regex tem um atributo "id" que é usado como uma referência para as regras de Entidade ou Afinidade correspondentes. Um único elemento Regex pode ser referenciado em várias regras de Entidade e Afinidade. A expressão Regex é definida como o valor do elemento Regex.

    <Regex id="CCRegex">
         \bcc\#\s|\bcc\#\:\s
    </Regex>
    ...
    <Regex id="ItinFormatted">
        (?:^|[\s\,\:])(?:9\d{2})[- ](?:[78]\d[-       ]\d{4})(?:$|[\s\,]|\.\s)
    </Regex>
    ...
    <Regex id="NorthCarolinaDriversLicenseNumber">
        (^|\s|\:)(\d{1,8})($|\s|\.\s)
    </Regex>

## Combinar vários elementos de correspondência

Uma técnica comum para aumentar a confiança da correspondência é definir a semântica entre várias elementos de Match, por exemplo, que seja necessário acontecer uma ou mais correspondências. O elemento Qualquer permite a definição da lógica com base em várias correspondências. O elemento Qualquer pode ser usado como subelemento no elemento padrão. Ele contém um ou mais elementos filho Match e define a lógica de correspondências entre eles. Veja abaixo exemplos de códigos XML para os elementos Qualquer com todas as correspondências, lógica "não" e a conta de correspondências exatas.

O atributo opcional minMatches pode ser usado (padrão = 1) para definir o número mínimo de elementos Match que devem ser atendidos para se satisfazer uma correspondência. Similarmente, o atributo opcional maxMatchs pode ser usado (padrão = número de elementos filho de Match) para definir o número máximo de elementos de Match que devem ser atendidos para satisfazer uma correspondência. Essas condições são combinadas usando-se operadores lógicos baseados no uso dos atributos minMatches e maxMatchs, permitindo estas semânticas:

  - Corresponder todos os elementos filhos de Match
    
    Não corresponder todos os elementos filhos de Match
    
    Corresponder um subconjunto exato dos elementos filhos de Match

<!-- end list -->

    <Any minMatches="3" maxMatches="3">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any maxMatches="0">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

    <Any minMatches="1" maxMatches="1">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>

## Aumentar o nível de confiança com mais evidências

Para regras de base de entidade, outra opção de aumentar a confiança é definir vários elementos Padrão, cada um com um número maior de evidência corroborativa. Isso é conseguido usando-se minMatches e maxMatches para o elemento Qualquer, para criar padrões independentes com um nível de confiança crescente, com base no número crescente de evidências corroborativas. Por exemplo:

  - se for encontrado uma peça de evidência corroborativa: nível de confiança é de 65%

  - se duas peças: nível de confiança é de 75%

  - se três peças: nível de confiança é de 85%

<!-- end list -->

    <Entity id="..." patternsProximity="300" >
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Any maxMatches="1">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="75">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="2" maxMatches="2">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="85">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="3">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity>

## Exemplo: Regra Seguro Social dos EUA

Essa seção inclui uma descrição introdutória para se autorar uma regra correspondente a um número do Seguro Social dos EUA. Primeiro, comece com uma descrição de como identificar conteúdo que contenha o número do seguro social. Um número de Seguro Social é encontrado se:

1.  Regex corresponde a um SSN formatado (e é o intervalo válido de SSN)

2.  Evidências Corroborativas   um dos seguintes devem ocorrer nas proximidades:
    
    1.  Correspondência de palavra-chave {Seguro Social, Soc Sec, SSN, SSNS, SSN\#, SS\#, SSID}
    
    2.  Texto que representa um endereço nos EUA
    
    3.  Texto que representa uma data
    
    4.  Texto que representa um nome

Em seguida, traduza a descrição para a representação do esquema de Regra:

    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77"
             patternsProximity="300" RecommendedConfidence="85">
        <Pattern confidenceLevel="85">
          <IdMatch idRef="FormattedSSN" />
          <Any minMatches="1">
              <Match idRef="SSNKeywords" />
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
        </Pattern>
    </Entity>

## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Definir seus próprios modelos de DLP e tipos de informações](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[Importar um modelo de política DLP personalizado de um arquivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

