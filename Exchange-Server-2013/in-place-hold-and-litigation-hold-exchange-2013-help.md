---
title: 'Retenção local e Retenção de litígio: Exchange Online Help'
TOCTitle: Retenção local e Retenção de litígio
ms:assetid: 71031c06-852d-44d8-b558-dff444eaef8c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff637980(v=EXCHG.150)
ms:contentKeyID: 50485796
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Retenção local e Retenção de litígio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2017-11-15_


> [!TIP]
> Adiamos o prazo de 1 de julho de 2017 para criar novos Bloqueios In-loco no Exchange Online (em planos autônomos do Office 365 e do Exchange Online). No entanto, mais para o fim deste ano ou no início do próximo ano, não será possível criar novos Bloqueios In-loco no Exchange Online. Como alternativa ao uso de Bloqueios In-loco, use <A href="https://go.microsoft.com/fwlink/?linkid=780738">casos de descoberta eletrônica</A> ou <A href="https://go.microsoft.com/fwlink/?linkid=827811">políticas de retenção</A> no Centro de Conformidade e Segurança do Office 365. Após encerrarmos os novos Bloqueios In-loco, você ainda conseguirá modificar os existentes, e a criação de novos bloqueios em implantações híbridas no Exchange Server 2013 e no Exchange ainda terão suporte. Além disso, você poderá posicionar caixas de entrada em Retenção de Litígio.



Quando existe uma expectativa razoável de litígio, as organizações são solicitadas a preservar informações armazenadas eletronicamente (ESI), incluindo emails, pertinentes ao caso. Essa expectativa geralmente existe antes que os detalhes do caso sejam conhecidos, e a preservação geralmente é total. As organizações podem precisar preservar todos os emails relacionados a um tópico específico ou todos os emails de determinados indivíduos. Dependendo das práticas de descoberta eletrônica (eDiscovery) da organização, as seguintes medidas podem ser adotadas para preservar emails:

  - Pode ser solicitado aos usuários finais que preservem emails sem excluir qualquer mensagem. No entanto, os usuários ainda podem excluir emails conscientemente ou inadvertidamente.

  - Mecanismos de exclusão automática, como o gerenciamento de registros de mensagens (MRM), podem ser suspensos. Isso poderia resultar em grandes volumes de email enchendo a caixa de correio do usuário, impactando assim na sua produtividade. Suspender a exclusão automática também não impede que usuários excluam emails manualmente.

  - Algumas organizações copiam ou movem emails para um arquivo morto, para garantir que não sejam excluídos, alterados ou violados. Isso aumenta os custos devido a esforços manuais exigidos para copiar ou mover mensagens para um arquivo morto, ou a produtos de terceiros usados para coletar e armazenar emails fora do Exchange.

A falha na preservação de emails pode expor a organização a riscos legais e financeiros, como exames detalhados da retenção de registros da organização e processos de descoberta, julgamentos legais adversos, sanções ou multas.

Você pode usar a Bloqueio In-loco ou a Retenção de Litígio para cumprir os seguintes objetivos:

  - Reter caixas de correio do usuário e preservar itens de caixa de correio imutavelmente

  - Preservar itens de caixa de correio excluídos por usuários ou por processos de exclusão automática, como o MRM

  - Use o Bloqueio In-Loco baseado em consulta para pesquisar e reter itens que correspondam a critérios especificados.

  - Preserve itens indefinidamente ou por um período específico.

  - Coloque um usuário em vários modos de espera para diferentes casos ou investigações.

  - Manter as retenções transparentes para o usuário não tendo que suspender o MRM

  - Habilitar pesquisas de Descoberta Eletrônica In-loco de itens colocados em retenção

**Sumário**

Situações de Retenção In-loco

Retenção local e Retenção de litígio

Colocar uma caixa de correio em Retenção In-loco

Colocar pastas públicas em retenção

Isenções e a pasta Itens recuperáveis

Isenções e cotas de caixa de correio

Isenções e encaminhamento de email

Preservar o conteúdo arquivado do Lync

Excluir uma caixa de correio em espera

Migração de caixas de correio em espera do Exchange 2013 para o Office 365

## Situações de Retenção In-loco

