---
title: 'Agentes de extensão de cmdlet: Exchange 2013 Help'
TOCTitle: Agentes de extensão de cmdlet
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50556134
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agentes de extensão de cmdlet

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Agentes de extensão de cmdlet são componentes do Microsoft Exchange Server 2013 invocados pelos cmdlets do Exchange 2013 quando os cmdlets são executados. Como o nome sugere, os agentes de extensão de cmdlet estendem as capacidades dos cmdlets que os invocam, auxiliando no processamento de dados ou realizando ações adicionais com base nas exigências do cmdlet. Agentes de extensão de cmdlet estão disponíveis em qualquer função de servidor.

Os agentes podem modificar, substituir ou estender a funcionalidade de cmdlets do Shell de Gerenciamento do Exchange. Um agente pode fornecer um valor para um parâmetro exigido que não seja fornecido em um comando, substituir um valor fornecido por um usuário, realizar outras ações externas ao fluxo de trabalho do cmdlet enquanto um cmdlet é executado e mais.

Por exemplo, o cmdlet **New-Mailbox** aceita o parâmetro *Database* que especifica o banco de dados de caixa de correio no qual será criada uma nova caixa de correio. No Microsoft Exchange Server 2007, se você não especificar o parâmetro *Database* ao executar o cmdlet **New-Mailbox**, o comando falhará. No entanto, com o Exchange 2013, o cmdlet **New-Mailbox** invoca o agente `Mailbox Resources Management` quando o cmdlet é executado. Se o parâmetro *Database* não for especificado, o agente `Mailbox Resources Management` determinará automaticamente um banco de dados de caixa de correio adequado para a criação da nova caixa de correio e irá inserir esse valor no parâmetro *Database*.

Os agentes de extensão de cmdlet somente podem ser invocados pelos cmdlets do Exchange 2013 e do Microsoft Exchange Server 2010. Exchange 2007 Os cmdlets e cmdlets fornecidos por outros produtos da Microsoft e de terceiros não invocam os agentes de extensão de cmdlet. Os scripts também não podem invocar agentes de extensão de cmdlet diretamente. Entretanto, se os scripts contiverem cmdlets do Exchange 2013, aqueles cmdlets continuarão chamando os agentes de extensão de cmdlet.

