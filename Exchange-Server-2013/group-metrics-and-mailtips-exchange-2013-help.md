---
title: 'Métricas de grupo e as dicas de email: Exchange 2013 Help'
TOCTitle: Métricas de grupo e as dicas de email
ms:assetid: 74a55072-4ba9-45bb-a18f-41afbf3de30b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ674302(v=EXCHG.150)
ms:contentKeyID: 50485934
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Métricas de grupo e as dicas de email

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-16_

Métricas de grupo é uma coleção dos seguintes dados sobre grupos de distribuição e grupos dinâmicos de distribuição em sua organização:

  - Número de membros

  - Número de membros que são externos à sua organização

Dados de métricas de grupo são usados para dar suporte a dicas de email no Microsoft Exchange Server 2013. Dicas de email são mensagens informativas exibidas aos remetentes enquanto eles compõem mensagens. Para obter mais informações sobre dicas de email, incluindo uma lista completa de dicas de email disponíveis no Exchange 2013, consulte [MailTips](mailtips-exchange-2013-help.md).

Dados de métricas de grupo são usados pelo dicas de email seguintes:

  - **Grande público**    Essa dica de email é exibida quando um remetente adicionar um grupo de distribuição cuja contagem de associação é considerada um grande público, conforme configurado em sua organização. Por padrão, qualquer mensagem endereçada aos destinatários mais de 25 é considerada um grande público.

  - **Destinatários externos**    Essa dica de email é exibida quando um remetente adicionar um grupo de distribuição que tenha membros que são externos à sua organização.

Dicas de email são avaliadas toda vez que um remetente adicionar um destinatário a uma mensagem. Para fornecer essas informações, Exchange calcula dados de métricas de grupo como um processo de plano de fundo que pode ser agendado para execução fora do horário comercial da regular da sua organização. Ao avaliar os destinatários para dicas de email, Exchange lê os dados de métricas de grupo.

## Geração de métricas de grupo

Em Exchange 2013, dados de métricas de grupo são armazenados nos atributos **msExchGroupMemberCount** e **msExchGroupExternalMemberCount** no objeto de grupo no Active Directory. Os seguintes arquivos na pasta % Caminhoinstalaçãoexchange % GroupMetrics também estão associados a métricas de grupo:

  - **Cookie\_*\<nnnnnnnn\>*.dsc**   Este arquivo de texto contém informações sobre o servidor de caixa de correio que está configurado para gerar dados de métricas de grupo e as métricas de grupo bem-sucedida a última hora de geração. Isso permite que as métricas de grupo gerar os dados para os grupos que foram alterados desde a última geração de métricas de grupo.

  - **ChangedGroups.txt** esse arquivo contém a lista de grupos que foram atualizados a última vez em que os dados de métricas de grupo foi gerados.

Geração de métricas de grupo é realizada por uma caixa de correio de arbitragem, que também é chamada de uma caixa de correio da organização. Quando o parâmetro *GMGen* em uma caixa de correio de arbitragem é definido como `$true`, a caixa de correio de arbitragem é responsável por gerar os dados de métricas de grupo.

O servidor de caixa de correio gera dados de métricas de grupo completa para todos os grupos de distribuição e grupos de distribuição dinâmica na primeira vez que executa o Assistente de caixa de correio de métricas de grupo e atualizações incrementais para todos os grupos que foram modificados desde a última geração completa. Por padrão, os dados de métricas de grupo são gerados diariamente às aleatório vez quando a carga de trabalho do Exchange server é claro. Se a carga de trabalho for constantemente alta, a geração de métricas de grupo pode ser ignorada.

Para configurar a geração de métricas de grupo, consulte [Configurar as métricas de grupo](configure-group-metrics-exchange-2013-help.md).

