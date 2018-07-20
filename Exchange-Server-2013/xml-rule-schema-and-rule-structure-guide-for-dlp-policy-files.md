---
title: 'Desenvolver arquivos de modelo de política de DLP: Exchange 2013 Help'
TOCTitle: Desenvolver arquivos de modelo de política de DLP
ms:assetid: 4b263547-aef4-4ee8-aa4f-fa64a5863189
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ674703(v=EXCHG.150)
ms:contentKeyID: 50485541
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desenvolver arquivos de modelo de política de DLP

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Esta visão geral explica os componentes de uma definição de esquema XML para arquivos de modelo de política de prevenção de perda de dados (DLP) e também oferece um arquivo de política de exemplo do formato XML. Ela será útil para compreender a arquitetura DLP geral e o processo de desenvolvimento de regras, antes de você começar. Para obter mais informações, consulte [Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) e [Definir seus próprios modelos de DLP e tipos de informações](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

Para tornar as soluções de prevenção de perda de dados fáceis de adotar e gerenciar, um modelo conceitual conhecido como políticas DLP e modelos de política é apresentado no Microsoft Exchange Server 2013. Modelos de política de DLP fornecem um design preliminar para a sua política de DLP pretendida. Para ter valor, um modelo de política de DLP deve encapsular todas as diretivas e objetos de dados que são necessários para atender a um objetivo de política específico, como uma regulamentação ou uma necessidade de negócios. O modelo não é específico para o ambiente. Ele é simplesmente uma definição ou modelo de uma política que pode ser fornecida como parte da configuração do produto ou fornecido por fornecedores de parceiros de software independentes. As políticas DLP, por outro lado, são instanciações dos modelos que são específicos para o ambiente de implantação. A sua estrutura de política de mensagens existente pode incorporar políticas DLP através do uso de regras de transporte. As regras de transporte oferecem grande flexibilidade para adaptar e expressar a riqueza das suas soluções DLP.

## Estrutura e fontes de modelo de política

Modelos de política de DLP são normalmente influenciados por várias fontes, como diretivas de processamento baseadas em servidor, políticas de computador cliente ou outras construções, conforme a imagem a seguir:

![Fatores que influenciam modelos de política](images/JJ674703.12f48e4f-d7b8-4ddd-87e8-8477983252ec(EXCHG.150).gif "Fatores que influenciam modelos de política")

Operações de gerenciamento simples estão disponíveis para modelos de política de DLP através tanto do Shell de Gerenciamento do Exchange quanto de interfaces baseadas na Internet, como o Centro de Administração do Exchange, incluindo capacidades de Importação, Exportação, Exclusão e Consulta. Uma política de DLP é criada fazendo referência a um modelo de política de DLP como parte do processo de criação. Esses modelos de política de DLP referenciados podem ser referências para os modelos instalados no sistema, que são armazenados nos Serviços de Domínio Active Directory, ou podem ser especificados como entrada diretamente de políticas fornecidas externamente.

Modelos de políticas de DLP são representados como documentos XML. Um único esquema XML é usado para políticas fornecidas dentro do Exchange e também externamente. A estrutura conceitual do documento XML é representada na tabela abaixo, que mostra os principais elementos. O conjunto de definições de componente de política ajuda você a atingir um objetivo de política específico, como uma regulamentação ou necessidade de negócios.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento Estrutural</th>
<th>Significado ou Exemplo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Editor</p></td>
<td><p>Microsoft ou Parceiro</p></td>
</tr>
<tr class="even">
<td><p>Versão</p></td>
<td><p>15.0.1.0</p></td>
</tr>
<tr class="odd">
<td><p>Nome da Diretiva</p></td>
<td><p>PCI-DSS</p></td>
</tr>
<tr class="even">
<td><p>Descrição</p></td>
<td><p>A política de DLP PCI-DSS ajuda a detectar a presença de informações sujeitos a segurança padrão de dados PCI (PCI DSS), incluindo informações sobre como o cartão de crédito ou números de cartão de débito. O uso dessa diretiva não garanta a conformidade com qualquer regulamentação. Depois que o teste for concluído, faça as alterações de configuração necessárias no Exchange para a transmissão de informações cumpre diretivas da sua organização. Exemplos incluem configurar TLS com parceiros comerciais conhecidos ou adicionar mais restritivas ações de regra de transporte, como a adição de proteção de direitos às mensagens que contêm este tipo de dados.</p></td>
</tr>
<tr class="odd">
<td><p>Metadados</p></td>
<td><p>Marcas para descrever o regulamento local, país ou região, palavras-chave e muito mais.</p></td>
</tr>
<tr class="even">
<td><p>Conjunto de construções de política</p></td>
<td><ol>
<li><p>Definições de regra de transporte, tais como condições e ações.</p></li>
<li><p>Definições de comportamento do cliente de email que controlam a experiência do cliente por meio de notificações interativas.</p></li>
<li><p>Opcionalmente, referências de configuração que precisam ser coordenadas com as configurações específicas do ambiente de cliente.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Conjunto de classificações de dados</p></td>
<td><ol>
<li><p>Especifica as entidades de classificação ou afinidades.</p></li>
<li><p>Entidades têm contagem e confiança; afinidades só tem uma confiança.</p></li>
<li><p>Vem com seu próprio conjunto de propriedades e esquema de classificação.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## Definição de formato do modelo de política

Modelos de política de DLP são expressos em documentos XML que respeitam o esquema a seguir. Observe que o XML diferencia maiúsculas e minúsculas. Por exemplo, `dlpPolicyTemplates` funcionará, mas `DlpPolicyTemplates` não.

    <?xml version="1.0" encoding="UTF-8"?>
    <dlpPolicyTemplates>
      <dlpPolicyTemplate id="F7C29AEC-A52D-4502-9670-141424A83FAB" mode="Audit" state="Enabled" version="15.0.2.0">
        <contentVersion>4</contentVersion>
        <publisherName>Microsoft</publisherName>
        <name>
          <localizedString lang="en">PCI-DSS</localizedString>
        </name>
        <description>
          <localizedString lang="en">Detects the presence of information subject to Payment Card Industry Data Security Standard (PCI-DSS) compliance requirements.</localizedString>
        </description>
        <keywords></keywords>
        <ruleParameters></ruleParameters>
        <ruleParameters/>
        <policyCommands>
          <!-- The contents below are applied/executed as rules directly in PS - -->
          <commandBlock>
            <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP Policy."]]>
          </commandBlock>
          <commandBlock>
            <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "%%DlpPolicyName%%" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP Policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]>
          </commandBlock>
        </policyCommands>
        <policyCommandsResources></policyCommandsResources>
      </dlpPolicyTemplate>
    </dlpPolicyTemplates>

