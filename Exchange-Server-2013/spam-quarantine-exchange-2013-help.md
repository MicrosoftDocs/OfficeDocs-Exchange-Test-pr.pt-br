---
title: 'Quarentena de spam: Exchange 2013 Help'
TOCTitle: Quarentena de spam
ms:assetid: 4535496f-de6a-43df-8e53-c9a97f65cccc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997692(v=EXCHG.150)
ms:contentKeyID: 50485454
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quarentena de spam

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-12_

Muitas organizações estão sujeitas a requisitos legais ou regulamentares para preservar ou entregar todas as mensagens de email legítimas. No Microsoft Exchange Server 2013, a quarentena de spam é um recurso do agente de Filtro de Conteúdo que reduz o risco de perda de mensagens legítimas. A quarentena de spam fornece um local de armazenamento temporário para mensagens identificadas como spam e que não devem ser entregues a uma caixa de correio de usuário dentro da organização.

Mensagens identificadas como spam pelo agente de Filtro de Conteúdo são agrupadas em uma notificação de falha na entrega e são entregues a uma caixa de correio de quarentena de spam dentro da organização. Você pode gerenciar as mensagens entregues à caixa de correio de quarentena de spam e tomar as medidas apropriadas. Por exemplo, você pode excluir mensagens ou sinalizá-las como falsos positivos na filtragem antispam, para que sejam roteadas para seus destinatários pretendidos. Também é possível configurar a caixa de correio de quarentena de spam para excluir mensagens automaticamente depois de um determinado período.

**Sumário**

Spam confidence level

Spam quarantine

## Nível de confiança de spam

Quando um usuário externo envia mensagens de email para um servidor Exchange que executa os recursos antispam, suas características são cumulativamente avaliadas e funcionam da seguinte maneira:

  - Essas mensagens suspeitas de spam serão filtradas.

  - Uma classificação é atribuída às mensagens com base na probabilidade de que sejam spam. Essa classificação é armazenada com a mensagem como uma propriedade chamada classificação de nível de confiança de spam (SCL).

A quarentena de spam usa a classificação de SCL para determinar se o email tem uma alta probabilidade de ser spam. A classificação de SCL é um valor numérico de 0 a 9, onde 0 é o menor índice de probabilidade de que a mensagem seja um spam e 9 é o maior.

Você pode configurar emails com uma determinada classificação de SCL para que sejam excluídos, rejeitados ou colocados em quarentena. A classificação que aciona qualquer uma dessas ações é denominada *limite de quarentena de SCL*. Na filtragem de conteúdo, você pode configurar o agente de Filtro de Conteúdo para basear suas ações no limite de quarentena de SCL. Por exemplo, você pode selecionar uma das seguintes condições:

  - Limite de exclusão de SCL está definido como 8.

  - Limite de rejeição de SCL está definido como 7.

  - Limite de quarentena de SCL está definido como 6.

  - O limite da pasta Lixo Eletrônico de SCL está definido como 5.

Com base nos limites de SCL acima, todos os emails com um SCL 6 serão entregues na caixa de quarentena de spam.

Para mais informações, consulte [Gerenciar filtragem de conteúdo](manage-content-filtering-exchange-2013-help.md).

Voltar ao início

## Quarentena de spam

Quando mensagens são recebidas pelo servidor Exchange que executa todos os agentes antispam padrão, o filtro de conteúdo é aplicado conforme segue:

  - Se a classificação de SCL for maior ou igual ao limite de quarentena de SCL, mas menor do que o limite de exclusão de SCL ou o limite de rejeição de SCL, a mensagem será direcionada para a caixa de correio de quarentena de spam.

  - Se a classificação de SCL for menor que o limite de quarentena de spam, a mensagem será entregue na Caixa de Entrada do destinatário.

O administrador de mensagens usa o Microsoft Outlook para monitorar a caixa de correio de quarentena de spam para falsos positivos. Se um falso positivo for encontrado, o administrador pode enviar a mensagem para a caixa de correio do destinatário.

O administrador de mensagens pode rever os carimbos antispam, se uma das seguintes condições for verdadeira:

  - Um número excessivo de falsos positivos é filtrado para a caixa de correio de quarentena de spam.

  - Um número muito baixo de spams é rejeitado ou excluído.

Para obter mais informações, consulte [Carimbos anti-spam](anti-spam-stamps-exchange-2013-help.md).

Você pode ajustar as configurações de SCL para filtrar com maior precisão os spams enviados para a organização. Para mais informações, consulte [Limite do Nível de Confiança de Spam](spam-confidence-level-threshold-exchange-2013-help.md).

Para usar a quarentena de spam, siga estas etapas:

1.  Verifique se a filtragem de conteúdo está habilitada.

2.  Crie uma caixa de correio dedicada de quarentena de spam.

3.  Especifique a caixa de correio de quarentena de spam.

4.  Configure o limite de quarentena de SCL.

5.  Gerencie a caixa de correio de quarentena de spam.

6.  Ajuste o limite de quarentena de SCL, conforme necessário.

Para instruções detalhadas, consulte [Configurar uma caixa de correio de quarentena de spam](configure-a-spam-quarantine-mailbox-exchange-2013-help.md).

Voltar ao início

