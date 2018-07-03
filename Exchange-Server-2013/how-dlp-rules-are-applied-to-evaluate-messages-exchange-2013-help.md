---
title: 'Como as regras DLP são aplicadas para avaliar mensagens: Exchange 2013 Help'
TOCTitle: Como as regras DLP são aplicadas para avaliar mensagens
ms:assetid: 1ac77020-26ff-410c-ab09-4f28a99d67a1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn329050(v=EXCHG.150)
ms:contentKeyID: 56270488
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Como as regras DLP são aplicadas para avaliar mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Você pode configurar as regras de informações confidenciais em suas políticas de prevenção de perda de dados (DLP) do Microsoft Exchange para detectar dados muito específicos em mensagens de email. Esse tópico ajudará você a entender como essas regras são aplicadas e como as mensagens são avaliadas. Você pode evitar interrupções do fluxo de trabalho para seus usuários de email e conseguir um elevado grau de precisão com suas detecções de DLP se souber como as regras são impostas. Vamos usar a regra de informações do cartão de crédito fornecido pela Microsoft como exemplo. Quando você ativa uma regra de transporte ou política de DLP, o agente de regras de transporte do Exchange compara todas as mensagens que seus usuários enviam com os conjuntos de regras que você criar.

## Atenda às suas necessidades com precisão

Suponha que você precise agir de acordo com as informações de cartão de crédito nas mensagens. As ações que você adotar ao encontrar não são o assunto deste tópico, mas você pode saber mais sobre isso em [Email ações de regra de fluxo no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919237\(v=exchg.150\)). Com a maior certeza possível, você precisa assegurar que o que é detectado em uma mensagem são dados reais de cartão de crédito e não outra coisa que possa ser um uso legítimo de grupos de números que simplesmente lembram dados de cartão de crédito; por exemplo, um código de reserva ou um número de identificação de veículo. Para atender a essa necessidade, vamos deixar claro que as seguintes informações devem ser classificadas como um cartão de crédito.

**    Margie’s Travel,  
    recebi as informações atualizadas do cartão de crédito do Spencer.  
    Spencer Badillo  
    Visa: 4111 1111 1111 1111  
    Expira: 2/2012  
    Por favor, atualize o perfil de viagem dele.**

Também vamos deixar claro que as seguintes informações não devem ser classificadas como um cartão de crédito.

**    Olá Alex,  
    eu espero estar no Havaí também. Meu código de reserva é 1234 1234 1234 1234 e estarei lá em 3/2012.  
    Atenciosamente, Lisa**

O seguinte trecho em XML mostra como as necessidades expressas anteriormente são definidas atualmente em uma regra de informação confidencial que é fornecida com o Exchange e ela é incorporada em um dos modelos de política de DLP fornecidos.

    <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>

## Correspondência de padrões em sua solução

