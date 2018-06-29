---
title: 'AutoReseed: Exchange 2013 Help'
TOCTitle: AutoReseed
ms:assetid: 61f9a8be-070e-4c62-b505-52644fcff0c5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn789209(v=EXCHG.150)
ms:contentKeyID: 62523811
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AutoReseed

 

_**Aplica-se a:**Exchange Server 2013 SP1_

_**Tópico modificado em:**2015-03-09_

Nova propagação automática ou AutoReseed, é um recurso que é o substituto do que é normalmente controlado pelo administrador de ação em resposta a uma falha de disco, evento de corrupção do banco de dados ou outro problema que necessita de uma nova propagação de uma cópia do banco de dados. AutoReseed foi projetado para restaurar automaticamente a redundância de banco de dados após uma falha de disco usando discos sobressalentes que tenham sido configurados no sistema.

## Visão geral da AutoReseed

Em uma configuração da AutoReseed, é usada uma estrutura de apresentação de armazenamento padronizada e o administrador escolhe o ponto de partida. A AutoReseed deve restaurar a redundância assim que possível após a falha de uma unidade. Isso envolve o pré-mapeamento de um conjunto de volumes (incluindo volumes de reserva) e bancos de dados que usam pontos de montagem. No caso de uma falha de disco em que o disco não está mais disponível para o sistema operacional ou para gravação, um volume de reserva é alocado pelo sistema, e as cópias de banco de dados afetadas são propagadas novamente de forma automática.

1.  O Microsoft Exchange serviço de replicação periodicamente verifica que têm um status de FailedAndSuspended. Se todas as cópias de banco de dados em um volume configuradas para o AutoReseed estiverem em um estado de FailedandSuspended por 15 minutos consecutivos, o fluxo de trabalho do AutoReseed é iniciado.

2.  AutoReseed tentará retomar as cópias com falha e suspensas até três vezes, com uma suspensão de 5 minutos entre cada tentativa. Às vezes, depois que uma cópia do banco de dados de FailedandSuspended é reiniciada, a cópia permanece em um estado de falha. Isso pode acontecer por vários motivos, portanto, esta etapa é desenvolvida para lidar com esses casos; AutoReseed suspenderá automaticamente uma cópia do banco de dados que falhou por 10 minutos consecutivos manter o fluxo de trabalho em execução. Se as ações de suspender e retomar não resultarem em uma cópia do banco de dados íntegro, o fluxo de trabalho continua.

3.  Quando encontrar uma cópia com esse status, ele executa algumas verificações de pré-requisito. Por exemplo, ele verificará se um disco sobressalente está disponível e se o banco de dados e seus arquivos de log estão configurados no mesmo volume e nos locais apropriados que coincidem com as convenções de nomeação necessárias.

4.  Se as verificações do pré-requisito forem aprovadas com êxito, o Disk Reclaimer função dentro do serviço de replicação do Microsoft Exchange aloca, mapeia novamente e formata um disco sobressalente de acordo com os cronogramas na tabela a seguir. AutoReseed tentará atribuir um volume sobressalente até 5 vezes, com 1 hora dormem entre cada tentativa.

5.  Depois que tiver sido atribuído um volume de reserva, AutoReseed irá realizar uma operação de InPlaceSeed usando o SafeDeleteExistingFiles switch de propagação. Todos os bancos de dados que estavam no disco afetado são propagados novamente, usando a cópia ativa do banco de dados como a fonte da propagação.

6.  Após o término da operação de propagação, o serviço de Replicação do Microsoft Exchange verifica se a cópia recém-propagada está adequada.

Depois que todas as novas tentativas são esgotadas, interrompe o fluxo de trabalho. Se, depois de 3 dias, a cópia do banco de dados ainda for FailedandSuspended, o estado de fluxo de trabalho é redefinido e ele inicia novamente da etapa 1. Esse comportamento reset/continuar é útil (e intencionais) desde que pode levar alguns dias para substituir um disco com falha, controlador, etc.

Neste ponto, se a falha tiver sido uma no disco, será preciso a intervenção manual de um operador ou administrador para remover e substituir o disco com falha e reconfigurar o disco de substituição como reserva.

A AutoReseed é configurada usando três propriedades do DAG. Duas das propriedades se referem aos dois pontos de montagem que estão em uso. O Exchange 2013 aproveita o fato de que o Windows Server permite vários pontos de montagem por volume. A propriedade *AutoDagVolumesRootFolderPath* se refere ao ponto de montagem que contém todos os volumes disponíveis. Isso inclui os volumes que hospedam bancos de dados e volumes de reserva. A propriedade *AutoDagDatabasesRootFolderPath* se refere ao ponto de montagem que contém os bancos de dados. Uma terceira propriedade do DAG, *AutoDagDatabaseCopiesPerVolume*, é usada para configurar a quantidade de cópias de banco de dados por volume.

