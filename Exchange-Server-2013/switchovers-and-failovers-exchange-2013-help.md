---
title: 'Switchovers e Failovers: Exchange 2013 Help'
TOCTitle: Switchovers e Failovers
ms:assetid: 75388645-cae1-402e-bf02-c4949d3e2c31
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298067(v=EXCHG.150)
ms:contentKeyID: 62523812
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Switchovers e Failovers

 

_**Aplica-se a:** Exchange Server 2013 SP1_

_**Tópico modificado em:** 2015-12-02_

Alternâncias e failovers são duas formas de interrupções no Microsoft Exchange Server 2013.

  - Uma *alternância* é uma interrupção agendada de um banco de dados ou o servidor que explicitamente é iniciado por um cmdlet ou pelo sistema de disponibilidade gerenciada no Exchange 2013. Alternâncias são normalmente feitas para se preparar para a realização de uma operação de manutenção. Alternâncias envolvem mover a cópia de banco de dados de caixa de correio ativas para outro servidor no grupo de disponibilidade de banco de dados (DAG). Se nenhum destino Íntegro for encontrado durante uma alternância, administradores receberá um erro e o banco de dados de caixa de correio permanecerá backup ou montado.

  - Um *failover* se refere a eventos inesperados que resultam em indisponibilidade de serviços, dados ou ambos. Um failover envolve o sistema automaticamente recuperar da falha por Ativando uma cópia do banco de dados de caixa de correio passiva para torná-la a cópia de banco de dados de caixa de correio ativas. Se nenhum destino Íntegro for encontrado durante um failover, o banco de dados de caixa de correio será desmontado.

O Exchange 2013 é projetado especificamente para lidar tanto com alternâncias quanto com failovers.

Procurando tarefas de gerenciamento relacionadas à alta disponibilidade e à resiliência de site? Consulte [Gerenciando a alta disponibilidade e resiliência do site](managing-high-availability-and-site-resilience-exchange-2013-help.md).

## Alternâncias

Há três tipos de alternâncias no Exchange 2013:

  - Alternâncias de banco de dados

  - Alternâncias de servidor

  - Alternâncias de datacenter

## Alternâncias de banco de dados

Uma *alternância de banco de dados* é o processo por meio do qual um banco de dados ativo individual é trocado por outra cópia do banco de dados (uma cópia passiva), e essa cópia do banco de dados torna-se a nova cópia do banco de dados ativo. Alternâncias de banco de dados podem acontecer dentro de datacenters e entre eles. Uma alternância de banco de dados pode ser realizada pelo Centro de administração do Exchange (EAC) ou pelo Shell. Independentemente da interface usada, o processo de alternância é o seguinte:

1.  O administrador inicia uma alternância de banco de dados para mover a cópia atual do banco de dados da caixa de correio ativa para outro servidor.

2.  O cliente utilizado para a tarefa realiza uma chamada RPC para o serviço de Replicação do Microsoft Exchange em um membro do DAG.

3.  Se o membro do DAG não mantiver a função de Gerenciador Ativo Primário (PAM), este remeterá a tarefa para o servidor que mantiver a função PAM.

4.  A tarefa realiza uma chamada RPC para o serviço de Replicação do Microsoft Exchange no servidor que mantém a função PAM.

5.  O PAM lê e atualiza as informações de localização do banco de dados que estão armazenadas no banco de dados de cluster do DAG.

6.  O PAM entra em contato com o serviço de Replicação do Microsoft Exchange no membro do DAG cuja cópia passiva está sendo ativada como a nova cópia do banco de dados da caixa de correio ativa.

7.  O serviço de Replicação do Microsoft Exchange no servidor de destino consulta os serviços de Replicação do Microsoft Exchange em todos os outros membros do DAG para determinar a melhor fonte de log para a cópia do banco de dados.

8.  O banco de dados do servidor atual é desmontado, e o serviço de Replicação do Microsoft Exchange no servidor de destino copia os logs restantes para o servidor de destino.

9.  O serviço de Replicação do Microsoft Exchange no servidor de destino solicita a montagem de um banco de dados.

10. O serviço de Armazenamento de Informações do Microsoft Exchange no servidor de destino repete os arquivos de log e monta o banco de dados.

