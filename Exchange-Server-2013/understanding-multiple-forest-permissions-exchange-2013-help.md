---
title: 'Compreendendo as permissões de várias florestas: Exchange 2013 Help'
TOCTitle: Compreendendo as permissões de várias florestas
ms:assetid: 8241033f-e201-4799-b17c-4f120c6e6445
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298099(v=EXCHG.150)
ms:contentKeyID: 50486048
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Compreendendo as permissões de várias florestas

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-07_

Muitas organizações implantam várias florestas para criar limites de segurança em suas organizações. O uso de várias florestas ajuda os administradores definam esses limites de segurança para melhor corresponder aos seus requisitos e se o que é garantir o menor número de pessoas têm acesso aos recursos ou segmentados divisões dentro de uma organização.

Microsoft Exchange Server 2013 suporta dois tipos de várias topologias de floresta:

  - **Entre florestas**   Topologias entre florestas podem ter várias florestas, cada um com seu próprios instalação do Exchange.

  - **Floresta de recursos**   Topologias de floresta de recursos tem uma floresta Exchange e uma ou mais florestas de contas.

Para os fins deste tópico, a floresta que contém os grupos de segurança universais (USGs) e os usuários fora da floresta onde Exchange 2013 estiver instalado, seja ela uma floresta de contas ou outra floresta de recursos, é chamada de uma floresta externa.

Configuração de permissões em uma topologia de floresta de várias depende da configuração correta de sincronização da GAL (lista) de endereços global para a criação de caixas de correio vinculadas e relações de confiança de floresta. A floresta Exchange 2013 deve confiar na floresta externa que contém o USGs associadas a grupos de função vinculado e os usuários associados a caixas de correio vinculadas.

Exchange 2013 usa um modelo de permissões de controle de acesso com base da função (RBAC). Os grupos de função de gerenciamento que os administradores são membros da e as diretivas de atribuição de função de gerenciamento que são atribuídos a usuários finais, determinam o que cada administrador e usuário final podem fazer. Para entender as permissões de várias florestas, você precisa estar familiarizado com RBAC. Para obter mais informações sobre o RBAC, grupos de função e políticas de atribuição de função, consulte os tópicos a seguir:

  - [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md)

  - [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md)

  - [Noções básicas sobre diretivas de atribuição de função de gerenciamento](understanding-management-role-assignment-policies-exchange-2013-help.md)

Procurando tarefas de gerenciamento relacionadas ao gerenciamento de permissões? Consulte [Permissões](permissions-exchange-2013-help.md).

**Sumário**

Permissões em uma topologia de várias florestas

Permissões de cross-limite

Configurar permissões de Cross-limite

## Permissões em uma topologia de floresta de várias

RBAC aplica permissões a todos os objetos Exchange em uma única floresta e a configuração de RBAC em cada floresta é configurada independentemente de todas as outras florestas. Quando você cria um grupo de funções em uma floresta, que o grupo de função não existe qualquer outra floresta e as permissões concedidas por esse grupo de funções se aplicam somente para a floresta na qual ele foi criado. Por exemplo, um membro de um grupo de função que concede permissões para criar uma caixa de correio pode criar uma caixa de correio somente na floresta que contém a esse grupo de função.

Se você tiver várias florestas Exchange e deseja configurar permissões de forma idêntica em cada floresta, você deve aplicar a mesma configuração explicitamente em cada floresta. Por exemplo, se você tiver duas florestas Exchange 2013 e deseja criar um grupo de funções de gerenciamento de conformidade para gerenciar permissões para o seu departamento jurídico, faça o seguinte:

  - Em cada floresta, crie um grupo de função chamado gerenciamento de conformidade. Se os seus administradores em uma floresta externa separada de uma das florestas Exchange, crie dois grupos de função vinculados como grupos de função. Para obter mais informações sobre grupos de função, consulte a seção Permissões de limite de cruz .

  - Em cada floresta, crie as atribuições de função entre os novos grupos de função e as funções que você deseja usar.

  - Como parte das novas atribuições de função, opcionalmente Adicione escopos de gerenciamento que abrangem os objetos de servidor e o destinatário dentro de cada floresta.

  - Se você criou os grupos de função, como os grupos de função vinculado, adicione membros ao USG associado na floresta externa.