Um exemplo de configuração da AutoReseed é ilustrado abaixo.

**Exemplo de configuração de AutoReseed**

![Exemplo de configuração de nova propagação automática](images/Dn789209.e3af7306-f5b4-4ec4-9ccf-222ec452699b(EXCHG.150).gif "Exemplo de configuração de nova propagação automática")

Nesse exemplo, há três volumes, dois dos quais conterão bancos de dados (VOL1 e VOL2) e um será um volume de reserva formatado em branco (VOL3).

Para configurar a AutoReseed:

1.  Os três volumes são montados sob um ponto de montagem único. Neste exemplo, o ponto de montagem C:\\ExchVols é usado. Isso representa o diretório usado para obter o armazenamento de bancos de dados do Exchange.

2.  O diretório raiz dos bancos de dados de caixa de correio é montado como outro ponto de montagem. Neste exemplo, o ponto de montagem C:\\ExchDBs é usado. Em seguida, uma estrutura de diretório é criada para que um diretório pai seja criado para o banco de dados. E, no diretório pai, dois subdiretórios são criados: um para arquivo de banco de dados e um para os arquivos de log.

3.  Bancos de dados são criados. O exemplo acima mostra um design simples que usa um banco de dados único por volume. Assim, em VOL1, existem três diretórios: o diretório pai e dois subdiretórios (um para o arquivo de banco de dados de MDB1 e um para seus logs). Embora não seja detalhado na imagem de exemplo, em VOL2, haveria também três diretórios: o diretório pai e, abaixo dele, um diretório para o arquivo de banco de dados de MDB2 e um para seus arquivos de log.

Nessa configuração, se MDB1 ou MDB2 falhar, uma cópia do banco de dados com falha será propagada novamente para VOL3 de forma automática.

## Disk Reclaimer

O componente da AutoReseed que aloca e formata discos sobressalentes é chamado de *Disk Reclaimer*. O componente Disk Reclaimer formata automaticamente os discos sobressalentes em preparação para nova propagação automática em diferentes intervalos, dependendo do estado do disco. Para que o Disk Reclaimer formate um disco, certas condições devem ser atendidas:

  - O Disk Reclaimer deve estar habilitado. Ele está ativado por padrão, mas pode ser desativado usando [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)).

  - O volume deve ter um ponto de montagem no caminho de volumes raiz (por padrão, C:\\ExchangeVolumes).

  - O volume não deve ter pontos de montagem no caminho dos volumes do banco de dados (por padrão, C:\\ExchangeDatabases).

  - Se o volume contiver algum arquivo, nenhum deles deve ter sido tocado por 24 horas.

Além das condições acima, o Disk Reclaimer só tentará formatar um determinado volume uma vez por dia. A tabela a seguir descreve o comportamento de formatação do Disk Reclaimer.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Estado do disco e cópias de banco de dados</th>
<th>Intervalo de formatação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Disco não formatado; formatado, mas vazio; ou formatado, mas contendo arquivos que não foram tocados por 24 horas, e há cópias ativas adequadas do banco de dados no site local do Active Directory que podem ser usadas como fonte de propagação.</p></td>
<td><p>1 dia</p></td>
</tr>
<tr class="even">
<td><p>Disco não formatado; formatado, mas vazio; ou formatado, mas contendo arquivos que não foram tocados por 24 horas, mas não há cópias ativas adequadas do banco de dados no site local do Active Directory que podem ser usadas como fonte de propagação.</p></td>
<td><p>2 dias</p></td>
</tr>
<tr class="odd">
<td><p>Disco não formatado; formatado, mas vazio; ou formatado, mas contendo arquivos que não foram tocados por 24 horas, e há cópias ativas adequadas do banco de dados no site local do Active Directory que podem ser usadas como fonte de propagação, mas há arquivos desconhecidos fora do arquivo do banco de dados (arquivo EDB) e arquivos de log.</p></td>
<td><p>2 semanas</p></td>
</tr>
<tr class="even">
<td><p>Disco não formatado; formatado, mas vazio; ou formatado, mas contendo arquivos que não foram tocados por 24 horas, e há cópias ativas adequadas do banco de dados no site local do Active Directory que podem ser usadas como fonte de propagação, mas há um ou mais arquivos de banco de dados (arquivos EDB) para bancos de dados que não aparecem no Active Directory.</p></td>
<td><p>2 semanas</p></td>
</tr>
</tbody>
</table>

