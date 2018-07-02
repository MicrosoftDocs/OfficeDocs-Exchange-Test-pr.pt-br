---
title: 'Arquivamento In-loco do Exchange 2013: Exchange 2013 Help'
TOCTitle: Arquivamento In-loco do Exchange 2013
ms:assetid: b5e4c0e9-0558-4b90-bc12-f67adbfb59ac
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd979800(v=EXCHG.150)
ms:contentKeyID: 50486461
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Arquivamento In-loco do Exchange 2013

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

O *Arquivo Morto In-Loco* ajuda você a recuperar o controle dos dados de mensagem da organização, eliminando a necessidade de arquivos de armazenamento pessoal (.pst) e permitindo que os usuários armazenem as mensagens em uma *caixa de correio de arquivo morto* que seja acessível pelo MicrosoftOutlook 2010 e posterior e pelo Microsoft OfficeOutlook Web App.

No Microsoft Exchange Server 2013, o Arquivo Morto In-Loco oferece aos usuários um local de armazenamento alternativo onde eles podem armazenar dados de histórico de mensagens. O Arquivo Morto In-Loco é uma caixa de correio adicional (conhecida como correio de arquivo morto) habilitada para usuários de caixas de correio. Os usuários do Outlook 2007 e mais recentes e do Outlook Web App têm acesso bem integrado às suas caixas de correio de arquivo morto. Usando qualquer desses aplicativos clientes, os usuários podem ver uma caixa de correio de arquivo morto e mover ou copiar mensagens entre a caixa de correio principal e o arquivo morto. O Arquivo Morto In-Loco apresenta uma visão consistente de dados de mensagem aos usuários e elimina a sobrecarga de usuários necessária para gerenciar arquivos .pst.

Você pode oferecer um arquivo morto de usuário no mesmo banco de dados de caixa de correio que abriga a caixa de correio principal do usuário, em outro banco de dados de caixa de correio ou em um banco de dados de caixa de correio em outro servidor de Caixa de Correio no mesmo site do Active Directory. Em implantações híbridas do Exchange 2010 ou versão posterior, também é possível provisionar um arquivo morto baseado em nuvem para caixas de correio localizadas em seus servidores locais de Caixa de Correio.

**Sumário**

Messaging data and .pst files

Client access to archive mailboxes

Delegate access

Moving messages to the archive mailbox

Archive and retention policies

Default MRM policy

Archive quotas

In-Place Archives and other Exchange features

Managing archive mailboxes

## Dados de mensagens e arquivos .pst

O Outlook usa arquivos .pst para armazenar dados localmente em computadores de usuários ou compartilhamentos de rede. Diferente dos arquivos de armazenamento offline (.ost) usados pelo Outlook no modo cache do Exchange para armazenar uma cópia da caixa de correio para acesso offline, os arquivos .pst não são sincronizados com a caixa de correio do Exchange do usuário. Se um usuário mover mensagens para um arquivo .pst, essas mensagens são removidas da caixa de correio.

O uso de arquivos .pst para gerenciar dados de mensagens pode resultar nos seguintes problemas:

  - **Arquivos não gerenciados**   Geralmente, os arquivos .pst são criados por usuários e residem em seus computadores ou compartilhamentos de rede. Eles não são gerenciados por sua organização. Com isso, os usuários podem criar vários arquivos .pst contendo as mesmas mensagens ou mensagens diferentes e armazená-las em locais diferentes, sem controle organizacional.

  - **Custos maiores de descoberta**   Ações legais e alguns requisitos de regulamentação ou negócios por vezes resultam em solicitações de descoberta. Localizar os dados de mensagem que residem em arquivos .pst nos computadores dos usuários pode ser um esforço manual caro. Como monitorar arquivos .pst não-gerenciados pode ser difícil, os dados .pst podem não ser descobertos, em muitos casos. Possivelmente, isso pode expor sua organização a riscos legais e financeiros.

  - **Impossibilidade de aplicar diretivas de retenção de mensagens**   As diretivas de retenção de mensagens não podem ser aplicadas a mensagens localizadas em arquivos .pst. Como resultado, dependendo das regulamentações de negócios ou aplicáveis, sua organização pode não estar em conformidade.

  - **Risco de roubo de dados**   Dados de mensagens que são armazenados em arquivos .pst estão vulneráveis a roubo de dados. Por exemplo, os arquivos .pst são frequentemente armazenados em dispositivos portáteis, como laptops, discos rígidos removíveis e mídias portáteis, como unidades USB, CDs e DVDs.

  - **Exibição fragmentada de dados de mensagem**   Usuários que armazenam informações em arquivos .pst não têm uma visão uniforme de seus dados. As mensagens armazenadas em arquivos .pst geralmente só estão disponíveis no computador onde o arquivo .pst reside. Com isso, quando os usuários acessam suas caixas de correio usando o Outlook Web App ou o Outlook em outro computador, as mensagens armazenadas em seus arquivos .pst ficam inacessíveis.

