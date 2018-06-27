---
title: 'Perguntas Frequentes: Centro de administração do Exchange: Exchange 2013 Help'
TOCTitle: 'Perguntas Frequentes: Centro de administração do Exchange'
ms:assetid: 3de0042f-74a6-458f-947c-3cd6eeacd6ab
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ552409(v=EXCHG.150)
ms:contentKeyID: 50485408
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Perguntas Frequentes: Centro de administração do Exchange

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Este tópico fornece uma lista de perguntas freqüentes para o novo centro de administração do Exchange (EAC) no Microsoft Exchange Server 2013. Outras dúvidas sobre EAT não respondidas aqui? Envie-em um email em [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com).

## A EAT desenvolvida exclusivamente para o Exchange Online?

A EAT serve todas as opções de implantação para Exchange 2013, incluindo os clientes que desejam implantar no local, na nuvem com Exchange Online ou uma implantação híbrida.

## Você removeu o Console de gerenciamento do Exchange (EMC) porque você está criando a interface principalmente para clientes de pequenos e médio porte?

O EAC foi desenvolvido para proporcionar uma experiência de gerenciamento única e intuitiva para todos os nossos clientes e foi projetado para ajudar a tornar a execução das tarefas mais comuns de administração mais simples.

Criamos uma interface única que fornece um subconjunto de cobertura de cenário sobre o Console de gerenciamento do Exchange (EMC) e o painel de controle do Exchange (ECP) e que endereçada principais desafios e cenários para clientes.

Além disso, podemos ouvida aos clientes de todos os tamanhos e suas principais preocupações foram o seguinte:

  - Manutenção e fazendo o download de patches para operar uma ferramenta administrativa é uma sobrecarga operacional para clientes que, por sua vez, aumenta os custos operacionais.

  - Como a força de trabalho IT se torna cada vez mais móvel, os clientes queriam poder gerenciar seus ambientes em qualquer lugar, não apenas a partir de desktops e servidores de onde suas ferramentas administrativas estão instaladas.

  - Usando várias ferramentas para opções de implantação diferentes fica confusa e aumenta os custos operacionais e de treinamento

## É o log do PowerShell e exposição de cmdlet voltem para EAT?

Estamos executou antecipado comentários do cliente sobre esse e estão avaliando a possibilidade de isso:/ / Tools.ietf.org em uma atualização futura.

## EMC seja reapresentado um pacote de serviço futuras?

Não. Oferecemos suporte para a experiência de EAT totalmente.

## Você pode usar o EMC do Exchange 2010 para gerenciar objetos do Exchange 2013?

Não. Você não pode usar o EMC do Exchange 2010 para gerenciar servidores e objetos Exchange 2013. Enquanto os clientes atualizem para Exchange 2013, recomendamos que eles usem o EAC para:

1.  Gerencie caixas de correio Exchange 2013, servidores e serviços correspondentes.

2.  Exibir e atualizar propriedades e caixas de correio do Exchange 2010.

3.  Exibir e atualizar propriedades e caixas de correio do Exchange 2007.

Recomendamos aos clientes usar o Exchange 2010 EMC para criar e gerenciar caixas de correio do Exchange 2010.

Recomendamos aos clientes usar o Exchange 2007 EMC para criar e gerenciar caixas de correio do Exchange 2007.

Os clientes podem continuar a executar tarefas de gerenciamento usando o Shell de gerenciamento do Exchange e tarefas de script.

## Por que a caixa de pesquisa sempre não ficará visível?

Como parte do nossos princípios de design para Exchange 2013, queríamos que ajudam a garantir que nada está em seu caminho até que precise dela. Essa simplicidade é representada em todas as nossas experiências de usuário final (incluindo a EAT). Caixa Pesquisar slides check-out após você clicar no ícone. Isso proporciona mais espaço para o usuário digite sua consulta, na caixa de texto e também fornece Mena tipo que exibem depois que a correspondência de consulta em tempo real ocorre. Essa melhoria nos permite ocultar complexidade desnecessária sem diminuir a experiência de gerenciamento. Podemos continuarão a melhorar a nossas experiências com base em comentários.

