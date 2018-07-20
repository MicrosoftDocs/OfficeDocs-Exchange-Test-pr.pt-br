---
title: 'Usando o Outlook Web App Web parts: Exchange 2013 Help'
TOCTitle: Usando o Outlook Web App Web parts
ms:assetid: 7272e3ab-430c-4d6c-8621-9535236ce463
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt574711(v=EXCHG.150)
ms:contentKeyID: 70076154
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usando o Outlook Web App Web parts

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-07-31_

Você pode usar o MicrosoftOfficeOutlook Web App Web Parts, abra a caixa de correio de especificar a pasta dentro abrir essa caixa de correio e o modo de exibição de conteúdo para usar.

Outlook Web App Web Parts permitem que você acessar o conteúdo do Outlook Web App diretamente a partir de uma URL. A URL pode ser inserida em um navegador da Web ou incorporada em um aplicativo. Geralmente, as Web Parts não são criadas manualmente. Em vez disso, eles são criados por meio de programação com base nas seleções feitas em uma interface de usuário (UI) ou elas incorporadas diretamente em um aplicativo, como uma página do SharePoint Server. Code-behind a interface do usuário, em seguida, cria a URL. Um uso Outlook Web App Web Parts é para exibir a caixa de entrada ou calendário de um usuário em uma página do SharePoint.


> [!TIP]
> Para usar Outlook Web App Web Parts, a caixa de correio do usuário e a caixa de correio que está sendo abertos por meio de uma Web Part devem estar localizados na mesma floresta Active Directory.



## Permissões para usar Web Parts do Outlook Web Access

Para usar Outlook Web App Web Parts, você deve, no mínimo, ser delegada "Revisor" acessem o conteúdo que você está abrindo. Se você tiver incorporado uma Outlook Web App que exija autenticação em um aplicativo Web Part, você deve passar as informações de autenticação por meio de junto com a solicitação para a Web Part. Uma maneira de fazer isso é, definindo o diretório virtual do Outlook Web App para usar a autenticação integrada Windows. Autenticação integrada Windows permite que os usuários que tenham já tiver feito logon usando suas de uso de conta Active DirectoryOutlook Web App sem ter de digitar suas credenciais novamente.

## Sintaxe de partes da Web do Outlook Web App

Outlook Web App no Exchange 2013 tem um formato de URL a ser usado para solicitações ao diretório virtual /owa. Essas solicitações podem ser feitas digitando uma URL diretamente em um navegador da Web ou incorporação a URL em um aplicativo Web, tal como uma página do SharePoint Server.

Outlook Web App Web Parts podem ser usados para criar URLs de complexidade variada. A Web Part URL simples pode ser usada para abrir a caixa de entrada de qualquer caixa de correio. A Web Part URL mais complexos poderiam ser usada para especificar para abrir a caixa de correio e a pasta dentro dessa caixa de correio para abrir o modo de exibição de conteúdo para usar.

Dependendo de medidas de segurança que tiverem sido aplicadas à sua rede, você precisa definir a codificação para a URL do Web Parts. Após configurar a codificação, o código por trás da interface do usuário criará a URL usando os parâmetros URL codificado. Os parâmetros codificados em URL usam % 20 no lugar de espaços e % 2f no lugar o delimitador de caminho "/". Todos os exemplos neste tópico usam parâmetros codificados.

A tabela a seguir lista os parâmetros de uma Web Part e exemplos de como eles são usados.

