---
title: 'Usar regras de fluxo de email para que mensagens poderá ignorar desorganização: Exchange 2013 Help'
TOCTitle: Usar regras de fluxo de email para que mensagens poderá ignorar desorganização
ms:assetid: 58e413f0-aa27-4307-bffd-4df03090a15e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn896639(v=EXCHG.150)
ms:contentKeyID: 64374720
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar regras de fluxo de email para que mensagens poderá ignorar desorganização

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Se desejar Certifique-se que você receber mensagens específicas, você pode criar uma regra de transporte do Exchange que garante que essas mensagens ignoram sua pasta confusão. Confira [Desorganização usar para classificar as mensagens de baixa prioridade no Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=528411) para obter mais informações sobre desorganização.

Para tarefas de gerenciamento adicionais relacionadas às regras de transporte, confira o tópico de PowerShell do [New-TransportRule](https://technet.microsoft.com/pt-br/library/bb125138\(v=exchg.150\)) and [Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) . Se estiver familiarizado com o PowerShell, confira os seguintes tópicos para obter ajuda sobre como usar o Powershell:

  - [Conectar-se ao Exchange Online usando o PowerShell Remoto](https://technet.microsoft.com/pt-br/library/jj984289\(v=exchg.150\))

  - [Conectar-se ao Exchange usando o Shell Remoto](https://technet.microsoft.com/pt-br/library/dd335083\(v=exchg.150\))

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Regras de transporte", no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Use a interface do Usuário para criar uma regra de transporte para ignorar a pasta desorganização

Este exemplo permite todas as mensagens com o título "Reunião" Ignorar desorganização.

1.  No Centro de administração do Exchange, navegue até **fluxo de emails** \> **regras**. Clique em ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e, em seguida, escolha **criar uma nova regra...**.

2.  Após concluir a criação da nova regra, clique em **Salvar** para iniciar a regra.

![Exemplo de arte: Se o assunto contiver reunião, ignore o email secundário](images/Dn896639.75957aa4-4b2a-4142-92ff-07f8ccc64d82(EXCHG.150).png "Exemplo de arte: Se o assunto contiver reunião, ignore o email secundário")

## Usar o Shell para criar uma regra de transporte para ignorar a pasta desorganização

Este exemplo permite todas as mensagens com o título "Reunião" Ignorar confusão.

    New-TransportRule -Name <name_of_the_rule> -SubjectContainsWords "Meeting" -SetHeaderName "X-MS-Exchange-Organization-BypassClutter" -SetHeaderValue "true"


> [!IMPORTANT]
> Neste exemplo, "X-MS-Exchange-organização-BypassClutter" e "true" diferencia maiusculas de minúsculas.



Para informações detalhadas de sintaxes e de parâmetros, consulte [New-TransportRule](https://technet.microsoft.com/pt-br/library/bb125138\(v=exchg.150\)).

## Como saber se funcionou?

Você pode verificar o desvio de cabeçalhos de mensagem de email para ver se as mensagens de email são inicial na caixa de entrada devido a regra de transporte desorganização. Selecione uma mensagem de email de uma caixa de correio em sua organização que tem a confusão Ignorar regra de transporte aplicada. Examinar os cabeçalhos marcados na mensagem, e você deverá ver a **X-MS-Exchange-organização-BypassClutter: true** cabeçalho. Isso significa que o desvio está funcionando. Confira o tópico de [Exibir as informações de cabeçalho de uma mensagem de email da Internet](https://go.microsoft.com/fwlink/p/?linkid=822530) para informações sobre como localizar as informações de cabeçalho.


> [!TIP]
> Itens de calendário, como reuniões aceitos, enviadas ou recusada não terão esses cabeçalhos neles. Estamos trabalhando em estendendo os recursos de desorganização a estes itens de calendário em breve.


