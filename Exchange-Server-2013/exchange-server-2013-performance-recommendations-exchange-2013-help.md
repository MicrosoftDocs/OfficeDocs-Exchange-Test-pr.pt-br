---
title: 'Recomendações de desempenho do Exchange Server 2013: Exchange 2013 Help'
TOCTitle: Recomendações de desempenho do Exchange Server 2013
ms:assetid: 6d0aea68-10d5-4a18-b632-a814ce3daa43
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn879084(v=EXCHG.150)
ms:contentKeyID: 63763724
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recomendações de desempenho do Exchange Server 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

ajuste e solução de problemas de desempenho de Exchange Server 2013 é mais eficiente quando seu ambiente foi corretamente porte e planejado. Enquanto o Exchange 2013 foi desenvolvido para simplificar a infra-estrutura de recurso subjacente, ele ainda poderá consumir uma grande quantidade de recursos do sistema, como memória, capacidade de armazenamento e capacidade da CPU.

Os artigos nesta seção foram gravados pela equipe de desempenho do Exchange. Elas contêm especialização a partir do grupo de produto do Exchange, também da melhor forma práticas aprendidas casos de suporte ao cliente. O objetivo destes artigos é para ajudá-lo a entender o impacto das alterações introduzidas no Exchange 2013 e a importância do dimensionamento apropriadamente sua infraestrutura do Exchange 2013. Também incluímos otimizações recomendadas e orientação sobre como identificar problemas de desempenho.

## Alterações de arquitetura no Exchange 2013 e outros recursos

As alterações de arquitetura no Exchange 2013 já estão documentadas no TechNet e no [Blog da equipe do Exchange](https://go.microsoft.com/fwlink/p/?linkid=35786). Primeiro mencionaremos após algumas alterações de alto níveis, você deve considerar para entender melhor desempenho dimensionamento e custo. Em seguida, abaixo, incluímos uma lista de referências recomendadas para fornecer mais contexto e plano de fundo nessas áreas importantes.


> [!NOTE]
> Consulte <A href="exchange-2013-virtualization-exchange-2013-help.md">Virtualização do Exchange 2013</A> para obter orientações de otimização de desempenho sobre a implantação do Exchange Server 2013 em um ambiente virtualizado.



No Exchange 2013, a função de servidor acesso para cliente é um servidor proxy sem estado. Agora é de responsabilidade de principal da função de servidor acesso para cliente para autenticar solicitações de entrada proxy e, em seguida, cada solicitação para o servidor de caixa de correio apropriado, aquele hospeda a cópia ativa da caixa de correio do usuário. Isso significa que não é mais necessário para configurar a afinidade entre o servidor de acesso para cliente e o balanceador de carga para protocolos específicos.

Outra alteração notável no Exchange 2013 é no repositório de informações. Armazenamento de informações agora consiste em dois tipos de processos: host e o funcionário. Cada instância de banco de dados está associada com seu próprio processo Microsoft.Exchange.Store.Worker.exe. Isso permite melhor isolamento de problemas de banco de dados problemática e pode reduzir o impacto no desempenho de um problema de banco de dados para apenas a instância de um trabalho ao banco de dados.

O serviço de replicação do Microsoft Exchange é responsável por todos os serviços de alta disponibilidade relacionados à função de servidor de caixa de correio. Este serviço de replicação hospeda o componente Gerenciador ativo, que é responsável pelo monitoramento de falhas e a tomada de ações corretivas.

Uma ótima postagem sobre mudanças de arquitetura, incluindo o impacto para um ambiente do Exchange 2013 novamente de dimensionamento de versões anteriores, pode ser encontrada na [Arquitetura de função de servidor do Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=523735).

Mais informações sobre mudanças de arquitetura do Exchange 2013 e informações de plano de fundo em outras áreas relevantes, podem ser encontradas no seguinte:

[Exchange Server 2013 arquitetura](https://go.microsoft.com/fwlink/p/?linkid=523769)

[Planejá-lo da maneira correta: cenários de dimensionamento do Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523773)

[Monitorando e ajustando o Microsoft Exchange Server 2013 desempenho](https://go.microsoft.com/fwlink/p/?linkid=523774)

[Implementar o Exchange Server 2013: (01) atualizar e implantar o Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523775)

[Implementação de servidor do Exchange 2013: (02) planejar a maneira de direita ele: Exchange Server 2013 dimensionamento](https://go.microsoft.com/fwlink/p/?linkid=523776)

[Implementar o Exchange Server 2013: (03) práticas recomendadas de virtualização Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523777)

[Implementar o Exchange Server 2013: arquitetura do Exchange (04): alta disponibilidade e resiliência do Site](https://go.microsoft.com/fwlink/p/?linkid=523779)

[Implementar o Exchange Server 2013: conectividade do Outlook (05)](https://go.microsoft.com/fwlink/p/?linkid=523781)

[A arquitetura preferencial](https://go.microsoft.com/fwlink/p/?linkid=523782)

[Função de servidor de acesso de cliente do Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=386373)

[Exchange Server 2013 Virtualization as práticas recomendadas](https://go.microsoft.com/fwlink/p/?linkid=523783)

[Balanceamento de carga](load-balancing-exchange-2013-help.md)

[Atualizações do Exchange Server: números de versão e datas de lançamento](https://technet.microsoft.com/pt-br/library/hh135098\(v=exchg.150\))

[Notas de versão do Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md)

[Atualizações para o Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md)

[Uso de Thread de ASP.NET no IIS 7.5, o IIS 7.0 e IIS 6.0](https://go.microsoft.com/fwlink/p/?linkid=169626)