## Acesso para Cliente a caixas de correio de arquivo morto

A tabela a seguir lista os aplicativos cliente que podem ser usados para acessar caixas de correio de arquivo morto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cliente</th>
<th>Acesso à caixa de correio de arquivo morto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013, Outlook 2010, Outlook 2007 e Outlook Web App</p></td>
<td><p>Sim. Os usuários do Outlook 2013, Outlook 2010, Outlook 2007 e do Outlook Web App podem copiar ou mover itens de suas caixas de correio principais para suas caixas de correio de arquivo morto, e também usar políticas de retenção para mover itens para o arquivo morto.</p>

> [!TIP]
> Outlook 2010 e posterior e os usuários do Outlook 2007 também podem copiar ou mover itens de arquivos. pst para suas caixas de correio de arquivo morto. Os usuários do Outlook 2007 exigem a atualização cumulativa do Office 2007 de fevereiro de 2011. Existem algumas diferenças no suporte de arquivamento entre o Outlook 2007 e o Outlook 2010 e posterior. Para obter mais informações, consulte o artigo de Blog da equipe do Exchange, consulte <A href="https://blogs.technet.com/b/exchange/archive/2010/12/20/3411710.aspx">Sim Virgínia, há suporte do Exchange 2010 arquivo morto no Outlook 2007</A>.


</td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><p>Não</p></td>
</tr>
</tbody>
</table>



> [!TIP]
> Arquivamento in-loco é um recurso premium e requer uma licença de acesso de cliente do Exchange Enterprise (CAL). Para obter detalhes sobre como licença Exchange, consulte <A href="https://go.microsoft.com/fwlink/?linkid=237292">Licenciamento do Exchange Server</A>. Para obter detalhes sobre as versões do Outlook necessárias para acessar uma caixa de correio de arquivo morto, consulte <A href="https://go.microsoft.com/fwlink/?linkid=237276">requisitos de licença para arquivo pessoal e políticas de retenção</A>.



O Outlook não cria uma cópia local da caixa de correio de arquivo morto no computador de um usuário, mesmo que esteja configurado para usar o Modo Cache do Exchange. Os usuários podem acessar uma caixa de correio de arquivo morto apenas em modo online.

## Acesso de representante

*Acesso de representante* é quando um usuário ou um conjunto de usuários recebe acesso à caixa de correio de outro usuário. Há vários cenários para o fornecimento de acesso de representante, incluindo:

  - Fornecer a um ou mais usuários o acesso à caixa de correio de um usuário que não é mais empregado da organização. Nesse caso, os usuários que podem receber o acesso de representante incluem o gerente ou supervisor do usuário que deixou a empresa, ou outro usuário que vá assumir as responsabilidades desse usuário.

  - Fornecer a um ou mais usuários o acesso a uma caixa de correio compartilhada.

  - Fornecer a assistentes executivos o acesso às caixas de correio dos executivos que eles estão auxiliando.

