---
title: 'Catálogos de endereços hierárquicos: Exchange 2013 Help'
TOCTitle: Catálogos de endereços hierárquicos
ms:assetid: a1d277a0-5437-40af-aade-e4730a0d1308
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff629379(v=EXCHG.150)
ms:contentKeyID: 50486270
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Catálogos de endereços hierárquicos

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-03-26_

O HAB (catálogo de endereços hierárquico) permite que os usuários procurem destinatários em seu catálogo de endereços usando uma hierarquia organizacional. Normalmente, usuários são limitados à lista de endereços global (GAL) padrão e suas propriedades de destinatários e a estrutura da GAL frequentemente não refletem as relações de gestão e tempo de serviço de destinatários na sua organização. A capacidade de personalizar um HAB que mapeia a estrutura corporativa exclusiva de sua organização propicia aos usuários um método eficiente para localizar destinatários internos.

## Usando os catálogos de endereços hierárquicos

Em um HAB, a organização raiz (por exemplo, Contoso, Ltd) é usada como camada de nível superior. Sob essa camada de nível superior, é possível adicionar diversas camadas subordinadas para criar um HAB personalizado segmentado por divisão, departamento ou qualquer outra camada organizacional que você queira especificar. As figuras a seguir ilustram um HAB para a Contoso, Ltd com a seguinte estrutura:

  - A camada superior representa a organização raiz, Contoso, Ltd.

  - A camada de segundo nível representa as divisões corporativas dentro da Contoso, Ltd: Escritório Corporativo, Organização de Suporte a Produtos e Organização de Vendas e Marketing.

  - As camadas filhas de terceiro nível representam os departamentos dentro da divisão do Escritório Corporativo: Human Resources, Accounting Group e Administration Group.

**Exemplo de HAB para a Contoso, Ltd**

![Caixa de diálogo Catálogo de Endereços Hierárquico](images/Ff607473.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Caixa de diálogo Catálogo de Endereços Hierárquico")

É possível fornecer um nível de estrutura hierárquica adicional usando o parâmetro *SeniorityIndex*. Ao criar um HAB, use o parâmetro *SeniorityIndex* para classificar os destinatários individuais ou os grupos organizacionais por antiguidade dentro desses níveis organizacionais. Essa classificação especifica a ordem em que os destinatários ou grupos são exibidos no HAB. Por exemplo, no exemplo anterior, o parâmetro *SeniorityIndex* para os destinatários na divisão do Escritório Corporativo é definido da seguinte forma:

  - `100` para David Hamilton

  - `50` para Rajesh M. Patel

  - `25` para Amy Alberts


> [!TIP]
> Se o parâmetro <EM>SeniorityIndex</EM> não for definido ou for igual para dois ou mais usuários, a ordem de classificação do HAB usará o valor do parâmetro <EM>PhoneticDisplayName</EM> para listar os usuários em ordem alfabética crescente. Se o valor do parâmetro <EM>PhoneticDisplayName</EM> não for definido, a ordem de classificação do HAB adotará como padrão o valor do parâmetro <EM>DisplayName</EM> e listará os usuários em ordem alfabética crescente.



## Configurando catálogos de endereços hierárquicos

Instruções detalhadas para criar HABs são incluídas no tópico [Habilitar ou desabilitar catálogos de endereços hierárquico](enable-or-disable-hierarchical-address-books-exchange-2013-help.md). As etapas gerais são as seguintes:

1.  Crie um grupo de distribuição que será usado para a organização raiz (camada de nível superior). Opcionalmente, você pode usar uma unidade organizacional existente em sua floresta do Exchange para o grupo de distribuição.

2.  Crie grupos de distribuição para as camadas subordinadas e designe-os como membros do HAB. Modifique o parâmetro *SeniorityIndex* desses grupos para que sejam listados na ordem hierárquica adequada dentro da organização raiz.

3.  Adicione membros à organização. Modifique o parâmetro *SeniorityIndex* dos membros para que sejam listados na ordem hierárquica adequada dentro das camadas subordinadas.

4.  Para fins de acessibilidade, você pode usar o parâmetro *PhoneticDisplayName*, que especifica uma pronúncia fonética do parâmetro *DisplayName*.