No Exchange Server 2010, a noção de retenção legal é reter todos os dados de caixa de correio de um usuário indefinidamente, ou até que a retenção seja removida. No Exchange 2013, a Retenção In-loco apresenta um novo modelo que permite especificar os seguintes parâmetros:

  - **O que reter**   Você pode especificar quais itens a serem retidos usando parâmetros de consulta como palavras-chave, remetentes e destinatários e datas de início e término, além de especificar os tipos de mensagens, como mensagens de email ou itens de calendário que deseja deixar em retenção.

  - **Por quanto tempo reter**   Você pode especificar uma duração para a retenção de itens.

Usando esse novo modelo, a Retenção In-loco permite que você crie diretivas de retenção granulares para preservar itens de caixa de correio nas seguintes situações:

  - **Retenção indefinida**   A situação de retenção indefinida é semelhante à retenção de litígio. Ela pretende preservar itens de caixa de correio para que você possa atender aos requisitos de Descoberta Eletrônica. Durante o período de litígio ou investigação, os itens nunca são excluídos. A duração não é conhecida de antemão e, portanto, nenhuma data de término é configurada. Para reter todos os itens de email indefinidamente, você não pode especificar nenhum parâmetro de consulta ou duração ao criar a Retenção In-loco.

  - **Retenção baseada em consulta**   Caso a sua organização preserve itens com base em parâmetros de consulta especificados, você poderá usar uma Retenção In-loco baseada em consulta. Você pode especificar parâmetros de consulta como palavras-chave, datas de início e término, endereços de remetentes e destinatários e tipos de mensagens. Após a criação de uma Retenção In-loco baseada em consulta, todos os itens de caixa de correio existentes e futuros (incluindo mensagens recebidas em uma data posterior) que correspondam aos parâmetros de consulta serão preservados.
    

    > [!IMPORTANT]
    > Itens que são marcados como não pesquisáveis, geralmente por causa da falha em indexar um anexo, também são preservados porque não é possível determinar se eles correspondem aos parâmetros de consulta. Para saber mais sobre o item não pesquisável, consulte <A href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Itens não pesquisáveis na descoberta eletrônica do Exchange</A>.



  - **Retenção baseada em tempo**   O Bloqueio In-loco e a Retenção de Litígio permitem que você especifique uma duração para a retenção de itens. A duração é calculada a partir da data em que um item de caixa de correio é recebido ou criado.
    
    Se sua organização exigir que todos os itens de caixa de correio sejam preservados por um período específico, como 7 anos por exemplo, você pode criar uma retenção baseada em tempo. No Exchange 2013, você pode especificar um período de retenção para itens em retenção. Itens em retenção envelhecem de acordo com sua data de recebimento. Por exemplo, considere uma caixa de correio colocada em uma Retenção In-loco baseada em tempo e que tenha um período de retenção definido como 365 dias. Se um item dessa caixa de correio for excluído após 300 dias da data de recebimento, ele será mantido por mais 65 dias antes de ser excluído permanentemente. Você pode usar uma Retenção In-loco baseada em tempo em conjunto com uma política de retenção para garantir que os itens sejam preservados pela duração especificada e removidos permanentemente após esse período.

Você pode usar o Bloqueio In-loco para colocar um usuário em várias retenções. Quando um usuário é colocado em diversas retenções, as consultas de pesquisa de qualquer retenção baseada na consulta são combinadas (com operadores **OR**). Nesse caso, o número máximo de palavras-chave em todas as retenções baseadas na consulta colocadas em uma caixa de correio é 500. Se houver mais de 500 palavras-chave, todo o conteúdo na caixa de correio será colocado em retenção (não apenas se o conteúdo que corresponde aos critérios da pesquisa). Todo o conteúdo é retido até que o número total de palavras-chave seja reduzido para 500 ou menos.

Voltar ao início

## Retenção local e Retenção de litígio

