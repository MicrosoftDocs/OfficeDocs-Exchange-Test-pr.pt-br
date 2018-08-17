---
title: 'Noções básicas sobre filtros do escopo de função de gerenciamento'
TOCTitle: Noções básicas sobre filtros do escopo de função de gerenciamento
ms:assetid: 6acc2922-ee9c-41f1-8a0f-10a541e8c273
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298043(v=EXCHG.150)
ms:contentKeyID: 50485772
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Noções básicas sobre filtros do escopo de função de gerenciamento

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Os filtros de escopo de função de gerenciamento podem ser usados para definir os escopos de gerenciamento que são altamente personalizáveis. Usando filtros de escopo, você pode criar um escopo que corresponda a como você segmenta seus destinatários, bancos de dados e servidores, de modo que os administradores possam gerenciar somente os objetos a que eles devem ter acesso. Os filtros de escopo podem usar praticamente qualquer propriedade de objeto de destinatário, banco de dados ou servidor.

Para usar os filtros de escopo de função de gerenciamento, você deve conhecer os escopos de função de gerenciamento. Para mais informações sobre escopos da função de gerenciamento, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Escopos personalizados filtrados no Microsoft Exchange Server 2013 são criados usando o cmdlet **New-ManagementScope**. Os dois tipos de escopos filtrados, destinatário e configuração (que consiste em escopos de banco de dados e servidor) são divididos em escopos regulares e exclusivos. A lista a seguir mostra que parâmetro usar no cmdlet **New-ManagementScope** para criar cada tipo de escopo filtrado:

  - **Escopo filtrado regular de destinatário**   Para criar esse tipo de escopo filtrado, use o parâmetro *RecipientRestrictionFilter*.

  - **Escopo filtrado exclusivo de destinatário**   Para criar esse tipo de escopo filtrado, use o parâmetro *RecipientRestrictionFilter* com a opção *Exclusive*.

  - **Escopo filtrado regular de configuração baseado em servidor**   Para criar esse tipo de escopo filtrado, use o parâmetro *ServerRestrictionFilter*.

  - **Escopo filtrado exclusivo de configuração baseado em servidor**   Para criar esse tipo de escopo filtrado, use o parâmetro *ServerRestrictionFilter* com a opção *Exclusive*.

  - **Escopo filtrado regular de configuração baseado em banco de dados**   Para criar esse tipo de escopo filtrado, use o parâmetro *DatabaseRestrictionFilter*.

  - **Escopo filtrado exclusivo de configuração baseado em banco de dados**   Para criar esse tipo de escopo filtrado, use o parâmetro *DatabaseRestrictionFilter* com a opção *Exclusive*.

Quando você cria um escopo filtrado personalizado, ele tenta combinar o filtro com quaisquer outros objetos acessíveis dentro do escopo de leitura implícito da função de gerenciamento. Se um objeto for encontrado, será incluído nos resultados retornados pelo filtro e será disponibilizado para a função de gerenciamento pelo escopo personalizado. Um filtro não pode retornar resultados fora do escopo de leitura implícito da função de gerenciamento.

Se você especificar um filtro de destinatário usando o parâmetro *RecipientRestrictionFilter*, poderá usar o parâmetro *RecipientRoot* para especificar uma unidade organizacional (OU) para a qual restringir o filtro. Quando você especifica uma OU no parâmetro *RecipientRoot*, o filtro de destinatário tenta combinar os destinatários que residem apenas naquela OU e não dentro de todo o escopo de leitura implícito.

