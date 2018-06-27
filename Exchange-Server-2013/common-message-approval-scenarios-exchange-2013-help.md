---
title: 'Cenários comuns de aprovação de mensagem: Exchange 2013 Help'
TOCTitle: Cenários comuns de aprovação de mensagem
ms:assetid: 5c13a07e-c21d-4502-a9f9-fb801197e1dd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298007(v=EXCHG.150)
ms:contentKeyID: 50485684
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cenários comuns de aprovação de mensagem

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2014-09-29_

Sua organização pode exigir a determinados tipos de mensagens ser aprovado, de forma que atenda aos requisitos legais ou normativos ou para implementar um fluxo de trabalho de negócios específicos. Aqui estão alguns exemplos de cenários comuns que você pode configurar usando Exchange:

  - O exemplo 1: Evite o excesso de email a um grupo de distribuição grandes

  - Exemplo 2: Encaminhar mensagens para o gerente de um remetente para aprovação

  - Exemplo 3: Configurar uma cadeia de aprovação de mensagem

  - O exemplo 4: Encaminhar mensagens que correspondam a um dos vários critérios

  - O exemplo 5: Encaminhar uma mensagem que contenha informações confidenciais

## O exemplo 1: Evite o excesso de email a um grupo de distribuição grandes

Para controlar mensagens a um grupo de distribuição grandes, você pode exigir que um moderador aprovar as mensagens enviadas a esse grupo. Se não houver nenhum critério para os quais mensagens exigem aprovação, a forma mais simples para configurar essa condição é configurar o grupo para exigir aprovação de mensagens.

Neste exemplo, devem ser aprovadas todas as mensagens ao grupo de todos os funcionários, exceto se os remetentes são membros do grupo de distribuição chamado Legal de equipe.

![Configurações de aprovação de mensagens para um grupo de distribuição](images/Dd298007.77721509-93f9-4a90-8d77-986db2b0acf4(EXCHG.150).png "Configurações de aprovação de mensagens para um grupo de distribuição")

Para exigir que seja aprovado mensagens a um grupo de distribuição específica, no Centro de administração do Exchange (EAC), vá para **destinatários** \> **grupos**, edite o grupo de distribuição e selecione **aprovação de mensagens**.

## Exemplo 2: Encaminhar mensagens para o gerente de um remetente para aprovação

Aqui estão alguns tipos comuns de mensagens para o qual você talvez queira exigem aprovação do gerente:

  - Mensagens enviadas de um usuário para determinados grupos de distribuição ou destinatários

  - Mensagens enviadas a usuários externos ou parceiros

  - Mensagem enviada entre dois grupos

  - Mensagens enviadas com conteúdo específico, como o nome de um cliente específico

  - Mensagens enviadas por um estagiário

Para exigir que uma mensagem seja enviada para aprovação, primeiro, criar uma regra usando o modelo de **Enviar mensagens para um moderador** e selecione as mensagens devem ir para o gerente do remetente, conforme mostrado na capturas de tela seguintes.

![Use um modelo para criar a nova regra](images/Dd298007.051a5653-1a09-4db4-908f-48b56cc8d13f(EXCHG.150).png "Use um modelo para criar a nova regra")

Em seguida, defina as mensagens que precisam de aprovação.

Aqui está um exemplo onde todas as mensagens enviadas por um estagiário, Garth Fort, para destinatários fora da organização requer aprovação do gerente.

![Regra que encaminha mensagens para o gerente do usuário](images/Dd298007.7f94c22e-b5ba-45a3-9ccd-31996b6c863a(EXCHG.150).png "Regra que encaminha mensagens para o gerente do usuário")

Para começar, vá para EAC \> **fluxo de emails** \> **regras** e criar uma nova regra usando o modelo de **Enviar mensagens para um moderador**.


> [!IMPORTANT]
> Algumas condições e ações, incluindo o encaminhamento para o gerente do remetente, estão ocultos por padrão na página <STRONG>nova regra</STRONG>. Para ver todas as condições e ações, selecione <STRONG>mais opções</STRONG>.



## Exemplo 3: Configurar uma cadeia de aprovação de mensagem

Você pode exigir vários níveis de aprovação para mensagens. Por exemplo, você pode exigir que as mensagens para um cliente específico ser aprovada primeiro por um gerente de relacionamento do cliente e depois por um responsável pela conformidade ou você pode exigir que os relatórios de despesas sejam aprovados por dois níveis de gerentes.