A figura a seguir mostra como os grupos de função configurados em florestas Exchange 2013 são vinculados a seus respectivas florestas. O grupo de funções de gerenciamento da organização no Exchange 2013 floresta uma concede permissões somente para gerenciar as caixas de correio e servidores que estão dentro dessa floresta. Da mesma forma, os grupos de função na floresta Exchange 2013 B para concedem permissões somente as caixas de correio e servidores dentro dessa floresta.

A figura também mostra a que o grupo de funções personalizados que um é criado em cada floresta. Mesmo que eles foram criados com o mesmo nome, cada uma é sua própria entidade separada. Na verdade, conforme mostra a figura, cada uma pode ser atribuída funções de gerenciamento diferentes em suas respectivas florestas. Grupo de função personalizada A na floresta Exchange 2013 A é atribuído a pesquisa de caixa de correio e funções Message Tracking enquanto o grupo de funções de sinalizador A na floresta Exchange 2013 B é atribuído a pesquisa de caixas de correio e funções de gerenciamento de retenção.

Finalmente, escopos de gerenciamento criados em cada floresta também estão ligados por floresta. Escopos de servidor criados em cada floresta podem conter apenas os servidores que são membros dessa floresta. Escopo de servidor uma pode conter apenas os servidores Exchange 2013 floresta A enquanto o escopo de servidor B pode conter apenas os servidores que estão dentro da floresta Exchange 2013 B. Da mesma forma, o escopo do destinatário na floresta Exchange 2013 B pode conter somente caixas de correio que estão dentro da floresta Exchange 2013 B.

**Relação de limite de escopo de floresta e RBAC**

![Relacionamentos de escopo de limite de floresta e RBAC](images/Dd298099.220da7c3-cbb8-42ac-9d58-084d996bf837(EXCHG.150).gif "Relacionamentos de escopo de limite de floresta e RBAC")

## Permissões de cross-limite

As permissões concedidas pelo RBAC apenas permitem aos usuários exibir ou modificar objetos Exchange dentro de uma floresta específico. No entanto, você pode conceder permissões para exibir e modificar objetos Exchange em uma floresta para usuários externos dessa floresta. Usando permissões de cross-limite, você poderá centralizar Exchange contas de gerenciamento em uma única floresta em vez de ter que autentica em cada floresta individual para realizar tarefas.


> [!TIP]
> As permissões são concedidas a um usuário fora de uma floresta Exchange ainda se aplicam apenas dessa floresta específico Exchange. Por exemplo, se um usuário em uma floresta externa é um membro do grupo de função vinculado de gerenciamento da organização que está localizado na florestaA, o usuário pode gerenciar apenas os objetos Exchange contidos FlorestaA. Um usuário deve ser membro dos grupos de função vinculado feito em cada floresta Exchange para receber permissões para gerenciar cada floresta.



Permissões de cross-limite também permitem que você aplicar políticas de atribuição de função às caixas de correio de usuários com caixas de correio em uma floresta Exchange, mas têm contas de usuário que residem em uma floresta de contas. Exchange 2013 oferece suporte a permissão de limite de entre usando grupos de função vinculado e caixas de correio vinculadas, que são abordadas nas seções a seguir.

## Permissões administrativas

São concedidas permissões administrativas dos limites da floresta cruzado pelo uso de grupos de função vinculado e caixas de correio vinculadas.

Um grupo de função vinculado é criado na organização Exchange 2013 e está vinculado a um USG através da fronteira da floresta na floresta externa. O USG de grupo de função vinculado está vinculado à pode ser qualquer um dos seguintes procedimentos:

  - Um USG dedicado para o uso específico do grupo de função vinculado

  - Um USG que está vinculada por grupos de função vinculado em várias florestas Exchange 2013

  - Um grupo de funções USG em outra floresta Exchange 2013

  - Um USG associado a um grupo de função Exchange Server 2007 função ou Exchange 2010 administrativo

O USG vinculado a um grupo de função vinculado deve estar em outra floresta. Você não pode vincular a um grupo de função vinculado a um USG na mesma floresta.