Para criar um escopo de gerenciamento usando as propriedades que podem ser filtradas incluídas neste tópico, consulte [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

## Sintaxe do filtro

Os filtros de destinatário e configuração usam a mesma sintaxe para criar uma consulta de filtro. Todas as consultas de filtro devem ter, no mínimo, os seguintes componentes:

  - **Chave de abertura**   A chave de abertura ({) indica o início da consulta de filtro.

  - **Propriedade a examinar**   A propriedade é o valor de um objeto que você deseja testar. Por exemplo, pode ser a cidade ou o departamento em um objeto de destinatário, um nome de site ou nome de servidor do Active Directory em um objeto de configuração de servidor ou um nome de banco de dados em um objeto de configuração de banco de dados.

  - **Operador de comparação**   O operador de comparação mostra como a consulta deve avaliar o valor que você especifica em relação ao valor armazenado na propriedade. Por exemplo, os operadores de comparação podem ser **Eq**, que significa "igual a"; **Ne**, que significa "diferente de"; ou **Like**, que significa "similar a" e assim por diante. Para uma lista completa dos operadores que você pode usar no Shell de Gerenciamento do Exchange, consulte [Operadores de comparação](https://technet.microsoft.com/pt-br/library/bb125229\(v=exchg.150\)).

  - **Valor a comparar**   O valor que você especificar na consulta de filtro será comparado ao valor armazenado na propriedade que você especificou. O valor especificado deve ser colocado entre aspas (""). Se você quiser especificar uma cadeia de caracteres parcial, você pode colocá-la entre caracteres-curinga (\*) e usar um operador de comparação que suporte curingas, como o **Like**. Qualquer cadeia de caracteres que contenha a sequência parcial corresponderá à consulta de filtro.

  - **Chave de fechamento**   A chave de fechamento (}) indica o final da consulta de filtro.

Estes componentes são opcionais e permitem que você crie consultas de filtro mais complexas:

  - **Parênteses**   Como na matemática, os parênteses, ( ) permitem que você defina a ordem em que uma operação ocorre numa consulta de filtro. Os parênteses mais internos são avaliados primeiro, e a consulta prossegue em direção aos parênteses mais externos.

  - **Operadores lógicos**   Os operadores lógicos ligam uma ou mais operações de comparação e exigem que a consulta de filtro avalie a instrução toda. Alguns exemplos de operadores lógicos são **And**, **Or** e **Not**.

Completa, uma consulta simples é semelhante a `{ City -Eq "Vancouver" }`. Esse filtro pega qualquer destinatário que tenha o valor da propriedade **City** igual à cadeia de caracteres "Vancouver".

Uma consulta mais complexa seria `{ ((City -Eq "Vancouver") -And (Department -Eq "Sales")) -Or (Title -Like "*Manager*") }`. A consulta de filtro é avaliada na seguinte ordem:

1.  As propriedades **City** e **Department** são avaliadas. Cada uma delas é definida para `True` ou `False`, dependendo dos valores armazenados em cada propriedade.

2.  Os resultados das instruções **City** e **Department** são avaliados. Se ambos forem `True`, toda a instrução **And** se tornará `True`. Se um ou ambos forem `False`, toda a instrução **And** se tornará `False`. O seguinte se aplica:
    
      - Se a instrução **And** for avaliada como `True`, toda a consulta de filtro se tornará `True`, porque o operador **Or** indica que um lado da consulta ou o outro deve ser `True`. O objeto é exposto à atribuição de função.
    
      - Se a instrução **And** for `False`, a consulta de filtro continuará, avaliando a propriedade **Title**.

3.  A propriedade **Title**, em seguida, é avaliada. Ela será definida para `True` ou `False`, dependendo do valor armazenado na propriedade **Title**. O seguinte se aplica:
    
      - Se a propriedade **Title** for avaliada como `True`, toda a consulta de filtro se tornará `True`, porque o operador **Or** indica que um lado da consulta ou o outro deve ser `True`. O objeto é exposto à atribuição de função.
    
      - Se a propriedade **Title** for avaliada como `False`, toda a consulta de filtro será avaliada como `False` e o objeto não será exposto à atribuição de função.

A tabela a seguir mostra um exemplo com valores, indicando quando a consulta complexa seria avaliada como `True` e quando seria como `False`.

### Consulta complexa

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>City</th>
<th>Department</th>
<th>Title</th>
<th>Resultado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Sales (True)</p></td>
<td><p>CEO (False)</p></td>
<td><p>True porque tanto <strong>City</strong> quanto <strong>Department</strong> foram avaliadas como True. <strong>Title</strong> não é avaliada porque as condições de consulta de filtro já foram atendidas.</p></td>
</tr>
<tr class="even">
<td><p>Seattle (False)</p></td>
<td><p>Sales (True)</p></td>
<td><p>IT Manager (True)</p></td>
<td><p>True porque <strong>Title</strong> foi avaliado como True. Os resultados da comparação entre <strong>City</strong> e <strong>Department</strong> são descartados porque <strong>Title</strong> foi avaliado como True, o que satisfez as condições da consulta de filtro.</p>

> [!NOTE]  
> "IT Manager" corresponde à consulta de filtro porque o operador de comparação <STRONG>Like</STRONG> foi usado, o que corresponde às cadeias de caracteres parciais, quando caracteres-curinga (*) são usados na consulta de filtro.


</td>
</tr>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Marketing (False)</p></td>
<td><p>Writer (False)</p></td>
<td><p>False porque <strong>City</strong> e <strong>Department</strong> não foram avaliados como True, e <strong>Title</strong> também não foi avaliado como True.</p></td>
</tr>
</tbody>
</table>


## Propriedades de destinatário que podem ser filtradas

Você pode usar praticamente qualquer propriedade em um objeto destinatário, quando você cria um filtro de destinatário. Para uma lista das propriedades de destinatário filtráveis, consulte [Propriedades filtráveis para o parâmetro - RecipientFilter](https://technet.microsoft.com/pt-br/library/bb738157\(v=exchg.150\)). Apesar de este tópico discutir as propriedades que podem ser usadas com o parâmetro *RecipientFilter* em outros cmdlets, a maioria dessas propriedades também funciona com o parâmetro *RecipientRestrictionFilter* no cmdlet **New-ManagementScope**.

## Propriedades de servidor que podem ser filtradas

Você pode usar as seguintes propriedades de servidor, quando cria um escopo de gerenciamento com o parâmetro *ServerRestrictionFilter*:

  - **CurrentServerRole**

  - **CustomerFeedbackEnabled**

  - **DataPath**

  - **DistinguishedName**

  - **ExchangeLegacyDN**

  - **ExchangeLegacyServerRole**

  - **ExchangeVersion**

  - **Fqdn**

  - **Guid**

  - **InternetWebProxy**

  - **Name**

  - **NetworkAddress**

  - **ObjectCategory**

  - **ObjectClass**

  - **ProductID**

  - **ServerRole**

  - **ServerSite**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

## Propriedades de banco de dados que podem ser filtradas

Você pode usar as seguintes propriedades de banco de dados ao criar um escopo de gerenciamento com o parâmetro *DatabaseRestrictionFilter*:

  - **AdminDisplayName**

  - **AllowFileRestore**

  - **BackgroundDatabaseMaintenance**

  - **CircularLoggingEnabled**

  - **DatabaseCreated**

  - **DeletedItemRetention**

  - **Description**

  - **DistinguishedName**

  - **EdbFilePath**

  - **EventHistoryRetentionPeriod**

  - **ExchangeLegacyDN**

  - **ExchangeVersion**

  - **Guid**

  - **IssueWarningQuota**

  - **LogFilePrefix**

  - **LogFileSize**

  - **LogFolderPath**

  - **MasterServerOrAvailabilityGroup**

  - **MountAtStartup**

  - **Name**

  - **ObjectCategory**

  - **ObjectClass**

  - **RetainDeletedItemsUntilBackup**

  - **Server**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