### Parâmetros de Web Part e como elas são usadas

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro de URL</th>
<th>Descrição</th>
<th>Valores e exemplos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome do servidor e diretório (necessário)</p></td>
<td><p>A URL do diretório virtual Outlook Web App.</p></td>
<td><p>Isso pode ser a mesma URL que os usuários usam para entrar no Outlook Web App, por exemplo:</p>
<p>https://&lt;;<em>server name</em>&gt; / owa</p></td>
</tr>
<tr class="even">
<td><p>Identificação de caixa de correio de logon explícito Exchange 2013 (opcional)</p></td>
<td><p>Qualquer endereço SMTP associado a caixa de correio a ser aberto.</p>
<p>Se essa seção do URL estiver ausente, a caixa de correio padrão do usuário autenticado é aberta.</p>
<p>Se nenhum parâmetro adicional for especificado, o comportamento padrão é abrir a caixa de entrada.</p></td>
<td><p>Para abrir a caixa de correio com o endereço SMTP tsmith@fourthcoffee.com, use a seguinte URL:</p>
<p>https://&lt;<em>server name</em>&gt;/owa/tsmith@fourthcoffee.com</p></td>
</tr>
<tr class="odd">
<td><p>cmd (necessário se você estiver especificando qualquer parâmetro que não seja a identificação da caixa de correio de logon explícita)</p></td>
<td><p>? cmd = contents exibe Outlook Web App Web Part que é especificada pelos parâmetros em vez da interface do usuário completa Outlook Web App.</p></td>
<td><p>Se nenhuma caixa de correio for especificada, o parâmetro cmd vem após o endereço de entrada, da seguinte maneira:</p>
<p>https://&lt;;<em>server name</em>&gt;/owa/?cmd = contents</p>
<p>Se uma caixa de correio for especificada, o parâmetro cmd vem após a identificação explícita da caixa de correio, da seguinte maneira:</p>
<p>https://&lt;;<em>server name</em>&gt; /owa/ &lt;<em>SMTP address</em>&gt; / ?cmd = contents</p>
<p>Se nenhum parâmetro adicional for especificado, o comportamento padrão é abrir a caixa de entrada.</p></td>
</tr>
<tr class="even">
<td><p>exsvurl</p></td>
<td><p>Este parâmetro deve ser incluído ao usar a autenticação de LiveID</p>
<p>Todos os parâmetros serão descartados durante a autenticação de LiveID se &quot;exsvurl = 1&quot; não está presente. Esse parâmetro destina-se somente a caixas de correio Office 365.</p></td>
<td><p>nome do HTTPS://&lt;Server &gt; /owa/? cmd = conteúdo &amp; exsvurl = 1</p></td>
</tr>
<tr class="odd">
<td><p>fpath (opcional)</p></td>
<td><p>Esta parte da URL pode precisar ser gravado, usando a codificação de URL para que ele possa atravessar firewalls.</p>
<p>Quando você usa a codificação de URL, um espaço se torna % 20 e um delimitador de caminho (/) se torna % 2f.</p>
<p>A hierarquia de pastas deve começar a partir da raiz da caixa de correio.</p>
<p>Este caminho de pasta pode apontar para pastas comuns ou pastas de pesquisa.</p></td>
<td><p>Para abrir a subpasta Projects na caixa de entrada, use a seguinte URL:</p>
<p>https://&lt;;<em>server name</em>&gt;/owa/?cmd = conteúdo &amp; f = a caixa de entrada % 2fprojects</p></td>
</tr>
<tr class="even">
<td><p>módulo (opcional)</p></td>
<td><p>Esse parâmetro pode ser usado para especificar qualquer uma das pastas padrão sem saber o nome localizado.</p></td>
<td><p>Valores para o parâmetro do módulo não diferenciam maiusculas de minúsculas e incluem o seguinte:</p>
<ul>
<li><p>Caixa de Entrada</p></li>
<li><p>Calendário</p></li>
<li><p>Teammailbox</p></li>
</ul>
<p>Para abrir o calendário de uma caixa de correio, independentemente da localização, use a seguinte URL:</p>
<p>https://&lt;;<em>server name</em>&gt;/owa/?cmd = conteúdo &amp; módulo = calendar</p></td>
</tr>
<tr class="odd">
<td><p>View (opcional)</p></td>
<td><p>Este parâmetro especifica o modo de exibição a ser exibido para a pasta.</p>
<p>As exibições padrão quando esse parâmetro não estiver presente são as seguintes:</p>
<ul>
<li><p>Calendário diário</p></li>
<li><p>Mensagens de mensagens</p></li>
</ul>

> [!TIP]
> As cadeias de caracteres para as exibições padrão são automaticamente codificadas no URL.


