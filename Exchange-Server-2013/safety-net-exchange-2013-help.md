---
title: 'Rede de Segurança: Exchange 2013 Help'
TOCTitle: Rede de Segurança
ms:assetid: d0abb807-3b12-4c7d-bc7e-769b87c84ccb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657495(v=EXCHG.150)
ms:contentKeyID: 50486698
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rede de Segurança

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

No Microsoft Exchange Server 2013, o mecanismo primário de alta disponibilidade de caixa de correio é o grupo de disponibilidade do banco de dados (DAG). Para obter mais informações sobre DAGs, consulte [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md). O *Transporte dumpster* foi introduzida primeiro no Exchange 2007 e foi aprimorado ainda mais no Exchange 2010 para fornecer cópias redundantes de mensagens após estiver entregue com êxito a caixas de correio em DAGs. Em Exchange 2010, o transporte dumpster ajudado proteger contra perda de dados, mantendo uma fila de mensagens entregues com êxito que não tivesse replicado para as cópias de banco de dados passiva no DAG. Quando uma falha de banco de dados ou o servidor de caixa de correio necessários a promoção de uma cópia desatualizada da caixa de correio do banco de dados, as mensagens no transporte dumpster foram reenviadas automaticamente para a nova cópia ativa do banco de dados de caixa de correio.

O transporte dumpster foi aprimorada no Exchange 2013 e agora é chamado de *rede de segurança*.

Aqui está como Safety Net é semelhante ao transporte dumpster em Exchange 2010:

  - Rede de segurança é uma fila que está associado ao serviço de transporte em um servidor de caixa de correio. Essa fila armazena cópias das mensagens que foram processadas com êxito pelo servidor.

  - Você pode especificar por quanto tempo Safety Net armazena cópias das mensagens processadas com êxito antes que elas expirem e serão excluídas automaticamente. O padrão é 2 dias.

Aqui está como Safety Net é diferente no Exchange 2013:

  - Rede de segurança não exige DAGs. Para servidores de caixa de correio que não pertencem a um DAGs, Safety Net armazena cópias das mensagens entregues em outros servidores de caixa de correio no site do Active Directory local.

  - Safety Net próprio agora é redundante e não é mais um único ponto de falha. Isso introduz o conceito do *principal Safety Net* e a *sombra Safety Net*. Se o Safety Net principal estiver indisponível por mais de 12 horas, reenvie solicitações se tornam as solicitações de reenvio de sombra e mensagens são entregues novamente da sombra Safety Net.

  - Safety Net assume alguma responsabilidade de redundância de sombra em ambientes de DAG. Redundância de sombra não precisa manter outra cópia da mensagem entregue em uma fila de sombra enquanto aguarda a mensagem entregue replicar para as cópias passivas do banco de dados de caixa de correio nos outros servidores de caixa de correio no DAG. A cópia da mensagem entregue já é armazenada na rede de segurança, portanto pode ser reenviada a mensagem da Safety Net, se necessário.

  - Em Exchange 2013, transporte de alta disponibilidade é mais do que apenas um melhor esforço para redundância de mensagem. Exchange 2013 tenta garantir a redundância de mensagem. Dessa forma, você não pode especificar um limite de tamanho máximo para Safety Net. Você só poderá especificar por quanto tempo o Safety Net armazena mensagens antes automaticamente excluídos.

**Sumário**

Como funciona a Safety Net

Reenvio de mensagem da Safety Net

Reenvio de mensagem da sombra Safety Net

## Como funciona a Safety Net

Redundância de sombra mantém uma cópia redundante da mensagem enquanto a mensagem estiver em trânsito. Safety Net mantém uma cópia redundante de uma mensagem depois que a mensagem é processada com êxito. Portanto, Safety Net começa onde a redundância de sombra termina. Os mesmos conceitos sobre a redundância de sombra, incluindo o limite de alta disponibilidade de transporte, mensagens principais, servidores primários, mensagens na sombra e servidores de sombra também se aplicam ao Safety Net. Para obter mais informações, consulte [Redundância de sombra](shadow-redundancy-exchange-2013-help.md).

