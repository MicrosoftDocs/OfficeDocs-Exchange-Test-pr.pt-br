---
title: 'Entendendo a anulação de página no Exchange 2013: Exchange 2013 Help'
TOCTitle: Entendendo a anulação de página no Exchange 2013
ms:assetid: 0ca7b188-efbc-4c0d-bcfe-5138cffc803c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg549096(v=EXCHG.150)
ms:contentKeyID: 61638519
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Entendendo a anulação de página no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

## Anulação de página no Exchange 2013

*Anulação* é um mecanismo de segurança que grava zeros ou um padrão binário sobre dados excluídos de modo que seja mais difícil recuperar os dados excluídos. No Exchange Server 2013, um banco de dados ESE usa *páginas* como sua unidade de armazenamento e, como resultado, implementa a *anulação de página*. A anulação de página está habilitada por padrão e não pode ser desabilitada. As operações de anulação de página são registradas nos arquivos de log de transações, para que todas as cópias de um banco de dados passem pela anulação de página de forma semelhante. Anular uma página em um banco de dados ativo faz com que a página seja zerada em uma cópia passiva do banco de dados.


> [!TIP]
> Não há mecanismo para que o Mecanismo de Armazenamento Extensível (ESE) dê prioridade à reutilização de páginas anuladas sobre a alocação de novo espaço. Tabelas com alocação de espaço sequencial atribuída irão ignorar propositalmente páginas fragmentadas ou anuladas em prol da utilização de páginas sequenciais novas ou livres. Esta abordagem reduz os IOPs do banco de dados.



No Exchange 2013, a anulação de página reduz o impacto no desempenho em servidores quando eles estão executando funções de anulação. Isso inclui:

  - **Capacidade otimizada de rede e armazenamento** O ESE grava um registro de anulação de página no arquivo de log de transações em vez de registrar toda a imagem da página. Essa abordagem reduz a E/S de gravação no log e reduz os requisitos de largura de banda para envio de arquivos de log.

  - **Disco de banco de dados otimizado e/s**   Na Exchange 2010 RTM anteriormente, anulação de página ocorreu durante o backup ou durante manutenção programada e ele causou e/s de disco de banco de dados significativas. Na Exchange 2010 SP1 e posterior (inclusive Exchange 2013 ), página anulação ocorre por padrão e acontece no momento da transação. Na maioria dos casos, anulação ocorre imediatamente depois de uma exclusão de disco rígida. Este projeto permite que o banco de dados utilizar a capacidade de profundidade do ponto de verificação do mecanismo de, que assegura que páginas dirty permaneçam no cache de banco de dados para um determinado período de tempo para que as atualizações de página adicional que ocorrem no fechar proximidade não causar a gravação do banco de dados adicionais e/SS de tempo. Devido a esse projeto, a anulação de página não tem nenhum banco de dados significativo impacto de e/s, o motivo pelo qual ele é habilitado por padrão.

## Implementação da anulação de página no banco de dados do ESE

A anulação de página grava um padrão binário sobre um registro que foi excluído de forma irreversível. O padrão de anulação de página é específico da operação do mecanismo do ESE, e é diferente para operações em tempo de execução e operações de manutenção. A tabela a seguir lista os padrões de preenchimento que correspondem a operações em tempo de execução específicas.

### Padrão de preenchimento da anulação de página durante o tempo de execução do ESE

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Operação em tempo real do ESE</th>
<th>Padrão de preenchimento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Substituir</p></td>
<td><p>N</p></td>
</tr>
<tr class="even">
<td><p>Exclusão de valor longo/registro</p></td>
<td><p>D</p></td>
</tr>
<tr class="odd">
<td><p>Liberação de espaço em página</p></td>
<td><p>H</p></td>
</tr>
</tbody>
</table>


A tabela a seguir lista os padrões de preenchimento que correspondem a operações específicas que ocorrem durante a manutenção de banco de dados em segundo plano do ESE.

### Padrão de preenchimento da anulação de página durante manutenção de banco de dados em segundo plano do ESE

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Operação de manutenção de banco de dados em segundo plano do ESE</th>
<th>Padrão de preenchimento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exclusão de gravação</p></td>
<td><p>D</p></td>
</tr>
<tr class="even">
<td><p>Exclusão de valor longo</p></td>
<td><p>L</p></td>
</tr>
<tr class="odd">
<td><p>Liberação de espaço em página parcialmente utilizada</p></td>
<td><p>Z</p></td>
</tr>
<tr class="even">
<td><p>Liberação de espaço em página não utilizada</p></td>
<td><p>U</p></td>
</tr>
</tbody>
</table>


## Manutenção de banco de dados em segundo plano

