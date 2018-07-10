---
title: 'Solicitações de importação e exportação da caixa de correio: Exchange 2013 Help'
TOCTitle: Solicitações de importação e exportação da caixa de correio
ms:assetid: 157a7d88-d3aa-4056-9a50-df67451b14be
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633455(v=EXCHG.150)
ms:contentKeyID: 50485077
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Solicitações de importação e exportação da caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Usando os conjuntos de cmdlets **MailboxImportRequest** ou **MailboxExportRequest** no Shell de Gerenciamento do Exchange, é possível importar ou exportar dados de arquivos .pst. Depois de iniciada uma solicitação de importação ou exportação, o processo é concluído de forma assíncrona pelo MRS (Serviço de Replicação de Caixa de Correio) do Microsoft Exchange. O MRS reside em todos os servidores de Acesso para Cliente do Exchange 2010 e é o serviço responsável por mover caixas de correio e importar e exportar arquivos .pst.

**Sumário**

Motivos para importar ou exportar dados de caixa de correio

Vantagens no uso de solicitações de importação e exportação

Considerações

Importar dados de caixa de correio

Exportar dados de caixa de correio

## Motivos para importar ou exportar dados de caixa de correio

Você pode querer importar ou exportar dados de caixa de correio pelos seguintes motivos:

  - **Satisfazer requisitos de conformidade**   O conteúdo de uma caixa de correio pode ser exportado para um arquivo .pst para descoberta legal. Depois que a exportação é concluída, você pode importar o conteúdo para uma caixa de correio usada especificamente para fins de conformidade.

  - **Criar um instantâneo pontual de uma caixa de correio**   Crie um instantâneo de caixas de correio específicas para não ter que manter um conjunto inteiro de backup para um banco de dados de caixa de correio.

  - **Mover o arquivo .pst de um usuário para sua respectiva caixa de correio ou arquivo morto pessoal**   Os usuários do Microsoft Outlook podem salvar seus emails localmente como arquivos .pst. Com o cmdlet [New-MailboxImportRequest](https://technet.microsoft.com/pt-br/library/ff607310\(v=exchg.150\)), você pode mover dados do arquivo .pst de um usuário para sua respectiva caixa de correio ou arquivo morto pessoal. Trata-se de um método simples para transferir emails do computador local de um usuário para os servidores do Exchange.

## Vantagens no uso de solicitações de importação e exportação

As vantagens de se usar solicitações de importação e exportação no Exchange 2013 incluem o seguinte:

  - Um provedor de .pst está incluído no Exchange 2013 e é capaz de ler e gravar arquivos .pst.

  - As solicitações de importação e exportação são assíncronas. O processo é realizado pelo MRS, que tira proveito das estruturas de enfileiramento e limitação.

  - Os arquivos .pst podem ser importados diretamente para o arquivo morto pessoal de um usuário.

  - Vários arquivos .pst podem ser importados ou exportados ao mesmo tempo.

  - Os arquivos .pst podem residir em qualquer unidade de rede compartilhada acessível pelos seus servidores do Exchange.

  - O Exchange 2013suporta estes arquivos .pst: Arquivos Unicode criados pelo Office Outlook 2007 e pelo Outlook 2010

## Considerações

Antes de importar ou exportar dados de caixa de correio, considere o seguinte:

  - Para importar ou exportar dados de caixa de correio, uma pasta compartilhada de rede acessível pelos seus servidores do Exchange deve estar configurada. Você também deve conceder permissões de leitura/gravação ao grupo Subsistema Confiável do Exchange para que o grupo possa acessar o compartilhamento de rede onde você importa e exporta dados de caixa de correio. Se você não conceder essa permissão, receberá uma mensagem de erro indicando que o Exchange não é capaz de estabelecer uma conexão com a caixa de correio de destino.

  - O tamanho máximo de arquivo .pst aceito pelo Outlook é de 50 gigabytes (GB). Portanto, não recomendamos a importação de um arquivos .pst maior do que 50 GB. Você pode criar vários arquivos .pst para caixas de correio com mais de 50 GB especificando pastas a serem incluídas ou excluídas, ou usando um filtro de conteúdo.

  - As solicitações de importação e exportação são realizadas pelo MRS, que também processa solicitações de movimentação e de restauração de caixa de correio. Todas as solicitações são enfileiradas e limitadas pelo MRS.

  - A importação e a exportação de dados de caixa de correio podem levar horas dependendo do tamanho do arquivo, da largura de banda da rede e da limitação do MRS.

  - Você não pode importar dados para uma pasta pública ou banco de dados de pasta pública.

## Importar dados de caixa de correio

Utilize o conjunto de cmdlets **MailboxImportRequest** para importar os dados de um arquivo .pst para uma caixa de correio ou arquivo morto pessoal. Esta é uma lista de opções que você pode especificar ao importar os dados de caixas de correio de um arquivo .pst:


> [!TIP]
> A caixa de correio para a qual você vai importar os dados precisa existir. Você não pode importar dados para uma conta de usuário que não possua uma caixa de correio.



  - Os dados podem ser importados para uma conta de usuário diferente da qual eles foram exportados. Por exemplo, é possível exportar dados de vinicius@contoso.com e importá-los para descobertajuridica@contoso.com.

  - Os itens podem ser importados apenas para o arquivo morto pessoal do usuário especificando o parâmetro *IsArchive*.

  - Se as mensagens de pastas associadas existirem no arquivo .pst, elas poderão ser importadas com o parâmetro *AssociatedMessagesCopyOption*. As mensagens associadas contêm dados ocultos com informações sobre regras, exibições e formulários. Se existirem no arquivo .pst, todas as mensagens da rede de segurança serão importadas.

  - Você pode incluir ou excluir pastas específicas usando o parâmetro *IncludeFolders* ou *ExcludeFolders*.

  - A pasta Itens Recuperáveis pode ser excluída com o parâmetro *ExcludeDumpster*. Por padrão, uma solicitação de importação inclui a pasta Itens Recuperáveis do usuário, caso esteja presente no arquivo .pst.

## Cmdlets de solicitação de importação de caixa de correio

Use os cmdlets a seguir para solicitações de importação de caixa de correio.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607310(v=exchg.150)">New-MailboxImportRequest</a></p></td>
<td><p>Inicia o processo de importação de um arquivo .pst para uma caixa de correio ou arquivo morto pessoal. Você pode criar mais de uma solicitação de importação por caixa de correio. Cada solicitação deve ter um nome exclusivo.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607317(v=exchg.150)">Set-MailboxImportRequest</a></p></td>
<td><p>Muda as opções de solicitação de importação depois que a solicitação é criada ou se recupera de uma solicitação fracassada.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607309(v=exchg.150)">Suspend-MailboxImportRequest</a></p></td>
<td><p>Suspende a qualquer momento uma solicitação de importação após ela ter sido criada e antes de ter atingido o status de Concluída.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607306(v=exchg.150)">Resume-MailboxImportRequest</a></p></td>
<td><p>Retoma uma solicitação de importação que foi suspensa ou falhou.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607311(v=exchg.150)">Remove-MailboxImportRequest</a></p></td>
<td><p>Remove completamente ou parcialmente as solicitações de importação concluídas. As solicitações de importação concluídas não são limpas automaticamente. Você deve usar este cmdlet para removê-las.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607368(v=exchg.150)">Get-MailboxImportRequest</a></p></td>
<td><p>Exibe informações gerais sobre uma solicitação de importação.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607315(v=exchg.150)">Get-MailboxImportRequestStatistics</a></p></td>
<td><p>Exibe informações detalhadas sobre uma solicitação de importação.</p></td>
</tr>
</tbody>
</table>


## Exportar dados de caixa de correio

Use o conjunto de cmdlets **MailboxExportRequest** para exportar dados de caixa de correio para um arquivo .pst. Você pode exportar uma ou várias caixas de correio, mas apenas uma solicitação é gravada em cada arquivo .pst por vez. Esta é uma lista de opções que você pode especificar ao exportar os dados de caixa de correio para um arquivo .pst:

  - Para exportar dados de arquivo morto pessoal, use o parâmetro *IsArchive*.

  - Para filtrar as mensagens que são exportadas, use o parâmetro *ContentFilter*. Você pode filtrar por conteúdo da mensagem, anexo, remetentes, destinatários, categoria de caixa de entrada, importância, tipo de mensagem, tamanho da mensagem e data de envio, recebimento ou expiração da mensagem.

  - Você pode incluir ou excluir pastas específicas usando o parâmetro *IncludeFolders* ou *ExcludeFolders*. Ao exportar dados de uma caixa de correio do Exchange 2013, você também pode excluir a pasta Itens Recuperáveis com o parâmetro *ExcludeDumpster*.

  - Para exportar mensagens associadas, use o parâmetro *AssociatedMessagesCopyOption*. As mensagens associadas contêm dados ocultos com informações sobre regras, exibições e formulários. Por padrão, os itens associados não são copiados para o arquivo .pst.

## Cmdlets de solicitação de exportação de caixa de correio

Use os cmdlets a seguir para solicitações de exportação de caixa de correio.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607299(v=exchg.150)">New-MailboxExportRequest</a></p></td>
<td><p>Inicia o processo de exportação de dados de uma caixa de correio principal ou arquivo morto pessoal para um arquivo .pst. Você pode criar mais de uma solicitação de exportação por caixa de correio. Cada solicitação deve ter um nome exclusivo.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607312(v=exchg.150)">Set-MailboxExportRequest</a></p></td>
<td><p>Muda as opções de solicitação de exportação depois que a solicitação é criada ou se recupera de uma solicitação fracassada.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607305(v=exchg.150)">Suspend-MailboxExportRequest</a></p></td>
<td><p>Suspende a qualquer momento uma solicitação de exportação após ela ter sido criada e antes de ter atingido o status de Concluída.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607476(v=exchg.150)">Resume-MailboxExportRequest</a></p></td>
<td><p>Retoma uma solicitação de exportação que foi suspensa ou falhou.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607464(v=exchg.150)">Remove-MailboxExportRequest</a></p></td>
<td><p>Remove completamente ou parcialmente as solicitações de exportação concluídas. As solicitações de exportação concluídas não são limpas automaticamente. Você deve usar este cmdlet para removê-las.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607479(v=exchg.150)">Get-MailboxExportRequest</a></p></td>
<td><p>Exibe informações gerais sobre uma solicitação de exportação.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/ff607316(v=exchg.150)">Get-MailboxExportRequestStatistics</a></p></td>
<td><p>Exibe informações detalhadas sobre uma solicitação de exportação.</p></td>
</tr>
</tbody>
</table>

