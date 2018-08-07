---
title: 'Criar conector de recebimento para receber emails de um sistema sem o Exchange'
TOCTitle: Criar um conector de recebimento para receber emails de um sistema não executa o Exchange
ms:assetid: 85f0864a-6502-49db-8804-16755a7292b4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657467(v=EXCHG.150)
ms:contentKeyID: 50486026
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um conector de recebimento para receber emails de um sistema não executa o Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Você pode ter uma situação em que você deseja receber mensagens de um sistema não executa o Exchange. Por exemplo, se você tiver um aparelho de rede que realiza política verifica e, em seguida, encaminha mensagens para seu servidor Exchange. Nesse caso, vamos pressupor que o aparelho usa SMTP. Caso contrário, você deve usar um conector estrangeiro ou um conector de agente de entrega.

Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Configurar o acesso de cliente e o fluxo de email](configure-mail-flow-and-client-access-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de recebimento" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md), se você estiver começando sua instalação. Depois da instalação, você pode seguir as instruções deste tópico para criar seu conector de recebimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para criar um conector para receber mensagens de um aparelho de mensagens de recebimento

1.  Na EAC, navegue até **Fluxo de emails** \> **Conectores de recebimento**. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para criar um conector de Recebimento.

2.  Na página **novo conector de recebimento**, especifique um nome para o conector de recebimento e selecione **Transporte de Hub** para a **função**. Nesse caso, você deseja que seu servidor de caixa de correio executando o serviço de transporte para receber mensagens do aparelho.

3.  Escolha **personalizado** para o tipo, desde que o conector de recebimento receberá o email de um aparelho de não-Microsoft Exchange Server 2013 em execução.

4.  Para as **ligações do adaptador de rede**, observe que **todos os IPV4 disponível** está listado na lista de **endereços IP**. Clique em **Avançar**.

5.  Para **configurações de rede remota**, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover") para remover o **0.0.0.0-255.255.255.255** da lista de **endereços IP**, desde que você deseja especificar que o conector aceita email de um dispositivo específico. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar um novo endereço IP e na janela de **endereço IP de adicionar**, adicione o endereço IP do seu aparelho. Clique em **Salvar**.

6.  Clique no botão **Concluir**, para criar o seu conector.

Assim que você tiver criado o conector de Recebimento, ele aparecerá na lista de conectores de Recebimento. Se você quiser ver um exemplo de como criar um conector de Recebimento com um cmdlet, consulte [New-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125139\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito um conector de recebimento para receber mensagens de um aparelho de mensagens, teste que você pode receber o email do aparelho. Se você pode receber emails, você sabe se a configuração funcionou com êxito.

## Para obter mais informações

[Criar um conector de recebimento para receber email da Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