11. Quaisquer códigos de erro são retornados para o serviço de Replicação do Microsoft Exchange do servidor de destino.

12. O PAM atualiza as informações do estado da cópia do banco de dados no banco de dados de cluster do DAG.

13. Quaisquer códigos de erro são retornados pelo serviço de Replicação do Microsoft Exchange do servidor de destino para o serviço de Replicação do Microsoft Exchange do PAM.

14. O serviço de Replicação do Microsoft Exchange do PAM retorna quaisquer erros para a interface administrativa em que a tarefa foi chamada.

15. O PowerShell Remoto retorna os resultados da operação para a interface administrativa de chamada.

Para obter etapas detalhadas sobre como realizar um alternância de banco de dados, consulte [Ativar uma cópia do banco de dados de caixa de correio](activate-a-mailbox-database-copy-exchange-2013-help.md).

## Alternâncias de servidor

Uma alternância de servidor é o processo pelo qual todos os bancos de dados ativos em um membro do DAG são ativados em um ou mais outros membros do DAG. Assim como a alternância de banco de dados, uma alternância de servidor pode ocorrer tanto dentro de um mesmo datacenter quanto entre datacenters, e pode ser iniciada com o uso do EAC e do Shell. Independentemente da interface utilizada, o processo de alternância do servidor é o seguinte:

1.  O administrador inicia uma alternância de servidor para mover todas as cópias atuais do banco de dados da caixa de correio ativas para um ou mais servidores diferentes.

2.  A tarefa segue as mesmas etapas descritas anteriormente, neste tópico, para alternâncias de banco de dados (Etapas 2 a 4) para cada um dos bancos de dados ativos no servidor atual.

3.  O PAM lê e atualiza as informações de localização do banco de dados que estão armazenadas no banco de dados de cluster do DAG.

4.  O PAM entra em contato com o serviço de Replicação do Microsoft Exchange de cada membro do DAG que possui uma cópia passiva sendo ativada.

5.  O serviço de Replicação do Microsoft Exchange nos servidores de destino consulta os serviços de Replicação do Microsoft Exchange em todos os outros membros do DAG para determinar a melhor fonte de log para a cópia do banco de dados.

6.  O banco de dados do servidor atual é desmontado, e o serviço de Replicação do Microsoft Exchange de cada servidor de destino copia os logs restantes.

7.  O serviço de Replicação do Microsoft Exchange em cada servidor de destino solicita a montagem de um banco de dados.

8.  O serviço de Armazenamento de Informações do Microsoft Exchange de cada servidor de destino repete os arquivos de log e monta o banco de dados.

9.  Quaisquer códigos de erro são retornados para o serviço de Replicação do Microsoft Exchange do servidor de destino.

10. O PAM atualiza as informações do estado da cópia do banco de dados no banco de dados de cluster do DAG.

11. Quaisquer códigos de erro são retornados pelo serviço de Replicação do Microsoft Exchange do servidor de destino para o serviço de Replicação do Microsoft Exchange do PAM.

12. O serviço de Replicação do Microsoft Exchange do PAM retorna quaisquer erros para a interface administrativa em que a tarefa foi chamada.

13. O PowerShell Remoto retorna os resultados da operação para a interface administrativa de chamada.

Para obter etapas detalhadas sobre como realizar uma alternância de servidor, consulte [Alternar um Servidor](perform-a-server-switchover-exchange-2013-help.md).

## Alternâncias de datacenter

Em uma configuração resiliente do site, a recuperação automática como resposta a uma falha no nível do site pode ocorrer dentro de um DAG, o que permite que o sistema de mensagens permaneça em um estado funcional. Essa configuração exige pelo menos três locais, devido ao fato de exigir a implantação dos membros DAG em dois locais e do servidor testemunha do DAG em um terceiro local.

Se você não tiver três locais, ou mesmo se tiver três locais mas não quiser controlar as ações de recuperação no nível do datacenter, é possível configurar o DAG para recuperação manual, caso haja uma falha de nível de site. Nesse caso, você executaria um processo chamado *alternância de datacenter*. Assim como em muitos cenários de recuperação de desastres, o planejamento e a preparação antecipados para uma alternância de datacenter podem simplificar o processo de recuperação e reduzir a duração da interrupção.