O principal Safety Net existe no servidor de caixa de correio que mantidos a mensagem principal antes da mensagem foi processada com êxito pelo serviço de transporte. Isso pode significar que a mensagem foi entregue para o serviço de transporte de caixa de correio no servidor de caixa de correio de destino. Ou então, a mensagem pode ter sido retransmitida através do servidor de caixa de correio em um site do Active Directory que é designado como um site de hub no caminho para o destino DAG ou de um site do Active Directory. Depois que o servidor primário processa a mensagem principal, a mensagem é movida da fila de ativo em Safety Net primário no mesmo servidor.

A sombra Safety Net existe no servidor de caixa de correio que conduzidas a mensagem de sombra. Depois que o servidor de sombra determina que o servidor primário tem processadas com êxito a mensagem principal, o servidor de sombra move a sombra mensagem da fila de sombra em sombra Safety Net no mesmo servidor. Embora possa parecer óbvia, a existência de sombra Safety Net requer redundância de sombra deverá ser habilitado e redundância de sombra está habilitada por padrão em Exchange 2013.

Os parâmetros usados pelo Safety Net são descritos na tabela a seguir.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>SafetyNetHoldTime</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p>2 dias</p></td>
<td><p>O período de tempo processados com êxito mensagens principais são armazenados no principal Safety Net e confirmados mensagens na sombra são armazenadas na rede de segurança de sombra.</p>
<p>Também é possível especificar esse valor no Centro de administração do Exchange (EAC) no <strong>fluxo de emails</strong> &gt; <strong>conectores de recebimento</strong> &gt; <strong>mais opções</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="Ícone Mais opções" alt="Ícone Mais opções" /> &gt; <strong>configurações de transporte da organização</strong> &gt; <strong>Safety Net</strong> &gt; <strong>Safety Net tempo de espera</strong>.</p>
<p>Mensagens na sombra não confirmados eventualmente expiração de sombra Safety Net após a soma de <em>SafetyNetHoldTime</em> e <em>MessageExpirationTimeout</em> em <strong>Set-TransportService</strong>.</p>
<p>Para evitar dados perda durante Safety Net reenvia, o valor de <em>SafetyNetHoldTime</em> deve ser maior ou igual ao valor de <em>ReplayLagTime</em> em <strong>Set-MailboxDatabaseCopy</strong> para a cópia com atraso do banco de dados de caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplayLagTime</em> em <strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>Não configurado</p></td>
<td><p>A quantidade de tempo que o serviço de replicação do Microsoft Exchange deve aguardar antes de repetir arquivos de log que foram copiados para a cópia passiva do banco de dados. A definição deste parâmetro como um valor maior do que 0 cria uma cópia com atraso do banco de dados de caixa de correio. O valor máximo é de 14 dias.</p>
<p>Para evitar dados perda durante Safety Net reenvia, o valor de <em>ReplayLagTime</em> deve ser menor ou igual ao valor de <em>SafetyNetHoldTime</em> em <strong>Set-TransportConfig</strong> para a cópia com atraso do banco de dados de caixa de correio.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> em <strong>Set-TransportService</strong></p></td>
<td><p>2 dias</p></td>
<td><p>Quanto tempo uma mensagem pode permanecer em uma fila antes que ela expire.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowRedundancyEnabled</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> permite que a redundância de sombra em todos os servidores de transporte na organização.</p></li>
<li><p><code>$false</code> desabilita a redundância de sombra em todos os servidores de transporte na organização.</p></li>
</ul>
<p>Uma rede de segurança redundantes requer redundância de sombra deverá ser habilitado.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Reenvio de mensagem da Safety Net

Reenvios mensagens da Safety Net são iniciados pelo componente Gerenciador ativo do serviço de replicação do Microsoft Exchange que gerencia a caixa de correio e DAGs cópias de banco de dados. Nenhuma ação manual é necessárias para reenviar mensagens da Safety Net. Para obter mais informações sobre o Active Manager, consulte [Active Manager](active-manager-exchange-2013-help.md).

Há dois cenários básicos de reenvio de mensagem Safety Net:

  - Após o failover automático ou manual de um banco de dados de caixa de correio em um DAG.

  - Após você ativa uma cópia com atraso de um banco de dados de caixa de correio.