A Retenção de Litígio, o recurso de retenção introduzido no Exchange 2010 para preservar dados para a Descoberta Eletrônica, ainda está disponível no Exchange 2013. A Retenção de Litígio usa a propriedade **LitigationHoldEnabled** de uma caixa de correio. Enquanto a Retenção In-loco oferece capacidade de retenção granular baseada em parâmetros de consulta e a habilidade de colocar várias retenções, a retenção de litígio permite colocar todos os itens em retenção. Você também pode especificar um período de duração para armazenar itens quando uma caixa de correio é colocada em Retenção de Litígio. A duração é calculada a partir da data em que um item de caixa de correio é recebido ou criado. Se uma duração não for definida, os itens serão retidos indefinidamente, ou até que a retenção seja removida.

Quando uma caixa de correio é colocada em uma ou mais Retenções In-loco e Retenção de litígio (sem um período de duração) ao mesmo tempo, todos os itens são retidos indefinidamente ou até que as retenções sejam removidas. Se você remover a retenção de litígio e o usuário ainda estiver em uma ou mais Retenções In-loco, os itens que correspondam aos critérios de Retenção In-loco serão retidos pelo período especificado nas configurações da retenção. Quando você move uma caixa de correio que está em retenção de litígio no Exchange 2010 para um servidor de Caixa de Correio do Exchange 2013, a configuração de retenção de litígio continua a ser aplicada, garantindo que os requisitos de conformidade sejam atendidos durante e após a mudança.


> [!TIP]
> Ao colocar uma caixa de correio em Bloqueio In-loco ou em Retenção de Litígio, a retenção será aplicada à caixa de correio principal e à caixa de correio de arquivo morto. Se você colocar uma caixa de correio principal local em espera em uma implantação híbrida do Exchange, a caixa de correio de arquivo morto baseada em nuvem (se estiver habilitada) também será colocada em espera.