Graças às numerosas mudanças de arquitetura no Exchange 2013, incluindo a consolidação das funções do servidor, executar uma alternância de datacenter no Exchange é significamente mais fácil do que era no Exchange 2010. Para obter instruções detalhadas de como executar uma alternância de datacenter, consulte [Switchovers do Datacenter](datacenter-switchovers-exchange-2013-help.md).

## Failovers

Um failover é um processo de ativação automático que pode ocorrer no banco de dados, no servidor ou no nível do datacenter. Os failovers ocorrem em resposta a uma falha que afeta um banco de dados individual (por exemplo, uma perda de armazenamento isolada), um servidor completo (por exemplo, uma falha na placa mãe ou perda de energia) ou um site completo (por exemplo, a perda de todos os membros DAG em um site).

Os ﻿DAGs e as cópias do banco de dados da caixa de correio fornecem redundância completa (e recuperação rápida) tanto dos dados como dos serviços que fornecem acesso aos dados. A tabela a seguir relaciona as ações de recuperação esperadas para várias falhas. Algumas falhas exigem que o administrador inicie a recuperação, e outras são tratadas automaticamente pelo sistema.


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
<thead>
<tr class="header">
<th>Descrição</th>
<th>Ativação automática</th>
<th>Ação de reparo automático</th>
<th>Estado durante o reparo: Ativo</th>
<th>Estado durante o reparo: Passivo</th>
<th>Ações de reparo</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Falha simples no banco de dados do Mecanismo de Armazenamento Extensível (ESE): As unidades que armazenam o banco de dados estão retornando erros em algumas leituras (por exemplo, um erro -1018).</p></td>
<td><p>Possível interrupção breve.</p>
<p>Possível failover automático.</p></td>
<td><p>Correção automática de página incorreta.</p></td>
<td><p>Alternância manual, failover automático ou reparo online.</p></td>
<td><p>Falhou</p></td>
<td><p>Recompilação de RAID, reparo do banco de dados e da cópia do banco de dados, restauração e execução da recuperação em vez de correção da página ou correção de página da cópia.</p></td>
<td><p>Pode haver outros códigos de falhas simples do banco de dados.</p>
<p>Não inclui falhas de bloco do sistema de arquivos NTFS.</p>
<p>Se o failover ou a alternância forem executados, o servidor de host será atualizado.</p></td>
</tr>
<tr class="even">
<td><p>Falha &quot;<em>semissuave&quot;</em> no banco de dados do ESE: As unidades que armazenam o banco de dados estão retornando erros em algumas gravações.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Recompilação automática do disco/volume após possível substituição da unidade.</p></td>
<td><p>Desmontado, se não puder ser recuperado.</p></td>
<td><p>Com falha</p></td>
<td><p>A recompilação de RAID pode resolver o problema.</p>
<p>Cópia e reparo, restauração e execução da recuperação ou recompilação do disco/volume após possível substituição.</p></td>
<td><p>Um erro semissuave de gravação do ESE significa que algumas gravações foram bem-sucedidas.</p>
<p>Não inclui falha de bloco NTFS.</p></td>
</tr>
<tr class="odd">
<td><p>Falha &quot;semissuave&quot; de log do ESE: As unidades que armazenam os dados de log estão retornando erros não recuperados em algumas leituras ou gravações.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Recompilação automática do disco/volume após possível substituição da unidade.</p></td>
<td><p>Desmontado, se não puder ser recuperado.</p></td>
<td><p>Com falha</p></td>
<td><p>A recompilação de RAID pode resolver o problema.</p>
<p>Cópia e reparo, restauração e execução da recuperação ou recompilação do disco/volume após possível substituição.</p></td>
<td><p>Um erro semissuave de leitura/gravação do ESE significa que algumas leituras/gravações foram bem-sucedidas.</p>
<p>Se o banco de dados falhar, a recuperação automática ocorrerá antes de o processo de recuperação de dados de log começar.</p></td>
</tr>
<tr class="even">
<td><p>Erro de software ou esgotamento de recursos do ESE: Um erro em que o ESE finaliza a instância (por exemplo, Evento ID 1022, profundidade do ponto de verificação muito alta).</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado, se não puder ser recuperado.</p></td>
<td><p>Com falha</p></td>
<td><p>Correção de problema de recurso subjacente.</p></td>
<td><p>Essa falha poderia ser o erro de superfície dos outros casos.</p></td>
</tr>
<tr class="odd">
<td><p>Falhas de bloco NTFS: As unidades que armazenam o banco de dados ou os logs apresentam erro de leitura ou gravação em uma estrutura de controle NTFS.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Volume completamente recompilado após possível substituição de unidade.</p></td>
<td><p>Desmontado, se não puder ser recuperado.</p></td>
<td><p>Com falha</p></td>
<td><p>A recompilação de RAID pode resolver o problema. Os utilitários para NTFS podem resolver os problemas com NTFS. Pode ser necessário recuperar o Exchange.</p></td>
<td><p>É mais provável que isso ocorra quando o RAID não estiver em uso. Se isso afetar o volume ativo de log, alguns arquivos de log recentes serão perdidos.</p>
<p>Não inclui erros corrigidos automaticamente pelo NTFS ou sua pilha de hardware ou software subjacente.</p></td>
</tr>
<tr class="even">
<td><p>Falha de unidade de log ou banco de dados: Uma unidade que armazena o banco de dados ou os logs falhou completamente e está inacessível.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Unidade reformatada ou substituída, seguida de recompilação completa de volume.</p></td>
<td><p>Desmontado, se não puder ser recuperado.</p></td>
<td><p>Com falha</p></td>
<td><p>Substituição de unidade seguida de possível recompilação de RAID.</p>
<p>Substituição de unidade seguida de recompilação completa de volume.</p>
<p>Recompilação completa de volume.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="odd">
<td><p>Falha de volume de log ou banco de dados: O volume falha por causa de problemas de volume de nível inferior ou NTFS.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Unidade reformatada ou substituída.</p></td>
<td><p>Desmontado, se não puder ser recuperado.</p></td>
<td><p>Com falha</p></td>
<td><p>Substituição de unidade seguida de possível recompilação de RAID.</p>
<p>Substituição de unidade seguida de recompilação completa de volume.</p>
<p>Recompilação completa de volume.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="even">
<td><p>Banco de dados ou volume de log sem espaço: O sistema de arquivos NTFS com o banco de dados ou os arquivos de log está sem espaço.</p></td>
<td><p>Failover automático se outra cópia não estiver em estado similar.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Com falha</p></td>
<td><p>Execução de backups completos ou incrementais, exclusão manual de logs, espera de intervalo de tempo, continuação da cópia do banco de dados ou reparo da cópia do banco de dados com falha.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="odd">
<td><p>O administrador desmonta o banco de dados errado.</p></td>
<td><p>Se o failover automático não estiver bloqueado pelo administrador, haverá uma breve interrupção.</p>
<p>Se o failover automático estiver protegido, haverá uma interrupção até que o banco de dados seja montado.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Não se aplica.</p></td>
<td><p>O administrador corrige o erro.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="even">
<td><p>O administrador suspende a cópia do banco de dados errada.</p></td>
<td><p>Dependendo da configuração e da cópia afetada, a recuperação automática poderá ser evitada.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Não se aplica.</p></td>
<td><p>Suspenso</p></td>
<td><p>O administrador corrige o erro.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="odd">
<td><p>O administrador desmonta um banco de dados para armazenamento, NTFS ou manutenção do volume.</p></td>
<td><p>Se o failover automático não estiver bloqueado pelo administrador, haverá uma breve interrupção.</p>
<p>Se o failover automático estiver bloqueado, haverá interrupção até que o administrador conclua a tarefa.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Não se aplica</p></td>
<td><p>O administrador conclui a tarefa.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="even">
<td><p>O administrador suspende uma cópia do banco de dados para armazenamento, NTFS ou manutenção do volume.</p></td>
<td><p>Dependendo da configuração e da cópia afetada, a recuperação automática poderá ser evitada.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Não se aplica.</p></td>
<td><p>Suspenso</p></td>
<td><p>O administrador conclui as ações.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="odd">
<td><p>O administrador desmonta um banco de dados para manutenção de banco de dados offline.</p></td>
<td><p>Interrupção até ser reparado.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Suspenso</p></td>
<td><p>O administrador conclui as ações.</p></td>
<td><p>Há divergência entre cópias ativas e passivas do banco de dados.</p>
<p>O administrador deve suspender as cópias.</p></td>
</tr>
<tr class="even">
<td><p>Falha do controlador de armazenamento, de disco ou da rede da área de armazenamento (SAN).</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Qualquer um</p></td>
<td><p>Reparo do hardware.</p></td>
<td><p>Uma cópia do banco de dados passiva estará no estado em que se encontrava quando o sistema apresentou falha.</p></td>
</tr>
<tr class="odd">
<td><p>Manutenção do hardware do servidor.</p></td>
<td><p>Breve interrupção durante o failover automático (a menos que bloqueado por um administrador).</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Conclusão das ações.</p></td>
<td><p>Uma cópia do banco de dados passiva estará no estado em que se encontrava quando o sistema foi encerrado.</p></td>
</tr>
<tr class="even">
<td><p>Manutenção do software do servidor.</p></td>
<td><p>Breve interrupção durante o failover automático (a menos que bloqueado por um administrador).</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Conclusão das ações.</p></td>
<td><p>Uma cópia do banco de dados passiva estará no estado em que se encontrava quando o sistema foi encerrado.</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange O serviço de Repositório de Informações do foi interrompido ou pausado por um administrador.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Reinicie o serviço de Armazenamento de Informações do Microsoft Exchange.</p></td>
<td><p>Não aplicável.</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange Falha no serviço de Armazenamento de Informações do ; o sistema operacional ainda está sendo executado.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>O Gerenciador de Controle de Serviços reinicia o serviço de Armazenamento de Informações do Microsoft Exchange.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Reiniciar manual ou automaticamente o serviço de Armazenamento de Informações do Microsoft Exchange.</p></td>
<td><p>Uma cópia do banco de dados passiva estará no estado em que se encontrava quando o serviço de Armazenamento de Informações do Microsoft Exchange apresentou falha.</p></td>
</tr>
<tr class="odd">
<td><p>Falha parcial do serviço de Armazenamento de Informações do Microsoft Exchange; algumas partes do armazenamento do Exchange pararam de funcionar, mas não puderam ser identificadas como uma falha completa.</p></td>
<td><p>Possível interrupção breve durante o failover automático.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Montado e parcialmente funcional.</p></td>
<td><p>Qualquer um, mas pode estar parcialmente funcional.</p></td>
<td><p>Reinicie o servidor, o sistema operacional ou o serviço de Armazenamento de Informações do Microsoft Exchange.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="even">
<td><p>Falha do servidor: O servidor apresentou falha por causa de um dos seguintes motivos:</p>
<ul>
<li><p>Falha completa de energia</p></li>
<li><p>Falha não recuperada do chip do processador, da placa-mãe ou do painel traseiro</p></li>
<li><p>Erro de parada do sistema operacional</p></li>
<li><p>O sistema operacional parou de responder</p></li>
<li><p>Falha total na comunicação</p></li>
</ul></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Reinicializar o computador.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Restauração de energia, alteração das configurações do sistema operacional, alteração das configurações de hardware, substituição do hardware, reinicialização do sistema operacional, manutenção do sistema operacional, manutenção do hardware ou reparo de problemas na comunicação.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="odd">
<td><p>O DAG apresenta falha de quorum.</p></td>
<td><p>Interrupção até ser reparado.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Reparo do quorum com falha, atribuição de novo quorum ou restauração da rede que está causando a falha no quorum.</p></td>
<td><p>Uma cópia do banco de dados passiva estará no estado em que se encontrava quando o sistema apresentou falha.</p></td>
</tr>
<tr class="even">
<td><p>Falha na comunicação da rede MAPI: O servidor não está mais disponível na rede MAPI.</p></td>
<td><p>Breve interrupção durante o failover automático; deve estar sem perdas.</p></td>
<td><p>Nenhuma. Continua havendo tentativas de comunicação.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Correção do problema de comunicação ao corrigir problemas de hardware ou software.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="odd">
<td><p>Falha na comunicação da rede de replicação: O servidor não consegue receber pulsações e cópias de logs ou propagar através da rede de replicação com falha.</p></td>
<td><p>Pode haver breve interrupção de cópias e propagações enquanto a carga de trabalho é transferida para outra rede.</p></td>
<td><p>Nenhuma. Continua havendo tentativas de comunicação.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>qualquer um</p></td>
<td><p>Correção do problema de comunicação ao corrigir problemas de hardware ou software.</p></td>
<td><p>Resiliência afetada por falha.</p></td>
</tr>
<tr class="even">
<td><p>Falha na comunicação de redes múltiplas: O servidor não consegue receber pulsações, cópias de log ou propagar através de várias redes.</p></td>
<td><p>Breve interrupção durante o failover automático; deve estar sem perdas.</p></td>
<td><p>Nenhuma. Continua havendo tentativas de comunicação.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Correção do problema de comunicação ao corrigir problemas de hardware ou software.</p></td>
<td><p>Pelo menos uma rede ainda está funcionando.</p></td>
</tr>
<tr class="odd">
<td><p>Falha parcial de uma ou mais redes: Redes apresentam altas taxas de erro.</p></td>
<td><p>Falha não detectada; nenhuma ação.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Montado, mas há possíveis problemas de desempenho.</p></td>
<td><p>qualquer um</p></td>
<td><p>Correção do problema de comunicação ao corrigir problemas de hardware ou software.</p></td>
<td><p>Redes apresentam taxas de erro mais altas do que o normal.</p></td>
</tr>
<tr class="even">
<td><p>Travamento não detectado do sistema operacional: O sistema operacional parou de responder, mas não foi detectado pelo monitoramento ou cluster.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Qualquer um.</p></td>
<td><p>qualquer um</p></td>
<td><p>Reiniciar ou encerrar os recursos que não estão respondendo.</p></td>
<td><p>O travamento não foi detectado, portanto nenhuma ação foi executada.</p>
<p>Algumas funcionalidades podem ser operacionais.</p></td>
</tr>
<tr class="odd">
<td><p>A unidade do sistema operacional apresenta falha.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Substituição da unidade e reconstrução do servidor ou do volume usando RAID.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="even">
<td><p>A unidade do sistema operacional está sem espaço.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Liberação manual de espaço no volume.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="odd">
<td><p>A unidade que contém os binários do Exchange apresentou falha de volume ou unidade.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Substituição da unidade e reinstalação do aplicativo ou reconstrução do volume usando a RAID.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="even">
<td><p>A unidade que contém os binários do Exchange está sem espaço.</p></td>
<td><p>Breve interrupção durante o failover automático.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>qualquer um</p></td>
<td><p>Liberação manual de espaço no volume.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
<tr class="odd">
<td><p>Novo log inválido detectado: A sequência de log foi interrompida por um arquivo existente.</p></td>
<td><p>Breve interrupção durante o failover automático; assume outras cópias que não têm o mesmo problema.</p></td>
<td><p>Nenhuma.</p></td>
<td><p>Desmontado.</p></td>
<td><p>Com falha</p></td>
<td><p>Remoção dos logs destrutivos após a determinação de sua origem.</p></td>
<td><p>Os logs destrutivos não devem replicar.</p></td>
</tr>
<tr class="even">
<td><p>A replicação contínua detecta log inválido: A repetição detecta um log inadequado durante uma cópia ou repetição.</p></td>
<td><p>Não se aplica.</p></td>
<td><p>Descartar log.</p></td>
<td><p>Não se aplica.</p></td>
<td><p>Com falha</p></td>
<td><p>Descarte do log inválido; movimentação do fluxo do log de impacto.</p></td>
<td><p>Não se aplica.</p></td>
</tr>
</tbody>
</table>


