---
title: 'Personalizar tipos de informações confidenciais de DLP internos'
TOCTitle: Personalizar os tipos de informações confidenciais de DLP internos
ms:assetid: 3f8bf141-2e7c-4ea7-b102-dfd6c41539da
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn781122(v=EXCHG.150)
ms:contentKeyID: 62757539
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Personalizar os tipos de informações confidenciais de DLP internos

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-05-26_

Procurando por informações confidenciais em email, você precisará descrevem essas informações no que é chamado de uma *regra*. Prevenção de perda de dados (DLP) inclui um pacote de 51 regras para os tipos mais comuns de informações confidenciais que você pode usar imediatamente. Para usar essas regras, você precisará incluí-los em uma política. Você pode encontrar o que você deseja ajustar essas regras internas para atender às necessidades específicas da sua organização, e você pode fazer isso criando um tipo de informação confidencial personalizado. Este tópico mostra como personalizar um arquivo XML que contém o conjunto existente de regra para detectar uma grande variedade de informações de cartão de crédito potenciais.

Você pode executar este exemplo e aplicá-lo a outros tipos de informações confidenciais internas. Para uma lista dos tipos de informações confidenciais padrão e definições de XML, consulte o tópico [O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) .

Este tópico fornece orientações para as seções a seguir para personalizações de regra XML:

  - Exportar o XML de regras atuais

  - Localize a regra que você deseja modificar no XML

  - Modificar o XML e criar um novo tipo de informações confidenciais

  - Exigem menos a evidência adicional

  - Procurar por palavras-chave que são específicas para sua organização

  - Carregar sua regra

Para saber o que as diferentes partes de regras estão e o que eles, confira o Glossário de termos no final deste tópico.

## Exportar o arquivo XML das regras atuais