Para obter mais informações, consulte:

  - [Colocar uma caixa de correio em Retenção de Litígio](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - [Colocar todas as caixas de correio em espera](place-all-mailboxes-on-hold-exchange-2013-help.md)

## Colocar uma caixa de correio em Retenção In-loco

Usuários autorizados que foram adicionados ao grupo de função de controle de acesso baseado em função (RBAC) do [Gerenciamento de Descobertas](discovery-management-exchange-2013-help.md) ou receberam funções de gerenciamento de Pesquisa de Caixa de Correio e Retenção Legal podem colocar usuários de caixa de correio em Retenção In-loco. Você pode delegar a tarefa para gerenciadores de registros, responsáveis pela conformidade ou advogados no departamento jurídico da sua organização, atribuindo os privilégios mínimos. Para saber mais sobre como atribuir o grupo de função Gerenciamento de Descobertas, consulte [Atribuir permissões de descoberta eletrônica no Exchange](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions).


> [!IMPORTANT]
> No Exchange 2010, a função de Retenção Legal oferecia permissões suficientes para que um usuário colocasse caixas de correio em retenção de litígio. No Exchange 2013, você pode usar a mesma permissão para colocar caixas de correio em uma Retenção In-loco indefinida ou baseada em tempo. Porém, para criar uma Retenção In-loco baseada em consulta, a função de Pesquisa de Caixa de Correio precisa ser atribuída ao usuário. O grupo de função Gerenciamento de Descobertas tem ambas essas funções atribuídas.



No Exchange 2013, a funcionalidade de Retenção In-loco é integrada com as pesquisas de Descoberta Eletrônica In-loco. Você pode usar o assistente de **Retenção & Descoberta Eletrônica In-loco** no Centro de Administração do Exchange ou o cmdlet **New-MailboxSearch** e cmdlets relacionados no Shell de Gerenciamento do Exchange para colocar uma caixa de correio em Retenção In-loco. Para saber mais sobre como colocar uma caixa de correio em Retenção In-loco, consulte [Criar ou remover um bloqueio In-loco](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/create-or-remove-in-place-holds).


> [!TIP]
> Se você usar o Arquivamento do Exchange Online para provisionar um arquivo baseado em nuvem para as suas caixas de correio locais, será necessário gerenciar a Retenção In-loco a partir de sua organização do Exchange 2013 no local. As configurações de retenção são propagadas automaticamente para o arquivo baseado em nuvem usando o DirSync. Como foi mencionado anteriormente, quando você coloca uma caixa de correio no local em retenção, o arquivo baseado na nuvem correspondente também é colocado em retenção.



Muitas organizações exigem que os usuários sejam informados quando forem colocados em retenção. Além disso, quando uma caixa de correio está em retenção, nenhuma diretiva de retenção aplicável ao usuário da caixa de correio precisa ser suspensa. Como as mensagens continuam a serem excluídas conforme o esperado, os usuários podem não perceber que estão em retenção. Se sua organização exige que os usuários em retenção sejam informados, você pode adicionar uma mensagem de notificação à propriedade **Retention Comment** do usuário da caixa de correio e usar a propriedade **RetentionUrl** para incluir um link para uma página web com mais informações. O Outlook 2010 ou posterior exibe a notificação e o URL na área de backstage. É necessário usar o Shell para adicionar e gerenciar essas propriedades para uma caixa de correio.

Voltar ao início

## Colocar pastas públicas em retenção

No Exchange Online, você pode colocar as pastas públicas em retenção, usando um Bloqueio In-loco. Não há suporte para uso de Retenção de Litígio de pastas públicas. Quando você cria um Bloqueio In-loco, a única opção é colocar uma retenção em todas as pastas públicas em sua organização. O resultado é que um Bloqueio In-loco é colocado em todas as caixas de correio de pasta pública.

Além disso, quando você coloca as pastas públicas em Bloqueio In-loco, as mensagens de email relacionadas ao processo de sincronização de hierarquia de pasta pública também são preservadas. Isso pode resultar em milhares de sincronizações de hierarquia relacionadas a itens de email sendo preservados. Essas mensagens podem preencher a cota de armazenamento da pasta de Itens Recuperáveis nas caixas de correio de pasta pública. Para evitar isso, você pode criar um Bloqueio In-loco baseado na consulta e adicionar o seguinte par `property:value` para a consulta da pesquisa:

    NOT(subject:HierarchySync*)

O resultado é que qualquer mensagem (relacionada à sincronização da hierarquia de pasta pública) que contiver a frase "HierarchySync" na linha de assunto não será colocada em retenção.

## Isenções e a pasta Itens recuperáveis

A Retenção In-loco e a Retenção de Litígio usam a pasta Itens Recuperáveis para preservar itens. A pasta Itens Recuperáveis substitui o recurso informalmente conhecido como *dumpster* em versões anteriores do Exchange. A pasta Itens Recuperáveis fica oculta no modo de exibição padrão do Outlook, do Outlook Web App e de outros clientes de email. Para saber mais sobre a pasta Itens Recuperáveis, consulte [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

Por padrão, quando um usuário exclui uma mensagem de uma pasta diferente da pasta Itens Excluídos, a mensagem é movida para a pasta Itens Excluídos. Isso é conhecido como *mudança*. Quando um usuário executa a *exclusão reversível* de um item (pressionando as teclas SHIFT e DELETE) ou exclui um item da pasta Itens Excluídos, a mensagem é movida para a pasta Itens Recuperáveis, e portanto desaparece da visualização do usuário.

Os itens na pasta Itens Recuperáveis são mantidos pelo período de retenção de itens excluídos configurado no banco de dados de caixa de correio do usuário. Por padrão, o período de retenção de itens excluídos é configurado como 14 dias em bancos de dados de caixas de correio. Você também pode configurar uma cota de armazenamento para a pasta Itens Recuperáveis. Isso protege a organização de um possível ataque de negação de serviço (DoS), devido ao rápido crescimento da pasta Itens Recuperáveis e, portanto, do banco de dados de caixas de correio. Se uma caixa de correio não for colocada em Retenção In-loco ou retenção de litígio, os itens serão removidos permanentemente da pasta Itens Recuperáveis no modo primeiro a entrar, primeiro a sair quando a cota de aviso dos Itens Recuperáveis for excedida ou se o item tiver sido mantido na pasta por um tempo maior que o período de retenção de itens excluídos.

A pasta Itens Recuperáveis tem as subpastas a seguir, usadas para armazenar itens excluídos em vários locais e facilitar a Retenção In-loco e a retenção de litígio:

  - **Deletions**   Itens removidos da pasta Itens Excluídos ou excluídos temporariamente de outras pastas são movidos para a subpasta Exclusões e são visíveis ao usuário quando o recurso Recuperar Itens Excluídos é usado no Outlook e no Outlook Web App. Por padrão, os itens permanecem nesta pasta até que o período de retenção de itens excluídos configurado no banco de dados de caixas de correio ou a própria caixa de correio expire.

  - **Purges**   Quando um usuário exclui um item da pasta Itens Recuperáveis (usando a ferramenta Recuperar Itens Excluídos no Outlook e no Outlook Web App), o item é movido para a pasta Remoções. Itens que excedem o período de retenção de itens excluídos configurado no banco de dados de caixa de correio ou na caixa de correio também são movidos para a pasta Remoções. Itens nesta pasta não ficam visíveis aos usuários se eles usarem a ferramenta Recuperar Itens Excluídos. Quando o assistente da caixa de correio processa a caixa de correio, os itens na pasta Remoções são removidos do banco de dados de caixa de correio. Quando o usuário da caixa de correio é colocado em retenção de litígio, o assistente da caixa de correio não remove itens desta pasta.

  - **DiscoveryHold**   Se um usuário for colocado em uma Retenção In-loco, os itens excluídos são movidos para essa pasta. Quando o assistente de caixa de correio processa a caixa de correio, ele avalia as mensagens nessa pasta. Itens que correspondam à consulta da Retenção In-loco são mantidos pelo período especificado na consulta. Se nenhum período de retenção for especificado, os itens são retidos indefinidamente ou até que o usuário seja removido da retenção.

  - **Versions**   Quando um usuário é colocado em Retenção In-loco ou retenção de litígio, os itens de caixa de correio precisam ser protegidos contra violações ou modificações pelo usuário ou por um processo. Isso é realizado usando um processo de *cópia-na-gravação*. Quando um usuário ou processo altera propriedades específicas de um item de caixa de correio, uma cópia do item original é salva na pasta Versões antes que a alteração seja aplicada. O processo é repetido para as alterações subsequentes. Itens capturados pela pasta Versões também são indexados e retornados em pesquisas de Descoberta Eletrônica In-loco. Após a remoção da retenção, as cópias na pasta Versões são removidas pelo Assistente de Pasta Gerenciada.

### Propriedades que iniciam a cópia-na-gravação

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de item</th>
<th>Propriedades que iniciam a cópia-na-gravação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mensagens (IPM.Note*)</p>
<p>Postagens (IPM.Post*)</p></td>
<td><ul>
<li><p>Subject</p></li>
<li><p>Body</p></li>
<li><p>Anexos</p></li>
<li><p>Remetentes/Destinatários</p></li>
<li><p>Datas Enviadas/Recebidas</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Itens diferentes de mensagens e postagens</p></td>
<td><p>Qualquer alteração em uma propriedade visível, exceto:</p>
<ul>
<li><p>Localização do item (quando um item é movido entre pastas)</p></li>
<li><p>Alteração de status do item (lidas ou não lidas)</p></li>
<li><p>Alterações na marca de retenção aplicada a um item</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Itens na pasta padrão Rascunhos</p></td>
<td><p>Nenhum (itens na pasta Rascunhos estão isentos de gravação de cópia)</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> A cópia-na-gravação é desabilitada em itens de calendário na caixa de correio do organizador quando respostas da reunião são recebidas de participantes e as informações de rastreamento referentes à reunião são atualizadas. Para itens de calendário e itens contendo um conjunto de lembretes, o recurso cópia em gravação está desabilitado para as propriedades ReminderTime e ReminderSignalTime. As alterações feitas nessas propriedades não são capturadas pelo recurso cópia em gravação. Alterações para feeds RSS não são capturadas pela gravação de cópia.



Embora as pastas Retenção de Descoberta, Remoções e Versões não fiquem visíveis para os usuários, todos os itens na pasta Itens Recuperáveis são indexados pela Pesquisa do Exchange e podem ser descobertos usando a Descoberta Eletrônica In-loco. Após um usuário de caixa de correio ser removido da Retenção In-loco ou da retenção de litígio, os itens nas pastas Retenção de Descoberta, Remoções e Versões são removidos pelo Assistente de Pasta Gerenciada.

Voltar ao início

## Isenções e cotas de caixa de correio

Itens na pasta Itens Recuperáveis não são calculados na cota de caixa de correio do usuário. No Exchange, a pasta Itens Recuperáveis tem sua própria cota. Para Exchange, os valores padrão para as propriedades de caixa de correio *RecoverableItemsWarningQuota* e *RecoverableItemsQuota* são definidos como 20 GB e 30 GB, respectivamente. Para modificar esses valores para um banco de dados de caixa de correio, para Exchange Server 2013, use o cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)). Para modificá-los para caixas de correio individuais, use o cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