A figura a seguir mostra que USGs em uma floresta de contas podem ser associados aos grupos de função em uma ou mais florestas de recurso Exchange 2013. Os membros dos USGs na floresta de contas efetivamente se tornar membros dos grupos de função através do USGs.

**Grupos de função vinculado associados USGs em uma floresta diferente**

![Grupo de funções vinculado e relações do USG](images/Dd298099.23f245e8-b80f-4082-8628-ee6701259be6(EXCHG.150).gif "Grupo de funções vinculado e relações do USG")

Quando você cria um grupo de função vinculado, você atribuir funções ao grupo de função vinculado na floresta Exchange 2013. As atribuições que associar as funções para o grupo de função vinculado podem incluir escopos de gerenciamento, se necessário. Estes escopos são confinados a floresta na qual o grupo de função vinculado é criado.

A associação do grupo de função vinculado é gerenciada adicionando e removendo membros para e do USG na floresta externa. Quando você adiciona membros a este USG, eles são concedidos as permissões atribuídas ao grupo de função vinculado na floresta Exchange 2013. Se você tiver vários grupos de função vinculado com o mesmo USG vinculado, os membros desse USG são concedidos as permissões atribuídas a cada grupo de função vinculado em cada floresta Exchange 2013.

Você não pode gerenciar a associação de um grupo de função vinculado da floresta Exchange 2013.

Um segundo método para atribuir permissões administrativas limites da floresta é devido ao uso de caixas de correio vinculadas. Para usuários em uma floresta de contas usar uma implantação Exchange 2013 em uma floresta de recursos separado Exchange 2013, você deve configurar as caixas de correio vinculadas para cada usuário. Caixas de correio vinculadas podem ser adicionadas como membros a grupos de funções dentro da floresta Exchange 2013. Quando uma caixa de correio vinculada se torna um membro de um grupo de função, que vinculado da caixa de correio e, por sua vez o usuário na floresta de contas associado à caixa de correio vinculada, recebe as permissões fornecidas pelo grupo de funções.

A figura a seguir mostra a relação entre usuários em uma floresta de contas, as caixas de correio vinculadas associadas e os grupos de função nos quais eles são membros.

**Usuários em uma floresta de contas associadas com caixas de correio vinculadas que são membros dos grupos de função**

![Grupo de funções e relacionamentos de caixa de correio vinculada](images/Dd298099.e59242f6-5c63-4114-90f7-6b6c2478570c(EXCHG.150).gif "Grupo de funções e relacionamentos de caixa de correio vinculada")

Grupos de função vinculado e caixas de correio vinculadas tem vantagens e desvantagens quando utilizado para atribuir permissão administrativa limites da floresta. A tabela a seguir descreve alguns deles.

### Função vinculado da caixa de correio do grupo e vinculadas vantagens e desvantagens

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Grupos de função vinculado ou caixas de correio vinculadas</th>
<th>Vantagem</th>
<th>Desvantagens</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Grupos de função vinculados</p></td>
<td><p>Você pode associar vários grupos de função vinculado de várias florestas Exchange 2013 para um único USG em uma floresta de contas ou outra floresta de recurso Exchange. Isso permite que você administre topologias de floresta complexa Exchange por meio de um conjunto pequeno de USGs em uma única floresta.</p></td>
<td><p>Um grupo de função regular não pode ser convertido em um grupo de função vinculado. Você deve criar manualmente os grupos de função vinculado para substituir cada grupo de função regular que tenha as permissões que você deseja conceder entre o limite de uma floresta. Para obter mais informações, consulte Configure cross-limite permissions.</p></td>
</tr>
<tr class="even">
<td><p>Caixas de correio vinculadas</p></td>
<td><p>Caixas de correio vinculadas permitem que você use os grupos de função existente dentro da floresta Exchange. Caixas de correio vinculadas são adicionadas como membros aos grupos de função existente, assim como as caixas de correio regulares, USGs e usuários na mesma floresta Exchange.</p></td>
<td><p>Se você conceder permissões em várias florestas Exchange 2013 usando caixas de correio vinculadas vinculadas a um único usuário em uma floresta de contas, você deve modificar a associação ao grupo de função de cada floresta Exchange 2013 se você deseja modificar as permissões concedidas ao usuário.</p></td>
</tr>
</tbody>
</table>


