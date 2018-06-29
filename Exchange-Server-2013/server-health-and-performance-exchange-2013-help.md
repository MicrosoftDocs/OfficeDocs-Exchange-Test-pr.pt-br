---
title: 'Desempenho e a integridade do servidor: Exchange 2013 Help'
TOCTitle: Desempenho e a integridade do servidor
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 50486257
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desempenho e a integridade do servidor

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Noções básicas sobre integridade de servidor e o desempenho é fundamental para a criação e manutenção de uma infraestrutura de mensagens de alto desempenho. Microsoft Exchange Server 2013 introduz melhorias no desempenho e a integridade do servidor.

Procurando uma lista de todos os tópicos de integridade e desempenho do servidor? Consulte a documentação de integridade e desempenho do servidor.

## Disponibilidade gerenciada

Exchange 2013 introduz o conceito de *disponibilidade gerenciada*. Gerenciados execuções de disponibilidade em cada servidor Exchange 2013. Ele é composto pelos dois processos, o serviço de Gerenciador de integridade do Exchange (MSExchangeHMHost.exe) e o processo de trabalho do Gerenciador de integridade do Exchange (MSExchangeHMWorker.exe) e os seguintes componentes assíncronos:

  - **Investigue o mecanismo**   O *mecanismo de sonda* leva medições no servidor.

  - **Mecanismo de sonda de monitoramento**   O *mecanismo de sonda de monitoramento* armazena a lógica de negócios sobre o que constitui um estado íntegro. Ele funciona como um mecanismo de reconhecimento padrão, procurando padrões e medidas diferem de um estado íntegro, e, em seguida, avaliando se um componente ou recurso não está íntegro.

  - **Mecanismo do Respondente**   Quando o *mecanismo do Respondente* é alertado sobre um componente não íntegro, sua primeira ação é para tentar recuperar esse componente. Ações de recuperação de várias fases habilita a disponibilidade de gerenciados. A primeira tentativa pode ser reiniciar o pool de aplicativos, a segunda tentativa pode ser reiniciar o serviço correspondente e a tentativa de terceira pode estar reiniciar o servidor. E, a tentativa final pode ser colocar o servidor offline, para que ele aceite o tráfego não é mais. Se todas essas ações falharem, um alerta é enviado à assistência.

Para obter mais informações sobre disponibilidade gerenciada, consulte [Disponibilidade Gerenciada](managed-availability-exchange-2013-help.md).

## Gerenciamento de carga de trabalho

gerenciamento de carga de trabalho Exchange 2013 inclui os seguintes componentes:

  - *Gerenciamento de carga de trabalho do usuário* é o novo nome para o usuário a limitação de recursos do Exchange Server 2010. Você pode personalizar essas configurações com base nas necessidades do seu ambiente.

  - *Gerenciamento de carga de trabalho do sistema* s new for Exchange 2013 e é usado para acelerar automaticamente as cargas de trabalho específicas do Exchange ao monitorar a integridade dos recursos de servidor de chave. Essas configurações devem ser personalizadas apenas sob a orientação do suporte e atendimento ao cliente Microsoft.

Para obter mais informações, consulte [Gerenciamento de carga de trabalho do Exchange](exchange-workload-management-exchange-2013-help.md).

## Documentação de integridade e desempenho do servidor

A tabela a seguir contém links para tópicos que ajudarão você a aprender sobre e gerenciar a integridade do servidor e o desempenho em Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tópico</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="exchange-workload-management-exchange-2013-help.md">Gerenciamento de carga de trabalho do Exchange</a></p></td>
<td><p>Saiba como gerenciar cargas de trabalho do Exchange por meio do controle como os recursos são consumidos por usuários individuais.</p></td>
</tr>
<tr class="even">
<td><p><a href="managed-availability-exchange-2013-help.md">Disponibilidade Gerenciada</a></p></td>
<td><p>Saiba mais sobre as ações de monitoramento e recuperação de recursos internas que estão disponíveis no Exchange 2013.</p></td>
</tr>
</tbody>
</table>

