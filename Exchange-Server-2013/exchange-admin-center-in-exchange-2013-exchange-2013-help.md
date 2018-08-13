---
title: 'Centro de administração do Exchange no Exchange 2013: Exchange 2013 Help'
TOCTitle: Centro de administração do Exchange no Exchange 2013
ms:assetid: a9aea11a-6ba3-4f4a-a76e-79072e7cfc7d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150562(v=EXCHG.150)
ms:contentKeyID: 50486361
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Centro de administração do Exchange no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-17_

O Centro de Administração do Exchange (EAC) é o console de gerenciamento baseado na web no Microsoft Exchange Server 2013 que é otimizado para implantações locais, online e híbridas do Exchange. O EAC substitui o EMC (Console de Gerenciamento do Exchange) e o ECP (Painel de Controle do Exchange), que eram as duas interfaces usadas para gerenciar o Exchange Server 2010.

Uma vantagem que o EAC baseado na Web oferece é a possibilidade de dividir o acesso à Internet e à Intranet por meio do diretório virtual do IIS do ECP. Com essa funcionalidade, é possível controlar se os usuários podem ter acesso à Internet para o EAC de fora de sua organização, ao mesmo tempo possibilitando que um usuário final acesse as Opções do Outlook Web App. Para saber mais, consulte [Desativar o acesso ao centro de administração do Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

Procurando a versão do Exchange Online deste tópico? Consulte [Centro de administração do Exchange no Exchange Online](https://technet.microsoft.com/pt-br/library/jj200743\(v=exchg.150\)).

Procurando a versão do Exchange Online Protection deste tópico? Consulte [Centro de administração do Exchange no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/jj723141\(v=exchg.150\)).

Conteúdo

Acessando o EAC

Elementos da interface do usuário comuns no EAC

Navegadores compatíveis

## Acessando o EAC

Como o EAC é agora um console de gerenciamento baseado na Web, você precisará usar o diretório virtual do ECP para acessar o console em seu navegador da Web. Na maioria dos casos a URL no EAC será semelhante à seguinte:

  - **URL interna: `https://<CASServerName>/ecp`**   A URL interna é usada para acessar o EAC por meio do firewall de sua organização.

  - **URL externa: `https://mail.contoso.com/ecp`**   A URL externa é usada para acessar o EAC por meio do firewall de sua organização. Algumas organizações podem querer desativar o acesso externo ao EAC. Para obter detalhes, consulte [Desativar o acesso ao centro de administração do Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

Para localizar a URL interna ou externa do EAC, é possível usar o cmdlet [Get-EcpVirtualDirectory](https://technet.microsoft.com/pt-br/library/dd351058\(v=exchg.150\)). Para obter detalhes, consulte [Encontre as URLs internas e externas para o Centro de administração do Exchange](find-the-internal-and-external-urls-for-the-exchange-admin-center-exchange-2013-help.md).

Se você estiver em um cenário de coexistência em que tem o Exchange Server 2010 e o Exchange Server 2013 na mesma organização, e sua caixa de correio ainda estiver hospedada no servidor de caixa de correio do Exchange 2010, o navegador utilizará o ECP do Exchange Server 2010 por padrão. É possível acessar o EAC adicionando a versão do Exchange à URL. Por exemplo, para acessar o EAC cujo diretório virtual está hospedado no servidor de Acesso para Cliente CAS15-NA, use esta URL: `https://CAS15-NA/ecp/?ExchClientVer=15`. Por outro lado, se você quiser acessar o ECP do Exchange 2010 e sua caixa de correio residir em um servidor de caixa de correio do Exchange 2013, use a seguinte URL: `https://CAS14-NA/ecp/?ExchClientVer=14`.

## Elementos da interface do usuário comuns no EAC

A seção descreve os elementos da interface de usuário que são comuns em todo o EAC.

![Centro de Administração do Exchange](images/JJ150562.cd617bc0-19ef-47d2-bba1-4e9546b12e0c(EXCHG.150).gif "Centro de Administração do Exchange")

## Navegação entre locais

A navegação entre locais permite alternar facilmente entre o seu Exchange Online e suas implantações do Exchange no local. Se você não tiver uma organização do Exchange Online, o link o direcionará para a página de entrada do Office 365. Para saber mais, consulte [Implantações Híbridas do Exchange Server](https://technet.microsoft.com/pt-br/library/jj200581\(v=exchg.150\)).

## Painel de recursos

Este é o primeiro nível de navegação para a maioria das tarefas que você executará no EAC. O painel de recursos é semelhante à árvore de console do EMC no Exchange 2010. No entanto, no Exchange 2013, o painel de recursos é organizado por áreas de recursos em vez de funções de servidor, e é necessário clicar menos para encontrar o que precisa.

  - **Destinatários** É onde você gerencia caixas de correio, grupos, caixas de correio de recursos, contatos, caixas de correio compartilhadas e migrações e movimentações de caixa de correio.

  - **Permissões** Aqui você gerenciará as funções de administrador, funções de usuário e políticas do Outlook Web App.

  - **Gerenciamento de conformidade** É onde você gerenciará a Descoberta Eletrônica In-loco, o Bloqueio In-loco, a auditoria, a prevenção contra perda de dados (DLP), as políticas de retenção, as marcas de retenção e as regras de diário.

  - **Organização** É onde você gerenciará as tarefas pertinentes à sua Organização do Exchange, incluindo compartilhamento federado, aplicativos do Outlook e listas de endereços.

  - **Proteção** É onde você gerenciará a proteção antimalware da sua organização.

  - **Fluxo de emails** É onde você gerenciará regras, relatórios de entrega, domínios aceitos, políticas de endereço de email e conectores de envio e recebimento.

  - **Celular** Aqui você gerenciará os dispositivos móveis que lhe permitem conectar-se a sua organização. Você pode gerenciar políticas de caixa de correio de dispositivos móveis e de acesso a dispositivos móveis.

  - **Pastas públicas** No Exchange 2010, você precisava gerenciar as pastas públicas usando o Console de Gerenciamento de Pasta Pública, que estava localizado fora do EMC na Caixa de Ferramentas. No Exchange 2013, as pastas públicas podem ser gerenciadas da área de recurso **pastas públicas**.

  - **Unificação de mensagens** É onde você gerenciará os planos de discagem de UM e os gateways IP de UM.

  - **Servidores** É onde você gerenciará seus servidores de Caixa de Correio e Acesso para Cliente, bancos de dados, grupos de disponibilidade de banco de dados (DAGs), diretórios virtuais e certificados.

  - **Híbrido** É onde você definirá e configurará uma organização Híbrida.

## Guias

As guias são seu segundo nível de navegação. Cada uma das áreas de recurso contém várias guias, cada uma representando um recurso completo. A única exceção a essa regra é a área de recurso Híbrido. Você deve primeiro habilitar sua organização para uma implantação híbrida usando o assistente Configuração Híbrida.

## Barra de ferramentas

Ao clicar na maioria das guias, você verá uma barra de ferramentas. A barra de ferramentas possui ícones que realizam ações específicas, A tabela a seguir, descreve os ícones mais comuns e suas ações. Para exibir a ação associada ao ícone, basta parar sobre o mesmo.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Ícone</th>
<th>Nome</th>
<th>Ação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="Ícone Adicionar" alt="Ícone Adicionar" /></p></td>
<td><p>Adicionar, Novo</p></td>
<td><p>Use esse ícone para criar um novo objeto. Alguns desses ícones têm uma seta para baixo associada, na qual é possível clicar para exibir objetos adicionais que você pode criar. Por exemplo, em <strong>Destinatários</strong> &gt; <strong>Caixas de Correio</strong>, clicar na seta para baixo exibe <strong>Caixa de Correio do Usuário</strong> e <strong>Caixa de Correio Vinculada</strong> como opções adicionais.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="Ícone de edição" alt="Ícone de edição" /></p></td>
<td><p>Editar</p></td>
<td><p>Use esse ícone para editar um objeto.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif" title="Excluir ícone" alt="Excluir ícone" /></p></td>
<td><p>Excluir</p></td>
<td><p>Use esse ícone para excluir um objeto. Alguns ícones excluídos têm uma seta para baixo na qual é possível clicar para mostrar opções adicionais.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif" title="Ícone Pesquisar" alt="Ícone Pesquisar" /></p></td>
<td><p>Pesquisa</p></td>
<td><p>Use esse ícone para abrir uma caixa de pesquisa na qual é possível digitar a frase de pesquisa de um objeto que você deseja encontrar. Verifique <a href="https://technet.microsoft.com/pt-br/library/jj156853(v=exchg.150)">[Destinatários &gt;] Pesquisa avançada</a> para obter mais opções de pesquisa.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="Ícone Atualizar" alt="Ícone Atualizar" /></p></td>
<td><p>Atualizar</p></td>
<td><p>Use essa opção para atualizar a exibição de lista.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Ícone Mais opções" alt="Ícone Mais opções" /></p></td>
<td><p>Mais opções</p></td>
<td><p>Use esse ícone para ver mais ações que podem ser realizadas para os objetos dessa guia. Por exemplo, em <strong>Destinatários</strong> &gt; <strong>Caixas de Correio</strong>, clicar nesse ícone mostra as seguintes opções: <strong>Desabilitar</strong>, <strong>Adicionar/Remover colunas</strong>, <strong>Exportar dados em um arquivo CSV</strong>, <strong>Conectar uma caixa de correio</strong> e <strong>Pesquisa Avançada</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif" title="Ícone Seta para cima" alt="Ícone Seta para cima" />   <img src="images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif" title="Ícone Seta para baixo" alt="Ícone Seta para baixo" /></p></td>
<td><p>Seta para cima e seta para baixo</p></td>
<td><p>Use esses ícones para mover a prioridade de um objeto para cima ou para baixo. Por exemplo, em <strong>Fluxo de emails</strong> &gt; <strong>Políticas de endereço de email</strong>, clique na seta para cima para aumentar a prioridade de uma política de endereço de email. Também é possível usar essas setas para navegar pela hierarquia de pasta pública e para mover as regras para cima e para baixo no modo de exibição de lista.</p></td>
</tr>
<tr class="even">
<td><p><img src="images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif" title="Ícone Copiar" alt="Ícone Copiar" /></p></td>
<td><p>Copiar</p></td>
<td><p>Utilize este ícone para copiar um objeto, para que você possa fazer alterações no mesmo sem alterar o objeto original. Por exemplo, em <strong>Permissões</strong> &gt; <strong>Funções do administrador</strong>, selecione uma função da lista e, em seguida, clique neste ícone para criar um novo grupo de funções baseado em um já existente.</p></td>
</tr>
<tr class="odd">
<td><p><img src="images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif" title="ícone Remover" alt="ícone Remover" /></p></td>
<td><p>Remover</p></td>
<td><p>Utilize este ícone para remover um item da lista. Por exemplo, na caixa de diálogo <strong>Permissões de Pasta Pública</strong> , é possível remover usuários da lista de usuários autorizados a acessarem a pasta pública, selecionando o usuário e clicando neste ícone.</p></td>
</tr>
</tbody>
</table>


## Modo de Exibição de Lista

Ao selecionar uma guia, na maioria dos casos, você verá uma exibição de lista. O modo de exibição da lista no EAC é projetado para remover as limitações que existiam no ECP. ECP pode exibir apenas até 500 objetos, e se você quiser visualizar os objetos que não estão listados no painel de detalhes, é necessário utilizar as opções de pesquisa e filtro para encontrar objetos específicos. No Exchange 2013, o limite visível no modo de exibição de lista do EAC é cerca de 20.000 objetos para implantações no local e 10.000 objetos no Exchange Online. Além disso, a paginação está incluída para que você possa paginar os resultados. No modo de exibição da lista de **Destinatários**, também é possível configurar o tamanho da página e exportar os dados para um arquivo CSV.

## Painel de detalhes

Quando você seleciona um objeto no modo de exibição de lista, informações sobre esse objeto são exibidas no painel de detalhes. Em alguns casos (por exemplo, com objetos de destinatários) o painel de detalhes inclui tarefas de gerenciamento rápido. Por exemplo, se você navegar até **Destinatários** \> **Caixas de Correio** e selecionar uma caixa de correio do modo de exibição de lista, o painel de detalhes exibe uma opção para habilitar ou desabilitar o arquivo morto dessa caixa de correio. O painel de detalhes também pode ser utilizado para edição em massa de vários objetos. Basta pressionar a tecla CTRL, selecionar os objetos que deseja editar em massa e utilizar as opções do painel de detalhes. Por exemplo, selecionar várias caixas de correio lhe permite atualizar em massa informações da organização e contatos dos usuário, atributos personalizados, cota de caixa de correio, configurações do Outlook Web App e muito mais.

## Notificações

O EAC inclui um visualizador de notificações que exibe o status de processos de execução longa e notificações quando o processo é concluído. Além disso, particularmente para processos de execução longa (como solicitações de movimentação), você pode optar por receber notificações por email.

## Bloco Eu e Ajuda

O *bloco Eu* permite sair do EAC e entrar como um usuário diferente. No menu suspenso Ajuda ![Ícone Ajuda](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Ícone Ajuda"), é possível realizar as seguintes ações:

  - **Ajuda**   Clique em ![Ícone Ajuda](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Ícone Ajuda") para visualizar o conteúdo de ajuda online.

  - **Desabilitar Bolha de ajuda**   A bolha de ajuda exibe a ajuda contextual por campos quando você cria ou edita um objeto. É possível desativar a bolha de Ajuda ou ativá-la quando ela estiver desabilitada.

  - **Direitos autorais e privacidade** Clique no link de direitos autorais e privacidade para ler as informações sobre direitos autorais e privacidade do Exchange 2013.

## Navegadores com suporte

Para uma melhor experiência com o EAC, use um dos sistemas operacionais e combinações de navegador rotulados como "Premium".


> [!TIP]
> Não há suporte para outras combinações de sistema operacional e navegador não listadas na tabela, inclusive recursos de toque.



  - **Premium:**  Todos os recursos funcionais têm suporte e foram totalmente testados.

  - **Com suporte:**  Tem o mesmo suporte de recurso funcional do Premium. No entanto, os recursos para os quais a combinação de navegador e sistema operacional não dá suporte estarão ausentes nos navegadores com suporte.

  - **Sem suporte:**  O navegador e o sistema operacional não têm suporte ou não foram testados.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Navegador</p></td>
<td><p>Windows XP e Windows Server 2003</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows 7 e Windows Server 2008</p></td>
<td><p>Windows 8 e Windows Server 2012</p></td>
<td><p>Mac OSX</p></td>
<td><p>Linux</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Premium</p></td>
<td><p>Sem suporte</p></td>
<td><p>Sem suporte</p></td>
<td><p>Sem suporte</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p>Sem suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Premium</p></td>
<td><p>Sem suporte</p></td>
<td><p>Sem suporte</p></td>
<td><p>Sem suporte</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10 ou posterior</p></td>
<td><p>Sem suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Sem suporte</p></td>
<td><p>Sem suporte</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 11 ou posterior</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Com suporte</p></td>
</tr>
<tr class="even">
<td><p>Safari 5.1 ou posterior</p></td>
<td><p>Sem suporte</p></td>
<td><p>Sem suporte</p></td>
<td><p>Sem suporte</p></td>
<td><p>Sem suporte</p></td>
<td><p>Premium</p></td>
<td><p>Sem suporte</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 18 ou posterior</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Premium</p></td>
<td><p>Sem suporte</p></td>
</tr>
</tbody>
</table>