Recomendamos que você use grupos de função vinculado conceder permissão limites da floresta, se você planeja ter várias florestas do recurso Exchange.

## Permissões de usuário final

Permissões de usuário final são atribuídas a caixas de correio individuais, usando políticas de atribuição de função. Quando Exchange 2013 é instalado em uma floresta de recurso, caixas de correio vinculadas são criadas na floresta de recursos e estão associadas a contas de usuário na floresta de contas.

Quando uma caixa de correio vinculada é criada, ele é atribuído a uma política de atribuição de função padrão exatamente como uma caixa de correio regular. A política de atribuição de função determina quais permissões de usuário final são concedidas à caixa de correio. Essas permissões permitem que os usuários exibam e modifiquem configurações relacionadas aos recursos a seguir e outros:

  - Informações de perfil de usuário final

  - Caixa postal do usuário final

  - Propriedade e a associação de distribuição do usuário final

Quando uma política de atribuição de função é atribuída a uma caixa de correio vinculada, o usuário na floresta de contas associado a caixa de correio vinculada recebe permissões para gerenciar os recursos disponíveis para o usuário. As permissões se aplicam somente aos recursos na floresta Exchange onde se encontra a caixa de correio vinculada. A figura a seguir mostra a relação entre o usuário final na floresta de contas, sua caixa de correio vinculada associada e a diretiva de atribuição de função atribuído à caixa de correio vinculada. Além disso, uma caixa de correio vinculada associada a um usuário administrativo na floresta de contas pode ser associada a vários grupos de função, além de uma política de atribuição de função.

**Usuários em uma floresta de contas associadas com caixas de correio vinculadas cada atribuída uma política de atribuição de função**

![Grupo de funções e relacionamentos de diretiva de atribuição](images/Dd298099.785b9b35-4292-43ce-917b-117d0174742e(EXCHG.150).gif "Grupo de funções e relacionamentos de diretiva de atribuição")

Voltar ao início

## Configurar permissões de cross-limite

Para configurar permissões de cross-limite em uma topologia de várias florestas, você deve criar grupos de função vinculado para cada um dos grupos de função que você deseja vincular USGs em uma floresta externa. Isso significa que você deve criar um grupo de função vinculado para cada grupo de funções internas. Você precisa:

1.  Crie um USG na floresta externa para cada grupo de função vinculado a ser criado. Adicione membros desse USG que você deseja conceder permissões para.

2.  Crie um grupo de função vinculado para cada grupo de função internos. Acontece o seguinte quando o grupo de função vinculado é criado:
    
      - As mesmas funções que estão atribuídas ao grupo de funções internas são atribuídas ao novo grupo de função vinculado.
    
      - O grupo de função vinculado é associado com o USG na floresta externa.

3.  Crie grupos de função vinculado para quaisquer grupos de função personalizada que você criou.

4.  Opcionalmente, atribua escopos personalizados para os novos grupos de função vinculado.

Para obter informações detalhadas sobre como executar essas etapas, consulte os tópicos a seguir:

  - [Criar grupos de função vinculado que espelham grupos de função internos](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

  - [Gerenciar grupos de função vinculado](manage-linked-role-groups-exchange-2013-help.md)

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

Se você precisar alterar o USG de um grupo de função vinculado está associado, consulte [Gerenciar grupos de função vinculado](manage-linked-role-groups-exchange-2013-help.md).

Quando uma caixa de correio vinculada é criada, ele é automaticamente atribuído a uma política de atribuição de função. Você pode alterar a política de atribuição de função é atribuída à caixa de correio vinculada ou alterar a política de atribuição de função é atribuída às caixas de correio por padrão quando são criados. Para obter mais informações, consulte os tópicos a seguir:

  - [Alterar a política de atribuição de uma caixa de correio](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

  - [Gerenciar políticas de atribuição de função](manage-role-assignment-policies-exchange-2013-help.md)