Se um parâmetro incluído em seu arquivo XML para qualquer elemento incluir um espaço, ele deverá estar entre aspas duplas ou não funcionará adequadamente. No exemplo abaixo, o parâmetro que segue `-SentToScope` é aceitável e não inclui aspas duplas porque é uma cadeia de caracteres contínua sem um espaço. Entretanto, o parâmetro fornecido para –`Comments` não aparecerá no Centro de administração do Exchange porque não há aspas duplas e ele inclui espaços.

    <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments Monitors payment card information sent inside the organization -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>

## Elemento localizedString

O formato de modelo oferece a capacidade de localizar cadeias de caracteres no domínio que podem ser apresentadas ao usuário final, por exemplo, como parte da seleção de que modelos de política DLP são instalados. O elemento localizedString pode ser usado para fornecer várias definições para os campos Nome e Descrição.

## Nó ruleParameters

Esse é um conjunto opcional de parâmetros que precisam ser fornecidos durante a fase de instanciação do modelo, ao se criar uma política de DLP a ser mapeada para objetos específicos de implantação. Por exemplo, um grupo de distribuição real que está disponível na implantação.

## Elemento dlpPolicyTemplate

Esse é o elemento raiz para o modelo de política de DLP e é necessário para cada modelo. Os atributos disponíveis são mostrados na tabela a seguir:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do Atributo</th>
<th>Obrigatório?</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Versão</p></td>
<td><p>Sim</p></td>
<td><p>O número de versão usado neste documento de modelo de política de DLP.</p></td>
</tr>
<tr class="even">
<td><p>State</p></td>
<td><p>Não</p></td>
<td><p>A configuração padrão opcional para o estado da política.</p></td>
</tr>
<tr class="odd">
<td><p>Modo</p></td>
<td><p>Não</p></td>
<td><p>A configuração padrão opcional para o modo da política.</p></td>
</tr>
<tr class="even">
<td><p>Id</p></td>
<td><p>Não</p></td>
<td><p>Um GUID para identificar exclusivamente essa definição de modelo de política de DLP no seguinte formato: &quot;A29C69BF-4F98-47F1-9A99-5771DFD2C27F&quot;.</p></td>
</tr>
</tbody>
</table>