A manutenção de banco de dados em segundo plano é um processo que realiza continuamente somas de verificação e examina cada banco de dados. Sua função principal é realizar a soma de verificação de páginas de banco de dados, mas também lida com a limpeza de espaço e anulação de registros e páginas que não foram anulados por uma falha do Armazenamento. A manutenção de banco de dados em segundo plano processa aproximadamente 1 MB por segundo por banco de dados. Se a anulação de página em tempo hábil for uma prioridade, é possível reduzir os tamanhos de bancos de dados para garantir que a anulação de página ocorra para os casos de recuperação de falhas em um período de tempo mais curto (por exemplo, 24 horas).

A manutenção de banco de dados em segundo plano é um processo contínuo, portanto não há eventos associados ao seu início e à sua conclusão. Você pode controlar o progresso da manutenção de banco de dados em segundo plano lendo o valor de um contador de desempenho:

  - Banco de dados do MSExchange -\>Instâncias -\>Duração da manutenção de banco de dados

Esse contador indica o número de segundos passados desde a última manutenção concluída em um banco de dados.

## Processo de anulação de página do banco de dados do ESE

A tabela a seguir discute os cenários de exclusão de banco de dados, e quando as funções de anulação de página ocorrem.

### Manutenção de banco de dados ESE em segundo plano

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cenário de exclusão de banco de dados</th>
<th>Processo do ESE e tempo para anulação dos dados do banco de dados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Cenário 1: A recuperação de item único está desabilitada, e o usuário limpa o item da pasta de Itens Recuperáveis.</p></li>
<li><p>Cenário 2: A recuperação de item único está desabilitada, e o período de retençãode Itens Recuperáveis está definido como zero.</p></li>
<li><p>Cenário 3: A recuperação de item único está habilitada, e o item expira com base no período de retenção de item excluído.</p></li>
</ul></td>
<td><p>Um thread assíncrono grava um padrão binário sobre os dados excluídos. Essa ação ocorre milissegundos após a exclusão do registro. Se o processo de armazenamento falhar enquanto a operação de anulação assíncrona estiver em curso (ou se a limpeza do armazenamento de versão for cancelada devido ao crescimento do armazenamento de versão), a anulação será concluída quando a manutenção de banco de dados em segundo plano processar essa seção do banco de dados.</p></td>
</tr>
<tr class="even">
<td><p>Cenário de exibição: Expiração de itens da exibição de pastas do Outlook/Outlook Web App (por exemplo, a exibição de conversa).</p></td>
<td><p>A anulação de dados ocorre quando uma manutenção de banco de dados em segundo plano processa esta seção do banco de dados.</p></td>
</tr>
<tr class="odd">
<td><p>Cenário de movimentação/exclusão de caixa de correio: Caixa de correio de origem excluída (expiração de caixa de correio excluída do dumpster)</p></td>
<td><p>A anulação de dados ocorre quando uma manutenção de banco de dados em segundo plano processa esta seção do banco de dados.</p></td>
</tr>
</tbody>
</table>


## Monitorando o comportamento da anulação de página

Você pode medir e monitorar a funcionalidade de anulação de página exibindo dois contadores de ESE:

  - Banco de dados do MSExchange-\>Páginas anuladas pela manutenção de banco de dados: Indica o número de páginas anuladas pelo mecanismo de banco de dados desde que o contador de desempenho foi invocado.

  - Banco de dados do MSExchange-\>Páginas anuladas pela manutenção de banco de dados por segundo: Indica a taxa de anulação de páginas.


> [!TIP]
> Para saber como habilitar esses contadores, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=101194">como habilitar contadores de desempenho de ESE estendido</A>.



A anulação de página é uma função de manutenção de banco de dados, portanto as informações de desempenho relacionadas tanto à anulação de página para transações em tempo de execução quanto à anulação de página causada pela manutenção de banco de dados em segundo plano estão incluídas nesse contador.

## Tipos de dados de caixa de correio sem anulação de página

Os seguintes tipos de dados de Caixa de correio não têm provisões para anulação de página:

  - Logs de transações de banco de dados de caixa de correio (.log)
    
    Quando logs de transações são excluídos (devido ao truncamento via backup ou log circular), não há processo para zerar os blocos no sistema de arquivos NTFS que armazenou o arquivo de log excluído. É provável que o NTFS reutilize rapidamente esse espaço disponível para a criação de novos logs, mas não há garantia de que isso vá acontecer.

  - Arquivos de catálogo de índice de conteúdo
    
    O Exchange 2013 usa o Search Foundation para a funcionalidade de indexação de pesquisa. O catálogo de índice de pesquisa é composto por várias dezenas de arquivos armazenados no mesmo volume do arquivo de banco de dados de caixa de correio. Quando um arquivo é excluído de forma irreversível do banco de dados de caixa de correio, o conteúdo associado no catálogo de pesquisa não é excluído imediatamente. A exclusão de conteúdo ocorre quando o Search Foundation faz uma sombra, ou mesclagem mestre, de vários pequenos arquivos de catálogo em um único arquivo maior. Depois que a mesclagem mestre é concluída, os arquivos menores de catálogo são excluídos. Não há processo para anular os blocos que armazenavam os arquivos de catálogo excluídos.