## EAT funcionarão em tablets?

Administração por meio de tablets e dispositivos móveis não é suportada no momento.

## Por que o Exchange 2010 ECP abrir quando tento acessar o EAC do Exchange 2013?

Se sua caixa de correio existir em um servidor de caixa de correio do Exchange 2010, o Exchange 2010 ECP serão carregados automaticamente no seu navegador. Isso ocorre por design. Você pode acessar o EAC, adicionando a versão do Exchange para a URL. Por exemplo, para acessar o EAC cujo diretório virtual está hospedado no servidor de acesso para cliente CAS01-NA, use a seguinte URL: `https://CAS01-NA/ecp?ExchClientVer=15`.

## Como limitar onde EAT pode ser usado?

Para limitar a Internet versus acesso à intranet, o Exchange oferece particionamento a nível do diretório virtual no IIS. Os administradores podem permitir ou negar cenários de gerenciamento de TI do sendo executadas pelos clientes da internet externos (por exemplo, a partir de clientes que não está Unidos a um domínio dentro do firewall corporativo) explicitamente. Para obter mais informações, consulte [Desativar o acesso ao centro de administração do Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

## O que mudou para a caixa de ferramentas do Exchange 2013?

No Exchange 2007 e Exchange 2010, o EMC contidos Toolbox, que fornecia acesso a diversas ferramentas de gerenciamento de sua organização do Exchange. A caixa de ferramentas do Exchange 2013 é consideravelmente mais simples do que as versões anteriores. O Visualizador de filas, Remote Connectivity Analyzer e o Editor de modelos de detalhes ainda estão disponíveis na caixa de ferramentas do Exchange 2013. As ferramentas restantes foram realocadas ou movidas para o EAC.

A tabela a seguir lista as alterações para a caixa de ferramentas do Exchange 2013:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ferramenta</th>
<th>Onde está agora?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practices Analyzer (ExBPA)</p></td>
<td><p>O ExBPA foi descontinuado. Verificações de preparação substituíram o ExBPA para certificar-se de que sua floresta do Active Directory e os servidores do Exchange estão prontos para o Exchange 2013. Cada tópico de verificação de preparação descreve as ações que podem ser realizadas para resolver os problemas encontrados quando as verificações de preparação são executadas. Você só deve executar as etapas descritas em um tópico da seleção de preparação se essa verificação de preparação foi exibida durante a instalação.</p></td>
</tr>
<tr class="even">
<td><p>Solucionador de problemas de fluxo de mensagens</p></td>
<td><p>Solução de problemas de fluxo de email foi descontinuada. Agora você pode usar o recurso de rastreamento de mensagens no EAC. Vá para <strong>fluxo de emails</strong> &gt; <strong>notificações de entrega</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Monitor de desempenho</p></td>
<td><p>O Monitor de desempenho foi descontinuado da caixa de ferramentas. Você ainda pode encontrar o Monitor de desempenho em <strong>Ferramentas administrativas</strong> no Windows Server 2008 e Windows Server 2012.</p></td>
</tr>
<tr class="even">
<td><p>Solução de problemas de desempenho</p></td>
<td><p>A solução de problemas de desempenho foi descontinuada da caixa de ferramentas.</p></td>
</tr>
<tr class="odd">
<td><p>Visualizador de Logs de Roteamento</p></td>
<td><p>O Visualizador de Log de roteamento foi descontinuado.</p></td>
</tr>
<tr class="even">
<td><p>Console de gerenciamento de pasta pública</p></td>
<td><p>Pastas públicas agora são gerenciadas no EAC. No EAC, vá para <strong>Pastas públicas</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Editor de usuário (RBAC) do controle de acesso baseado em função</p></td>
<td><p>RBAC agora é gerenciado no EAC. No EAC, vá para <strong>permissões</strong>.</p></td>
</tr>
</tbody>
</table>

