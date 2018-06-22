---
title: 'Fatores de desempenho e práticas recomendadas para migrações híbridas: Exchange 2013 Help'
TOCTitle: Fatores de desempenho e práticas recomendadas para migrações híbridas
ms:assetid: 120a7832-d2d3-47d7-b305-918360c2ef66
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt483789(v=EXCHG.150)
ms:contentKeyID: 70118017
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Fatores de desempenho e práticas recomendadas para migrações híbridas

 

_<strong>Aplica-se a:</strong>Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2016-12-09_

Há muitos caminhos para migrar os dados de uma organização de email local para o Office 365. Ao planejar uma migração para o Office 365, uma pergunta comum é como melhorar o desempenho da migração de dados e otimizar a velocidade da migração. Este artigo discute o desempenho da migração para implantações híbridas do Exchange. Para informações sobre o desempenho de outros métodos de migração, confira [Desempenho de migração do Office 365 e práticas recomendadas](http://go.microsoft.com/fwlink/p/?linkid=623651).

## Fatores de desempenho e práticas recomendadas para migrações híbridas

A migração de implantação híbrida é compatível com a migração suave entre servidores locais do Exchange e o Exchange Online no Office 365.

A migração híbrida é, com certeza, o método de migração mais rápido para migrar dados da caixa de correio para o Office 365. Já foi observada uma taxa de transferência de até 100 GB/h durante implantações reais de cliente. A tabela a seguir oferece uma lista de fatores que se aplicam a cenários de migração híbrida nativa do Office 365.

Se o seu ambiente local contém vários sites em localizações geograficamente espalhadas, é possível melhorar o desempenho da migração criando pontos de extremidade de migração geograficamente próximos. Isso ocorre porque, nesse cenário, a migração usa a rede da Microsoft em comparação com o uso de um ponto de extremidade de migração centralizado que usa a sua rede local.

## Fator 1: Fonte de dados (Exchange Server)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Lista de verificação</th>
<th>Descrição</th>
<th>Práticas recomendadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Desempenho do sistema</p></td>
<td><p>A extração de dados é uma tarefa que usa muitos recursos. O sistema de origem deve ter recursos suficientes, como tempo e memória da CPU, para oferecer um melhor desempenho de migração. No momento da migração, o sistema de origem geralmente está próximo da capacidade total para servir cargas de trabalho do usuário final regulares—cargas de trabalho de migração adicional algumas vezes diminuem o acesso dos usuários finais, devido à falta de recursos do sistema.</p></td>
<td><p>Monitore o desempenho do sistema durante um teste de migração piloto. Se o sistema está ocupado, recomendamos evitar uma programação de migração agressiva para o sistema específico, devido a potencial lentidão da migração e problemas de disponibilidade do serviço. Se possível, melhore o desempenho do sistema de origem, adicionando recursos de hardware e reduzindo a carga no sistema, movendo as tarefas e os usuários para outros servidores que não estejam envolvidos na migração.</p>
<p>Para obter mais informações, consulte:</p>
<ul>
<li><p><a href="http://go.microsoft.com/fwlink/?linkid=723566">Pergunte a Perf Guy: Dimensionamento de implantações do Exchange 2016</a></p></li>
<li><p><a href="https://technet.microsoft.com/pt-br/library/jj150551(v=exchg.150)">Desempenho e a integridade do servidor</a></p></li>
<li><p><a href="http://technet.microsoft.com/pt-br/library/dd351192.aspx">Noções básicas Sobre o Desempenho do Exchange 2010</a></p></li>
</ul>
<p>Ao se migrar de uma organização do Exchange local quando há vários servidores de caixa de correio e vários bancos de dados, recomendamos criar uma lista de usuário de migração que é distribuída igualmente entre vários servidores de caixa de correio e bancos de dados. Com base no desempenho individual do servidor, a lista pode ser melhor ajustada para maximizar o resultado.</p>
<p>Por exemplo, se o servidor A possui 50% mais disponibilidade de recursos do que o servidor B, é razoável ter 50% mais usuários no servidor A, no mesmo lote de migração. Práticas semelhantes podem ser aplicadas a outros sistemas de origem.</p>
<p>Realize migrações quando os servidores tiverem uma disponibilidade máxima de recursos, como depois do expediente ou em finais de semana e feriados.</p></td>
</tr>
<tr class="even">
<td><p>Tarefas de back-end</p></td>
<td><p>Outras tarefas de back-end executadas durante o momento da migração. Como é uma prática recomendada realizar a migração após o horário comercial, é comum que as migrações entrem em conflito com outras tarefas de manutenção executadas em seus servidores locais, como o backup de dados.</p></td>
<td><p>Revise outras tarefas do sistema que podem estar sendo executadas durante a migração. Recomendamos que você realize a migração de dados quando não estiver sendo executada nenhuma outra tarefa que consuma muitos recursos.</p>
<p><strong>Observação</strong>   Para clientes usando o Microsoft Exchange local, as tarefas de back-end comuns são soluções de backup e <a href="http://technet.microsoft.com/pt-br/library/aa996226(exchg.65).aspx">manutenção de repositório do Exchange</a>.</p></td>
</tr>
</tbody>
</table>


## Fator 2: Servidor de migração

A migração de implantação híbrida é uma migração de dados pull/push iniciada na nuvem, e um servidor híbrido do Exchange atua como o servidor de migração. Isso é frequentemente ignorado, e os clientes usam uma máquina virtual de baixo desempenho para atuar como o servidor híbrido. Isso resulta em um baixo desempenho na migração.

**Práticas recomendadas**

Além de aplicar as práticas recomendadas descritas anteriormente, testamos as práticas recomendadas a seguir, que resultaram em um desempenho de migração melhor em migrações reais de clientes:

  - Usar máquinas físicas potentes de classe do servidor em vez de máquinas virtuais para os servidores híbridos do Exchange.

  - Usar vários servidores híbridos por trás de um balanceador de carga de rede do cliente.

Por exemplo, em migrações reais de clientes, atingimos um resultado consistente de 30 GB/h usando a seguinte configuração:

  - **Rede **  Canalização de saída de 500 MB para a Internet; a rede interna está em 1 GB com backbone de fibra de 10 GB.

  - **Hardware**   As especificações para os dois servidores de Acesso para Cliente/HUB (físico) são:
    
      - CPU: Intel® Xeon® CPU E5520 @ 2.27 GHz 2.26 GHz (dois processadores).
    
      - RAM: 24 GB.
    
      - Discos: Oito, com 146 GB por disco. Configuração RAID 5 = espaço bruto total de 960 GB.

  - **MRSProxy**   Configurado com uma simultaneidade de 100.

## Fator 3: Mecanismo de migração

A migração de implantação híbrida usa ferramentas nativas do Office 365. Essa ferramenta está sujeita à limitação do serviço de migração do Office 365.

**Exchange 2003 versus versões posteriores do Exchange**

Há uma diferença fundamental com relação à experiência do usuário final quando a migração é a partir do Exchange 2003. Ao contrário das versões posteriores do Exchange, os usuários finais do Exchange 2003 não podem acessar as caixas de correio enquanto os dados estiverem sendo migrados. Portanto, os clientes que usam o Exchange 2003 estão geralmente mais preocupados sobre quando programar as migrações e sobre o tempo necessário para executá-las, especialmente quando o desempenho da migração é baixo devido a caixas de correio de tamanho grande ou a uma rede lenta.

A migração do Exchange 2003 é também muito sensível a interrupções. Por exemplo, em uma migração real de um cliente, durante a migração de uma caixa de correio de 10 GB, ocorreu um incidente com o serviço quando a migração da caixa estava em 50%. O servidor de acesso para cliente do Office 365, que estava processando os dados da migração, teve de ser reiniciado para solucionar o problema. Nesse caso, a migração dessa caixa de correio teve de ser reiniciada e, sendo assim, o cliente teve de migrar os 10 GB de dados novamente. Não foi possível retomar a migração de onde ela tinha parado. Entretanto, no Exchange 2010 e nas versões posteriores é possível retomar as migrações após interrupções.

**Práticas recomendadas**

Alguns clientes escolhem migrações de dois saltos para caixas de correio do Exchange 2003 grandes e importantes:

  - **Primeiro salto**   Migrar caixas de correio do Exchange 2003 para um servidor Exchange 2010 ou posterior, que geralmente é o servidor híbrido. O primeiro salto é um movimento offline, mas geralmente é uma migração muito rápida em uma rede local.

  - **Segundo salto**   Migrar caixas de correio do Exchange 2010 ou posteriores para o Office 365.

O segundo salto é um movimento online, que oferece uma melhor experiência para o usuário, além da tolerância a falhas. Essa abordagem de dois saltos exige uma licença do Exchange para a caixa de correio do usuário local temporária.

**Proxy de Serviço de Replicação de Caixa de Correio (MRSProxy)**

O proxy MRS é o recurso de migração local que funciona com o Serviço de Replicação de Caixa de Correio executado no lado do Office 365. Para mais informações, consulte [Noções Básicas Sobre Solicitações de Movimentação](http://technet.microsoft.com/pt-br/library/dd298174.aspx).

**Práticas recomendadas**

É possível configurar a quantidade máxima de conexões do MRSProxy para o servidor híbrido local do Exchange. Execute o seguinte comando do Windows PowerShell:

    Set-WebServicesVirtualDirectory -Identity "EWS (Default Web Site)" -MRSMaxConnections <number between 0 and unlimited; default is 100>


> [!TIP]
> Para a maioria das migrações do cliente, é necessário alterar o valor padrão MRSMaxConnections. Se você precisa proteger o servidor de origem da sobrecarga pela carga de migração, os clientes podem reduzir o número de conexões. Essa configuração é por servidor MRSProxy. Se um cliente possui dois servidores MRSProxy, cada um definido para 10 conexões, eles obterão 20 (2 x 10) como a quantidade total de conexões do MRSProxy. Para obter mais informações sobre a configuração do serviço MRSProxy na sua organização local do Exchange 2010, consulte <A href="http://technet.microsoft.com/pt-br/library/ee732395.aspx">Iniciar o serviço MRSProxy em um servidor de acesso remoto para cliente</A>.



## Fator 4: Rede

**Testes de verificação**

Para clientes que estejam executando o Exchange 2010 ou posterior, o teste de desempenho da rede para migrações híbridas pode ser realizado, efetuando-se vários testes de migrações de caixa de correio. Como alternativa, é possível migrar caixas de correio reais do usuário com a opção -SuspendWhenReadyToComplete para obter uma indicação do desempenho da migração. Quando o teste for concluído, remova a solicitação de movimento para evitar afetar os usuários finais.

Para mais informações sobre solicitações de movimento, confira [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

## Fator 5: Serviço do Office 365

A limitação baseada em integridade dos recursos do Office 365 afeta as migrações usando as migrações de implantação híbrida do Office 365. Consulte a seção de otimização baseada na saúde os recursos do Office 365 acima para obter mais detalhes.

