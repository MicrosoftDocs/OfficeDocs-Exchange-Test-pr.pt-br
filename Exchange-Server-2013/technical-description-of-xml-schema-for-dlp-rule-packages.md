---
title: 'Desenvolver pacotes de regras de informações confidenciais: Exchange 2013 Help'
TOCTitle: Desenvolver pacotes de regras de informações confidenciais
ms:assetid: c4ab8707-0839-4855-9390-3dbcb43475a7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ674704(v=EXCHG.150)
ms:contentKeyID: 50486582
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desenvolver pacotes de regras de informações confidenciais

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-07-28_

O esquema XML e a orientação neste tópico ajudará você começar a criar seu próprio perda de dados básicos arquivos XML prevention (DLP) que definem os seus próprios tipos de informações confidenciais em um pacote de regras de classificação. Depois de criar um arquivo XML válido, você pode importá-lo usando o Centro de administração do Exchange ou o shell de gerenciamento do Exchange para ajudar a criar uma solução do Microsoft Exchange Server 2013 DLP. Um arquivo XML que é um modelo de política DLP personalizado pode conter o XML que é seu pacote de regras de classificação. Para obter uma visão geral sobre como definir seus próprios modelos DLP, como arquivos XML, consulte [Definir seus próprios modelos de DLP e tipos de informações](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

**Sumário**

Visão geral da regra de processo de criação

Descrição da regra

Estrutura de regra básica

Usando os idiomas locais em seu arquivo XML

Pacote de regra de classificação definição de esquema XML

Para saber mais

## Visão geral da regra de processo de criação

A processo de criação de regra é formada pelas seguintes etapas gerais.

1.  Prepare um conjunto de documentos de teste representativos do ambiente de destino. Características principais a serem considerados para o conjunto de documentos de teste incluem: um subconjunto dos documentos contêm a entidade ou afinidade para o qual a regra é criada e um subconjunto dos documentos que não contenham a entidade ou afinidade para o qual a regra está sendo criada.

2.  Identifica as regras que atendem aos requisitos de aceitação (precisão e o cancelamento) para identificar conteúdo qualificado. Isso pode exigir o desenvolvimento de várias condições, dentro de uma regra, acoplado com lógica de booleana, que juntos satisfazer os requisitos mínimos de correspondência para identificar documentos de destino.

3.  Estabelece o nível de confiança recomendada para as regras de acordo com os requisitos de aceitação (precisão e o cancelamento). O elemento de confiança recomendada pode ser considerado o nível de confiança padrão para a regra.

4.  Valide as regras instanciando uma política com eles e monitorando o conteúdo de teste de exemplo. Com base nos resultados, ajuste as regras, ou o nível de confiança para maximizar o conteúdo detectado, minimizando negativos e falsos positivos. Continue o ciclo de validação e ajustes de regra até um nível satisfatório de detecção de conteúdo é atingido para amostras de positivas e negativas.

Para obter informações sobre a definição de esquema XML para arquivos de modelo de política, consulte [Desenvolver arquivos de modelo de política de DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

## Descrição da regra

Dois tipos principais de regra podem ser criados para o mecanismo de detecção de informações confidenciais de DLP: entidade e afinidade. O tipo de regra escolhido baseia-se ao tipo de lógica de processamento que deve ser aplicada ao processamento do conteúdo, conforme descrito nas seções anteriores. As definições de regra são configuradas em um documento XML no formato descrito pelo XSD regras padronizado. As regras descrevem ambas o tipo de conteúdo para o nível de confiança que a correspondência descrita representa o conteúdo de destino e correspondência. Nível de confiança especifica a probabilidade da entidade estar presentes se um padrão for encontrado no conteúdo ou a probabilidade para a afinidade estar presentes se evidência for encontrada no conteúdo.

## Estrutura de regra básica

A definição de regra é construída a partir de três componentes principais:

1.  **Entidade** define a lógica de contagem e correspondente para essa regra

2.  **Afinidade** define a lógica correspondente para a regra

3.  Localização de **Cadeias de caracteres localizadas** para nomes de regra e suas descrições

Três elementos de suportados adicionais são usados que definem os detalhes do processamento e referenciada dentro os componentes principais: palavra-chave, Regex e função. Usando referências, uma única definição dos elementos de suporte, como um número de seguridade social, pode ser usada em várias regras de entidade ou afinidade. A estrutura básica de regra em formato XML pode ser vista da seguinte maneira.

```powershell
    <?xml version="1.0" encoding="utf-8"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
    
      <RulePack id="DAD86A92-AB18-43BB-AB35-96F7C594ADAA">
        <Version major="1" minor="0" build="0" revision="0"/>
        <Publisher id="619DD8C3-7B80-4998-A312-4DF0402BAC04"/>
        <Details defaultLangCode="en-us">
          <LocalizedDetails langcode="en-us">
            <PublisherName>DLP by EPG</PublisherName>
            <Name>CSO Custom Rule Pack</Name>
            <Description>This is a rule package for a EPG demo.</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
    
      <Rules>
    
        <!-- Employee ID -->
        <Entity id="E1CC861E-3FE9-4A58-82DF-4BD259EAB378" patternsProximity="300" recommendedConfidence="75">
          <Pattern confidenceLevel="75">
            <IdMatch idRef="Regex_employee_id" />
            <Match idRef="Keyword_employee" />
          </Pattern>
        </Entity>
    
        <Regex id="Regex_employee_id">(\s)(\d{9})(\s)</Regex>
        <Keyword id="Keyword_employee">
          <Group matchStyle="word">
            <Term>Identification</Term>
            <Term>Contoso Employee</Term>
          </Group>
        </Keyword>
    
    
        <LocalizedStrings>
    
          <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB378">
            <Name default="true" langcode="en-us">
              Employee ID
            </Name>
            <Description default="true" langcode="en-us">
              A custom classification for detecting Employee ID's
            </Description>
          </Resource>
    
        </LocalizedStrings>
      </Rules>
    </RulePackage>
```

## Regras da entidade

Regras da entidade são voltadas para os identificadores bem definidos, como número de Seguridade Social e são representadas por um conjunto de countable padrões. Regras da entidade retorna uma contagem e o nível de confiança de uma coincidência, onde Count é o número total de instâncias da entidade que foram encontrados e o nível de confiança é a probabilidade de que a determinada entidade existe no documento determinado. Entidade contém o atributo "id" como seu identificador exclusivo. O identificador é usado para consultar, controle de versão e localização. A id da entidade deve ser um GUID e não deve ser duplicada em outras entidades ou afinidades. Ele é mencionado na seção de cadeias de caracteres localizadas.

Contém o atributo patternsProximity opcional de regras de entidade (padrão = 300) que é usado quando a aplicação de lógica booleana para especificar a proximidade padrões de múltiplos necessários para satisfazer a condição de correspondência. Elemento de entidade contém 1 ou mais padrão elementos filho, onde cada padrão é uma representação distinta da entidade como entidade do cartão de crédito ou de motorista da entidade de licença. O elemento padrão tem um atributo necessário do confidenceLevel que representa a precisão do padrão com base no conjunto de dados de amostra. Elemento padrão pode ter três elementos filho:

1.  IdMatch - é necessário.

2.  Correspondência

3.  Qualquer um

Se qualquer um dos elementos padrão retornar "true", o padrão será satisfeito. A contagem do elemento de entidade é igual à soma de todos os detectado contagens de padrão.

![Fórmula matemática para contagem de entidades](images/JJ674704.25309939-98bc-4460-8f89-8560bbad7981(EXCHG.150).gif "Fórmula matemática para contagem de entidades")

onde k é o número de elementos de padrão para a entidade.

Um elemento de padrão deve ter exatamente um elemento IdMatch. IdMatch representa o identificador que o padrão deve corresponder, por exemplo um número de cartão de crédito ou número ITIN. A contagem de um padrão é o número de IdMatches comparadas com o elemento padrão. Elemento IdMatch Ancora a janela de proximidade para os elementos de correspondência.

Outro elemento sub-recurso opcional do elemento padrão é a correspondência que representa a evidência corroborativa que é necessária a serem comparadas com para suportar localizando o elemento IdMatch. Por exemplo, a regra de confiança mais alta pode exigir que, além de localizar um número de cartão de crédito, artefatos adicionais existirem no documento, em uma janela de proximidade do cartão de crédito, como o endereço e o nome. Esses artefatos adicionais seriam representados por meio do elemento de correspondência ou qualquer elemento (eles são descritos em detalhes na seção Matching Methods and Techniques). Vários elementos de correspondência podem ser incluídos em uma definição padrão que pode ser incluída diretamente no elemento padrão ou combinados usando o elemento de qualquer para definir semântica correspondente. Ele retornará true se uma correspondência for encontrada na janela de proximidade ancorada ao redor do conteúdo IdMatch.

Elementos de correspondência e IdMatch não definem os detalhes do qual o conteúdo deve ser correspondido mas em vez disso, referenciá-lo por meio do atributo idRef. Isso promove a capacidade de reutilização de definições em várias construções de padrão.

```powershell
    <Entity id="..." patternsProximity="300" > 
        <Pattern confidenceLevel="85">
            <IdMatch idRef="FormattedSSN" />
            <Any minMatches="1">
                <Match idRef="SSNKeyword" />
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>  
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Match idRef="SSNKeyword" />
            <Any minMatches="1">        
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity> 

```
O elemento de id da entidade, representado no XML anterior por "..." deve ser um GUID e é referenciado na seção de cadeias de caracteres localizadas.

## Janela de proximidade do padrão de entidade

Entidade contém o valor do atributo patternsProximity opcional (inteiro, padrão = 300) usada para encontrar os padrões. Para cada padrão o valor do atributo define a distância (em caracteres Unicode) do local IdMatch para todas as outras correspondências especificado para aquele padrão. A janela de proximidade é ancorada pela localização IdMatch, com estendendo a janela para a esquerda e direita do IdMatch.

![Padrão de texto com elementos de correspondência destacados](images/JJ674704.65d52989-f50f-4097-b39a-9612f860d727(EXCHG.150).gif "Padrão de texto com elementos de correspondência destacados")

O exemplo a seguir ilustra como a janela de proximidade afeta o algoritmo de correspondência onde o elemento de SSN IdMatch requer pelo menos 1 de endereço, o nome ou o data corroborating correspondências. Apenas SSN1 e SSN4 corresponderem porque para SSN2 e SSN3, ambos não ou apenas evidência corroborating parcial for localizada dentro da janela de proximidade.

![Exemplos de correspondência e não correspondência de regras de proximidade](images/JJ674704.8117deb3-d8c8-4d4e-a011-ac5f9990b08e(EXCHG.150).gif "Exemplos de correspondência e não correspondência de regras de proximidade")

Observe que o corpo da mensagem e cada anexo são tratados como itens independentes. Isso significa que a janela de proximidade não estende além do final de cada um desses itens. Para cada item (anexo ou corpo), a idMatch e a evidência corroborativa deve residir em cada uma.

## Nível de confiança de entidade

Nível de confiança do elemento de entidade é a combinação de níveis de confiança do todo o seu nível de satisfação padrão. Eles são combinados usando a seguinte equação:

![Fórmula matemática para o nível de confiabilidade da entidade](images/JJ674704.9b8bb9c8-3ded-4ea5-a609-71d8034b1017(EXCHG.150).gif "Fórmula matemática para o nível de confiabilidade da entidade")

onde k é o número de elementos de padrão para a entidade e um padrão que não corresponda retorna o nível de confiança de 0.

Referência de volta para o exemplo de código do exemplo entidade elemento estrutura, se ambos os padrões forem correspondentes, o nível de confiança da entidade é % 94.75 com base no seguinte cálculo:

CLEntidade= 1-\[(1-CLPattern1) x (1-CLPattern1)\]

*= 1-\[(1-0.85) x (1-0.65)\]*

*= 1-(0,15 x 0.35)*

*= 94.75%*

Da mesma forma, se apenas o segundo padrão corresponde, o nível de confiança da entidade é 65% com base no seguinte cálculo:

CLEntidade= 1 – \[(1 – CLPattern1) X (1 – CLPattern1)\]

*= 1 – \[(1 – 0) X (1 – 0.65)\]*

*= 1 – (1 X 0.35)*

*= 65%*

Esses valores de confiança são atribuídos nas regras de padrões individuais com base no conjunto de documentos de teste validado como parte da regra de processo de criação.

## Regras de afinidade

Regras de afinidade direcionadas rumo conteúdo sem identificadores bem definidos, por exemplo, Sarbanes-Oxley ou conteúdo financeiro corporativo. Nenhum identificador consistente único para este conteúdo pode ser encontrada e em vez disso, análise, é necessário determinar se uma coleção de evidência estiver presente. Regras de afinidade não retorna uma contagem, em vez disso, elas retornam se encontrado e o nível de confiança associado. Conteúdo de afinidade é representado como uma coleção de outras evidências independentes. Evidência é uma agregação de correspondências necessárias em determinados proximidade. Regra de afinidade, proximidade é definida pelo atributo evidencesProximity (o padrão é 600) e o nível de confiança mínimos pelo atributo thresholdConfidenceLevel.

Regras de afinidade contém o atributo id para o identificador exclusivo que é usado para a localização, controle de versão e consultas. Diferentemente das regras de entidade, porque as regras de afinidade não contam com identificadores bem definidos, elas não contêm o elemento IdMatch.

Cada regra de afinidade contém um ou mais elementos de evidência filho que definem a evidência que deve ser encontrado e o nível de confiança que contribuem para a regra de afinidade. A afinidade não é considerada encontrar se não houver o nível de confiança resultantes abaixo do nível de limite. Cada evidência logicamente representa a evidência corroborativa este "tipo" de documento e o atributo confidenceLevel é a precisão para essa evidência no conjunto de dados de teste.

Elementos de evidência têm uma ou mais de correspondência ou quaisquer elementos filho. Se todos os filhos de correspondência e quaisquer elementos coincidirem, a evidência for encontrada e o nível de confiança é contribuíram para o cálculo de nível de confiança de regras. A mesma descrição se aplica a correspondência ou quaisquer elementos para regras de afinidade às propriedades de regras da entidade.

```powershell
    <Affinity id="..." 
              evidencesProximity="1000"
              thresholdConfidenceLevel="65">
        <Evidence confidenceLevel="40">
            <Any> 
                <Match idRef="AssetsTerms" /> 
                <Match idRef="BalanceSheetTerms" /> 
                <Match idRef="ProfitAndLossTerms" /> 
            </Any> 
        </Evidence>
        <Evidence confidenceLevel="40">
            <Any minMatches="2"> 
                <Match idRef="TaxTerms" /> 
                <Match idRef="DollarAmountTerms" /> 
                <Match idRef="SECTerms" /> 
                <Match idRef="SECFilingFormTerms" /> 
                <Match idRef="DollarTotalRegex" /> 
            </Any> 
        </Evidence>
    </Affinity>
```

## Janela de proximidade afinidade

Janela proximidade para fins de afinidade é calculada de forma diferente que para padrões de entidade. Proximidade afinidade segue um modelo de janela deslizante. O algoritmo de proximidade afinidade tenta localizar o número máximo de outras evidências correspondentes na janela de determinado. Outras evidências na janela de proximidade devem ter um nível de confiança maior do que o limite definido para a regra de afinidade serão encontradas.

![Texto em proximidade de uma correspondência de regra de afinidade](images/JJ674704.2601ec86-0094-43fa-8d22-9d97f7465942(EXCHG.150).gif "Texto em proximidade de uma correspondência de regra de afinidade")

## Nível de confiança de afinidade

Nível de confiança para a afinidade é igual a combinação das outras evidências localizadas dentro da janela de proximidade para a regra de afinidade. Embora semelhante para o nível de confiança da regra de entidade, a principal diferença é o aplicativo da janela de proximidade. É o nível de confiança do elemento de afinidade semelhante às regras de entidade, a combinação de todos os satisfeito evidência confiança níveis, mas para a regra de afinidade apenas representa a combinação mais alta dos elementos de evidência encontrados dentro da janela de proximidade. Os níveis de confiança evidência são combinados usando a seguinte equação:

![Fórmula matemática para confiabilidade da regra de afinidade](images/JJ674704.8a5da4ca-af02-4c5a-ab60-0072dc7e7a0f(EXCHG.150).gif "Fórmula matemática para confiabilidade da regra de afinidade")

onde k é o número de elementos de evidência para a afinidade correspondido dentro da janela de proximidade.

Voltando à estrutura de regra da Figura 4 exemplo afinidade, se todas as outras evidências de três são comparadas dentro a proximidade janela deslizante, o nível de confiança de afinidade é % de 85.6 com base no cálculo abaixo. Isso excede o limite de regra de afinidade de 65 que resulta em uma correspondência de regra.

CLAfinidade= 1 – \[(1 – CLEvidência 1) X (1 – CLEvidência 2) X (1 – CLEvidência 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0.4) X (1 – 0.4)\]*

*= 1 – (0.4 x 0,6 X 0,6)*

*= 85.6%*

![Exemplo de correspondência de regra de afinidade com alta confiabilidade](images/JJ674704.e17b2e22-18c3-40c4-8f19-0993bb556675(EXCHG.150).gif "Exemplo de correspondência de regra de afinidade com alta confiabilidade")

Usando a mesma definição de regra de exemplo, se somente a primeira evidência corresponde porque a segunda evidência está fora da janela de proximidade, o nível mais alto de confiança de afinidade é 60% com base no cálculo abaixo e a regra de afinidade não corresponde desde que o limite de 65 não foi atingido.

CLAfinidade= 1 – \[(1 – CLEvidência 1) X (1 – CLEvidência 2) X (1 – CLEvidência 2)\]

*= 1 – \[(1 – 0.6) X (0 – 1) X (1 – 0)\]*

*= 1 – (0.4 x 1X1)*

*= 60%*

![Exemplo de correspondência de regra de afinidade com baixa confiabilidade](images/JJ674704.077095b1-6eb0-40df-b254-f33437725720(EXCHG.150).gif "Exemplo de correspondência de regra de afinidade com baixa confiabilidade")

## Ajuste de níveis de confiança

Um dos principais aspectos da regra de processo de criação é o ajuste dos níveis de confiança para regras de entidade e afinidade. Depois de criar as definições de regra, execute a regra em relação ao conteúdo representativo e coletar os dados de precisão. Compare os resultados retornados por cada padrão ou a evidência contra os resultados esperados para os documentos de teste.

![Tabela com a comparação de evidências de correspondência de regra](images/JJ674704.25a7d9a1-d02f-447e-a88b-8e78bdc0413a(EXCHG.150).gif "Tabela com a comparação de evidências de correspondência de regra")

Se as regras de atender aos requisitos de aceitação, ou seja, o padrão ou a evidência tem uma taxa de confiança acima um limite estabelecido (por exemplo, 75%) — a expressão de correspondência está concluída e ela pode ser movida para a próxima etapa.

Se o padrão ou a evidência não atenderem o nível de confiança, em seguida, novamente criá-lo (por exemplo, adicionar evidência corroborativa mais; remover ou adicionar padrões obter/outras evidências; etc.) e repita esta etapa.

Em seguida, ajuste o nível de confiança para cada padrão ou a evidência nas regras com base nos resultados da etapa anterior. Para cada padrão ou a evidência, agregadas o número de True positivos (PA), subconjunto dos documentos que contenham a entidade ou afinidade para o qual a regra é criada e que resultou em uma correspondência e o número de falsos positivos (FP), um subconjunto de documentos que não contêm a entidade ou afinidade para a qual a regra é criada e que também retornado uma correspondência. Definir o nível de confiança para cada padrão/evidência usando o seguinte cálculo:

*Nível de confiança = True positivos / (True positivos + falsos positivos)*


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Padrão ou a evidência</th>
<th>True positivos</th>
<th>Falsos positivos</th>
<th>Nível de confiança</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>P1ou f1</p></td>
<td><p>4</p></td>
<td><p>1</p></td>
<td><p>80%</p></td>
</tr>
<tr class="even">
<td><p>P2ou f2</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Pnou fn</p></td>
<td><p>9</p></td>
<td><p>10</p></td>
<td><p>47%</p></td>
</tr>
</tbody>
</table>


## Usando os idiomas locais em seu arquivo XML

O esquema de regra suporta o armazenamento de nome localizado e uma descrição para cada um dos elementos da entidade e afinidade. Cada elemento da entidade e afinidade deve conter um elemento correspondente na seção LocalizedStrings. Para localizar cada elemento, inclua um elemento de recurso como um filho do elemento LocalizedStrings para armazenar o nome e as descrições para várias localidades para cada elemento. O elemento de recurso inclui um atributo idRef necessários que corresponde ao atributo idRef correspondente para cada elemento que está sendo localizado. Os elementos filho de localidade do elemento de recurso contém o nome localizado e descrições para cada localidade especificada.

```powershell
    <LocalizedStrings>
        <Resource idRef="guid">
            <Locale langcode="en-US" default="true"> 
                <Name>affinity name en-us</Name> 
                <Description>
                    affinity description en-us
                </Description> 
            </Locale> 
            <Locale langcode="de"> 
                <Name>affinity name de</Name> 
                <Description>
                    affinity description de
                </Description> 
            </Locale> 
        </Resource>
    </LocalizedStrings>
```

## Pacote de regra de classificação definição de esquema XML

```powershell
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:mce="http://schemas.microsoft.com/office/2011/mce"
               targetNamespace="http://schemas.microsoft.com/office/2011/mce" 
               xmlns:xs="http://www.w3.org/2001/XMLSchema"
               elementFormDefault="qualified"
               attributeFormDefault="unqualified"
               id="RulePackageSchema">
      <xs:simpleType name="LangType">
        <xs:union memberTypes="xs:language">
          <xs:simpleType>
            <xs:restriction base="xs:string">
              <xs:enumeration value=""/>
            </xs:restriction>
          </xs:simpleType>
        </xs:union>
      </xs:simpleType>
      <xs:simpleType name="GuidType" final="#all">
        <xs:restriction base="xs:token">
          <xs:pattern value="[0-9a-fA-F]{8}\-([0-9a-fA-F]{4}\-){3}[0-9a-fA-F]{12}"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulePackageType">
        <xs:sequence>
          <xs:element name="RulePack" type="mce:RulePackType"/>
          <xs:element name="Rules" type="mce:RulesType">
            <xs:key name="UniqueRuleId">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueProcessorId">
              <xs:selector xpath="mce:Regex|mce:Keyword"></xs:selector>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueResourceIdRef">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:key>        
            <xs:keyref name="ReferencedRuleMustExist" refer="mce:UniqueRuleId">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:keyref>
            <xs:keyref name="RuleMustHaveResource" refer="mce:UniqueResourceIdRef">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:keyref>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="RulePackType">
        <xs:sequence>
          <xs:element name="Version" type="mce:VersionType"/>
          <xs:element name="Publisher" type="mce:PublisherType"/>
          <xs:element name="Details" type="mce:DetailsType">
            <xs:key name="UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="mce:LocalizedDetails"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:keyref name="DefaultLangCodeMustExist" refer="mce:UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="."/>
              <xs:field xpath="@defaultLangCode"/>
            </xs:keyref>
          </xs:element>
          <xs:element name="Encryption" type="mce:EncryptionType" minOccurs="0" maxOccurs="1"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="VersionType">
        <xs:attribute name="major" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="minor" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="build" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="revision" type="xs:unsignedShort" use="required"/>
      </xs:complexType>
      <xs:complexType name="PublisherType">
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="LocalizedDetailsType">
        <xs:sequence>
          <xs:element name="PublisherName" type="mce:NameType"/>
          <xs:element name="Name" type="mce:RulePackNameType"/>
          <xs:element name="Description" type="mce:OptionalNameType"/>
        </xs:sequence>
        <xs:attribute name="langcode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="DetailsType">
        <xs:sequence>
          <xs:element name="LocalizedDetails" type="mce:LocalizedDetailsType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="defaultLangCode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="EncryptionType">
        <xs:sequence>
          <xs:element name="Key" type="xs:normalizedString"/>
          <xs:element name="IV" type="xs:normalizedString"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="RulePackNameType">
        <xs:restriction base="xs:token">
          <xs:minLength value="1"/>
          <xs:maxLength value="64"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="NameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="1"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="OptionalNameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="0"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="RestrictedTermType">
        <xs:restriction base="xs:string">
          <xs:minLength value="1"/>
          <xs:maxLength value="512"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulesType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Entity" type="mce:EntityType"/>
            <xs:element name="Affinity" type="mce:AffinityType"/>
          </xs:choice>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Regex" type="mce:RegexType"/>
            <xs:element name="Keyword" type="mce:KeywordType"/>
          </xs:choice>
          <xs:element name="LocalizedStrings" type="mce:LocalizedStringsType"/>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="EntityType">
        <xs:sequence>
          <xs:element name="Pattern" type="mce:PatternType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="patternsProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="recommendedConfidence" type="mce:ProbabilityType"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="PatternType">
        <xs:sequence>
          <xs:element name="IdMatch" type="mce:IdMatchType"/>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="AffinityType">
        <xs:sequence>
          <xs:element name="Evidence" type="mce:EvidenceType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="evidencesProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="thresholdConfidenceLevel" type="mce:ProbabilityType" use="required"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="EvidenceType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="IdMatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="MatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="AnyType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="minMatches" type="xs:nonNegativeInteger" default="1"/>
        <xs:attribute name="maxMatches" type="xs:nonNegativeInteger" use="optional"/>
      </xs:complexType>
      <xs:simpleType name="ProximityType">
        <xs:restriction base="xs:positiveInteger">
          <xs:minInclusive value="1"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="ProbabilityType">
        <xs:restriction base="xs:integer">
          <xs:minInclusive value="1"/>
          <xs:maxInclusive value="100"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="WorkloadType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Exchange"/>
          <xs:enumeration value="Outlook"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RegexType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="id" type="xs:token" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="KeywordType">
        <xs:sequence>
          <xs:element name="Group" type="mce:GroupType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="xs:token" use="required"/>
      </xs:complexType>
      <xs:complexType name="GroupType">
        <xs:sequence>
          <xs:choice>
            <xs:element name="Term" type="mce:TermType" maxOccurs="unbounded"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="matchStyle" default="word">
          <xs:simpleType>
            <xs:restriction base="xs:NMTOKEN">
              <xs:enumeration value="word"/>
              <xs:enumeration value="string"/>
            </xs:restriction>
          </xs:simpleType>
        </xs:attribute>
      </xs:complexType>
      <xs:complexType name="TermType">
        <xs:simpleContent>
          <xs:extension base="mce:RestrictedTermType">
            <xs:attribute name="caseSensitive" type="xs:boolean" default="false"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="LocalizedStringsType">
        <xs:sequence>
          <xs:element name="Resource" type="mce:ResourceType" maxOccurs="unbounded">
            <xs:key name="UniqueLangCodeUsedInNamePerResource">
              <xs:selector xpath="mce:Name"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:key name="UniqueLangCodeUsedInDescriptionPerResource">
              <xs:selector xpath="mce:Description"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="ResourceType">
        <xs:sequence>
          <xs:element name="Name" type="mce:ResourceNameType" maxOccurs="unbounded"/>
          <xs:element name="Description" type="mce:DescriptionType" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="idRef" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="ResourceNameType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="DescriptionType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
    </xs:schema>
```

## Para obter mais informações

[Prevenção de perda de dados](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Definir seus próprios modelos de DLP e tipos de informações](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

