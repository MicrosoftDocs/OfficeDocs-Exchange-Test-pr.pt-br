---
title: 'Pastas padrão que suportam marcas de diretiva de retenção: Exchange 2013 Help'
TOCTitle: Pastas padrão que suportam marcas de diretiva de retenção
ms:assetid: d2e2064f-4102-4018-b688-504d09da6d39
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn783294(v=EXCHG.150)
ms:contentKeyID: 62835911
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pastas padrão que suportam marcas de diretiva de retenção

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2017-04-20_

Você pode usar [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md) para gerenciar o ciclo de vida de email. Políticas de retenção contêm marcas de retenção, que são configurações que você pode usar para especificar quando uma mensagem deve ser movida automaticamente para o arquivo morto ou quando ele deve ser excluído.

Uma marca de política de retenção (RPT) é um tipo de marca de retenção que você pode aplicar às pastas padrão em uma caixa de correio, **caixa de entrada** e **Itens excluídos**.

![Crie uma RPT (Marca de Política de Retenção)](images/Dn783294.b59a96fd-94e1-4c9b-bff6-97a1bd98dfe7(EXCHG.150).png "Crie uma RPT (Marca de Política de Retenção)")

## Pastas padrão com suporte

Você pode criar RPTs para as pastas padrão mostradas na tabela a seguir.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome da pasta</th>
<th>Detalhes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Arquivo morto</p></td>
<td><p>Essa pasta é o destino padrão para mensagens arquivadas com o botão de arquivo morto no Outlook. O recurso de arquivamento oferece uma maneira rápida para que os usuários removam mensagens da sua caixa de entrada sem excluí-las.</p>
<p>Este RPT está disponível somente no Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p>Calendário</p></td>
<td><p>Essa pasta padrão é usada para armazenar compromissos e reuniões.</p></td>
</tr>
<tr class="odd">
<td><p>Email secundário</p></td>
<td><p>Essa pasta contém mensagens de email que estão baixa prioridade. Desorganização analisa o que foi feito no passado para determinar as mensagens que provavelmente ignorar. Ele move essas mensagens para a pasta <strong>desorganização</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Histórico de Conversa</p></td>
<td><p>Essa pasta é criada pelo Microsoft Lync (anteriormente Microsoft Office Communicator). Embora não tratada como uma pasta padrão pelo Outlook, ela é tratada como uma pasta especial pelo Exchange e pode ter RPTs aplicadas.</p></td>
</tr>
<tr class="odd">
<td><p>Itens Excluídos</p></td>
<td><p>Essa pasta padrão é usada para armazenar itens excluídos de outras pastas na caixa de correio. Os usuários do Outlook e do Outlook Web App podem esvaziar essa pasta manualmente. Os usuários podem também configurar o Outlook para esvaziar a pasta no fechamento do Outlook.</p></td>
</tr>
<tr class="even">
<td><p>Rascunhos</p></td>
<td><p>Essa pasta padrão é usada para armazenar mensagens de rascunho que ainda não foram enviadas pelo usuário. O Outlook Web App também usa essa pasta para salvar mensagens que foram enviadas pelo usuário, mas não enviadas ao servidor de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de Entrada</p></td>
<td><p>Essa pasta padrão é usada para armazenar mensagens entregues a uma caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p>Diário</p></td>
<td><p>Essa pasta padrão contém ações selecionadas pelo usuário. Essas ações são automaticamente gravadas pelo Outlook e colocadas em uma exibição de linha de tempo.</p></td>
</tr>
<tr class="odd">
<td><p>Lixo Eletrônico</p></td>
<td><p>Essa pasta padrão é usada para salvar mensagens marcadas como lixo eletrônico pelo filtro de conteúdo em um servidor do Exchange ou por um filtro antispam no Outlook.</p></td>
</tr>
<tr class="even">
<td><p>Notas</p></td>
<td><p>Essa pasta contém notas criadas pelos usuários no Outlook. Essas notas estão também visíveis no Outlook Web App.</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de Saída</p></td>
<td><p>Essa pasta padrão é usada para armazenar mensagens temporariamente enviadas pelo usuário até elas serem enviadas a um servidor de Transporte de Hub. Uma cópia das mensagens enviadas é salva na pasta padrão Itens Enviados. Como as mensagens geralmente permanecem nessa pasta por um breve período, não é necessário criar uma RPT para essa pasta.</p></td>
</tr>
<tr class="even">
<td><p>Alimentações RSS</p></td>
<td><p>Essa pasta padrão contém feeds RSS.</p></td>
</tr>
<tr class="odd">
<td><p>Itens Recuperáveis</p></td>
<td><p>Esta é uma pasta oculta na árvore sub-recurso Non-IPM. Ele contém as subpastas exclusões, versões, limpezas, DiscoveryHolds e auditorias. Marcas de retenção para essa pasta mover itens da pasta itens recuperáveis na caixa de correio principal do usuário para a pasta itens recuperáveis em correio de arquivo morto do usuário. Você pode atribuir a ação de retenção <strong>Mover para arquivo morto</strong> para marcas particulares para essa pasta. Para saber mais, consulte <a href="recoverable-items-folder-exchange-2013-help.md">Pasta Itens Recuperáveis</a>.</p></td>
</tr>
<tr class="even">
<td><p>Itens Enviados</p></td>
<td><p>Essa pasta padrão é usada para armazenar mensagens enviadas a um servidor de Transporte de Hub.</p></td>
</tr>
<tr class="odd">
<td><p>Problemas de Sincronização</p></td>
<td><p>Essa pasta contém os logs de sincronização. Para saber mais, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=198215">pastas de erro de sincronização</a>.</p></td>
</tr>
<tr class="even">
<td><p>Tarefas</p></td>
<td><p>Essa pasta padrão é usada para armazenar tarefas. Para criar um RPT para a pasta de tarefas, você precisará usar o Shell de Gerenciamento do Exchange. Para obter mais informações, consulte <a href="https://technet.microsoft.com/pt-br/library/dd335226(v=exchg.150)">New-RetentionPolicyTag</a>. Depois que o RPT para a pasta tarefas é criado, você pode gerenciá-lo usando o Centro de administração do Exchange.</p></td>
</tr>
</tbody>
</table>