## Failovers de banco de dados

Um failover de banco de dados ocorre quando uma cópia do banco de dados que estava ativa não é mais capaz de permanecer ativa. Ocorre o seguinte como parte de um failover de banco de dados:

1.  A falha do banco de dados é detectada pelo serviço de Armazenamento de Informações do Microsoft Exchange.

2.  O serviço de Armazenamento de Informações do Microsoft Exchange grava eventos de falha no log de eventos do canal vermelho.

3.  O Gerenciador Ativo do servidor que contém o banco de dados com falha detecta os eventos de falha.

4.  O Gerenciador Ativo solicita o status da cópia do banco de dados dos outros servidores que mantêm uma cópia do banco de dados.

5.  Os outros servidores retornam o status da cópia do banco de dados solicitado pelo Gerenciador Ativo solicitador.

6.  O PAM inicia a movimentação do banco de dados ativo para outro servidor no DAG usando um algoritmo de seleção de melhor cópia.

7.  O PAM atualiza o local de montagem do banco de dados no banco de dados do cluster para consultar o servidor selecionado.

8.  O PAM envia uma solicitação para o Gerenciador Ativo do servidor selecionado para se tornar o mestre do banco de dados.

9.  O Gerenciador Ativo do servidor selecionado solicita que o serviço de Replicação do Microsoft Exchange tente copiar os últimos logs do servidor anterior e defina o sinalizador montável do banco de dados.

