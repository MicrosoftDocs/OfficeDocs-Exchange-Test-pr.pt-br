---
title: 'Pasta Itens Recuperáveis: Exchange 2013 Help'
TOCTitle: Pasta Itens Recuperáveis
ms:assetid: efc48fb4-2ed8-4d05-93af-f3505fbc389d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee364755(v=EXCHG.150)
ms:contentKeyID: 50486966
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Pasta Itens Recuperáveis

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Para proteger contra exclusões intencionais ou acidentais e facilitar os esforços de descoberta geralmente empreendidos antes ou durante litígios ou investigações, o Microsoft Exchange Server 2013 e o Exchange Online usam a pasta Itens Recuperáveis. A pasta Itens Recuperáveis substitui o recurso conhecido como *dumpster* nas versões mais recentes do Exchange. A pasta Itens Recuperáveis é usada pelos seguintes recursos do Exchange:

  - Retenção de item excluído

  - Recuperação de item único

  - Bloqueio In-loco

  - Retenção de litígio

  - Registro em log de auditoria da caixa de correio

  - Registro em log de calendário

**Sumário**

Terminologia

Pasta Itens Recuperáveis

  - Retenção de item excluído

  - Recuperação de item único

  - Bloqueio In-loco e Retenção de Litígio

  - Proteção de página contra gravação de cópia e itens modificados

Cotas de caixa de correio de Itens Recuperáveis

## Terminologia

O conhecimento dos seguintes termos o ajudará a entender o conteúdo deste tópico.

  - **Excluir**  
    Descreve quando um item é excluído de qualquer pasta e colocado na pasta padrão Itens Excluídos.

<!-- end list -->

  - **Excluir permanentemente**  
    Descreve quando um item é excluído da pasta padrão Itens Excluídos e colocado na pasta Itens Recuperáveis. Além disso, descreve quando o usuário do Microsoft Outlook exclui um item pressionando as teclas Shift+Delete, que ignora a pasta Itens Excluídos e coloca o item diretamente na pasta Itens Recuperáveis.

<!-- end list -->

  - **Apagado**  
    Descreve quando um item é marcado para ser excluído do banco de dados da caixa de correio. Isso é conhecido também como *armazenar para exclusão irreversível*.

Voltar ao início

## Pasta Itens Recuperáveis

A pasta Itens Recuperáveis está localizada na subárvore não IPM de cada caixa de correio. A subárvore não IPM é uma área de armazenamento dentro da caixa de correio que contém os dados operacionais sobre a caixa de correio. Essa subárvore não é visível aos usuários com o Outlook, o Microsoft OfficeOutlook Web App ou outros clientes de email.

Essa alteração de arquitetura fornece as seguintes vantagens:

  - Quando uma caixa de correio é movida para outro banco de dados de caixa de correio, a pasta Itens Recuperáveis é movida com ela.

  - A pasta Itens Recuperáveis é indexada pela Pesquisa do Exchange e pode ser descoberta com o uso da Descoberta Eletrônica In-loco.

  - A pasta Itens Recuperáveis tem sua própria cota de repositório.

  - O Exchange pode evitar que os dados sejam excluídos da pasta Itens Recuperáveis.

  - O Exchange pode controlar edições de determinado conteúdo.

A pasta Itens Recuperáveis contém as seguintes subpastas:

  - **Exclusões**   Esta subpasta contém todos os itens excluídos da pasta Itens Excluídos. No Outlook, o usuário pode excluir um item permanentemente pressionando Shift+Delete. Essa subpasta é exibida aos usuários pelo recurso Recuperar Itens Excluídos no Outlook e no Outlook Web App.

  - **Versões**   Quando o recurso Bloqueio In-loco ou Retenção de Litígio está habilitado, esta subpasta inclui as cópias originais e modificadas dos itens excluídos. Esta pasta não é visível para os usuários finais.

  - **Limpezas**   Quando o recurso Retenção de Litígio ou recuperação de item individual está habilitado, esta subpasta inclui todos os itens apagados. Esta pasta não é visível para os usuários finais.

  - **Auditorias**   Quando os logs de auditoria de caixa de correio estão habilitados para uma caixa de correio, esta subpasta inclui as entradas do log de auditoria. Para saber mais sobre os logs de auditoria de caixa de correio, confira [Registro em log de auditoria da caixa de correio](mailbox-audit-logging-exchange-2013-help.md).

  - **Retenções de Descoberta**   Quando o Bloqueio In-loco está habilitado, esta subpasta inclui todos os itens que atendem aos parâmetros de consulta de retenção e são apagados.

  - **Logs do Calendário**   Esta subpasta contém alterações de calendário que ocorrem em uma caixa de correio. Esta pasta não está disponível aos usuários.

