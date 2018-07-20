---
title: Como o pacote do Exchange Server 2013 relata a integridade do sistema
TOCTitle: Entendendo Como o Pacote de Gerenciamento do Exchange Server 2013 Relata a Integridade do Sistema
ms:assetid: 6ca8847f-93fe-458d-bd43-7afad7fdd2f4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn195910(v=EXCHG.150)
ms:contentKeyID: 53275643
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Entendendo Como o Pacote de Gerenciamento do Exchange Server 2013 Relata a Integridade do Sistema

 

_**Tópico modificado em:**  2013-04-17_

Este tópico fornece informações sobre como o Pacote de Gerenciamento do Exchange Server 2013 monitora e relata a integridade do sistema do Exchange. No Pacote de Gerenciamento do Exchange 2013, as informações do estado de integridade são acumuladas de maneira simples. Sempre que uma configuração de integridade não estiver íntegra e o respondente escalonado for acionado, o evento a seguir é registrado no log de eventos do Windows:

## Disponibilidade Gerenciada

Foram feitas alterações de arquitetura no Exchange Server 2013. Uma das principais alterações é o recurso *Disponibilidade Gerenciada* no qual todos os componentes do Exchange 2013 possuem monitores internos que detectam problemas e tentam recuperar a disponibilidade do serviço O Pacote de Gerenciamento do Exchange Server 2013 se vale desse recurso. Qualquer problema que não puder ser resolvido automaticamente é escalonado para o Pacote de Gerenciamento do Exchange Server 2013 como um alerta. Cada componente do Exchange 2013 monitora a si mesmo usando três componentes básicos chamados de sondas, monitores e respondentes.

![Disponibilidade gerenciada](images/Dn195910.dd5febae-d05e-4089-a3f5-1691b2d9a3d7(EXCHG.150).png "Disponibilidade gerenciada")

  - **Sondas**   São conjuntos de coletores de dados que medem vários componentes. Existem três tipos diferentes de sondas:
    
      - Transações sintéticas que medem operações sintéticas de usuário de ponta a ponta e verificações que medem o tráfego real.
    
      - Verificações que medem o tráfego real de consumo.
    
      - Notificações que permitem que o Exchange tome ações imediatas. Um bom exemplo disso é a notificação que é acionada quando um certificado expira.

  - **Monitores**   Os dados coletados pelas sondas são passados para os monitores que analisam condições específicas dos dados e dependendo destas condições determinam se um componente específico está íntegro ou não.

  - **Respondentes**   Se um monitor determinar que um componente não está íntegro, o mesmo acionará um respondente Se o problema for recuperável, o respondnete tenta recuperar o componente usando uma lógica interna. Existem muitos respondentes disponíveis para cada componente, mas o respondente relevante para o Pacote de Gerenciamento do Exchange 2013 é o *Respondente Escalonado*. Quando o Respondente Escalonado é acionado, ele gera um evento que o Pacote de Gerenciamento do Exchange 2013 reconhece e fornece as informações apropriadas para o alerta que fornece aos administradores as informações necessárias para tratar o problema.

Cada componente no Exchange 2013 usa um conjunto específico de sondas, monitores e respondentes para monitorarem a si mesmos. Estes conjuntos de sondas e monitores são conhecidos como *conjuntos de integridade*. Por exemplo, existem várias sondas que coletam dados sobre vários aspectos do serviço ActiveSync. Estes dados são processados por um conjunto designado de monitores que acionam os respondentes apropriados para corrigir quaisquer problemas que eles detectem no serviço ActiveSync. Coletivamente, estes componentes constituem o conjunto de integridade do ActiveSync.

Os conjuntos de integridade são organizados nas quatro categorias a seguir que correspondem ao painel do pacote de gerenciamento:

  - Pontos Sensíveis ao Toque do Consumidor

  - Componentes de Serviço

  - Recursos do Servidor

  - Principais Dependências

Para uma lista completa dos conjuntos de integridade do Exchange, veja [Appendix A: Exchange health sets](appendix-a-exchange-health-sets.md).