Elementos filho incluem a seguinte sequência de elementos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento filho</th>
<th>(mínimo, máximo)</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PublisherName</p></td>
<td><p>(1, 1)</p></td>
<td><p>Metadados para o editor do modelo</p></td>
</tr>
<tr class="even">
<td><p>Nome</p></td>
<td><p>(1, 1)</p></td>
<td><p>Nome localizável para esse modelo.</p></td>
</tr>
<tr class="odd">
<td><p>Descrição</p></td>
<td><p>(1, 1)</p></td>
<td><p>Descrição localizável para esse modelo.</p></td>
</tr>
<tr class="even">
<td><p>Palavras-chave</p></td>
<td><p>(1, 1)</p></td>
<td><p>Lista de palavras-chave que se aplica a esse modelo. Um modelo pode ter uma lista vazia de palavras-chave.</p></td>
</tr>
<tr class="odd">
<td><p>RuleParameters</p></td>
<td><p>(0, 1)</p></td>
<td><p>Lista de parâmetros de modelo que usada na definição de política.</p></td>
</tr>
<tr class="even">
<td><p>PolicyCommands</p></td>
<td><p>(0, 1)</p></td>
<td><p>Lista de definições de regra de transporte para essa política. Esse é um elemento opcional.</p></td>
</tr>
</tbody>
</table>


## Modelo de Política de DLP: PolicyCommands

Essa parte do modelo de política contém a lista de comandos do Shell de Gerenciamento do Exchange que são usados para instanciar a definição de política. O processo de importação irá executar cada um dos comandos, como parte do processo de instanciação. Comandos de política de exemplo são fornecidos aqui.

    <PolicyCommands>
        <!-- The contents below are applied/executed as rules directly in PS - -->
          <CommandBlock> <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "PCI-DSS" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP policy."]]></CommandBlock>
          <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
      </PolicyCommands> 

O formato dos cmdlets é a sintaxe padrão dos cmdlets do Shell de Gerenciamento do Exchange para os cmdlets usados. Os comandos são executados em sequência. É possível, para cada nó de comando, que ele contenha um bloco de scripts que devem ser compostos de vários comandos. Veja a seguir um exemplo que ilustra como inserir um pacote de regras de classificação dentro de um modelo de política de DLP e instalar esse pacote de regras como parte do processo de criação de políticas. O pacote de regras de classificação é inserido no modelo da política e passado como um parâmetro para o cmdlet no modelo:

``` 
<CommandBlock>
  <![CDATA[
$rulePack = [system.Text.Encoding]::Unicode.GetBytes('<?xml version="1.0" encoding="utf-16"?>
<rulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">

  <RulePack id="c3f021a3-c265-4dc2-b3a7-41a1800bf518">
    <Version major="1" minor="0" build="0" revision="0"/>
    <Publisher id="e17451d3-9648-4117-a0b1-493a6d5c73ad"/>
    <Details defaultLangCode="en-us">
      <LocalizedDetails langcode="en-us">
        <PublisherName>Contoso</PublisherName>
        <Name>Contoso Sample Rule Pack</Name>
        <Description>This is a sample rule package</Description>
      </LocalizedDetails>
    </Details>
  </RulePack>

  <Rules>
    <Entity id="7cc35258-6b35-4415-baff-a76d1a018980" patternsProximity="300" recommendedConfidence="85" workload="Exchange">     

      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_Contoso" />
        <Any minMatches="1">
          <Match idRef="Regex_conf" />
        </Any>
      </Pattern>
    </Entity>

    <Regex id="Regex_Contoso">(?i)(\bContoso\b)</Regex>
    <Regex id="Regex_conf">(?i)(\bConfidential\b)</Regex>

    <LocalizedStrings>
      <Resource idRef="7cc35258-6b35-4415-baff-a76d1a018980">
        <Name default="true" langcode="en-us">
          Confidential Information Rule
        </Name>
        <Description default="true" langcode="en-us">
          Sample rule pack - Detects Contoso confidential information
        </Description>
      </Resource>
    </LocalizedStrings>
  </Rules>

</RulePackage>

')


New-ClassificationRuleCollection -FileData $rulePack 
New-TransportRule -name "customEntity" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -MessageContainsDataClassifications @{Name="Confidential Information Rule"} -SetAuditSeverity High]]>
</CommandBlock> 
```

Elementos filho incluem a seguinte sequência ordenada de elementos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento Filho</th>
<th>(Mínimo, Máximo)</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CommandBlock</p></td>
<td><p>(1, n)</p></td>
<td><p>Um bloco de comando que é executado no PowerShell. Cada bloco de comando é executado em sequência.</p></td>
</tr>
</tbody>
</table>


## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Definir seus próprios modelos de DLP e tipos de informações](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[Importar um modelo de política DLP personalizado de um arquivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

