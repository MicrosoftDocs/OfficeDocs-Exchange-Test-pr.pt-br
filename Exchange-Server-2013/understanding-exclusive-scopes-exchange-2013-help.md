---
title: 'Noções básicas sobre escopos exclusivos: Exchange 2013 Help'
TOCTitle: Noções básicas sobre escopos exclusivos
ms:assetid: 32492622-3b01-4e3b-8288-ed39525eea75
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638110(v=EXCHG.150)
ms:contentKeyID: 50485277
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Noções básicas sobre escopos exclusivos

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

*Escopos exclusivos* são um tipo especial de escopo de gerenciamento explícito que pode ser associado com atribuições de função de gerenciamento. Os escopos exclusivos são projetados para permitir situações em que você tem um grupo de objetos altamente valiosos, como a caixa de correio de um CEO, e é necessário estabelecer um controle estrito de quem tem acesso para administrar esses objetos.

Uma atribuição de função que tem um escopo exclusivo é chamada de *atribuição de função exclusiva*.

Quando você cria um escopo exclusivo, somente aqueles a quem esse escopo (ou um escopo exclusivo equivalente) foi atribuído poderão modificar os objetos que correspondem a esse escopo. Os destinatários de função que não receberam esse escopo exclusivo ou um equivalente não poderão modificar os objetos que correspondem a esse escopo, mesmo se suas próprias funções tiverem escopos que, de outra forma, incluiriam os objetos. Escopos exclusivos substituem qualquer escopo regular que não seja exclusivo. Este comportamento é similar ao funcionamento de uma entrada de controle de acesso (ACE) de negação em Active Directory uma lista de controles de acessos (ACL).

Um *escopo exclusivo equivalente* se refere a outro escopo exclusivo que corresponde a alguns dos mesmos objetos que outro escopo exclusivo. Os escopos não precisam corresponder ao mesmo conjunto completo de objetos. Ambos os escopos podem modificar alguns, ou todos os objetos que correspondem a eles.

## Criando escopos exclusivos

Escopos exclusivos podem ser criados como qualquer outro escopo explícito. Você pode especificar um escopo relativo predefinido; um destinatário, um banco de dados, um filtro de destinatários ou uma lista de servidores ou de bancos de dados. Ao contrário dos escopos regulares, que não entram em vigor até que você associe um escopo a uma atribuição de função de gerenciamento, o aspecto de negação de um escopo exclusivo entra em vigor imediatamente. Isto significa que tão logo um escopo exclusivo é criado, os objetos contidos nesse escopo imediatamente deixam de ser acessíveis por qualquer usuário até que a atribuição de função tenha sido criada.

Depois que a atribuição tiver sido criada, o escopo exclusivo fornece acesso aos usuários que receberam a função de gerenciamento e escopo. Se um outro escopo exclusivo equivalente corresponder aos mesmos objetos, a atribuição de função associada a esse escopo exclusivo ainda pode acessar os objetos.

Para obter mais informações sobre filtros de escopo de gerenciamento, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).


> [!IMPORTANT]
> Active Directory os tempos de replicação devem ser levados em conta ao fazer mudanças em qualquer componente de função de gerenciamento, incluindo escopos exclusivos.



Se você tiver objetos contidos em mais de um escopo exclusivo, ser designado para qualquer um dos escopos exclusivos fornece acesso aos objetos. Para obter mais informações, consulte Exclusive and regular scope interaction, posteriormente neste tópico.

Escopos exclusivos controlam somente o destinatário explícito ou escopo de gravação de configuração de uma atribuição de função. O destinatário implícito ou escopo de leitura de configuração da função atribuída ainda se aplica a um usuário ou grupo. Isso significa que o seguinte se aplica:

  - Aqueles com uma função atribuída continuam a ver objetos que correspondem ao escopo de leitura implícita da função.

  - Aqueles designados para outras funções podem ver objetos contidos em um escopo exclusivo, se os escopos de leitura de outras funções incluírem os objetos. No entanto, os objetos só podem ser modificados por aqueles que foram designados para uma função associada ao escopo exclusivo.

Escopos exclusivos só podem ser usados com funções administrativas ou especializadas e não podem ser usados com funções de usuários finais. Para obter mais informações sobre funções, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

## Interação exclusiva e regular do escopo