Para saber mais sobre Disponibilidade Gerenciada, veja [Funcionamento e Desempenho do Servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Como a integridade é acumulada

Este tópico fornece informações sobre como o Pacote de Gerenciamento do Exchange Server 2013 monitora e relata a integridade do sistema do Exchange. No Pacote de Gerenciamento do Exchange 2013, as informações do estado de integridade são acumuladas de maneira simples. Sempre que um conjunto de integridade não estiver íntegro e o respondente escalonado for acionado, o evento a seguir é registrada no log de eventos do Windows:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Nome do log</p></td>
<td><p>Monitoramento/Disponibilidade-Gerenciada-Microsoft-Exchange</p></td>
</tr>
<tr class="even">
<td><p>Origem</p></td>
<td><p>DisponibilidadeGerenciada</p></td>
</tr>
<tr class="odd">
<td><p>Data</p></td>
<td><p>&lt;<em>data e hora do evento</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>ID do Evento</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>Categoria da tarefa</p></td>
<td><p>Monitoramento</p></td>
</tr>
<tr class="even">
<td><p>Nível</p></td>
<td><p>Erro</p></td>
</tr>
<tr class="odd">
<td><p>Palavras-chave</p></td>
<td><p>&lt;<em>nenhuma</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Usuário</p></td>
<td><p>SISTEMA</p></td>
</tr>
<tr class="odd">
<td><p>Computador</p></td>
<td><p>&lt;<em>FQDN do servidor Exchange</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Descrição</p></td>
<td><p>&lt;<em>dinamicamente gerada pelo respondente escalonado</em>&gt;</p></td>
</tr>
</tbody>
</table>


O agente do Pacote de Gerenciamento detecta e processa este evento. Usando este evento, a Disponibilidade Gerenciada pode gerar alertas dentro do SCOM. Quando o problema correspondente é resolvido e o conjunto de integridade retorna para o estado íntegro, o evento a seguir é registrado no log de eventos do Windows:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Nome do log</p></td>
<td><p>Monitoramento/Disponibilidade-Gerenciada-Microsoft-Exchange</p></td>
</tr>
<tr class="even">
<td><p>Origem</p></td>
<td><p>DisponibilidadeGerenciada</p></td>
</tr>
<tr class="odd">
<td><p>Data</p></td>
<td><p>&lt;<em>data e hora do evento</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>ID do Evento</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>Categoria da tarefa</p></td>
<td><p>Monitoramento</p></td>
</tr>
<tr class="even">
<td><p>Nível</p></td>
<td><p>Informações</p></td>
</tr>
<tr class="odd">
<td><p>Palavras-chave</p></td>
<td><p>&lt;<em>nenhuma</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Usuário</p></td>
<td><p>SISTEMA</p></td>
</tr>
<tr class="odd">
<td><p>Computador</p></td>
<td><p>&lt;<em>FQDN do servidor Exchange</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Descrição</p></td>
<td><p>&lt;<em>dinamicamente gerada pelo respondente escalonado</em>&gt;</p></td>
</tr>
</tbody>
</table>


Os pacotes de gerenciamento que monitoravam versões anteriores do Exchange eram completamente centralizados. Os agentes em cada servidor do Exchange coletava os dados e um mecanismo de correlação comparava e avaliava todos os dados relatados pelos agentes para determinar a integridade geral do serviço. Em ambientes em grande escala, este processo resultou em correlações complexas, causando atrasos na geração do alerta. No Exchange 2013, a correlação de alerta não é mais usada. Ao invés disso, cada servidor realiza o seu próprio monitoramento e alerta o SCOM se necessário, permitindo um arquitetura altamente escalonável.

Dependendo do impacto do evento e do conjunto de integridade que o aciona, o problema é mostrado no console do SCOM em uma categoria diferente. Se o evento causar impacto no usuário, então o indicador dos pontos sensíveis ao toque do consumidor é mostrado como não íntegro. Se fizer com que um componente inteiro como o OWA fique indisponível, então o indicador do componente do serviço é mostrado como não íntegro. Se for um problema com um servidor específico, então o indicador de integridade do servidor é mostrado como não íntegro. E se o problema for relacionado com um recurso do qual o Exchange depende, o indicador das principais dependências é mostrado como não íntegro. Para mais informações sobre estas categorias, veja [Introdução ao Pacote de Gerenciamento do Exchange Server 2013](getting-started-with-exchange-server-2013-management-pack.md).