Quando a pasta Itens Recuperáveis de um usuário exceder a cota de aviso para itens recuperáveis (conforme especificado pelo parâmetro *RecoverableItemsWarningQuota*), um evento é registrado no log de eventos do Aplicativo do servidor de Caixa de Correio. Quando a pasta exceder a cota para itens recuperáveis (conforme especificado no parâmetro *RecoverableItemsQuota*), os usuários não poderão esvaziar a pasta Itens Excluídos ou excluir itens da caixa de correio permanentemente. A gravação de cópia também não poderá criar cópias de itens modificados. Portanto, é essencial que as cotas de Itens Recuperáveis para usuários de caixa de correio colocados em Retenção In-loco sejam monitoradas.

No Exchange Online, a cota da pasta Itens Recuperáveis (na caixa principal do usuário) é automaticamente aumentada para 100 GB quando você coloca uma caixa de correio em Retenção de Litígio ou em Bloqueio In-loco. Quando a cota de armazenamento da pasta Itens Recuperáveis na caixa de correio principal de uma caixa de correio em espera está quase atingindo o limite, você pode fazer o seguinte:

  - **Habilitar a caixa de correio de arquivo morto e ativar o arquivamento de expansão automática**   Você pode habilitar uma capacidade de armazenamento ilimitado para a pasta Itens Recuperáveis simplesmente habilitando a caixa de correio de arquivo morto e ativando o recurso de arquivamento de expansão automática no ExchangeOnline. Isso resulta em 100 GB para a pasta Itens Recuperáveis na caixa de correio principal e um volume ilimitado de capacidade de armazenamento para a pasta Itens Recuperáveis no arquivo morto do usuário. Veja como: [Habilitar caixa de correio de arquivo morto no Centro de Conformidade e Segurança do Office 365](https://go.microsoft.com/fwlink/p/?linkid=863320) e [Habilitar o arquivamento ilimitado no Office 365](https://go.microsoft.com/fwlink/p/?linkid=844569).
    
    **Observações**:
    
      - Após habilitar o arquivamento para uma caixa de correio que está prestes a exceder a cota de armazenamento da pasta Itens Recuperáveis, convém executar o Assistente de Pasta Gerenciada para disparar manualmente o assistente para processar a caixa de correio, de modo que os itens expirados sejam movidos para a pasta Itens Recuperáveis na caixa de correio de arquivo morto. Para obter instruções, confira a Etapa 4 em [Aumentar a cota de Itens Recuperáveis para caixas de correio em espera](https://support.office.com/pt-br/article/aumentar-a-cota-de-itens-recuper%c3%a1veis-para-caixas-de-correio-em-espera-a8bdcbdd-9298-462f-b889-df26037a990c?ui=pt-br%26rs=pt-br%26ad=br).
    
      - Os demais itens na caixa de correio do usuário podem ser movidos para a nova caixa de correio de arquivo morto. Considere informar ao usuário que isso pode acontecer depois que você habilita a caixa de correio de arquivo morto.

  - **Criar uma política de retenção personalizada para caixas de correio em espera**   Além de habilitar a caixa de correio de arquivamento e o arquivamento de expansão automática para caixas de correio em Retenção de Litígio ou Bloqueio In-loco, também convém criar uma política de retenção personalizada para caixas de correio em espera. Isso permite aplicar uma política de retenção para caixas de correio em espera diferente da Política de MRM Padrão que é aplicada às caixas de correio que não estão em espera. Isso permite aplicar marcas de retenção projetadas especificamente para caixas de correio em espera. Isso inclui a criação de uma nova marca de retenção para a pasta Itens Recuperáveis.

Para saber mais, confira [Aumentar a cota de Itens Recuperáveis para caixas de correio em espera](https://support.office.com/pt-br/article/aumentar-a-cota-de-itens-recuper%c3%a1veis-para-caixas-de-correio-em-espera-a8bdcbdd-9298-462f-b889-df26037a990c?ui=pt-br%26rs=pt-br%26ad=br).

## Isenções e encaminhamento de email

Os usuários podem usar Outlook e Outlook Web App para configurar o encaminhamento de email para sua caixa de correio. O encaminhamento de email permite que os usuários configurem suas caixas de correio para encaminhar mensagens de email recebidas para outra caixa de correio localizada dentro ou fora de sua organização. O encaminhamento de email pode ser configurado para que qualquer mensagem enviada para a caixa de correio original não seja copiada para essa caixa de correio e seja somente enviada para o endereço de encaminhamento.

Se o encaminhamento de email estiver configurado para uma caixa de correio e as mensagens não forem copiadas na caixa de correio original, o que acontece se a caixa de correio estiver em espera? O comportamento é diferente com base em se a caixa de correio está em uma organização Exchange 2013 ou Exchange Online.

  - **Exchange Online**   As configurações em espera da caixa de correio são verificadas durante o processo de entrega. Se a mensagem atender aos critérios de espera da caixa de correio, uma cópia da mensagem é salva na pasta Itens recuperáveis. Isso significa que você pode usar a descoberta eletrônica In-loco para pesquisar a caixa de correio original a fim de localizar as mensagens que foram encaminhadas para outra caixa de correio.

  - **Exchange 2013**   Se as mensagens forem encaminhadas para outra caixa de correio e não forem copiadas na caixa de correio original, elas não são capturadas e copiadas na pasta Itens recuperáveis. Isso significa que as mensagens encaminhadas não serão retornadas em uma pesquisa de descoberta eletrônica In-loco. Para resolver esse problema, as organizações de Exchange 2013 podem considerar a remoção da capacidade de os usuários configurarem o encaminhamento de email.

Voltar ao início

## Preservar o conteúdo arquivado do Lync

O Exchange 2013, o Microsoft Lync 2013 e o Microsoft SharePoint 2013 oferecem uma experiência integrada de preservação e Descoberta Eletrônica para permitir que você preserve e pesquise itens entre os diferentes repositórios de dados. O Exchange 2013 permite que você arquive conteúdo do Lync Server 2013 no Exchange, removendo a necessidade de usar um banco de dados separado do SQL Server para armazenar conteúdo arquivado do Lync. A capacidade integrada de retenção e Descoberta Eletrônica no SharePoint 2013 permite que você preserve e pesquise dados entre todos os repositórios em um único console.

Quando você coloca uma caixa de correio do Exchange 2013 em Retenção In-loco ou retenção de litígio, o conteúdo do Microsoft Lync 2013 (como conversas de mensagens instantâneas e arquivos compartilhados em uma reunião online) são arquivados na caixa de correio. Se você pesquisar a caixa de correio usando o Centro de Descoberta Eletrônica no Microsoft SharePoint 2013 ou a Descoberta Eletrônica In-loco no Exchange 2013, qualquer conteúdo arquivado do Lync que corresponda à consulta da pesquisa também será retornado nos resultados da pesquisa. Você também pode restringir a pesquisa a conteúdo arquivado do Lync na caixa de correio.

Para habilitar o arquivamento de conteúdo do Lync na caixa de correio do Exchange 2013, é necessário configurar a integração do Lync 2013 com o Exchange 2013. Para obter informações detalhadas, consulte os seguintes tópicos:

  - [Planejamento para arquivamento](https://technet.microsoft.com/pt-br/library/jj205069\(v=ocs.15\))

  - [Implantando o arquivamento](https://technet.microsoft.com/pt-br/library/jj205147\(v=ocs.15\))

Voltar ao início

## Excluir uma caixa de correio em espera

Quando você exclui uma caixa de correio colocada em Retensão de litígio ou Bloqueio In-loco, o resultado é diferente com base em se a caixa de correio está em uma organização Exchange 2013 ou Exchange Online.

  - **Exchange 2013**   Se um administrador excluir uma conta de usuário que tem uma caixa de correio, o Armazenamento de Informações do Exchange eventualmente detectará que a caixa de correio não está mais conectada a uma conta de usuário e marcará essa caixa de correio para exclusão, mesmo se ela estiver em espera. Se você deseja manter a caixa de correio, deve fazer o seguinte:
    
    1.  Em vez de excluir a conta de usuário, desabilite a conta de usuário.
    
    2.  Altere as propriedades da caixa de correio para restringir o seu uso e acesso à caixa de correio. Por exemplo, defina as cotas de envio e de recebimento como 1, bloqueie quem pode enviar mensagens à caixa de correio e restrinja quem pode acessar a caixa de correio.
    
    3.  Retenha a caixa de correio até que todos os dados sejam eliminados ou até que preservar os dados não seja mais necessário.

  - **Exchange Online**   Se a caixa de correio do usuário for colocada em Bloqueio In-loco ou Retenção de litígio, e a conta do Office 365 correspondente for excluída, a caixa de correio é convertida em uma *caixa de correio inativa*, que é um tipo de caixa de correio excluída por software. Caixas de correio inativas são usadas para preservar o conteúdo da caixa de correio de um usuário depois que ele deixar a organização. Os itens em uma caixa de correio inativa são preservados durante a retenção colocada na caixa de correio antes de ela se tornar inativa. Isso permite que administradores, responsáveis pela conformidade ou gerentes de registro usem a Descoberta Eletrônica no Local para acessar e pesquisar o conteúdo de uma caixa de correio inativa. As caixas de correio inativas não podem receber emails e não são exibidas no catálogo de endereços compartilhado nem em outras listas de sua organização. Para saber mais, consulte [Caixas de correio inativas no Exchange Online](https://technet.microsoft.com/pt-br/library/dn798632\(v=exchg.150\)).

Voltar ao início

## Migração de caixas de correio em espera do Exchange 2013 para o Office 365

Se você tiver uma implantação híbrida de Exchange, as seguintes condições são verdadeiras quando você mover (internamente) uma caixa de correio local Exchange 2013 para Exchange Online em Office 365:

  - Se a caixa de correio local estiver em Retenção de litígio ou Bloqueio In-loco, as configurações em espera são preservadas depois que a caixa de correio for movida para Exchange Online.

  - Se a caixa de correio local estiver em Retenção de litígio ou Bloqueio In-loco, qualquer conteúdo da pasta Itens recuperáveis é movido para a caixa de correio Exchange Online.


> [!TIP]
> As configurações de retenção e o conteúdo na pasta Itens Recuperáveis também são preservados quando você mover (externamente) uma caixa de correio do Exchange Online para a sua organização do Exchange 2013 local.



Existem outras maneiras de migrar os dados de email no local para o Office 365, como o uso de uma migração Exchange em estágios ou de uma migração Exchange de substituição.

  - Uma migração em estágios pode ser usada para migrar caixas de correio do Exchange 2003 ou do Exchange 2007 para o Office 365. Nessas versões do Exchange, a pasta Itens Recuperáveis (e sua funcionalidade) não existe. Portanto, quando você migrar caixas de correio do Exchange 2003 ou do Exchange 2007 para o Office 365, não há nenhum conteúdo da pasta Itens Recuperáveis a mover.

  - Uma migração de substituição pode ser usada para migrar caixas de correio do Exchange 2003, do Exchange 2007 e do Exchange 2010 para o Office 365. Conforme anteriormente mencionado, as caixas de correio do Exchange 2003 e do Exchange 2007 não têm uma pasta Itens Recuperáveis que pode ser migrada. Como a pasta Recuperar Itens foi introduzida no Exchange 2010, o conteúdo da pasta Itens Recuperáveis será migrado para o Office 365, quando você usar uma migração de substituição para migrar caixas de correio do Exchange 2010.


> [!TIP]
> Para o Exchange 2013 e o Exchange 2010, uma implantação híbrida do Exchange é a maneira recomendada de migrar caixas de correio locais para o Office 365.



Voltar ao início