Uma *cópia do banco de dados de caixa de correio de atraso* ou *atraso de cópia* é uma cópia passiva de um banco de dados de caixa de correio onde atualizações ao banco de dados intencionalmente serão atrasadas para proteger contra corrupção lógica do banco de dados de caixa de correio. Para obter mais informações, consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

A única diferença significativa entre os dois cenários é quanto em tempo para ir para reenviar mensagens da Safety Net. Geralmente, para failover em um DAG, a nova cópia ativa do banco de dados de caixa de correio é geralmente alguns minutos para várias horas atrás ativa antiga copiar. Uma cópia com atraso de um banco de dados de caixa de correio é normalmente vários dias atrás a cópia ativa antigo.

O requisito principal para reenvio bem-sucedida da Safety Net para uma cópia com atraso é o período de tempo, as mensagens são armazenadas em Safety Net deve ser maior ou igual ao tempo de retardo de cópia com atraso do banco de dados de caixa de correio. Em outras palavras, o valor da *SafetyNetHoldTime* em **Set-TransportConfig** deve ser maior ou igual ao valor do *ReplayLagTime* em **Set-MailboxDatabaseCopy** para a cópia com atraso.

Voltar ao início

## Reenvio de mensagem da sombra Safety Net

Como reenvio de mensagem do principal Safety Net, reenvios de mensagem da sombra Safety Net são totalmente automatizados e nenhuma intervenção manual.

Quando as solicitações do Gerenciador ativo de mensagem reenvio da Safety Net durante um período de tempo específico, a solicitação vai para o serviço de transporte nos servidores de caixa de correio onde Safety Net primário está mantendo as cópias da mensagem para o período de tempo necessária. Em grandes organizações do Exchange, é provável que as mensagens necessárias existem na rede de segurança em vários servidores de caixa de correio, especialmente se o período de tempo necessária é grande.

Sem otimização, reenviar mensagens da Safety Net for resultar em número potencialmente grande de entregas duplicados. Entregas duplicadas dentro da organização do Exchange não são um problema, porque a detecção de mensagem duplicada impede que os usuários de caixa de correio vendo cópias duplicadas de uma mensagem. Mas entrega da mensagem duplicados para destinatários fora da organização do Exchange resultará em cópias de mensagens. Felizmente, o reenvio de mensagens da Safety Net foi otimizado em Exchange 2013 para reduzir a entrega da mensagem duplicados.

Se o principal Safety Net inicialmente não responde ou não responde durante o reenvio de mensagem, o Active Manager continua a tentativa de contatar o 12 horas antes abandonada. Após 12 horas, uma transmissão é enviada para o serviço de transporte em todos que os servidores de caixa de correio em alta disponibilidade de transporte acoplada solicitante reenvio de mensagem da Safety Net para o intervalo de tempo necessário para o banco de dados de caixa de correio necessários. Quando uma sombra Safety Net responde, ele reenvia as mensagens para o banco de dados de caixa de correio necessários durante o intervalo de tempo necessária somente.

Há algumas considerações importantes para as mensagens de sombra armazenadas na sombra Safety Net:

  - Sombra Safety Net não sabe em que o servidor primário transmitidas a mensagem principal.

  - As mensagens na sombra na sombra Safety Net contenham apenas os destinatários de envelope de mensagem original, não os destinatários reais em que a mensagem principal foi entregue. Por exemplo, o destinatário de envelope da mensagem pode ser um grupo de distribuição que exige expansão.

  - As mensagens na sombra Safety net não têm nenhuma das atualizações de mensagem que ocorreu depois que o servidor primário processado a mensagem. Por exemplo, conversão de conteúdo ou de codificação de mensagem.

Mensagem de sombra reenviada da sombra Safety Net exigem processamento pelo serviço de transporte no servidor de caixa de correio e categorização completa. Reenvio de grandes números de mensagens na sombra da sombra Safety Net poderá ser caro em termos de recursos do servidor de caixa de correio. Felizmente, reenvio de mensagens na sombra da sombra Safety Net também é otimizadas mensagens de modo que somente a sombra Safety Net para o intervalo de tempo solicitado e o banco de dados de caixa de correio solicitada são reenviadas.

A interação do Safety Net principal e sombra Safety Net durante o reenvio de mensagem é descrita no cenário a seguir.