A figura no final desta seção ilustra como os escopos exclusivos interagem entre si e com escopos regulares. Todos os usuários na figura têm os seguintes atributos associados a eles.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Usuário</th>
<th>Cidade</th>
<th>Cargo</th>
<th>Departamento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Terry</p></td>
<td><p>Vancouver</p></td>
<td><p>Contador</p></td>
<td><p>Contabilidade</p></td>
</tr>
<tr class="even">
<td><p>David</p></td>
<td><p>Vancouver</p></td>
<td><p>Escritor</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="odd">
<td><p>Walter</p></td>
<td><p>Vancouver</p></td>
<td><p>Gerente</p></td>
<td><p>Marketing</p></td>
</tr>
<tr class="even">
<td><p>Bob</p></td>
<td><p>Vancouver</p></td>
<td><p>CEO</p></td>
<td><p>Tabuleiro</p></td>
</tr>
<tr class="odd">
<td><p>Christine</p></td>
<td><p>Vancouver</p></td>
<td><p>Presidente</p></td>
<td><p>Tabuleiro</p></td>
</tr>
<tr class="even">
<td><p>Fred</p></td>
<td><p>Vancouver</p></td>
<td><p>CFO</p></td>
<td><p>Executivos</p></td>
</tr>
<tr class="odd">
<td><p>Martin</p></td>
<td><p>Vancouver</p></td>
<td><p>CIO</p></td>
<td><p>Executivos</p></td>
</tr>
<tr class="even">
<td><p>Kim</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice-presidente, operações</p></td>
<td><p>Executivos</p></td>
</tr>
<tr class="odd">
<td><p>Jennifer</p></td>
<td><p>Vancouver</p></td>
<td><p>Vice-presidente, Tecnologia</p></td>
<td><p>Executivos</p></td>
</tr>
</tbody>
</table>


As três atribuições de função de gerenciamento a seguir na figura gerenciam os usuários na tabela anterior. Cada um tem um escopo associado, dos quais alguns são escopos exclusivos.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Atribuição de função</th>
<th>Filtro de escopo</th>
<th>Exclusivo ou regular</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administradores de destinatário</p></td>
<td><p>Cidade = Vancouver</p></td>
<td><p>Regular</p></td>
</tr>
<tr class="even">
<td><p>Administradores VIP</p></td>
<td><p>Cargo = CEO, CFO ou CIO ou presidente</p></td>
<td><p>Exclusivo</p></td>
</tr>
<tr class="odd">
<td><p>Administradores executivos</p></td>
<td><p>Departamento = executivos</p></td>
<td><p>Exclusivo</p></td>
</tr>
</tbody>
</table>


A atribuição de função de Administradores destinatários tem um escopo que corresponde a todos os usuários, porque todos estão localizados em Vancouver. Sem qualquer escopo exclusivo, isso significa que a atribuição de função de Administradores destinatários poderia gerenciar qualquer um dos usuários. No entanto, essa organização criou dois escopos exclusivos: Administradores VIP e administradores executivos. Esses escopos exclusivos restringem quem pode gerenciar os usuários que correspondem a seus respectivos filtros de escopo. A atribuição da função de Administradores VIP em um filtro de escopo que corresponde a qualquel usuário que tem um cargo de CEO, CFO, CIO ou Presidente. A atribuição da função de Administradores executivos tem um filtro de escopo que corresponde a qualquer usuário que esteja no departamento dos Executivos.

Quando os escopos regulares e exclusivos forem avaliados, o resultado é o seguinte:

  - A atribuição da função de Administradores Destinatários pode gerenciar os usuários Terry, David e Walter. Esta atribuição de função não pode gerenciar qualquer dos outros usuários porque eles correspondem aos filtros de escopo exclusivo das atribuições de função de Administradores VIP e Administradores executivos.

  - A atribuição da função de Administradores VIP pode gerenciar os usuários Bob, Christine, Fred e Martin. Isso ocorre porque o filtro de escopo exclusivo associado a essa atribuição de função corresponde aos atributos desses objetos. Esta atribuição de função não pode gerenciar os usuários Kim e Jennifer porque seus atributos não correspondem a este escopo exclusivo.

  - A atribuição da função de Administradores executivos pode gerenciar os usuários Kim, Jennifer, Fred e Martin. Isso ocorre porque o filtro de escopo exclusivo associado a essa atribuição de função corresponde aos atributos desses objetos. Esta atribuição de função não pode gerenciar os usuários Bob e Christine porque seus atributos não correspondem a este escopo exclusivo.

Observe que Fred e Martin podem ser acessados por ambos os escopos exclusivos. Isto é porque os atributos nesses usuários correspondem aos filtros de ambos os escopos exclusivos.

**Interação entre escopos exclusivos e escopos regulares**

![Interação exclusiva e regular do escopo](images/Dd638110.0aa26d1d-1fa6-44d8-802d-83d75cd2624c(EXCHG.150).jpg "Interação exclusiva e regular do escopo")

Para obter mais informações sobre escopos de gerenciamento, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