10. O serviço de Replicação do Microsoft Exchange copia os logs do servidor que anteriormente tinham a cópia ativa do banco de dados.

11. O Gerenciador Ativo lê o número de geração de log máximo a partir do banco de dados do cluster.

12. O serviço de Armazenamento de Informações do Microsoft Exchange monta a nova cópia ativa do banco de dados.

## Failovers de servidor

Um failover de servidor ocorre quando o membro do DAG não é mais capaz de prestar serviços à rede MAPI ou quando o serviço do Cluster de um membro do DAG não é mais capaz de contatar os demais membros do DAG. Ocorre o seguinte como parte de um failover de servidor:

1.  O serviço de Cluster do PAM envia uma notificação para o PAM mediante uma de duas condições:
    
    1.  **Desativação do nó**   O servidor é alcançável, mas não é capaz de participar das operações do DAG.
    
    2.  **Desativação da rede MAPI**   O servidor não pode ser contatado pela rede MAPI e, por isso, não pode participar das operações do DAG.

2.  Se o servidor for alcançável, o PAM entra em contato com o Gerenciador Ativo do servidor afetado e solicita que todos os bancos de dados sejam desmontados imediatamente.

3.  Para cada cópia do banco de dados afetada:
    
    1.  O PAM solicita o status da cópia do banco de dados de todos os servidores do DAG.
    
    2.  O PAM recebe uma resposta de todos os membros alcançáveis e ativos do DAG.
    
    3.  O PAM tenta determinar a melhor fonte de log dentre todos os servidores que respondem ao consultar o número mais recente de geração de log de cada um dos respondentes.
    
    4.  Cada um dos servidores responde com o número de geração de log.