A definição da regra de XML mostrada anteriormente inclui a correspondência de padrões, que aumentam a probabilidade da regra de detectar informações importantes e não detectar informações vagas relacionadas. Para mais informações sobre o esquema XML para regras e modelos de DLP, consulte [Definir seus próprios modelos de DLP e tipos de informações](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

Na regra de cartão de crédito, existe uma seção de código XML para padrões, que inclui um identificador de correspondência principal e algumas evidências corroborativas adicionais. Todas essas três exigências são explicadas aqui:

1.  `<IdMatch idRef="Func_credit_card" />  ` — Exige uma correspondência de função, cartão de crédito com titularidade, definida internamente. Essa função inclui algumas validações:
    
    1.  Ela corresponde a uma expressão regular—nessa instância de 16 dígitos—que também poderia incluir variações como um delimitador de espaço para que ela também correspondesse a **4111 1111 1111 1111** ou um delimitador com hífen para que ela também correspondesse a **4111-1111-1111-1111**.
    
    2.  Ela avalia o algoritmo da soma de verificação da Lhun em relação ao número de 16 dígitos para assegurar que a probabilidade de ser um número de cartão de crédito é elevada.
    
    3.  Ela requer uma correspondência obrigatória, depois da qual a evidência corroborativa é avaliada.

2.  `<Any minMatches="1">  ` — Essa seção indica que a presença de pelo menos um dos seguintes itens de evidência é obrigatória.

3.  A evidência corroborativa pode ser uma correspondência de uma destas três:
    
    `<Match idRef="Keyword_cc_verification" />`
    
    `<Match idRef="Keyword_cc_name" />`
    
    `<Match idRef="Func_expiration_date" />`
    
    Essas três significam simplesmente que uma lista de palavras-chave para cartões de crédito, os nomes dos cartões de crédito ou uma data de expiração são necessários. A data de expiração é definida e avaliada internamente como outra função.

## O processo de avaliação de conteúdo em relação às regras

As cinco etapas aqui representam ações que o Exchange adota para comparar sua regra a mensagens de email. Para nosso exemplo de regra de cartão de crédito, as seguintes etapas são adotadas.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Etapa</th>
<th>Ação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1. Obter conteúdo</p></td>
<td><p>Badillo Silva</p>
<p>Visa: 4111 1111 1111 1111</p>
<p>Validade: 2/2012</p></td>
</tr>
<tr class="even">
<td><p>2. Análise de expressão regular</p></td>
<td><p>4111 1111 1111 1111 -&gt; um número de 16 dígitos foi detectado</p></td>
</tr>
<tr class="odd">
<td><p>3. Análise de função</p></td>
<td><ul>
<li><p>4111 1111 1111 1111 -&gt; corresponde à soma de verificação</p></li>
<li><p>1234 1234 1234 1234 -&gt; não corresponde</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>4. Evidência adicional</p></td>
<td><ol>
<li><p>A palavra-chave Visa está perto do número.</p></li>
<li><p>Uma expressão regular para uma data (2/2012) está perto do número.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>5. Conclusão</p></td>
<td><ol>
<li><p>Há uma expressão regular que corresponde a uma soma de verificação.</p></li>
<li><p>A evidência adicional aumenta a confiança.</p></li>
</ol>
<p></p></td>
</tr>
</tbody>
</table>


A forma como essa regra é configurada pela Microsoft torna obrigatória que a corroboração de evidências, como palavras-chave, faça parte do conteúdo da mensagem de email para corresponder à regra. Assim, o seguinte conteúdo de email não seria detectado como contendo um cartão de crédito:

**    Margie’s Travel,  
    recebi as informações atualizadas do Spencer.  
    Spencer Badillo  
    4111 1111 1111 1111  
    Por favor, atualize o perfil de viagem dele.**

Você pode usar uma regra personalizada que define um padrão sem evidências extras, conforme é apresentado no exemplo a seguir. Ela só detectaria mensagens com números de cartões de crédito e nenhuma evidência corroborativa.

``` 
      <Pattern confidenceLevel="85">
         <IdMatch idRef="Func_credit_card" />
      </Pattern>
    </Entity>
```

A ilustração de cartões de crédito neste artigo também pode se aplicar a outras regras de informações confidenciais. Para ver uma lista completa de regras fornecidas pela Microsoft no Exchange, use o cmdlet [Get-ClassificationRuleCollection](https://technet.microsoft.com/pt-br/library/jj218696\(v=exchg.150\)) no Shell de Gerenciamento do Exchange da seguinte forma:

    $rule_collection = Get-ClassificationRuleCollection

    $rule_collection[0].SerializedClassificationRuleCollection | Set-Content oob_classifications.xml -Encoding byte

## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\))

[Usando o PowerShell com o Exchange 2013 (Shell de gerenciamento do Exchange)](https://technet.microsoft.com/pt-br/library/bb123778\(v=exchg.150\))

[PowerShell do Exchange Online](https://technet.microsoft.com/pt-br/library/jj200677\(v=exchg.150\))