<p>A classificação de padrão para um modo de exibição é a maneira que a pasta será classificada se ela for aberta no cliente Outlook Web App.</p>
<p>As cadeias de caracteres que identificam as exibições não são localizadas e não diferenciam maiusculas de minúsculas.</p></td>
<td><p>As exibições disponíveis variam de acordo com o tipo da pasta.</p>
<p>Exibições de calendário:</p>
<ul>
<li><p>Diariamente a exibição de calendário diário</p></li>
<li><p>Semanal a exibição de calendário semanal</p></li>
<li><p>Mensalmente exibição do calendário mensal</p></li>
</ul>
<p>Exibições de mensagem:</p>
<ul>
<li><p>Mensagens exibições de mensagem, com classificação padrão</p></li>
<li><p>Por % 20Sender exibição de mensagem classificada por de com nomes de remetentes que começam com &quot;a&quot; na parte superior</p></li>
<li><p>Por % 20Subject exibição de mensagem classificada por assunto com assuntos que começam com &quot;a&quot; na parte superior</p></li>
<li><p>Por % 20Conversation % 20Topic exibição de conversas, não está disponível na versão light do Outlook Web App</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>d, m, y (opcional)</p></td>
<td><p>Especifica a data para o qual o calendário deve ser exibido. Esses parâmetros podem ser inseridos em qualquer ordem e podem ser usados individualmente, ou juntos.</p>
<p>Se qualquer um desses parâmetros não forem especificados, os valores padrão são os valores atuais do dia, mês e ano. Por exemplo, se o dia atual for 3 de maio de 2016, e você especifica um valor de mês do &quot;9&quot; para setembro, a data exibida será 3 de setembro de 2016.</p></td>
<td><p>Os valores válidos para os parâmetros de dados são:</p>
<p>d = [1-31]</p>
<p>m = [1-12]</p>
<p>y = [ano com quatro dígitos]</p>
<p>Para abrir um calendário para a data 3 de maio de 2016, você usaria o seguinte URL: https://&lt;;<em>server name</em>&gt;/owa/?cmd = conteúdo &amp; f = calendário &amp; view = diariamente &amp; d = 3 &amp; m = 5 &amp; y = 2016</p></td>
</tr>
<tr class="odd">
<td><p>Part (opcional)</p></td>
<td><p>Especifica que Outlook Web App deve exibir uma Web Part menor.</p></td>
<td><p>Quando você usar Web Parts para acessar o conteúdo de Outlook Web App, a interface do usuário que é exibido será menor que Outlook Web App completa da interface do usuário. O parâmetro part reduz ainda mais a interface do usuário. A URL de exemplo a seguir mostra a lista de tarefas no formato de Web Part menor:</p>
<p>https://&lt;;<em>server name</em>&gt;/owa/?cmd = conteúdo &amp; part = 1</p>
<p>O parâmetro part não se aplica ao módulo de calendário.</p></td>
</tr>
<tr class="even">
<td><p>FolderList</p></td>
<td><p>Esse parâmetro part inclui o controle de lista de pasta para os usuários alternem entre as subpastas. Isso se aplica apenas às pastas de email.</p></td>
<td><p>nome do HTTPS://&lt;Server &gt; /owa/? cmd = conteúdo &amp; folderlist = 1</p></td>
</tr>
</tbody>
</table>


## Insira as Web Parts do Outlook Web App manualmente

Outlook Web App Web Parts ser também podem ser inseridos manualmente em um navegador da Web. Por exemplo, um usuário pode usar um Outlook Web App URL da Web Part para abrir o calendário de outro usuário.

Os exemplos a seguir mostram como acessem diretamente os modos de exibição comuns do Outlook Web App:

  - **Caixa de entrada:**  https://*\<server name\>*/owa/?cmd = conteúdo & módulo = a caixa de entrada

  - **(Hoje) de calendário:** https://*\<server name\>*/owa/?cmd = conteúdo & módulo = calendário & exsvurl = 1

  - **(Semanalmente) de calendário:**  https://*\<server name\>*/owa/?cmd = conteúdo & módulo = calendário & view = weekly & exsvurl = 1

  - **(Mensalmente) de calendário:**  https://*\<server name\>*/owa/?cmd = conteúdo & módulo = calendário & view = mensal & exsvurl = 1

## Para Obter Mais Informações

  - [Personalizar as páginas de entrada do Outlook Web App, de seleção de idioma e de erro](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)

  - [Criar um tema para o Outlook Web App](create-a-theme-for-outlook-web-app-exchange-2013-help.md)