4.  O PAM recupera o status do catálogo de índices de pesquisa atual do banco de dados do cluster.

5.  Com base no número de geração de log e a integridade do catálogo de cada cópia do banco de dados, o PAM seleciona as melhores cópias a fim de ativá-las.

6.  O PAM atualiza o local de montagem do banco de dados no banco de dados do cluster.

7.  O PAM inicia o failover do banco de dados comunicando-se com o Gerenciador Ativo de um ou mais outros servidores.

8.  O Gerenciador Ativo dos servidores selecionados solicitam que o serviço de Replicação do Microsoft Exchange tente copiar os últimos logs do servidor anterior e defina o sinalizador montável.

9.  Quando o banco de dados é montável, o Gerenciador Ativo dos servidores monta os bancos de dados.

Para obter mais informações sobre o melhor processo de seleção de cópias do Gerenciador Ativo, consulte [Active Manager](active-manager-exchange-2013-help.md).

## Failovers de datacenter

Mudanças significativas foram feitas no Exchange 2013 que resolvem os desafios apresentados na configuração de resiliência de site do Exchange 2010. Com a simplificação de namespace, consolidação das funções do servidor, separação do servidor de Acesso para Cliente e recuperação do DAG (no Exchange 2013, o namespace não precisa ser movido com o DAG) e as mudanças do balanceamento de carga o Exchange 2013 fornece novas opções de resilência de site, como a capacidade de usar um único namespace global. Além disso, se você tiver mais do que dois locais para implantar componentes de serviço de mensagem, o Exchange 2013 também fornece a capacidade de configurar o serviço de mensagens para failover em resposta a falhas que exigem intervenção manual no Exchange 2010.

