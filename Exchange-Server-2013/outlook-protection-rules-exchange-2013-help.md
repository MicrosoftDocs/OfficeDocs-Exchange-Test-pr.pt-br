---
title: 'Regras de proteção do Outlook: Exchange 2013 Help'
TOCTitle: Regras de proteção do Outlook
ms:assetid: bd7d0ad7-1f8e-46da-a74b-58c58f3eff93
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638178(v=EXCHG.150)
ms:contentKeyID: 50486520
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Regras de proteção do Outlook

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Todos os dias, as informações que trabalhadores trocam de informações confidenciais por email, incluindo relatórios financeiros e dados, cliente e informações do funcionário e informações sobre o produto confidencial e especificações. No Microsoft Exchange Server 2013, Microsoft Outlook e Microsoft OfficeOutlook Web App, os usuários podem aplicar proteção de gerenciamento de direitos de informação (IRM) às mensagens aplicando um modelo de diretiva de direitos do Active Directory Rights Management Services (AD RMS). Isso requer uma implantação do AD RMS na organização. Para obter mais informações sobre o AD RMS, consulte [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823).

No entanto, quando deixado a critério de usuários, as mensagens podem ser enviadas em texto não criptografado sem proteção de IRM. Em organizações que usam email como um serviço hospedado, há algum risco de vazamento de informações como uma mensagem deixa o cliente e é roteada e armazenada fora dos limites de uma organização. Embora empresas de hospedagem de email pode ter verificações para ajudar a reduzir o risco de vazamento de informações, depois que uma mensagem deixa o limite de uma organização e procedimentos bem definidos, a organização perde o controle das informações. Regras de proteção do Outlook podem ajudar a proteger contra esse tipo de vazamento de informações.

Para tarefas de gerenciamento relacionadas ao gerenciamento de IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## Proteção de IRM automática no Outlook

Em Exchange 2013, as regras de proteção de Outlook proteger sua organização contra o risco de vazamento de informações aplicando automaticamente a proteção de IRM às mensagens no Exchange 2013. As mensagens são protegidas por IRM antes de sair do cliente Outlook. Essa proteção também é aplicada a todos os anexos usando os formatos de arquivo com suporte.

Quando você cria regras de proteção de Outlook em um servidor de Exchange 2013, as regras são automaticamente distribuídas para Outlook 2010 usando Exchange serviços da Web. Para Outlook 2010 aplicar a regra, o modelo de diretiva de direitos do AD RMS especificado deve ser disponível nos computadores dos usuários.


> [!IMPORTANT]
> Se um modelo de diretiva de direitos é removido do servidor AD RMS, você deve modificar quaisquer regras de proteção de Outlook que usam o modelo removido. Se uma regra de proteção de Outlook continua a usar um modelo de diretiva de direitos é foram removido, e a descriptografia de transporte está habilitada na organização, o agente de descriptografia falhará descriptografar a mensagem protegida com um modelo que não está mais disponível. Se a descriptografia de transporte é configurada como obrigatória, o serviço de transporte rejeitar a mensagem e envia um relatório de entrega (NDR) ao remetente. Para obter mais detalhes sobre a descriptografia de transporte, consulte <A href="transport-decryption-exchange-2013-help.md">Descriptografia de transporte</A>. Para obter mais detalhes sobre os modelos de diretiva de direitos do AD RMS, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=179455">Considerações de modelo de política do AD RMS</A>.<BR>No Windows Server 2008 e posterior, direitos modelos de política podem ser arquivados, em vez de excluído. Os modelos arquivados ainda podem ser usados para licenciar conteúdo, mas quando você cria ou modificar uma regra de proteção de Outlook, os modelos arquivados não estão incluídos na lista de modelos.



regras de proteção de Outlook são semelhantes às regras de proteção de transporte. Ambos são aplicados com base nas condições da mensagem, e ambas protegem mensagens aplicando um modelo de proteção de direitos do AD RMS. No entanto, as regras de proteção de transporte são aplicadas no serviço de transporte no servidor de caixa de correio pelo agente de regras de transporte. regras de proteção de Outlook são aplicadas na Outlook 2010, antes da mensagem sair do computador do usuário. Mensagens protegidas por uma regra de proteção de Outlook insira o pipeline de transporte com a proteção de IRM já aplicada. Além disso, as mensagens protegidas com uma regra de proteção de Outlook também são salvas em um formato criptografado na pasta Itens enviados da caixa de correio do remetente.


> [!NOTE]
> Se a descriptografia de transporte estiver habilitada em sua organização Exchange, as mensagens que são protegidas por IRM por uma regra de proteção de Outlook usando o servidor do AD RMS em sua organização podem ser descriptografadas pelo agente de descriptografia no serviço de transporte. Conteúdo da mensagem pode ser inspecionado, o agente de regras de transporte e outros agentes de transporte instalados no serviço de transporte. Para obter mais detalhes sobre a descriptografia de transporte, consulte <A href="transport-decryption-exchange-2013-help.md">Descriptografia de transporte</A>.



Quando você usa as regras de proteção de transporte, os usuários não têm nenhuma indicação de que se uma mensagem vai ser protegidas automaticamente o serviço de transporte. Quando uma regra de proteção de Outlook é aplicada a uma mensagem em Outlook 2010, os usuários saber se uma mensagem serão protegidas por IRM. Se for necessário, os usuários também podem selecionar um modelo de diretiva de direitos diferentes.

## Criando regras de proteção do Outlook

Para criar regras de proteção de Outlook, você deve usar o cmdlet [New-OutlookProtectionRule](https://technet.microsoft.com/pt-br/library/dd298182\(v=exchg.150\)) no Exchange Management Shell. Para obter instruções detalhadas, consulte [Criar uma regra de proteção do Outlook](create-an-outlook-protection-rule-exchange-2013-help.md).

Ao criar uma regra, você pode especificar se o usuário pode fazer substituição, removendo a proteção de IRM ou aplicando um modelo de diretiva de direitos do AD RMS diferente daquele com o especificadas na regra. Se um usuário substitui a proteção de IRM aplicada por uma regra de proteção de Outlook, Outlook 2010 insere o cabeçalho `X-MS-Outlook-Client-Rule-Overridden` na mensagem, que permite determinar se a regra foi substituída pelo usuário.

## Predicados nas regras de proteção do Outlook

regras de proteção Outlook permitem que você use três predicados para aplicar automaticamente a proteção de IRM no Outlook 2010:

  - **FromDepartment**   O predicado *FromDepartment* procura o atributo do remetente departamento na Active Directory e automaticamente protege o IRM a mensagem se o departamento do remetente corresponde o departamento especificado na regra. Por exemplo, você pode criar uma regra de proteção Outlook para proteger automaticamente todas as mensagens enviadas pelo departamento de Research.

  - **SentTo**   Sua organização, talvez seja necessário proteger as mensagens enviadas para certos destinatários confidenciais, como os grupos de distribuição de empresa de todos ou Finance. Usando o predicado *SentTo* , você pode criar uma regra de proteção de Outlook para automaticamente IRM Proteja as mensagens enviadas para destinatários especificados.

  - **SentToScope**   O predicado *SentToScope* permite que você crie uma regra de proteção de Outlook para automaticamente IRM Proteja as mensagens enviadas dentro ou fora da organização. Por exemplo, você pode usar o predicado *SentToScope* com o predicado *FromDepartment* para proteger o IRM as mensagens enviadas por um determinado departamento para usuários internos.