A imagem a seguir mostra as subpastas nas pastas Itens Recuperáveis. Ela mostra também a retenção de itens excluídos, a recuperação de item individual e mantém os processos de fluxo de trabalho descritos nas seções a seguir.

![Pasta Itens Recuperáveis](images/Ee364755.a1a08afc-3617-4adb-83ab-a6904516954e(EXCHG.150).gif "Pasta Itens Recuperáveis")

Voltar ao início

## Retenção de item excluído

Um item é considerado excluído permanentemente nos seguintes casos:

  - Um usuário exclui um item ou esvazia todos os itens da pasta Itens Excluídos.

  - Um usuário pressiona Shift+Delete para excluir um item de qualquer outra pasta da caixa de correio.

Os itens excluídos permanentemente são movidos para a subpasta Exclusões da pasta Itens Recuperáveis. Isso fornece uma camada adicional de proteção para que os usuários possam recuperar itens excluídos permanentemente sem intervenção do Suporte Técnico. Os usuários podem usar o recurso Recuperar Itens Excluídos no Outlook ou no Outlook Web App para recuperar um item excluído. Os usuários também podem usar esse recurso para excluir permanentemente um item. Para saber mais, consulte:

  - [Restaurar itens excluídos no Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)

  - [Recuperar itens ou emails excluídos no Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

Os itens permanecem na subpasta Exclusões até que o período de retenção do item excluído seja atingido. O período de retenção do item excluído padrão para um banco de dados de caixa de correio é de 14 dias. É possível modificar esse período para um banco de dados da caixa de correio ou para uma caixa de correio específica. Além do período de retenção de item excluído, a pasta Itens Recuperáveis também está sujeita a cotas. Para saber mais, confira Cotas de caixas de correio de itens recuperáveis mais adiante neste tópico.

Após o término do período de retenção do item excluído, o item é movido para a pasta Limpezas e não ficará mais visível ao usuário. Quando o Assistente de Pasta Gerenciada processa a caixa de correio, os itens na subpasta Limpezas são apagados do banco de dados de caixa de correio e não podem ser recuperados.

Voltar ao início

## Recuperação de item único

Caso um item seja removido da subpasta Exclusões, seja usando o recurso Recuperar Itens Excluídos ou por meio de um processo automatizado, como o Assistente de Pasta Gerenciada, o item não pode ser recuperado pelo usuário. Nas versões anteriores do Exchange, a recuperação desses itens exigia que o administrador restaurasse o banco de dados de caixa de correio ou uma caixa de correio a partir de cópias de backup. Esse processo geralmente atrasava a recuperação em minutos ou horas, dependendo do mecanismo de backup usado.

No Exchange 2013, você pode usar a *recuperação de item individual* para recuperar itens sem ter que restaurar os bancos de dados de caixa de correio com uma mídia de backup. Isso resulta em períodos de recuperação consideravelmente mais curtos. Quando o Assistente de Pasta Gerenciada processa a pasta Itens Recuperáveis de uma caixa de correio com a recuperação de item individual habilitada, nenhum item na subpasta Limpezas é removido, caso o período de retenção do item excluído não tenha expirado para esse item.

A tabela a seguir lista o conteúdo e as ações que podem ser executadas na pasta Itens Recuperáveis se a recuperação de item único estiver habilitada.

### Pasta Itens Recuperáveis e recuperação de item único

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
<th>Estado da recuperação de item único</th>
<th>A pasta Itens Recuperáveis contém itens excluídos permanentemente</th>
<th>A pasta Itens Recuperáveis contém itens apagados</th>
<th>Os usuários podem apagar itens da pasta Itens Recuperáveis</th>
<th>O Assistente de Pasta Gerenciada apaga automaticamente itens da pasta Itens Recuperáveis</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Habilitado</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
<td><p>Sim. Os usuários podem apagar itens usando o recurso Recuperar Itens Excluídos no Outlook ou Outlook Web App. No entanto, os itens apagados não serão permanentemente removidos do banco de dados de caixa de correio até o período de retenção de item excluído expirar.</p></td>
<td><p>Sim. Por padrão, todos os itens são apagados após 14 dias, com a exceção dos itens de calendário, que são apagados após 31 dias.</p></td>
</tr>
<tr class="even">
<td><p>Desabilitado</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
<td><p>Sim. Nesse caso, os itens apagados são marcados para remoção permanente do banco de dados de caixa de correio e não podem ser recuperados.</p></td>
<td><p>Sim. Por padrão, todos os itens são apagados após 14 dias, com a exceção dos itens de calendário, que são apagados após 31 dias. Se a cota de avisos da pasta Itens Recuperáveis for atingida antes de o período de retenção do item excluído decorrer, as mensagens serão excluídas na ordem PEPS (primeiro a entrar, primeiro a sair).</p></td>
</tr>
</tbody>
</table>


No Exchange 2013, a recuperação de item individual não está habilitada por padrão para novas caixas de correio ou para caixas de correio migradas de uma versão anterior do Exchange. Use o Shell de Gerenciamento do Exchange para habilitar a recuperação de item individual de uma caixa de correio e configure ou modifique o período de retenção de itens excluídos. Para saber mais sobre como realizar uma recuperação de item individual, confira [Recuperar mensagens excluídas na caixa de correio de um usuário](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md).

Voltar ao início

## Retenção local e Retenção de litígio

No Exchange 2013 e no Exchange Online, os gerenciadores de descoberta podem usar a Descoberta Eletrônica In-loco com permissões delegadas do [Gerenciamento de Descobertas](discovery-management-exchange-2013-help.md) para realizar pesquisas de descoberta eletrônica de conteúdo de caixa de correio. O Exchange 2013 e o Exchange Online também apresentam o recurso Bloqueio In-loco, que serve para manter itens de caixa de correio correspondentes a parâmetros de consulta e para proteger itens contra exclusão por usuários ou por processos automatizados. Você também pode usar a Retenção de Litígio para manter todos os itens em caixas de correio de usuário e proteger itens contra exclusão por usuários ou por processos automatizados.

Colocar uma caixa de correio em Bloqueio In-loco ou em Retenção de Litígio impede que o Assistente de Pasta Gerenciada remova mensagens automaticamente das subpastas Retenções de Descoberta e Limpezas. Além disso, a proteção de página contra gravação de cópia também é habilitada para a caixa de correio. A proteção de página contra gravação de cópia cria uma cópia do item original antes de qualquer modificação ser gravada no repositório do Exchange. Depois que a caixa de correio é removida da retenção, o Assistente de Pasta Gerenciada retoma o processo de limpeza automática.

A tabela a seguir descreve o conteúdo e as ações que podem ser executadas na pasta Itens Recuperáveis quando a Retenção de Litígio está habilitada.

### Pasta Itens Recuperáveis e retenções

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
<th>Estado de retenção</th>
<th>A pasta Itens Recuperáveis contém itens excluídos permanentemente</th>
<th>A pasta Itens Recuperáveis contém itens modificados e apagados</th>
<th>Os usuários podem apagar itens da pasta Itens Recuperáveis</th>
<th>O Assistente de Pasta Gerenciada apaga automaticamente itens da pasta Itens Recuperáveis</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Habilitado</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
<td><p>Sim. Os usuários podem apagar itens usando o recurso Recuperar Itens Excluídos no Outlook ou Outlook Web App. No entanto, o Assistente de Pasta Gerenciada não remove permanentemente os itens do banco de dados da caixa de correio se ela estiver em espera.</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>Desabilitado</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


Para saber mais sobre a Descoberta Eletrônica In-loco, o Bloqueio In-loco e a Retenção de Litígio, confira os seguintes tópicos:

  - [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md)

  - [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md)

Voltar ao início

## proteção de página contra gravação de cópia e itens modificados

Quando um usuário colocado no Bloqueio In-loco ou na Retenção de Litígio modifica propriedades específicas de um item da caixa de correio, uma cópia do item da caixa de correio original é criada antes de o item modificado ser gravado. A cópia original é salva na subpasta Versões. Esse processo é conhecido como *proteção de página contra gravação de cópia*. A proteção de página contra gravação de cópia se aplica a itens que residem em qualquer pasta da caixa de correio. A subpasta Versões não é visível para os usuários.

A tabela a seguir lista as propriedades de mensagem que disparam a proteção de página contra gravação de cópia.

### Propriedades que disparam a proteção de página contra gravação de cópia

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de item</th>
<th>Propriedades que disparam a proteção de página contra gravação de cópia</th>
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
<li><p>Destinatários e remetentes</p></li>
<li><p>Datas de envio e recebimento</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Itens diferentes de mensagens e postagens</p></td>
<td><p>Qualquer alteração em uma propriedade visível, exceto:</p>
<ul>
<li><p>Localização do item (quando um item é movido entre pastas)</p></li>
<li><p>Alteração de status do item (lidas ou não lidas)</p></li>
<li><p>Alterações em uma marca de retenção aplicada a um item</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Itens na pasta padrão Rascunhos</p></td>
<td><p>Nenhum(a). Os itens na pasta Rascunhos são isentos da proteção de página contra gravação de cópia.</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> A proteção de página contra gravação de cópia não salva uma versão da reunião quando um organizador de reuniões recebe respostas dos participantes e as informações de controle da reunião são atualizadas. Além disso, as alterações em feeds RSS não são capturadas pela proteção de página contra gravação de cópia.



Quando uma caixa de correio é removida do Bloqueio In-loco ou da Retenção de Litígio, as cópias dos itens modificados na pasta Versões são removidas.

Voltar ao início

## Cotas de caixa de correio de Itens Recuperáveis

Quando um item é movido para a pasta Itens Recuperáveis, seu tamanho é deduzido da cota da caixa de correio e somado ao tamanho da pasta Itens Recuperáveis. No Exchange 2013, os bancos de dados de caixa de correio têm uma Cota de Aviso de Itens Recuperáveis configurável (*limite flexível*) de 20 GB e uma cota de Itens Recuperáveis (*limite rígido*) de 30 GB. Por padrão, esses limites são herdados por todas as caixas de correio no banco de dados. No entanto, é possível configurar caixas de correio individuais com cotas diferentes. Para saber mais, confira [Configurar cotas de itens recuperáveis e retenção de Item excluído](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md).

No Exchange Online, os limites padrão para a cota de Itens Recuperáveis são as mesmas do Exchange 2013; um limite flexível de 20 GB e um limite rígido de 30 GB. No entanto, as cotas da pasta Itens Recuperáveis é aumentada automaticamente para 90 GB e 100 GB, respectivamente, quando você coloca uma caixa de correio em Retenção de Litígio ou em Bloqueio In-loco.

Quando a pasta Itens Recuperáveis de uma caixa de correio atinge a cota de Itens Recuperáveis, nenhum outro item pode ser armazenado na pasta. Isso afeta a funcionalidade da caixa de correio das seguintes maneiras:

  - Os usuários da caixa de correio não podem excluir itens.

  - O Assistente de Pasta Gerenciada não pode excluir itens com base na marca de retenção ou nas configurações de pasta gerenciada.

  - Para caixas de correio com recuperação de item individual, Bloqueio In-loco ou Retenção de Litígio habilitados, o processo de proteção de página contra gravação de cópia não pode manter versões dos itens editados pelo usuário.

  - Para caixas de correio com log de auditoria de caixa de correio habilitada, nenhuma entrada de log de auditoria de caixa de correio pode ser salva na subpasta Auditorias.

Para caixas de correio colocadas em Bloqueio In-loco ou em Retenção de Litígio, o Assistente de Pasta Gerenciada limpa automaticamente os itens da pasta Itens Recuperáveis, quando o período de retenção de item excluído expira. Se a pasta atingir a Cota de Aviso de Itens Recuperáveis, o assistente removerá automaticamente os itens na ordem PEPS (primeiro a entrar, primeiro a sair).

Quando a pasta Itens Recuperáveis atinge os limites flexível e rígido padrão, o usuário é notificado por meio de um log de evento e um alerta do Microsoft System Center Operations Manager. Esse alerta é acionado quando a pasta Itens Recuperáveis primeiro atinge os limites flexível e rígido padrão e, depois disso, uma vez por dia.

A tabela a seguir lista os eventos registrados quando a pasta Itens Recuperáveis atinge os limites flexível e rígido padrão.

### Avisos e erros de cota de Itens Recuperáveis

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ID do Evento</th>
<th>Tipo</th>
<th>Origem</th>
<th>Mensagem</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10024</p></td>
<td><p>Aviso</p></td>
<td><p>Repositório de Caixas de Correio MSExchangeIS</p></td>
<td><p>A caixa de correio de &lt;<em>mailbox user</em>&gt; (<em>GUID</em>) excedeu a Cota de Aviso de Itens Recuperáveis. Remova itens dos Itens Recuperáveis ou aumente a Cota de Aviso de Itens Recuperáveis e a Cota de Itens Recuperáveis. Se a Cota de Itens Recuperáveis for excedida, o usuário não poderá excluir itens da caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p>10023</p></td>
<td><p>Erro</p></td>
<td><p>Repositório de Caixas de Correio MSExchangeIS</p></td>
<td><p>A caixa de correio de &lt;<em>mailbox user</em>&gt; (<em>GUID</em>) excedeu o nível máximo da Cota de Itens Recuperáveis. Não é possível excluir itens dessa caixa de correio. Informe ao proprietário da caixa de correio sobre o estado dessa caixa o mais rápido possível. Remova itens dos Itens Recuperáveis ou aumente a Cota de Itens Recuperáveis para restaurar a funcionalidade.</p></td>
</tr>
<tr class="odd">
<td><p>10023</p></td>
<td><p>Aviso</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>O tamanho dos Itens Recuperáveis da caixa de correio:&lt;<em>mailbox user</em>&gt; excedeu o limite de cota de avisos. Os itens foram excluídos das pastas de Itens Recuperáveis para evitar interrupção da caixa de correio. Cota de Aviso de Itens Recuperáveis: 20 GB (21.474.836.480 bytes) Tamanho original de Itens Recuperáveis: 21475005311 Tamanho atual de Itens Recuperáveis: Estatísticas da pasta 21474823820: – pastas processadas: RecoverableItemsRoot, RecoverableItemsVersions, RecoverableItemsPurges, RecoverableItemsDeletions - Tamanho original da pasta: 21391661934, 55190914, 1987247, 26157788 (contagem de item: 276828, 400, 84, 646) - Tamanho atual da pasta: 21391480443, 55190914, 1987247, 26157788 (contagem de item: 276817, 400, 84, 646)</p></td>
</tr>
</tbody>
</table>


Quando a caixa de correio é colocada em Bloqueio In-loco ou em Retenção de Litígio, a proteção de página contra gravação de cópia não pode manter versões de itens modificados. Para manter versões de itens modificados, é necessário reduzir o tamanho da pasta Itens Recuperáveis. Use o cmdlet [Search-Mailbox](https://technet.microsoft.com/pt-br/library/dd298173\(v=exchg.150\)) para copiar mensagens da pasta Itens Recuperáveis de uma caixa de correio para uma caixa de correio de descoberta e, em seguida, exclua os itens da caixa de correio. Como alternativa, também é possível aumentar a cota de Itens Recuperáveis para a caixa de correio. Para saber mais, confira [Limpar a pasta itens recuperáveis](clean-up-the-recoverable-items-folder-exchange-2013-help.md).

Voltar ao início

## Mais informações

  - A cópia em gravação é habilitada apenas quando a caixa de correio está em Bloqueio In-loco ou em Retenção de Litígio.

  - Caso os usuários precisem recuperar itens excluídos da pasta Itens Recuperáveis, direcione-os para os tópicos a seguir:
    
      - [Restaurar itens excluídos no Outlook](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [Recuperar itens ou emails excluídos no Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=524924)

Voltar ao início