A resiliência de site foi simplificada operacionalmente no Exchange 2013. O Exchange utiliza a tolerância a falhas integrada ao namespace por meio de vários endereços IP, balanceamento de carga (e, se necessário, a capacidade de colocar os servidores em operação e tirá-los de operação). Uma das mudanças mais significativas feitas no Exchange 2013 foi a de utilizar a capacidade do cliente de armazenar em cache vários endereços IP retornados de um servidor DNS como resposta de uma solicitação de resolução de nomes. Considerando que o cliente tem a capacidade de armazenar em cache vários endereços IP (quase todos os HTTP do cliente armazenam, e já que quase todos os protocolos de acesso para cliente no Exchange 2013 são baseados em HTTP (Outlook, Outlook Anywhere, EAS, EWS, OWA, EAC, RPS, etc.) e todos os clientes HTTP suportados têm a capacidade de usar vários endereços IP), fornecendo dessa forma failover no lado do cliente. Você pode configurar o DNS para lidar com vários endereços IP para um cliente durante uma resolução de nome. O cliente solicita mail.contoso.com e recebe de volta dois endereços IP ou quatro endereços IP, por exemplo. Contudo, vários endereços IP que o cliente recebe de volta serão usados de maneira confiável pelo cliente. Isso torna o cliente bem melhor porque se um dos endereços IP falhar, o cliente tem outros para tentar se conectar. Se um cliente tentar um e ele falhar, ele aguardará cerca de 20 segundos e tentará o próximo na lista. Dessa forma, se perder a conectividade com a sua matriz CAS principal e tiver um endereço IP secundário publicado de uma matriz CAS secundária, a recuperação dos clientes acontecerá automaticamente e em aproximadamente 21 segundos.