1.  Gerenciador ativo solicita um reenvio de mensagens da Safety Net para um banco de dados de caixa de correio para o tempo intervalo 5:00 às 9:00. No entanto, o servidor de caixa de correio que contém o principal Safety Net falhou devido a uma falha de hardware. Active Manager tenta repetidamente entre em contato com o principal Safety Net 12 horas.

2.  Após 12 horas, o Active Manager envia uma mensagem de difusão para o serviço de transporte em todos os servidores de caixa de correio do limite de alta disponibilidade de transporte procurando por outras redes de segurança que contêm mensagens para o banco de dados de caixa de correio de destino para o tempo intervalo 5:00 às 9:00. O responde de sombra Safety Net é reenvia mensagens para o banco de dados de caixa de correio para o tempo intervalo 5:00 às 9:00.

Uma interação interessante ocorrerá se o principal Safety Net estava offline durante uma parte do intervalo de reenvio solicitada, conforme descrito no cenário a seguir.

1.  O banco de dados de fila no servidor de caixa de correio que retém o Safety Net primário está corrompido, e um novo banco de dados de fila é criado às 7:00. Todas as mensagens principais armazenadas no principal Safety Net entre 1:00 como 7:00 são perdidas, mas o servidor é capaz de armazenar cópias de mensagens entregues com êxito na rede de segurança começando 7:00.

2.  Gerenciador ativo solicita um reenvio de mensagens da Safety Net para um banco de dados de caixa de correio para o tempo intervalo 1:00 às 9:00.

3.  O principal Safety Net reenvia mensagens para o tempo intervalo 7:00 às 9:00.

4.  O principal Safety Net envia uma mensagem de transmissão para o serviço de transporte em todos os servidores de caixa de correio do limite de alta disponibilidade de transporte procurando por outras redes de segurança que contêm mensagens para o banco de dados de caixa de correio de destino para o tempo de intervalo 1:00 às 7:00 para o qual o principal Safety Net não tem nenhuma mensagem. A sombra Safety Net gerará uma segunda solicitação de reenvio em nome do principal Safety Net para reenviar as mensagens de sombra para o banco de dados de caixa de correio de destino para o tempo de intervalo 1:00 às 7:00.

Há algumas outras questões a considerar quando as mensagens são reenviadas da Safety Net.

1.  Todas as notificações de status de entrega (DSNs) e relatórios de falha na entrega (NDRs) são suprimidos para reenvia Safety Net. Por exemplo, se a mensagem principal resultou em uma NDR, o NDR da mensagem enviado novamente não entregue.

2.  Removido de um grupo de distribuição de usuários não podem receber uma mensagem submetidos novamente quando a sombra Safety Net reenvia a mensagem. Por exemplo, uma mensagem é enviada a um grupo que contém o usuário B e usuário e ambos os destinatários receberão a mensagem. O usuário B é subsequentemente removido do grupo. Mais tarde, uma solicitação de reenvio de principal Safety Net é feita para o banco de dados de caixa de correio que contém a caixa de correio do usuário B. No entanto, o Safety Net principal não está disponível por mais de 12 horas, para que o servidor de sombra Safety Net responde e reenvia a mensagem afetada. Durante o reenvio quando o grupo de distribuição é expandido, o usuário B não é um membro do grupo e não receberá uma cópia da mensagem enviado novamente.

3.  Novos usuários adicionados a um grupo de distribuição podem receber uma mensagem de submetidos novamente antiga, quando a sombra Safety Net reenvia a mensagem. Por exemplo, uma mensagem é enviada a um grupo que contém o usuário B e usuário e ambos os destinatários receberão a mensagem. Usuário C subsequentemente é adicionado ao grupo. Mais tarde, uma solicitação de reenvio de principal Safety Net é feita para o banco de dados de caixa de correio que contém a caixa de correio do usuário C. No entanto, o servidor primário Safety Net não está disponível por mais de 12 horas, para que o servidor de sombra Safety Net responde e reenvia as mensagens afetadas. Durante o reenvio quando o grupo de distribuição é expandido, C do usuário é membro do grupo e receberá uma cópia da mensagem enviado novamente.

Voltar ao início