Procurando tarefas de gerenciamento relacionadas a agentes de extensão de cmdlet? Consulte [Gerenciar agentes de extensão de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Prioridade do agente

A prioridade de um agente determina a ordem em que o agente é invocado quando um cmdlet é executado. Agentes de maior prioridade, próxima a zero, são invocados primeiro. A prioridade de um agente se torna importante quando dois ou mais agentes tentam definir o valor da mesma propriedade. O agente de maior prioridade a tentar definir um valor de propriedade será bem-sucedido, e todas as tentativas subsequentes de definir a mesma propriedade por agentes de menor prioridade são ignoradas. Por exemplo, se a propriedade **Name** em um objeto for modificada por um agente com prioridade três e outro agente com prioridade seis modificar o mesmo objeto, a modificação feita pelo agente com a prioridade seis será ignorada.

Se quiser que usar o `Scripting agent` para definir o valor de propriedades que possam ser definidas por outros agentes de maior prioridade, você terá as seguintes opções:

  - Desabilitar o agente que define a propriedade no momento.

  - Definir o `Scripting agent` com uma prioridade maior do que a do agente existente que você deseja substituir.

  - Manter as prioridades dos agente iguais e certificar-se de que o script executado sob o `Scripting agent` respeite o valor fornecido pelos outros agentes.


> [!WARNING]
> Alterar a prioridade ou substituir a funcionalidade de uma agente integrado é uma operação avançada. Certifique-se de ter entendido completamente as alterações que está realizando.



Para mais informações sobre a alteração da prioridade de um agente, consulte [Gerenciar agentes de extensão de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Agentes de transporte internos

Exchange 2013 inclui vários agentes que podem ser invocados quando um cmdlet é executado. A tabela a seguir lista os agentes, sua ordem e se os agentes estão habilitados por padrão. Não é possível adicionar ou remover agentes de um servidor que executa o Exchange 2013. No entanto, você pode usar o `Scripting agent` para executar os scripts do Windows PowerShell para estender a funcionalidade dos cmdlets que o usam. Para obter mais informações sobre `Scripting agent`, consulte a seção "Agente de script" posteriormente neste tópico.

É possível habilitar ou desabilitar a maioria dos agentes ou alterar a prioridade dos agentes se você quiser substituir a funcionalidade de um agente em particular pela que você fornecer em um script personalizado que possa chamar usando o `Scripting agent`. No entanto, alguns agentes não podem ser desativados. Os agentes que não podem ser desabilitados são chamados de *agentes do sistema* e têm sua propriedade *IsSystem* definida como `$True`. A tabela a seguir fornece informações sobre agentes de extensão de cmdlet do Exchange 2013, incluindo agentes do sistema.

A configuração para agentes é armazenada no nível da organização. Quando você ativa ou desativa um agente, ou quando determina sua prioridade, você define a configuração daquele agente em todos os servidores da organização. A exceção é adicionar scripts ao `Scripting agent`. Você deve atualizar os scripts em cada servidor individualmente. Para obter mais informações sobre como configurar scripts para usar com o `Scripting agent`, consulte a seção "Agente de script" posteriormente neste tópico.


> [!WARNING]
> Alterar a prioridade de agentes, ou habilitar e desabilitar agentes, pode causar efeitos indesejados se você não compreender completamente o que cada agente faz e como eles interagem com os cmdlets do Exchange. Antes de alterar a configuração de um agente, certifique-se de compreender totalmente as alterações e os resultados que deseja, e de verificar se o script personalizado irá funcionar conforme o pretendido.



### Agentes de extensão de cmdlet do Exchange 2013

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do Agente</th>
<th>Prioridade</th>
<th>Habilitado por padrão</th>
<th>Agente de sistema</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>Verdadeiro</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>Falso</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>Verdadeiro</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>Verdadeiro</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>Verdadeiro</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>Verdadeiro</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>Verdadeiro</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>Verdadeiro</p></td>
<td><p>Não</p></td>
</tr>
</tbody>
</table>


## Agente de script

Você pode usar o agente de extensão de cmdlet `Scripting agent` do Exchange 2013 para inserir sua própria lógica de scripts na execução dos cmdlets do Exchange. Ao usar o `Scripting agent`, você pode adicionar condições, substituir valores e configurar relatórios.


> [!WARNING]
> Quando você habilita o agente de extensão do cmdlet <CODE>Scripting agent</CODE>, o agente é invocado sempre que um cmdlet é executado em um servidor em execução no Exchange 2013. Isso inclui não só os cmdlets executados diretamente por você no Shell de Gerenciamento do Exchange, mas também os cmdlets executados pelos serviços do Exchange e o Centro de Administração do Exchange (EAC). É altamente recomendado testar seus scripts e todas as alterações efetuadas no arquivo de configuração, antes de copiar seu arquivo de configuração atualizado para os servidores do Exchange 2013 e habilitar o agente de extensão do cmdlet do <CODE>Scripting agent</CODE>.



Toda vez que um cmdlet do Exchange é executado, o cmdlet invoca o agente de extensão do cmdlet do `Scripting agent`. Quando esse agente é chamado, o cmdlet verifica se algum script está configurado para ser invocado por ele. Caso um script deva ser executado para um cmdlet, este tentará invocar todas as APIs definidas no script. As seguintes APIs estão disponíveis e são invocadas na seguinte ordem:

1.  **ProvisionDefaultProperties**   Essa API pode ser usada para definir os valores das propriedades em objetos quando elas são criadas. Quando um valor é definido, esse valor é retornado ao cmdlet e o cmdlet define o valor na propriedade. Você pode preencher os valores nas propriedades se o usuário não tiver especificado um valor ou substituir o valor especificado pelo usuário. Essa API respeita os valores definidos pelos agentes de prioridade mais alta. O agente de extensão do cmdlet do `Scripting agent` não substituirá os valores definidos por agentes de prioridade mais alta.

2.  **UpdateAffectedIConfigurable**   Essa API pode ser usada para definir valores de propriedades em objetos após todos os outros processamentos terem sido concluídos, mas a API `Validate` não tinha ainda sido invocada. Essa API respeita os valores definidos pelos agentes de prioridade mais alta. O agente de extensão do cmdlet do `Scripting agent` não substituirá os valores definidos por agentes de prioridade mais alta.

3.  **Validate**   Essa API pode ser usada para validar os valores das propriedades de um objeto que estão para ser definidos pelo cmdlet. Essa API é chamada um pouco antes de um cmdlet gravar algum dado. Você pode configurar verificações de validação que permitem que um cmdlet tenha êxito ou falhe. Se um cmdlet for aprovado nas verificações de validação nessa API, ele terá permissão para gravar os dados. Se o cmdlet não for aprovado nas verificações de validação, ele retornará todos os erros definidos nessa API.

4.  **OnComplete**   Essa API é usada após todo o processamento do cmdlet terminar. Pode ser usada para executar tarefas posteriores ao processamento, como gravação de dados em um banco de dados externo.


> [!TIP]
> O agente de extensão do cmdlet do <CODE>Scripting agent</CODE> não é invocado quando os cmdlets com o verbo <CODE>Get</CODE> são executados.



## Arquivo de configuração do Agente de script

O arquivo de configuração do `Scripting agent` contém todos os scripts que você deseja que o `Scripting agent` execute. Os scripts no arquivo de configuração estão contidos nas marcas XML que definem o começo e o fim do script e os vários parâmetros de entrada necessários para passar os dados ao script. Os scripts são escritos com o uso da sintaxe Windows PowerShell. O arquivo de configuração é um arquivo XML que usa os elementos ou atributos na tabela a seguir.

### Atributos do arquivo de configuração do Agente de script

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Atributo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>Não se aplica</p></td>
<td><p>Esse elemento contém todos os scripts que o agente de extensão do cmdlet do <code>Scripting agent</code> pode executar. A marca <code>Feature</code> é um filho dessa marca.</p>
<p>Há somente uma marca <code>Configuration</code> no arquivo de configuração.</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>Não aplicável</p></td>
<td><p>Esse elemento contém um conjunto de scripts relacionados a um recurso. Cada script, definido na marca filho <code>ApiCall</code>, estende uma parte específica do pipeline de execução do cmdlet. Essa marca contém os atributos <code>Name</code> e <code>Cmdlets</code>.</p>
<p>Pode haver várias marcas <code>Feature</code> na marca <code>Configuration</code>.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Esse atributo contém o nome do recurso. Use esse atributo para ajudar a identifica qual recurso é estendido pelos scripts contidos na marca.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>Esse atributo contém uma lista dos cmdlets do Exchange usados pelo conjunto de scripts dessa extensão de recurso. É possível especificar vários cmdlets separando cada cmdlet com uma vírgula.</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>Não aplicável</p></td>
<td><p>Esse elemento contém scripts que podem estender uma parte do pipeline de execução do cmdlet. Cada script é definido pelo nome de chamada da API no pipeline de execução do cmdlet sendo estendido. A seguir, os nomes de API que podem ser estendidos:</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>Esse atributo inclui o nome da chamada de API que está estendendo o pipeline de execução do cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>Não aplicável</p></td>
<td><p>Esse elemento contém funções que podem ser usadas por qualquer script no arquivo de configuração.</p></td>
</tr>
</tbody>
</table>


Cada servidor do Exchange 2013 inclui o arquivo ScriptingAgentConfig.xml.sample na pasta \<*caminho de instalação*\>\\V15\\Bin\\CmdletExtensionAgents. Esse arquivo deve ser renomeado como ScriptingAgentConfig.xml em cada servidor Exchange 2013 se você habilitar o agente de extensão do cmdlet Scripting Agent. O arquivo de configuração de amostra contém scripts de amostra que podem ser usados para ajudá-lo a entender como adicionar scripts ao arquivo de configuração.

Após você adicionar um script ao arquivo de configuração ou se você fizer uma mudança no arquivo de configuração, será preciso atualizar o arquivo em todos os servidores Exchange 2013 de sua organização. Isso deve ser feito para garantir que todos os servidores tenham uma versão atualizada dos scripts que o agente de extensão do cmdlet do `Scripting Agent` executa.

Alguns caracteres geralmente usados nos scripts também têm um significado especial no XML. Para usar esses caracteres no seu script, seu sequências de escape. Por exemplo, os seguintes caracteres usam uma sequência de escape:

  - Em vez de um sinal de maior que ( `>` ), use `&gt;`

  - Em vez de um sinal de menor que ( `<` ), use `$lt;`

  - Em vez de um sinal de "e" comercial ( `&` ), use `&amp;`

## Habilitar o Agente de script

O agente de extensão do cmdlet do `Scripting agent` está desabilitado por padrão. Quando você habilita o `Scripting agent`, o agente é habilitado para toda a organização do Exchange 2013. Antes de habilitar o `Scripting agent`, verifique se o arquivo de configuração do `Scripting agent` foi renomeado corretamente e atualizado com os seus scripts em todos os servidores do Exchange 2013. Você receberá uma mensagem de erro sempre que um cmdlet for executado se não renomear o arquivo de configuração corretamente ou copiar um arquivo de configuração para esse computador a partir de outro servidor do Exchange 2013.

Para habilitar o `Scripting agent`, é preciso proceder da seguinte forma:

1.  Renomeie o arquivoScriptingAgentConfig.xml.sample em **\<caminho de instalação\>\\V15\\Bin\\CmdletExtensionAgents** como ScriptingAgentConfig.xml em todos os servidores do Exchange 2013 de sua organização.
    

    > [!TIP]
    > É possível copiar o arquivo de configuração de um servidor Exchange 2013 para outros servidores Exchange 2013. Certifique-se de atualizar o arquivo de configuração que deseja copiar antes de copiá-lo.



2.  Adicione seu script ao arquivo de configuração renomeado em cada servidor Exchange 2013 de sua organização.

3.  Habilitar o agente de extensão de cmdlet do `Scripting agent`. Para mais informações sobre como habilitar os agentes de extensão do cmdlet, consulte [Gerenciar agentes de extensão de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Prioridade do Agente de Scripts

Por padrão, o agente de extensão do cmdlet do `Scripting agent` é executado no esquema um agente sim, outro não, com a exceção do agente do `Scripting agent`. Se quiser que um script que você criou substitua um agente existente, será preciso desabilitar o outro agente ou alterar a prioridade de qualquer um dos agentes para que o agente de extensão do cmdlet do `Scripting agent` seja executado primeiro. Para obter mais informações sobre como desabilitar ou alterar as prioridades dos agentes, consulte [Gerenciar agentes de extensão de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