HTTP moderno dos clientes (operando sistemas e navegadores da web que tem dez anos ou menos) simplesmente funcionam com esta redundância automaticamente. A pilha HTTP pode aceitar vários endereços IP de um FQDN, e se o primeiro IP que ele tentar apresentar uma falha grave (por exemplo, não conseguir se conectar), ela tentará o próximo IP na lista. Em uma falha de software (conexão perdida após estabelecimento da sessão, talvez devido a uma falha intermitente no serviço em que, por exemplo, um dispositivo está ignorando pacotes e precisa ser retirado de operação), pode ser que o usuário precise atualizar seu navegador.

Com a configuração correta, o failover pode ocorrer no nível de cliente, e os clientes serão automaticamente redirecionados para um segundo datacenter que tem servidores de Acesso para Cliente operacionais, e esses servidores usam um proxy na comunicação de volta para o servidor de Caixa de Correio, que permanece não afetado pela interrupção (porque você não faz uma alternância). Em vez de trabalhar para recuperar o serviço, o serviço se autorrecupera e você pode se concentrar na correção do problema principal (por exemplo, substituir o balanceador de carga com falha).

Como você pode fazer o failover do namespace entre os data centers, tudo o que você precisa para realizar um failover de data center é um mecanismo de failover da função de Caixa de Correio entre data centers. Para obter um failover automático para o DAG, você simplesmente arquiteta uma solução em que o DAG é dividido igualmente entre dois data centers e coloca o servidor testemunha em um terceiro local, de forma que possa ser arbitrado pelo membros do DAG em qualquer um dos data centers, independentemente do estado da rede entre os data centers que contêm os membros do DAG. A chave é isolar a terceira localização falhas de rede que afetam as localizações contendo membros DAG.

Se você só têm dois datacenters e gostaria de conseguir configurar o failover automático, você pode utilizar o Microsoft Azure como seu local de terceiro. Você precisará criar uma rede virtual do Azure e conectá-lo à suas dois datacenters usando uma VPN multipontos. Em seguida, você poderá colocar o servidor de testemunha em uma máquina virtual de Microsoft Azure. Para obter mais informações, consulte [Usando uma VM do Microsoft Azure como um servidor de testemunha do DAG](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md).