Para exportar o XML, você precisa usar o Shell de Gerenciamento do Exchange ou. Para Exchange Server 2013, consulte [Usando o PowerShell com o Exchange 2013 (Shell de gerenciamento do Exchange)](https://technet.microsoft.com/pt-br/library/bb123778\(v=exchg.150\)). Para Exchange Online, consulte [Conectar-se ao Exchange Online usando o PowerShell Remoto](https://technet.microsoft.com/pt-br/library/jj984289\(v=exchg.150\)).

1.  Na Shell de Gerenciamento do Exchange ou Exchange Online PowerShell, digite **Get-ClassificationRuleCollection** para exibir as regras da sua organização na tela. Se você não tiver criado suas próprias, você verá apenas o padrão, as regras internas, rotulada como "Pacote Microsoft Rule."

2.  Armazenar regras da sua organização em um em uma variável, digitando **$ruleCollections = Get-ClassificationRuleCollection**. Armazenando algo em uma variável disponibiliza facilmente posteriormente em um formato que funciona para comandos do PowerShell remotos.

3.  Fazer um arquivo XML formatado com todos esses dados digitando **Set-Content - caminho "C:\\custompath\\exportedRules.xml"-Encoding Byte-valor $ruleCollections.SerializedClassificationRuleCollection**. (**Set-content** é a parte do cmdlet que grava o XML no arquivo.)
    

    > [!IMPORTANT]
    > Certifique-se que você use o local de arquivo onde seu pacote de regra na verdade é armazenado. <STRONG>C:\custompath\</STRONG> é um espaço reservado.



## Localize a regra que você deseja modificar no XML

Os cmdlets acima exportados toda a *coleção de regras*, que inclui as regras 51 padrão que fornecemos. Em seguida, você precisará procure especificamente a regra número cartão de crédito que você deseja modificar.

1.  Use um editor de texto para abrir o arquivo XML que você exportou na seção anterior.

2.  Role para baixo até a marca de **\<Rules\>** , que é o início da seção que contém as regras DLP. (Como este arquivo XML contém as informações para o conjunto regra inteira, ele contém outras informações no topo que você precise rolar passado obter às regras.)

3.  Procure **Func\_credit\_card** localizar a definição de regra do número do cartão de crédito. (No XML, nomes de regra não podem conter espaços, para que os espaços geralmente são substituídos por sublinhados e nomes de regra às vezes são abreviados. Um exemplo disso é a regra de número de Seguridade Social de EUA, qual será abreviado "SSN." A regra número cartão de crédito XML deve parecer com o seguinte código de exemplo.
    
  ```powershell
  <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085"
          patternsProximity="300" recommendedConfidence="85">
        <Pattern confidenceLevel="85">
          <IdMatch idRef="Func_credit_card" />
          <Any minMatches="1">
            <Match idRef="Keyword_cc_verification" />
            <Match idRef="Keyword_cc_name" />
            <Match idRef="Func_expiration_date" />
          </Any>
        </Pattern>
      </Entity>
  ```

Agora que você tiver localizado a definição da regra de número de cartão de crédito no XML, você pode personalizar o XML da regra para atender suas necessidades. (Para um atualizador nas definições XML, consulte o Glossário de termos no final deste tópico.)

## Modificar o XML e crie um novo tipo de informações confidenciais

Primeiro, você precisa criar um novo tipo de informações confidenciais, porque você não pode modificar diretamente as regras padrão. Você pode fazer uma ampla variedade de coisas com tipos de informações confidenciais personalizadas, que são descritos nas [Desenvolver pacotes de regras de informações confidenciais](technical-description-of-xml-schema-for-dlp-rule-packages.md). Neste exemplo, vamos mantê-lo simples e apenas remover a evidência corroborativa e adicionar palavras-chave para a regra de número de cartão de crédito.

Todas as definições de regras XML são criadas no seguinte modelo geral. Você precisa para copiar e colar o XML de definição do número de cartão de crédito no modelo, modificar alguns valores (Observe "..." espaços reservados no exemplo a seguir) e, em seguida, carregue o XML modificado como uma nova regra que pode ser usada em políticas.

  ```xml
  <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id=". . .">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id=". . ." /> 
        <Details defaultLangCode=". . .">
          <LocalizedDetails langcode=" . . . ">
             <PublisherName>. . .</PublisherName>
             <Name>. . .</Name>
             <Description>. . .</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
       <!-- Paste the Credit Card Number rule definition here.--> 
    
          <LocalizedStrings>
             <Resource idRef=". . .">
               <Name default="true" langcode=" . . . ">. . .</Name>
               <Description default="true" langcode=". . ."> . . .</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>
  ```

Agora, você ter algo parecido com o XML a seguir. Como pacotes de regras e regras são identificadas por seus GUIDs exclusivos, você precisará gere dois GUIDs: uma para o pacote de regras e outra para substituir o GUID da regra número de cartão de crédito. (O GUID para a ID da entidade do exemplo de código a seguir é aquele para nossa definição de regra interna, é necessário substituir com um novo). Há várias maneiras para gerar GUIDs, mas você pode executá-la facilmente no PowerShell digitando **\[guid\]::NewGuid()**.

  ```xml
  <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id="8aac8390-e99f-4487-8d16-7f0cdee8defc">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id="8d34806e-cd65-4178-ba0e-5d7d712e5b66" />
        <Details defaultLangCode="en">
          <LocalizedDetails langcode="en">
            <PublisherName>Contoso Ltd.</PublisherName>
            <Name>Financial Information</Name>
            <Description>Modified versions of the Microsoft rule package</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f"
           patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    
          <LocalizedStrings>
             <Resource idRef="db80b3da-0056-436e-b0ca-1f4cf7080d1f"> 
    <!-- This is the GUID for the preceding Credit Card Number entity because the following text is for that Entity. -->
               <Name default="true" langcode="en-us">Modified Credit Card Number</Name>
               <Description default="true" langcode="en-us">Credit Card Number that looks for additional keywords, and another version of Credit Card Number that doesn't require keywords (but has a lower confidence level)</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>
  ```

## Remover a exigência de evidência corroborativa de um tipo de informações confidenciais

Agora que você tem um novo tipo de informações confidenciais que você está capaz de carregar ao seu ambiente de Exchange, a próxima etapa é tornar a regra mais específica. Modificar a regra para que ele procura apenas um número de 16 dígitos passa a soma de verificação, mas não exige a evidência adicional (corroborativa) (por exemplo, palavras-chave). Para fazer isso, você precisa remover a parte do XML que procura a evidência corroborativa. Evidência corroborativa é muito útil em reduzir os falsos positivos porque geralmente, há determinadas palavras-chave ou uma data de validade perto do número de cartão de crédito. Se você remover essa evidência, você também deve ajustar você tem certeza que você encontrou um número de cartão de crédito reduzindo o **confidenceLevel**, que é de 85 no exemplo.

  ```powershell
  <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="300"
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
          </Pattern>
        </Entity>
  ```

## Procurar por palavras-chave que são específicas para sua organização

Talvez você queira exigem a evidência corroborativa mas deseja diferente ou adicional de palavras-chave e talvez você queira alterar onde procurar por essa evidência. Você pode ajustar o **patternsProximity** para expandir ou reduzir a janela para a evidência corroborativa em torno do número de 16 dígitos. Para adicionar sua próprias palavras-chave, você precisará definir uma lista de palavra-chave e a referência a ele dentro de sua regra. O XML a seguir adiciona as palavras-chave "empresa cartão" e "Contoso cartão" para que qualquer mensagem que contém essas frases dentro de 150 caracteres de um número de cartão de crédito será identificada como um número de cartão de crédito.

  ```xml
  <Rules>
    <! -- Modify the patternsProximity to be "150" rather than "300." -->
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="150" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
    <!-- Add the following XML, which references the keywords at the end of the XML sample. -->
              <Match idRef="My_Additional_Keywords" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    <!-- Add the following XML, and update the information inside the <Term> tags with the keywords that you want to detect. -->
        <Keyword id="My_Additional_Keywords">
          <Group matchStyle="word">
            <Term caseSensitive="false">company card</Term>
            <Term caseSensitive="false">Contoso card</Term>
          </Group>
        </Keyword>
  ```

## Carregar sua regra

Para carregar sua regra, você precisará fazer o seguinte.

1.  Salvá-lo como um arquivo XML com a codificação Unicode. Isso é importante porque a regra não funcionará se o arquivo for salvo com uma codificação diferente.

2.  Conecte o PowerShell Shell de Gerenciamento do Exchange ou Exchange Online. Para Exchange Server 2013, consulte [Usando o PowerShell com o Exchange 2013 (Shell de gerenciamento do Exchange)](https://technet.microsoft.com/pt-br/library/bb123778\(v=exchg.150\)). Para Exchange Online, consulte [Conectar-se ao Exchange Online usando o PowerShell Remoto](https://technet.microsoft.com/pt-br/library/jj984289\(v=exchg.150\)).

3.  Na Shell de Gerenciamento do Exchange ou Exchange Online PowerShell, digite **New-ClassificationRuleCollection - FileData (Get-Content - caminho "C:\\custompath\\MyNewRulePack.xml"-Encoding Byte)**.
    

    > [!IMPORTANT]
    > Certifique-se de que você use o local do arquivo onde o seu pacote de regra realmente está armazenado. <STRONG>C:\custompath\</STRONG> é um espaço reservado.



4.  Confirmar, digite **Y** e pressione **Enter**.

5.  Verifique se que a nova regra foi carregada digitando o **Get-DataClassification**, que agora exibe o nome de sua regra.

Para começar a usar a nova regra para detectar informações confidenciais, você precisará adicionar a regra a uma política de DLP. Para saber como adicionar a regra a uma política, consulte [Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md).

## Glossário de termos

Essas são as definições para os termos que você encontrou durante esse procedimento.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Termo</th>
<th>Definição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Entidade</p></td>
<td><p>As entidades são o que chamamos de tipos de informações confidenciais, como números de cartão de crédito. Cada entidade possui um GUID exclusivo, como sua identificação. Se você copiar um GUID e pesquisar por ele no XML, você encontrará a definição de regra XML e todas as traduções localizadas desta regra de XML. Você também pode encontrar essa definição localizando o GUID para a conversão e, em seguida, procurando por esse GUID.</p></td>
</tr>
<tr class="even">
<td><p>Funções</p></td>
<td><p>O arquivo XML referencia <strong>Func_credit_card</strong>, que é uma função no código compilado. Funções são usadas para executar regexes complexa e verifique se correspondem somas de verificação para nossas regras internas.) Porque isso acontece no código, algumas das variáveis não aparecem no arquivo XML.</p></td>
</tr>
<tr class="odd">
<td><p>IdMatch</p></td>
<td><p>Isso é o identificador que o padrão deve se assemelhar — por exemplo, um número de cartão de crédito. Você pode ler mais sobre isso e as marcas de <strong>Match</strong> em <a href="technical-description-of-xml-schema-for-dlp-rule-packages.md">Entity rules</a>.</p></td>
</tr>
<tr class="even">
<td><p>Listas de palavra-chave</p></td>
<td><p>Arquivo XML também referencia <strong>keyword_cc_verification</strong> e <strong>keyword_cc_name</strong>, que são listas de palavras-chave da qual estamos buscando correspondências dentro do <strong>patternsProximity</strong> para a entidade. Eles não estejam sendo exibidos no XML.</p></td>
</tr>
<tr class="odd">
<td><p>Padrão</p></td>
<td><p>O padrão contém a lista do que o tipo confidencial está procurando. Isso inclui funções internas (que executem tarefas como verificação somas de verificação), regexes e palavras-chave. Tipos de informações confidenciais podem ter vários padrões com confidences exclusivos. Isso é útil ao criar um tipo de informação confidencial que retorna uma confiança alta se evidência corroborativa for encontrada e uma confiança inferior se pouca ou nenhuma evidência corroborativa for encontrada.</p></td>
</tr>
<tr class="even">
<td><p>ConfidenceLevel padrão</p></td>
<td><p>Este é o nível de confiança do mecanismo DLP encontrada uma correspondência. Este nível de confiança está associado com uma correspondência para o padrão se que sejam cumpridos os requisitos do padrão. Essa é a medida de confiança que devem ser considerados ao usar o transporte do Exchange (ETRs) de regras.</p></td>
</tr>
<tr class="odd">
<td><p>patternsProximity</p></td>
<td><p>Quando encontramos o que se parece com um padrão de número de cartão de crédito, <strong>patternsProximity</strong> é proximidade alternativa para esse número onde vamos ver para evidência corroborativa.</p></td>
</tr>
<tr class="even">
<td><p>recommendedConfidence</p></td>
<td><p>Este é o nível de confiança, que é recomendável para esta regra. A confiança recomendada se aplica a entidades e afinidades. Para entidades, esse número nunca é avaliado em relação a <strong>confidenceLevel</strong> padrão de. É apenas uma sugestão para ajudá-lo a escolher um nível de confiança, se você quiser aplicar um tema. Para afinidades, o <strong>confidenceLevel</strong> do padrão deve ser maior do que o número de <strong>recommendedConfidence</strong> para uma ação de ETR a ser chamado. A <strong>recommendedConfidence</strong> é o padrão nível de confiança usado em ETRs que chama uma ação. Se desejar, você pode alterar manualmente o ETR a ser chamado com base em nível de confiança do padrão, em vez disso.</p></td>
</tr>
</tbody>
</table>


## Para saber mais

  - [Como as regras DLP são aplicadas para avaliar mensagens](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/dlp-rule-application)

  - [Criar uma política DLP personalizada](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/create-custom-dlp-policy)

  - [O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