Para criar esse tipo de aprovação de vários níveis, crie uma regra de transporte para cada nível de aprovação. Cada regra detecta os mesmos padrões nas mensagens, da seguinte maneira:

  - A primeira regra encaminha a mensagem para o primeiro aprovador. Quando o primeiro aprovador aceita a mensagem, a mensagem se depara automaticamente ao aprovador a segunda regra.

  - Se todos os aprovadores na cadeia selecionar **Approve** quando recebem a solicitação de aprovação, quando a última aprovação na cadeia estiver concluída, a mensagem original é enviada aos destinatários pretendidos.

  - Se qualquer pessoa da cadeia de aprovação seleciona **Rejeitar** quando recebem a solicitação de aprovação, o remetente recebe uma mensagem de rejeição.

  - Se algum da aprovação de solicitações não são aprovadas dentro do tempo de expiração (2 dias para Exchange Online, 5 dias para Exchange Server 2013 ), o remetente recebe uma mensagem de expiração.

O exemplo a seguir pressupõe que você tiver um cliente chamado da Blue Yonder Airlines e desejar que o Gerenciador de relação de clientes e o responsável pela conformidade para aprovar todas as mensagens que vá para este cliente. Você criar duas regras, uma para cada aprovador. A primeira regra vai para o aprovador de primeiro nível. A segunda regra vai para o aprovador de segundo nível.

![Duas regras usadas para dois níveis de aprovação](images/Dd298007.29686c05-eaa0-42b9-86ad-d577f656392c(EXCHG.150).png "Duas regras usadas para dois níveis de aprovação")

A primeira regra identifica todas as mensagens com o nome da empresa da Blue Yonder Airlines no assunto ou na mensagem e envia essas mensagens para o gerente de relacionamento do cliente interno para Blue Yonder Airlines, Garret Vargas.

![Regra para aprovador de primeiro nível](images/Dd298007.e22d1c04-85c5-4227-88e6-b118d5593350(EXCHG.150).png "Regra para aprovador de primeiro nível")

A segunda regra envia essas mensagens para o responsável pela conformidade, Tony Krijnen.

![Regra de aprovação de segundo nível, com os mesmos critérios](images/Dd298007.5d888786-8e48-4459-ab86-8a4b9a016d58(EXCHG.150).png "Regra de aprovação de segundo nível, com os mesmos critérios")

## O exemplo 4: Encaminhar mensagens que correspondam a um dos vários critérios

Dentro de uma regra de transporte, configuradas na regra de todas as condições devem ser verdadeiras para a regra a ser correspondida. Se desejar que as mesmas ações aplicadas para uma das condições, você deve criar uma regra separada para cada um deles.

Para fazer isso, na página **regras** no EAC, crie uma regra para a primeira condição. Selecione a regra, selecione **Copiar** e alterar as condições em que a nova regra para corresponder a segunda condição.

Tenha cuidado ao criar várias regras com condições "Ou" para que você não terminem com uma mensagem está sendo enviada várias vezes ao aprovador. Para evitar isso, adicione uma exceção à regra de segundo para que ele ignora as mensagens que correspondem a primeira regra.

Por exemplo, uma única regra não pode verificar se uma mensagem tem "venda quote" na linha de assunto ou no título do anexo. Para evitar a mensagem está sendo enviada várias vezes ao aprovador, se a primeira regra verifica "venda quote" no assunto ou corpo da mensagem, a segunda regra verifica "venda quote" no conteúdo de anexo precisa uma exceção que contém os critérios da regra primeiro.

![Use uma exceção para a segunda regra](images/Dd298007.c39bbdcf-c619-4f84-8922-114ad1da824d(EXCHG.150).png "Use uma exceção para a segunda regra")


> [!TIP]
> Exceções são oculta por padrão na página <STRONG>nova regra</STRONG>. Para ver todas as condições e ações, selecione <STRONG>mais opções</STRONG>.



## O exemplo 5: Encaminhar uma mensagem que contenha informações confidenciais

Se você tiver o recurso de [Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)(DLP), muitos tipos de informações confidenciais são predefinidos. Com DLP, você verá que a mensagem contém uma condição de informações confidenciais. Se você não tenha DLP, você pode criar condições que identificam os padrões de informações confidenciais específicas que são exclusivos de sua organização.

Aqui está um exemplo de onde as mensagens com informações confidenciais exigem aprovação. Neste exemplo, as mensagens que contêm um número de cartão de crédito exigem aprovação.

![Regra que encaminha mensagens com informações confidenciais](images/Dd298007.7ec1ca74-5d20-42ea-a9ee-3a8b25beb7df(EXCHG.150).png "Regra que encaminha mensagens com informações confidenciais")

## Consulte também


[Gerenciar a aprovação de mensagens](manage-message-approval-exchange-2013-help.md)

