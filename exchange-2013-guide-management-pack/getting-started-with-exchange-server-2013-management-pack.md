---
title: Introdução ao Pacote de Gerenciamento do Exchange Server 2013
TOCTitle: Introdução ao Pacote de Gerenciamento do Exchange Server 2013
ms:assetid: 72d1609f-ab32-44d8-aa40-b1de587442d2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn195908(v=EXCHG.150)
ms:contentKeyID: 53275645
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Introdução ao Pacote de Gerenciamento do Exchange Server 2013

 

_**Tópico modificado em:** 2013-04-08_

O Pacote de Gerenciamento do Exchange Server 2013 adiciona um contêiner na seção de **Monitoramento** do console SCOM. Ao expandir o contêiner do Exchange Server 2013, você verá que há apenas três exibições no mesmo.

![Contêineres do Pacote de Gerenciamento do Exchange 2013](images/Dn195908.253b4ec5-2103-4b0c-a22e-5ebd24d08600(EXCHG.150).png "Contêineres do Pacote de Gerenciamento do Exchange 2013")

## Alertas Ativos – Existe algo errado com o Exchange?

A exibição de **Alertas Ativos** mostram para você todos os alertas que são acionados e estão ativos na sua organização do Exchange. Você pode clicar em qualquer alerta e ver mais informações sobre o alerta no painel de detalhes. Esta exibição está essencialmente fornecendo a você um resposta Sim/Não para "existe algo errado com a implantação do meu Exchange?" Cada alerta corresponde a um ou mais problemas para uma configuração particular de integridade. Além disso, dependendo do problema em particular, pode haver mais de um alerta acionado.

## Integridade da Organização - Qual é o impacto?

Se você visualizar um alerta na exibição de Alertas Ativos, a primeira coisa que você deve fazer pe verificar a exibição da **Integridade da Organização** . Está é a principal origem das informações para a integridade como um todo da sua organização. Ela dá a você especificamente o que é impactado na sua organização como os Sites do Active Directory e os Grupos de Disponibilidade do Banco de Dados.

![Integridade da organização](images/Dn195908.603c920b-7b88-4956-87d9-09d93fa6cba3(EXCHG.150).png "Integridade da organização")

## Integridade do Servidor - Devo resolver o problema de qual servidor?

A exibição de **Integridade do Servidor** fornece detalhes sobre servidores individuais na sua organização Aqui você pode visualizar a integridade individual de todos os seus servidores. Usando esta exibição, você pode limitar quaisquer problemas a um servidor em particular.

![Integridade do Servidor](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "Integridade do Servidor")

## Monitorando Categorias

Enquanto navega pelas três exibições no painel do Exchange Server 2013, você pode ter notado que além da coluna **Estado** , você tem quatro indicadores de integridade adicionais.

![Indicadores de integridade do Exchange](images/Dn195908.dd10ed0b-abe5-41aa-8d43-b4fb10133984(EXCHG.150).png "Indicadores de integridade do Exchange")

Cada um destes indicadores de integridade fornecem a você uma visão geral de aspectos específicos da implantação do seu Exchange.

  - **Pontos Sensíveis ao Toque do Cliente**  Mostra o que os seus usuários estão experimentando. Se o indicador estiver íntegro, significa que o problema provavelmente não impacta os seus usuários. Por exemplo, assumir que um membro da DAG está tendo problemas, mas o banco de dados fez fail over com sucesso. Neste caso, você verá indicadores de não íntegro para aquela DAG em particular, mas o indicador dos pontos sensíveis ao toque do cliente mostrarão íntegro porque os usuários não estão experimentando qualquer interrupção do serviço.

  - **Componentes do Serviço** Mostra o estado de um serviço em particular associado com o componente. Por exemplo, o indicador do componente do serviço para o OWA indica se o serviço de OWA como um todo está íntegro.

  - **Recursos do Servidor** Mostra se o estado dos recursos físicos que impactam a funcionalidade de um servidor.

  - **Principais Dependências** Mostra o estado dos recursos externos dos quais o Exchange depende como conectividade de rede, DNS ou Active Directory.

As exibições do pacote de gerenciamento do Exchange Server 2013 fornecem uma visualização simples, mas poderosa que faz com que a determinação da integridade da sua organização seja mais rápida e fácil. Entretanto, as exibições também são estruturadas de forma a guiar você rapidamente até a raiz do problema no caso de um alerta. Veja [Como usar o Exchange Server 2013 Management Pack para a Solução de Problemas](using-the-exchange-server-2013-management-pack-for-troubleshooting.md) para saber mais sobre como usar o Pacote de Gerenciamento do Exchange Server 2013 para resolver problemas.

