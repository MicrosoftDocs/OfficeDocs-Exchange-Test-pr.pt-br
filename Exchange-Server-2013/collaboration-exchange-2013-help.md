---
title: 'Colaboração: Exchange 2013 Help'
TOCTitle: Colaboração
ms:assetid: f45c1be1-2a66-4610-a28d-4adc6d212769
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ218725(v=EXCHG.150)
ms:contentKeyID: 50487002
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Colaboração

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Exchange 2013 fornece os seguintes recursos avançados que podem ajudar os usuários finais facilmente colaboram em email:

  - Caixas de correio de site

  - Pastas públicas

  - Caixas de correio compartilhadas

  - Grupos de distribuição

Cada um desses recursos tem uma experiência de usuário diferente e recurso definido e deve ser usado com base no qual o usuário precisa realizar e o que sua organização pode fornecer. Por exemplo, caixas de correio de site fornecem documentação excelente recursos de colaboração. No entanto, contam com caixas de correio do site do SharePoint Server 2013, portanto, se você não estiver planejando sobre como implantar o SharePoint, você deve usar pastas públicas para compartilhar documentos.

Este tópico compara estes recursos de colaboração para ajudar você a decidir quais os recursos a serem oferecidos para os seus usuários.

## Caixas de correio de site

Um mailboxe site funcionalmente é composta por uma associação de site do SharePoint 2013 (proprietários e membros), armazenamento por meio de uma caixa de correio do Exchange 2013 para mensagens de email e um site do SharePoint 2013 para armazenar e compartilhar compartilhado. Basicamente, caixas de correio de site reunir email do Exchange e documentos do SharePoint. Para usuários, uma caixa de correio de site serve como um arquivo convencional central para o projeto, fornecendo um lugar para email de projeto do arquivo e documentos que podem ser acessados e editados apenas por membros do site. Além disso, as caixas de correio do site têm um ciclo de vida especificado e otimizadas para ser usado para projetos que definiu as datas de início e término. Para implementar totalmente caixas de correio de site, os usuários finais deve usar o Outlook 2013.

Para saber mais, consulte [Caixas de correio locais](site-mailboxes-exchange-2013-help.md).

## Pastas públicas

As pastas públicas são feitas para acesso compartilhado e oferecem um jeito fácil e eficaz de coletar, organizar e compartilhar informações com outros pessoas no seu grupo de trabalho ou organização.

Pastas públicas organizam o conteúdo em uma hierarquia profunda fácil navegar. Usuários descubram o conteúdo relevante e interessante navegando pelos ramificações da hierarquia que são relevantes para eles. Os usuários sempre ver a hierarquia completa no seu modo de exibição de pasta do Outlook. Pastas públicas são uma excelente tecnologia para arquivamento de grupo de distribuição. Uma pasta pública pode ser habilitado para email e adicionada como um membro do grupo de distribuição. Emails enviados para o grupo de distribuição é automaticamente adicionado à pasta pública para referência futura. Pastas públicas também fornecem o compartilhamento de documentos simples e não exigem o SharePoint Server 2013 para ser instalado em sua organização. Finalmente, usuários finais podem usar pastas públicas com os seguintes clientes com suporte do Outlook: Outlook 2007, Outlook 2010 e Outlook 2013.

Para saber mais, consulte [Pastas públicas](public-folders-exchange-2013-help.md).

## Caixas de Correio compartilhadas

Uma caixa de correio compartilhada é uma caixa de correio que vários usuários desigados podem acessar para ler e enviar mensagens e para compartilhar um calendário comum. As caxas de correio compartilhadas fornecem um endereço de email genérico (tais como info@contoso.com ou vendas@contoso.com) que os clientes podem usar para pesquisar a sua empresa. Se a caixa de correio compartilhada possuir a permissão de Enviar Como quando um usuário representante responder à mensagem de email, pode parecer que a caixa de correio (por exemplo, vendas@contoso.com) está respondendo, não o usuário real.

Para saber mais, consulte [Caixas de correio compartilhadas](shared-mailboxes-exchange-2013-help.md).

## Grupos

Grupos (também chamados de grupo de distribuição) são um conjunto de dois ou mais destinatários que aparecem no catálogo de endereços compartilhado. Quando uma mensagem email é enviada para um grupo, é recebida por todos os membros do grupo. Os grupos de distribuição podem ser organizados para um assunto particular de discussão (tais como "Amantes de Cachorro") ou por usuários que compartilham uma estrutura de trabalho comum que exija que eles se comuniquem frequentemente.

Para saber mais, consulte [Destinatários](recipients-exchange-2013-help.md).

## Qual deve ser usado?

A tabela a seguir oferece uma pequena amostra de cada um dos recursos de colaboração para ajudar você a decidir qual usar.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Caixas de correio de site</th>
<th>Pastas públicas</th>
<th>Caixas de Correio compartilhadas</th>
<th>Grupos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Tipo de grupo</strong></p></td>
<td><p>Usuários que trabalham juntos como uma equipe em um projeto específico com data de início e de término definidas.</p></td>
<td><p>Com as devidas permissões, todos na sua organização podem acessar e pesquisar pastas públicas. As pastas públicas são ideais para manter um histórico ou as conversas de um grupo de distribuição.</p></td>
<td><p>Representantes que trabalham em nome de uma identidade virtual, e eles podem responder ao email como essa identidade de caixa de correio compartilhada. Exemplo: suporte@tailspintoys.com</p></td>
<td><p>Usuários que precisam enviar email para um grupo de destinatários com um interesse ou característica comum.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tamanho ideal do grupo</strong></p></td>
<td><p>Pequeno</p></td>
<td><p>Grande</p></td>
<td><p>Pequeno</p></td>
<td><p>Grande</p></td>
</tr>
<tr class="odd">
<td><p><strong>Acesso</strong></p></td>
<td><p>Proprietários e membros da caixa de correio de site.</p></td>
<td><p>Acessível para qualquer um na sua organização.</p></td>
<td><p>Os usuários podem ter permissões de Acesso Total e/ou Enviar Como. Se as permissões de Acesso Total forem dadas, os usuários devem também adicionar a caixa de correio compartilhada ao seu perfil do Outlook para acessar a caixa de correio compartilhada.</p></td>
<td><p>Para grupos de distribuição, membros, devem ser adicionados manualmente. Para grupos dinâmicos de distribuição, os membros serão adicionados com base nos critérios de filtragem.</p></td>
</tr>
<tr class="even">
<td><p><strong>Calendário compartilhado?</strong></p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p><strong>O email chega na Caixa de Entrada pessoal do usuário?</strong></p></td>
<td><p>Não. O email chega na caixa de correio de site.</p></td>
<td><p>Não, O email chega na pasta pública.</p></td>
<td><p>Não. O email chega na Caixa de Entrada da caixa de correio compartilhada.</p></td>
<td><p>Sim. O email chega na Caixa de Entrada de um membro do grupo de distribuição.</p></td>
</tr>
<tr class="even">
<td><p><strong>Clientes suportados</strong></p></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>SharePoint 2013</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
</tr>
</tbody>
</table>