No Exchange 2013, ao atribuir permissões de Acesso Completo a uma caixa de correio, o representante ao qual você atribui as permissões também pode acessar o arquivo morto do usuário. Os representantes precisam usar o Outlook para acessar a caixa de correio, e precisam se conectar a um servidor de Acesso para Cliente do Exchange 2010 SP1 ou posterior para fins de Descoberta Automática. A Descoberta Automática é um serviço do Exchange que fornece definições para a configuração automática de clientes do Outlook. Quando os representantes usam o Outlook para acessar uma caixa de correio do Exchange 2013, tanto a caixa de correio principal quanto o arquivo morto aos quais eles têm acesso são visíveis pelo Outlook.

## Movendo mensagens para a caixa de correio de arquivo morto

Existem várias maneiras de se mover mensagens para caixas de correio de arquivo morto:

  - **Mover ou copiar mensagens manualmente**   Os usuários de caixa de correio podem mover ou copiar mensagens manualmente de suas caixas de correio principais ou de um arquivo .pst para suas caixas de correio de arquivo morto. A caixa de correio de arquivo morto aparece como outra caixa de correio ou arquivo .pst no Outlook e no Outlook Web App.

  - **Mover ou copiar mensagens usando regras de caixa de entrada**   Os usuários de caixa de correio podem criar regras de caixa de entrada no Outlook ou no Outlook Web App para mover mensagens automaticamente para uma pasta na caixa de correio de arquivo morto. Para saber mais, consulte [Aprender sobre regras de caixa de entrada](http://help.outlook.com/pt-br/140/bb899620.aspx).

  - **Mover mensagens usando políticas de retenção**   É possível usar políticas de retenção para mover mensagens automaticamente para o arquivo morto. Os usuários também podem aplicar uma marca pessoal para mover mensagens para o arquivo morto. Para obter detalhes sobre as políticas de arquivo morto e retenção, consulte Archive and retention policies mais adiante neste tópico.
    

    > [!TIP]
    > Marcas pessoais estão disponíveis somente no Outlook Web App e no Outlook 2010 e posteriores.



  - **Importar mensagens de arquivos .pst**   No Exchange 2013, você pode usar uma solicitação de importação de caixa de correio para importar mensagens de um arquivo .pst para o arquivo morto ou caixa de correio principal de um usuário. Para obter detalhes, confira [Solicitações de importação e exportação da caixa de correio](mailbox-import-and-export-requests-exchange-2013-help.md). Você também pode usar a ferramenta de Captura PST para pesquisar arquivos .pst em computadores em sua organização e importar dados de arquivos .pst para os arquivos mortos dos usuários.

## Políticas de arquivo morto e retenção

No Exchange 2013, é possível aplicar políticas de arquivo morto a uma caixa de correio para mover automaticamente mensagens de uma caixa de correio principal de um usuário para a caixa de correio de arquivo morto, após um período específico. As políticas de arquivo morto são implementadas criando-se marcas de retenção que usam a ação de retenção **Mover para o arquivo morto**.

As mensagens são movidas para uma pasta na caixa de correio de arquivo morto que tem o mesmo nome da pasta de origem na caixa de correio principal. Se uma pasta com o mesmo nome não existir na caixa de correio de arquivo morto, ela será criada quando o Assistente de Pasta Gerenciada mover uma mensagem. A recriação da mesma hierarquia de pastas na caixa de correio de arquivo morto ajuda os usuários a localizarem as mensagens mais facilmente.

Para saber mais sobre políticas de retenção, marcas de retenção e a ação de retenção **Mover para o arquivo morto**, consulte [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md).

## Diretiva padrão de MRM

A configuração do Exchange 2013 cria um arquivo morto padrão e uma política de retenção denominada **Política MRM Padrão**. Essa política contém marcas de retenção que contêm a ação **Mover para o arquivo morto**, como mostra a tabela a seguir.


> [!TIP]
> No Exchange 2010, a política padrão de arquivo morto e retenção criada pela instalação do Exchange é nomeada como <STRONG>Política de arquivo morto e de retenção padrão</STRONG>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome da marcação de retenção</th>
<th>Tipo de marca</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Movimentação de 2 anos para arquivo padrão</strong></p></td>
<td><p>Padrão (DPT)</p></td>
<td><p>As mensagens são movidas automaticamente para a caixa de correio de arquivo morto após dois anos. Aplica-se a itens em toda a caixa de correio que não tenham uma marca de retenção aplicada explicitamente ou herdada da pasta.</p></td>
</tr>
<tr class="even">
<td><p><strong>Movimentação de 1 anos para arquivo pessoal</strong></p></td>
<td><p>Pessoal</p></td>
<td><p>As mensagens são movidas automaticamente para a caixa de correio de arquivo morto após um ano.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Movimentação de 5 anos para arquivo pessoal</strong></p></td>
<td><p>Pessoal</p></td>
<td><p>As mensagens são movidas automaticamente para a caixa de correio de arquivo após cinco anos.</p></td>
</tr>
<tr class="even">
<td><p><strong>Pessoal: nunca mover para arquivo morto</strong></p></td>
<td><p>Pessoal</p></td>
<td><p>As mensagens nunca são movidas para a caixa de correio de arquivo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mover itens recuperáveis com 14 dias para arquivo</strong></p></td>
<td><p>Pasta Itens Recuperáveis</p></td>
<td><p>As mensagens são movidas da pasta Itens Recuperáveis da caixa de correio principal do usuário para a pasta Itens Recuperáveis da caixa de correio de arquivo morto. Os usuários que tentarem recuperar itens excluídos no arquivo morto devem usar o recurso Recuperar itens excluídos na caixa de correio de arquivo morto.</p></td>
</tr>
</tbody>
</table>


Se você habilitar um Arquivo Morto In-Loco para um usuário de caixa de correio e a caixa de correio já não possuir uma política de retenção atribuída, a política de arquivo morto e de retenção padrão será atribuída automaticamente. Depois que o Assistente de caixa de correio processar a caixa de correio, essas marcas ficarão disponíveis para o usuário, que poderá, então, marcar pastas ou mensagens para serem movidas para a caixa de correio de arquivo morto. Por padrão, as mensagens de email de toda a caixa de correio são movidas após dois anos.

Antes de fornecer caixas de correio de arquivo morto aos seus usuários, é recomendável informar a eles sobre as políticas de arquivo morto que serão aplicadas à caixa de correio e oferecer treinamento ou documentação para atender às necessidades deles. Isso deve incluir detalhes sobre:

  - Funcionalidade disponível no arquivo morto, arquivo morto padrão e políticas de retenção.

  - Informações sobre quando as mensagens serão movidas automaticamente para o arquivo morto.

  - Informações sobre a hierarquia de pastas criada na caixa de correio de arquivo morto.

  - Como aplicar marcas pessoais (exibidas no menu Política de arquivo morto no Outlook e no Outlook Web App).


> [!TIP]
> Se você aplicar uma política de retenção aos usuários que têm uma caixa de correio de arquivo morto, a política de retenção substituirá a política padrão de MRM. Você pode criar uma ou mais marcas de retenção com a ação <STRONG>Mover para o arquivo morto</STRONG> e, depois, vincular as marcas à diretiva de retenção. Você também pode adicionar as marcas padrão <STRONG>Mover para o arquivo morto</STRONG> (que são criadas pela Instalação e vinculadas à Política padrão de MRM) a quaisquer políticas de retenção que você criar.



Para obter informações sobre conformidade e arquivamento no Outlook 2010 e posterior, consulte [Planejar conformidade e arquivamento no Outlook 2010](https://go.microsoft.com/fwlink/?linkid=210902).

## Cotas de arquivo morto

As caixas de correio de arquivo morto são projetadas para que os usuários possam armazenar dados de mensagem de histórico fora de sua caixa de correio principal. Frequentemente, os usuários usam arquivos .pst devido às baixas cotas de armazenamento de caixas de correio e às restrições impostas quando essas cotas são excedidas. Por exemplo, os usuários podem ser impedidos de enviar mensagens quando o tamanho da caixa de correio excede a *cota de proibição de envio*. Da mesma forma, os usuários podem ser impedidos de enviar e receber mensagens quando o tamanho da caixa de correio excede a *cota de proibição de envio e recebimento*.

Para eliminar a necessidade de arquivos .pst, você pode fornecer uma caixa de correio de arquivo morto com limites de armazenamento que cumpram os requisitos do usuário. Entretanto, você ainda pode querer reter algum controle sobre as cotas de armazenamento e o crescimento das caixas de correio de arquivo morto para ajudar a monitorar custos e expansão.

Para ajudar nesse controle, você pode configurar as caixas de correio de arquivo com uma *cota de aviso de arquivo* e uma *cota de arquivo*. Quando uma caixa de correio de arquivo morto exceder a cota de aviso especificada, um evento de aviso é registrado no log de eventos do aplicativo. Quando uma caixa de correio de arquivo morto excede a cota de arquivo especificada, as mensagens não são mais movidas para o arquivo, um evento de aviso é registrado no log de eventos do aplicativo e uma mensagem de cota é enviada para o usuário da caixa de correio. Por padrão, no Exchange 2013, a cota de aviso de arquivo morto é configurada em 45 gigabytes (GB) e a cota de arquivo morto é configurada em 50 GB.

A tabela a seguir lista os eventos registrados em log e as mensagens de aviso enviadas quando a cota de aviso de arquivo morto e a cota de arquivo morto são atingidas.


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Cota</th>
<th>ID do Evento</th>
<th>Tipo</th>
<th>Origem</th>
<th>Categoria</th>
<th>Mensagem</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cota de aviso de arquivo morto</p></td>
<td><p>10022</p></td>
<td><p>Aviso</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Assistente de Pasta Gerenciada</p></td>
<td><p>A caixa de correio de arquivo morto '&lt;Nome para exibição&gt;:&lt;GUID&gt;:&lt;Banco de dados de caixa de correio&gt;:&lt;FQDN do servidor&gt;' excedeu a cota de aviso de arquivo morto '&lt;Cota de aviso de arquivo morto&gt;'. O tamanho da caixa de correio de arquivo morto é de '&lt;Tamanho&gt;' bytes.</p></td>
</tr>
<tr class="even">
<td><p>Cota de arquivo morto</p></td>
<td><p>8537</p></td>
<td><p>Aviso</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>Geral</p></td>
<td><p>A caixa de correio de arquivo morto de &lt;DN herdado&gt; excedeu o tamanho máximo de caixa de correio de arquivo morto. Não é possível copiar ou mover itens para a caixa de correio de arquivo morto. Todas as ações de retenção de mensagens que movem itens para a caixa de correio de arquivo morto irão falhar, e a caixa de correio principal pode conter itens com marcas de retenção expiradas até que a caixa de correio de arquivo morto esteja dentro do limite de tamanho máximo. O proprietário da caixa de correio deve ser notificado da condição da caixa de correio de arquivo morto.</p></td>
</tr>
</tbody>
</table>


## Arquivos Mortos In-Loco e outros recursos do Exchange

Esta seção explica a funcionalidade entre Arquivos Mortos In-Loco e vários recursos do Exchange:

  - **Pesquisa do Exchange   **A capacidade de pesquisar mensagens rapidamente se torna ainda mais crítica com as caixas de correio de arquivo morto. Para a Pesquisa do Exchange, não há diferença entre a caixa de correio principal e a de arquivo morto. O conteúdo das duas caixas de correio é indexado. Como a caixa de correio de arquivo morto não é armazenada no cache do computador do usuário (mesmo se o Outlook estiver sendo usado no modo em cache do Exchange), os resultados de pesquisa para o arquivo morto sempre serão fornecidos pela Pesquisa do Exchange. Ao pesquisar toda a caixa de correio no Outlook 2010 e posterior e no Outlook Web App, os resultados da pesquisa incluem a caixa de correio principal e a de arquivo morto do usuário.

  - **In-Place eDiscovery**   Quando um gerenciador de descobertas executa uma pesquisa In-Place eDiscovery, as caixas de correio de arquivo morto também são pesquisadas. Não há opção para excluir caixas de correio de arquivo morto ao criar uma pesquisa de descoberta a partir do Centro de Administração do Exchange (EAC). Ao usar o Shell de Gerenciamento do Exchange para criar uma pesquisa de descoberta, você pode excluir o arquivo morto usando a opção *DoNotIncludeArchive*. Para detalhes, consulte [New-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd298064\(v=exchg.150\)). Para obter mais informações, consulte [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > A In-Place eDiscovery não pode ser usada para pesquisar uma caixa de correio desconectada.



  - **Retenção de litígio e In-loco**   Quando uma caixa de correio é colocada em retenção de litígio ou In-loco, a retenção é imposta à caixa de correio principal e à de arquivo morto. Para obter mais informações sobre Retenção In-Loco e Retenção de litígio, consulte [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - **Pasta Itens Recuperáveis   **A caixa de correio de arquivo morto contém sua própria pasta Itens Recuperáveis e está sujeita às mesmas cotas da pasta Itens Recuperáveis que a caixa de correio principal. Para saber mais sobre itens recuperáveis, consulte [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

  - **Arquivar conteúdo do Lync no Exchange**   É possível arquivar conversas de mensagens instantâneas e documentos de reunião online compartilhados na caixa de correio principal do usuário. A caixa de correio deve residir em um servidor de Caixa de Correio do Exchange 2013 e é necessário implementar o Microsoft Lync 2013 em sua organização. Para detalhes, consulte [Integração com o SharePoint e o Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

## Gerenciando caixas de correio de arquivo morto

No Exchange 2013, criar e gerenciar caixas de correio de arquivo morto é algo integrado a tarefas comuns de gerenciamento de caixas de correio, incluindo:

  - **Criar uma caixa de correio de arquivo morto**   Você pode criar uma caixa de correio de arquivo morto ao criar uma caixa de correio, ou habilitar uma caixa de correio de arquivo morto para uma caixa de correio existente. Para detalhes, consulte [Gerenciar arquivos mortos de In-loco no Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

  - **Mover uma caixa de correio de arquivo morto**   Você pode mover uma caixa de correio de arquivo morto de um usuário para outro banco de dados de caixa de correio no mesmo servidor de Caixa de Correio ou para outro servidor, independentemente da caixa de correio principal. Para mover a caixa de correio de arquivo morto de um usuário, crie uma solicitação de movimentação de caixa de correio. Para detalhes, consulte [Gerenciar movimentações de local](manage-on-premises-moves-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Localizar a caixa de correio de um usuário e arquivar em diferentes versões do Exchange Server não é suportado.



  - **Desabilitar uma caixa de correio de arquivo morto**   Você pode querer desabilitar a caixa de correio de arquivo morto de um usuário para fins de solução de problemas ou se estiver movendo a caixa de correio principal para uma versão do Exchange que não seja compatível com Arquivos Mortos In-loco. Desabilitar um arquivo morto é semelhante a desabilitar uma caixa de correio principal. Para detalhes, consulte [Gerenciar arquivos mortos de In-loco no Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md). Em implementações locais, uma caixa de correio de arquivo morto desabilitada é retida no banco de dados de caixa de correio até que o período de retenção de caixa de correio excluída para esse banco de dados seja atingido. Durante esse período, você pode reconectar o arquivo morto a um usuário de caixa de correio. Quando o período de retenção de caixa de correio excluída for atingido, a caixa de correio de arquivo morto desconectada será apagada do banco de dados de caixa de correio.

  - **Recuperando estatísticas de caixa de correio e pasta**   Você pode recuperar estatísticas de caixa de correio e pasta de caixa de correio de uma caixa de correio de arquivo morto de um usuário utilizando a opção *Archive* com os cmdlets [Get-MailboxStatistics](https://technet.microsoft.com/pt-br/library/bb124612\(v=exchg.150\)) e [Get-MailboxFolderStatistics](https://technet.microsoft.com/pt-br/library/aa996762\(v=exchg.150\)).

  - **Testar a conectividade do arquivo morto**   No Exchange 2013, você pode usar o cmdlet [Test-ArchiveConnectivity](https://technet.microsoft.com/pt-br/library/hh529914\(v=exchg.150\)) para testar a conectividade com o arquivo morto local ou baseado na nuvem de determinado usuário.