## Mais Informações

  - RPTs são marcas de retenção para pastas padrão. Você só pode selecionar uma ação de excluir para RPTs – a **Excluir e permitir recuperação** ou **Excluir permanentemente**.

  - Não é possível criar uma RPT para mover mensagens para o arquivo morto. Para mover itens antigos para arquivo morto, você pode criar uma *Marca de política padrão* (DPT), que se aplica à caixa de correio inteira, ou *Marcas pessoais*, que são exibidos no Outlook e Outlook Web App (OWA) como políticas de arquivamento. Os usuários podem aplicá-las a pastas ou mensagens individuais.

  - Não é possível aplicar RPTs à pasta Contatos.

  - Você só pode adicionar um RPT para uma pasta padrão particular a uma política de retenção. Por exemplo, se uma política de retenção tiver uma marca de caixa de entrada, não é possível adicionar outra RPT do tipo de caixa de entrada para essa política de retenção.

  - Para saber como criar RPTs ou outros tipos de marcas de retenção e adicioná-los a uma política de retenção, consulte [Criar uma política de retenção](create-a-retention-policy-exchange-2013-help.md).

  - Em Exchange 2013 e Exchange Online, um DPT também se aplica às pastas padrão **calendário** e **tarefas** . Isso pode resultar em itens que está sendo excluído ou movido para o arquivo morto baseado nas configurações DPT. Para evitar que as configurações de DPT excluam itens nessas pastas, crie RPTs à retenção desabilitada. Para evitar que as configurações do DPT da movimentação de itens em uma pasta padrão, você pode criar um a marca pessoal desabilitada com a mudança para arquivar ação, adicioná-lo à diretiva de retenção e então tiver usuários aplicá-la à pasta padrão. Para obter detalhes, consulte [impedir o arquivamento de itens em uma pasta padrão no Exchange 2010](https://go.microsoft.com/fwlink/?linkid=511071).

