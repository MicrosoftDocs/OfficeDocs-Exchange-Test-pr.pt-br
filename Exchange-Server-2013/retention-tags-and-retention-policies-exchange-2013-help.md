---
title: 'Marcas e políticas de retenção: Exchange Online Help'
TOCTitle: Marcas e políticas de retenção
ms:assetid: 48c13be5-3f01-4849-a089-766210e54f89
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd297955(v=EXCHG.150)
ms:contentKeyID: 50485481
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Marcas e políticas de retenção

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

No Microsoft Exchange Server 2013 e no Exchange Online, o Gerenciamento de Registros de Mensagens (MRM) ajuda as organizações a gerenciar o ciclo de vida do email e reduzir os riscos legais associados a emails e outras comunicações. Com o MRM fica mais fácil manter mensagens necessárias para conformidade com políticas da empresa, regulamentações do governo ou necessidades legais, e remover conteúdo que não tenha valor legal ou de negócios.

Assista ao [vídeo](https://go.microsoft.com/fwlink/?linkid=825854) para uma visão geral sobre como aplicar uma política de retenção e marcas de retenção a uma caixa de correio no Exchange Online.

Você está procurando os procedimentos passo a passo para gerenciar MRM? Confira [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

**Sumário**

Estratégia de Gerenciamento de Registros de Mensagens

Marcas de retenção

Diretivas de retenção

Assistente de Pasta Gerenciada

Retenção

## Estratégia de Gerenciamento de Registros de Mensagens

O MRM do Exchange 2013 e do Exchange Online é feito com o uso de *marcas de retenção* e *políticas de retenção*. Antes de abordar os detalhes de cada um desses recursos de retenção, é importante saber como os recursos são usados em toda a estratégia de MRM. Essa estratégia é baseada no seguinte:

  - Atribuir de *marcas de diretiva de retenção* (RPTs) a pastas padrão, como Caixa de Entrada e Itens Excluídos.

  - Aplicação de DPTs (*marcas de política padrão*) a caixas de correio para gerenciar a retenção de todos os itens sem marca.

  - Permissão para o usuário atribuir *marcas pessoais* a pastas personalizadas e itens individuais.

  - Separação da funcionalidade de MRM a partir dos hábitos de gerenciamento e arquivamento da caixa de entrada do usuário. Os usuários não são obrigados a arquivar mensagens em pastas gerenciadas com base em requisitos de retenção. Mensagens individuais podem ter uma marca de retenção diferente em relação à aplicada à pasta em que estão localizadas.

A figura a seguir ilustra as tarefas envolvidas na implementação dessa estratégia.

![Usando Diretivas de Retenção para Retenção de Mensagens](images/Dd297955.429b51d5-51b8-4816-b8a4-221e0915d0c0(EXCHG.150).gif "Usando Diretivas de Retenção para Retenção de Mensagens")

Voltar ao início

## Marcas de retenção

Como mostrado na figura anterior, as marcas de retenção são usadas para aplicar configurações de retenção a pastas e itens individuais, como mensagens de email e caixa postal. Essas configurações especificam por quanto tempo uma mensagem fica em uma caixa de entrada e a ação a ser tomada quando a mensagem atinge o período de retenção especificado. Quando uma mensagem atinge seu período de retenção, ela é movida para Arquivo Morto In-loco do usuário ou excluída.

![Configurações em uma marca de retenção](images/Dd297955.936edd6a-8bc4-4c03-94a3-c240ffe7dd6a(EXCHG.150).png "Configurações em uma marca de retenção")

As marcas de retenção permitem que os usuários marquem suas próprias pastas de caixa de correio e itens individuais para retenção. Os usuários não precisam mais ter itens de arquivo em pastas gerenciadas fornecidas por um administrador com base nos requisitos de retenção de mensagens.

## Tipos de marcas de retenção

As marcas de retenção são classificadas nos três seguintes tipos com base em quem pode aplicá-las e onde elas podem ser aplicadas em uma caixa de correio.


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
<th>Tipo de marca de retenção</th>
<th>Aplicado...</th>
<th>Aplicado por...</th>
<th>Ações disponíveis...</th>
<th>Detalhes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Marca de política padrão (DPT)</p></td>
<td><p>Automaticamente à caixa de correio inteira</p>
<p>Um DPT aplica-se a itens <em>não marcados</em>, que são itens de caixa de correio que não têm uma marca de retenção aplicada diretamente ou por herança da pasta.</p></td>
<td><p>Administrador</p></td>
<td><ul>
<li><p>Mover para arquivo morto</p></li>
<li><p>Excluir e permitir recuperação</p></li>
<li><p>Excluir permanentemente</p></li>
</ul></td>
<td><p>Os usuários não podem alterar DPTs aplicados a uma caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p>Marca de diretiva de retenção (RPT)</p></td>
<td><p>Automaticamente para uma pasta padrão</p>
<p>Pastas padrão são pastas criadas automaticamente em todas as caixas de correio, por exemplo: <strong>Caixa de entrada</strong>, <strong>Itens excluídos</strong> e <strong>Itens enviados</strong>. Consulte a lista de pastas padrão com suporte em <a href="default-folders-that-support-retention-policy-tags-exchange-2013-help.md">Pastas padrão que suportam marcas de diretiva de retenção</a>.</p></td>
<td><p>Administrador</p></td>
<td><ul>
<li><p>Excluir e permitir recuperação</p></li>
<li><p>Excluir permanentemente</p></li>
</ul></td>
<td><p>Os usuários não podem alterar o relatório aplicado a uma pasta padrão.</p></td>
</tr>
<tr class="odd">
<td><p>Marca pessoal</p></td>
<td><p>Manualmente para itens e pastas</p>
<p>Os usuários podem automatizar a marcação usando regras de caixa de entrada para mover uma mensagem para uma pasta que contém uma marca específica ou aplicar uma marca pessoal à mensagem.</p></td>
<td><p>Usuários</p></td>
<td><ul>
<li><p>Mover para arquivo morto</p></li>
<li><p>Excluir e permitir recuperação</p></li>
<li><p>Excluir permanentemente</p></li>
</ul></td>
<td><p>Marcas pessoais permitem que os usuários determinem quanto tempo um item deve ser retido. Por exemplo, a caixa de correio pode ter um DPT para excluir itens em sete anos, mas os usuários podem criar uma exceção para itens como boletins informativos e notificações automatizadas, aplicando uma marca pessoal para excluí-los em três dias.</p></td>
</tr>
</tbody>
</table>


## Mais sobre marcas pessoais

Marcas pessoais estão disponíveis para usuários do Outlook 2010 e o Outlook Web App como parte das suas políticas de retenção. No Outlook 2010 e no Outlook Web App, as marcas pessoais com a ação **Mover para o arquivo morto** aparecem como **Política de arquivamento**, e as marcas pessoais com as ações **Excluir e Permitir Recuperação** ou **Excluir permanentemente** são exibidas como **Política de retenção**, conforme mostrado na figura a seguir.

![Marcas pessoais no Outlook 2010 e no Outlook Web App](images/Dd297955.2dbaee13-fdd0-4c30-b821-e662ce2587bb(EXCHG.150).gif "Marcas pessoais no Outlook 2010 e no Outlook Web App")

Os usuários podem aplicar marcas pessoais a pastas que eles criaram ou a itens individuais. As mensagens que têm uma marca pessoal aplicada sempre são processadas com base nas configurações da marca pessoal. Os usuários podem aplicar uma marca pessoal a uma mensagem para que ela seja movida ou excluída mais cedo ou mais tarde do que as configurações especificadas na DPT ou nas RPTs aplicadas à caixa de correio desse usuário. Também é possível criar marcas pessoais com a retenção desabilitada. Isso permite aos usuários marcar itens para que eles nunca sejam movidos para um arquivo morto ou nunca expirem.


> [!TIP]
> Os usuários podem aplicar políticas de arquivo morto a pastas padrão, pastas ou subpastas criadas pelos usuários e a itens individuais. Os usuários podem aplicar uma política de retenção a pastas ou subpastas criadas pelos usuários e a itens individuais (incluindo subpastas e itens em uma pasta padrão), mas não a pastas padrão.



Os usuários podem utilizar o Centro de Administração do Exchange (EAC) para selecionar marcas pessoais adicionais que não estejam vinculadas à sua política de retenção. As marcas selecionadas ficam disponíveis no Outlook 2010 e no Outlook Web App. Para permitir que os usuários selecionem marcas adicionais pelo EAC, adicione [Função MyRetentionPolicies](myretentionpolicies-role-exchange-2013-help.md) à política de atribuição de função do usuário. Para saber mais sobre as políticas de atribuição de funções para usuários, consulte [Noções básicas sobre diretivas de atribuição de função de gerenciamento](understanding-management-role-assignment-policies-exchange-2013-help.md). Se você permitir que os usuários selecionem marcas pessoais adicionais, todas as marcas pessoais em sua organização do Exchange ficam à disposição deles.


> [!TIP]
> As marcas pessoais são um recurso premium. As caixas de correio com políticas que incluam essas marcas (ou resultantes da adição dessas marcas às caixas de correio por parte dos usuários) exigem uma CAL (licença de acesso para cliente) do Exchange Enterprise.



Voltar ao início

## Tempo de retenção

Quando você habilita uma marca de retenção, você deve especificar um tempo de retenção para a marca. Esse tempo indica o número de dias para reter uma mensagem após ela chegar na caixa de correio do usuário.

O tempo de retenção para itens não recorrentes (como emails) é calculado de maneira diferente dos itens que têm uma data final ou itens recorrentes (como reuniões e tarefas). Para saber como o tempo de retenção é calculado para tipos diferentes de itens, consulte [Como a idade de retenção é calculada](how-retention-age-is-calculated-exchange-2013-help.md).

Você pode também criar marcas de retenção com a retenção desabilitada ou desabilitar as marcas após elas serem criadas. Como as mensagens com uma marca desabilitada aplicada não são processadas, nenhuma ação de retenção é executada. Como resultado, os usuários podem utilizar uma marca pessoal desabilitada como uma marca **Nunca Mover** ou **Nunca Excluir** para substituir uma DPT ou RPT que de outra forma se aplicaria à mensagem.

## Ações de retenção

Ao criar ou configurar uma marca de retenção, você pode selecionar uma das seguintes ações de retenção a serem executadas quando um item alcançar seu tempo de retenção:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Ação de retenção</th>
<th>Ação executada...</th>
<th>Exceto...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Mover para arquivo morto</strong> 1</p></td>
<td><ul>
<li><p>Move a mensagem para a caixa de correio de arquivo morto do usuário</p></li>
<li><p>Disponível somente para DPTs e marcas pessoais</p></li>
</ul>
<p>Para obter detalhes sobre o arquivamento, consulte:</p>
<ul>
<li><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Arquivamento In-loco do Exchange 2013</a></p></li>
<li><p><a href="https://technet.microsoft.com/pt-br/library/dn922147(v=exchg.150)">Caixas de correio de arquivo morto no Exchange Online</a></p></li>
</ul></td>
<td><ul>
<li><p>Se o usuário não tiver uma caixa de correio de arquivo morto, nenhuma ação será executada.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Excluir e permitir recuperação</strong></p></td>
<td><ul>
<li><p>Emula o comportamento quando o usuário esvazia a pasta Itens Excluídos.</p></li>
<li><p>Os itens são movidos para <a href="recoverable-items-folder-exchange-2013-help.md">Pasta Itens Recuperáveis</a> na caixa de correio e preservados até o período de <em>retenção de itens excluídos</em>.</p></li>
<li><p>Fornece aos usuários uma segunda chance de recuperar o item usando a caixa de diálogo <strong>Recuperar Itens Excluídos</strong> no Outlook ou no Outlook Web App</p></li>
</ul></td>
<td><ul>
<li><p>Se você definiu o período de retenção de item excluído como zero dias, os itens serão excluídos permanentemente. Para obter detalhes, consulte <a href="https://technet.microsoft.com/pt-br/library/dn163584(v=exchg.150)">Alterar quanto tempo os itens permanentemente excluídos são mantidos em uma caixa de correio do Exchange Online</a>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Excluir permanentemente</strong></p></td>
<td><ul>
<li><p>Exclui permanentemente as mensagens.</p></li>
<li><p>Você não pode recuperar as mensagens depois de elas serem excluídas permanentemente.</p></li>
</ul></td>
<td><ul>
<li><p>Se a caixa de correio for colocada em <a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Retenção local e Retenção de litígio</a> ou Retenção de Litígio, os itens serão preservados na pasta Itens Recuperáveis com base em parâmetros de retenção. <a href="in-place-ediscovery-exchange-2013-help.md">Descoberta Eletrônica In-loco</a> ainda retornará esses itens nos resultados da pesquisa.</p>
<p></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Marcar como fora do limite de retenção</strong></p></td>
<td><ul>
<li><p>Marca uma mensagem como expirada. No Outlook 2010 ou posterior, e no Outlook Web App, os itens expirados são exibidos com a notificação informando &quot;Este item expirou&quot; e &quot;Este item expirará em 0 dias&quot;. No Outlook 2007, os itens marcados como expirados são exibidos usando texto tachado.</p></li>
</ul></td>
<td><p>N. A.</p></td>
</tr>
</tbody>
</table>



> [!TIP]
> 1&nbsp;&nbsp;&nbsp;Em uma implantação híbrida do Exchange, você pode habilitar uma caixa de correio de arquivo morto baseada em nuvem para uma caixa de correio principal local. Se você atribuir uma política de arquivo morto a uma caixa de correio local, os itens serão transferidos para o arquivo morto baseado em nuvem. Se um item for transferido para a caixa de correio de arquivo morto, nenhuma cópia será mantida na caixa de correio local. Se a caixa de correio local for colocada em espera, uma política de arquivo morto ainda moverá os itens para a caixa de correio de arquivo morto baseada em nuvem, na qual serão preservados durante o período especificado pela retenção.



Para detalhes sobre como criar marcas de retenção, consulte [Criar uma política de retenção](create-a-retention-policy-exchange-2013-help.md).

Voltar ao início

## Diretivas de retenção

Para aplicar um ou mais marcas de retenção a uma caixa de correio, adicione as marcas a uma política de retenção e depois aplique a política às caixas de correio. Uma caixa de correio não pode ter mais de uma diretiva de retenção. As marcas de retenção podem ser vinculadas a uma política de retenção ou desvinculadas dela a qualquer momento, e as alterações automaticamente entram em vigor para todas as caixas de correio que tenham a política aplicada.

Uma diretiva de retenção pode ter as seguintes marcas de retenção:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de marca de retenção</th>
<th>Marcas em uma política</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Marca de política padrão (DPT)</p></td>
<td><ul>
<li><p>Uma DPT com a ação <strong>Mover para Arquivo Morto</strong></p></li>
<li><p>Uma DPT com a ação <strong>Excluir e Permitir Recuperação</strong> ou <strong>Excluir Permanentemente</strong></p></li>
<li><p>Uma DPT para mensagens de caixa postal com as ações <strong>Excluir e Permitir Recuperação</strong> ou <strong>Excluir Permanentemente</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Marcas de diretiva de retenção (RPTs)</p></td>
<td><ul>
<li><p>Um RPT para cada pasta padrão com suporte</p>

> [!TIP]
> Não é possível vincular mais de uma RPT para uma pasta padrão particular (como <STRONG>Itens Excluídos</STRONG>) à mesma política de retenção.


</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Marcas pessoais</p></td>
<td><ul>
<li><p>Qualquer número de marcas pessoais</p></li>
</ul>

> [!TIP]
> Muitas marcas pessoais de uma política podem confundir os usuários. Recomendamos adicionar no máximo 10 marcas pessoais a uma diretiva de retenção.


</td>
</tr>
</tbody>
</table>



> [!TIP]
> Embora uma diretiva de retenção não precise ter nenhuma marca de retenção vinculada a ela, não recomendamos usar esse cenário. Se as caixas de correio com políticas de retenção não tiverem marcas de retenção vinculadas a elas, isso poderá fazer com que os itens de caixa de correio nunca expirem.



Uma política de retenção pode conter marcas de arquivo morto (marcas que movem itens para a caixa de correio de arquivo morto pessoal) e marcas de exclusão (marcas que excluem itens). Um item de caixa de correio pode ter também ambos os tipos de marcas aplicados. As caixas de correio de arquivo morto não têm uma política de retenção separada. A mesma política de retenção é aplicada à caixa de correio principal e de arquivo morto.

Ao planejar criar políticas de retenção, você deve considerar se elas incluirão as marcas de arquivo morto e exclusão. Como mencionado antes, uma política de retenção pode ter uma DPT que usa a ação **Mover para Arquivo Morto** e uma DPT que usa a ação **Excluir e Permitir Recuperação** ou **Excluir Permanentemente**. A DPT com a ação **Mover para Arquivo Morto** deve ter um tempo de retenção inferior à DPT com uma ação de exclusão. Por exemplo, você pode usar uma DPT com a ação **Mover para Arquivo Morto** para mover itens para a caixa de correio de arquivo morto em dois anos, e uma DPT com uma ação de exclusão para remover itens da caixa de correio em sete anos. Itens nas caixas de correio principal e de arquivo morto serão excluídas após sete anos.

Para uma lista de tarefas de gerenciamento relacionadas a políticas de retenção, consulte [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

## Política de retenção padrão

A instalação do Exchange cria a política de retenção **Política MRM Padrão**. A política MRM padrão é aplicada automaticamente a novas caixas de correio em Exchange Online. No Exchange Server, a política será aplicada automaticamente se você criar um arquivo morto para o novo usuário e não especificar uma política de retenção

Você pode modificar as marcas incluídas na política MRM padrão, por exemplo, alterando a idade de retenção ou a ação de retenção, desabilitar uma marca ou modificar a política adicionando ou removendo marcas dela. A política atualizada é aplicada às caixas de correio na próxima vez em que elas forem processadas pelo Assistente de Pasta Gerenciada.

Para obter mais detalhes, incluindo uma lista de marcas de retenção vinculadas à política, consulte [Política de retenção padrão no Exchange Online e Exchange Server](default-retention-policy-in-exchange-online-and-exchange-server-exchange-2013-help.md).

Voltar ao início

## Assistente de Pasta Gerenciada

O Assistente de Pasta Gerenciada, um assistente de caixa de correio executado em servidores de Caixa de Correio, processa caixas de correio que tenham uma política de retenção aplicada.

O Assistente de Pasta Gerenciada aplica a política de retenção inspecionando itens na caixa de correio e determinando se eles estão sujeitos à retenção. Em seguida, ele marca os itens sujeitos à retenção com as marcas de retenção apropriadas e usa a ação de retenção especificada em itens que atingiram seu período de retenção.

O Assistente de Pasta Gerenciada é um assistente baseado em limitação. Esses assistentes estão sempre em execução e não precisam ser programados. Os recursos do sistema que eles consomem são limitados. Você pode configurar o Assistente de Pasta Gerenciada para processar todas as caixas de correio em um servidor de Caixa de Correio dentro de um determinado período (conhecido como um *ciclo de trabalho*). Além disso, em um intervalo específico (conhecido como o *ponto de verificação do ciclo de trabalho*), o assistente atualiza a lista de caixas de correio a serem processadas. Durante a atualização, o assistente adiciona as caixas de correio movidas ou recém-criadas à fila. Ele também redefine a prioridade das caixas de correio existentes que não foram processadas com êxito devido a falhas e as move mais para cima na fila para que possam ser processadas durante o mesmo ciclo de trabalho.

Você pode também usar o cmdlet [Start-ManagedFolderAssistant](https://technet.microsoft.com/pt-br/library/aa998864\(v=exchg.150\)) para disparar manualmente o assistente para que processe uma caixa de correio especificada. Para obter mais informações, consulte [Configurar o Assistente de pasta gerenciada](configure-the-managed-folder-assistant-exchange-2013-help.md).


> [!TIP]
> O Assistente de Pasta Gerenciada não executa nenhuma ação nas mensagens não sujeitas à retenção, o que é especificado desabilitando a marca de retenção. Você pode também desabilitar uma marca de retenção para impedir temporariamente que itens com essa marca sejam processados.



## Mover itens entre pastas

Um item de caixa de correio movido de uma pasta para outra herda todas as marcas aplicadas à pasta para a qual é movido. Se um item for movido para uma pasta que não tenha uma marca atribuída, a DPT será aplicada a ela. Se o item tiver uma marca explicitamente atribuída a ele, a marca sempre prevalecerá sobre qualquer outra marca em nível de pasta ou sobre a marca padrão.

## Aplicar uma marca de retenção a uma pasta no arquivo morto

Quando o usuário aplica uma marca pessoal a uma pasta do arquivo morto, se houver uma pasta com o mesmo nome na caixa de correio principal e esta tiver uma marca diferente, a marca na pasta do arquivo morto mudará para coincidir com a da caixa de correio principal. Isso é projetado para evitar qualquer confusão sobre itens em uma pasta no arquivo morto que podem vir a ter comportamento de expiração diferente do que a mesma pasta na caixa de correio principal do usuário. Por exemplo, o usuário tem uma pasta denominada Projeto Contoso na caixa de correio principal com uma marca *Excluir – 3 anos* e uma pasta Projeto Contoso também existe na caixa de correio de arquivo morto. Se o usuário aplicar uma marca pessoal *Excluir – 1 ano* para excluir itens na pasta depois de 1 ano, quando a caixa de correio for processada novamente, a pasta será revertida para a marca Excluir – 3 anos.

## Remover ou excluir uma marca de retenção de uma política de retenção

Quando uma marca de retenção é removida da diretiva de retenção aplicada a uma caixa de correio, a marca não fica mais disponível ao usuário e não pode ser aplicada aos itens da caixa de correio.

Os itens existentes que receberam essa marca continuam sendo processados pelo Assistente de Pasta Gerenciada com base nessas configurações, e qualquer ação de retenção especificada na marca é aplicada a essas mensagens.

Entretanto, se você excluir a marca, a definição de marca armazenada no Active Directory será removida. Isso faz com que o Assistente de Pasta Gerenciada processe todos os itens de uma caixa de correio e marque novamente os que têm a marca removida aplicada. Dependendo do número de caixas de correio e mensagens, esse processo poderá resultar em um consumo significativo de recursos em todos os servidores de Caixa de Correio que contêm caixas de correio com diretivas de retenção que incluem a marca removida.


> [!IMPORTANT]
> Se uma marca de retenção for removida de uma diretiva de retenção, qualquer item de caixa de correio existente com a marca aplicada continuará a expirar com base nas configurações da marca. Para impedir que as configurações da marca sejam aplicadas a algum item, essa marca deverá ser excluída. A exclusão de uma marca a remove de quaisquer diretivas de retenção em que está presente.



## Desabilitar uma marca de retenção

Se você desabilitar a marca de retenção, o Assistente de Pasta Gerenciada ignorará os itens que tenham essa marca aplicada. Os itens que tenham uma marca de retenção para a qual a retenção está desabilitada não são nunca movidos ou excluídos, dependendo da ação de retenção especificada. Como esses itens ainda são considerados itens com marca, a DPT não é aplicada a eles. Por exemplo, se quiser solucionar problemas das configurações de marca de retenção, você poderá desabilitar temporariamente uma marca de retenção para impedir que o Assistente de Pasta Gerenciada processe mensagens com essa marca.


> [!TIP]
> O período de retenção de uma marca de retenção desabilitada é exibido ao usuário como <STRONG>Nunca</STRONG>. Se o usuário marcar um item acreditando que ele nunca será excluído, habilitar a marca posteriormente poderá resultar em exclusão não intencional de itens que o usuário não queria excluir. O mesmo é verdadeiro para marcas com a ação <STRONG>Mover para Arquivo Morto</STRONG>.



Voltar ao início

## Retenção

Quando os usuários ficam temporariamente afastados do trabalho e não têm acesso ao seu email, as configurações de retenção poderão ser aplicadas a novas mensagens antes de eles retornarem ao trabalho. Dependendo da diretiva de retenção, as mensagens podem ser excluídas ou movidas para o arquivo morto pessoal do usuário. Você pode impedir temporariamente que as diretivas de retenção processem uma caixa de correio por um determinado período colocando a caixa de correio em retenção. Ao colocar uma caixa de correio em retenção, você poderá também especificar um comentário de retenção informando o usuário de caixa de correio (ou outro usuário autorizado a acessar a caixa de correio) sobre a retenção, incluindo quando a retenção está programada para iniciar e terminar. Comentários de retenção são exibidos em clientes com suporte do Outlook. Você pode também localizar o comentário de retenção no idioma preferido do usuário.


> [!TIP]
> Colocar uma caixa de correio em retenção não afeta o modo como as cotas de armazenamento de caixa de correio são processadas. Dependendo do uso da caixa de correio e das cotas de caixa de correio aplicáveis, considere aumentar temporariamente a cota de armazenamento da caixa de correio para os usuários quando eles estiverem em férias ou não tiverem acesso ao email por um longo período. Para obter mais informações sobre as cotas de armazenamento de caixa de correio, consulte <A href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configurar cotas de armazenamento para uma caixa de correio</A>.



Durante as longas ausências do trabalho, os usuários podem acumular uma grande quantidade de email. Dependendo do volume de email e do tempo de ausência, esses usuários podem levar várias semanas para classificar suas mensagens. Nesses casos, considere o tempo adicional que pode ser necessário para que os usuários fiquem em dia com seus emails antes de remover essas mensagens da retenção.

Caso a sua organização nunca tenha implementado MRM e seus usuários não estejam familiarizados com os recursos, você poderá também usar as retenções durante a fase inicial de *preparação e treinamento* de sua implantação de MRM. Você pode criar e implantar políticas de retenção e treinar os usuários sobre as políticas sem o risco de ter itens movidos ou excluídos antes que os usuários possam marcá-los. Alguns dias antes do período de preparação e treinamento terminar, você deverá lembrar os usuários do prazo de preparação. Após o prazo, você poderá remover a retenção das caixas de correio do usuário, permitindo que o Assistente de Pasta Gerenciada processe os itens de caixa de correio e executem a ação de retenção especificada.

Para obter detalhes sobre como colocar uma caixa de correio em retenção, consulte [Retenção local de uma caixa de correio em retenção](place-a-mailbox-on-retention-hold-exchange-2013-help.md).

Voltar ao início

