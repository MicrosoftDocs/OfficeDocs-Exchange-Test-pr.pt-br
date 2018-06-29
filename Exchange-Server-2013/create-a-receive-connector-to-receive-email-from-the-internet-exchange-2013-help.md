---
title: 'Criar um conector de recebimento para receber email da Internet: Exchange 2013 Help'
TOCTitle: Criar um conector de recebimento para receber email da Internet
ms:assetid: 534bbd32-a0db-4d50-9579-4933b156d7b3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657447(v=EXCHG.150)
ms:contentKeyID: 50485596
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um conector de recebimento para receber email da Internet

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-15_

Esse procedimento mostra como configurar um conector de recebimento para receber email da Internet.


> [!TIP]
> Na maioria dos casos, você não precisa definir explicitamente um conector de recebimento para receber email da Internet, porque um conector de recebimento para aceitar email da Internet é criado implicitamente na instalação do Exchange. Consulte <A href="receive-connectors-exchange-2013-help.md">Conectores de recebimento</A> para obter mais informações.



Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Configurar o acesso de cliente e o fluxo de email](configure-mail-flow-and-client-access-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de recebimento" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md), se você estiver começando sua instalação. Depois da instalação, você pode seguir as instruções deste tópico para criar seu conector de recebimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para criar um conector de recebimento para receber mensagens da Internet

1.  Na EAC, navegue até **Fluxo de emails** \> **Conectores de recebimento**. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para criar um conector de Recebimento.

2.  Na página **Novo conector de recebimento**, especifique um nome para o conector de recebimento e selecione **Transporte de Front-end** como **Função**. Como você está recebendo email da Internet neste caso, recomendamos que a princípio você encaminhe o email para seus servidores de Front-end para simplificar e consolidar o fluxo de email.

3.  Escolha **Internet** como tipo. O conector de recebimento receberá emails de remetentes da Internet.

4.  Para **Ligações de adaptador de rede**, observe que **Todos os IPV4 disponíveis** está na lista **Endereços IP** e que a **Porta** é 25. (o protocolo SMTP usa a porta 25.) Isso indica que o conector escuta conexões de todos os endereços IP atribuídos a adaptadores de rede no servidor local.
    

    > [!TIP]
    > Se você tiver vários adaptadores de rede, nessa página você pode adicionar um endereço IP atribuído a um adaptador de rede específico no servidor local, mas isso não é necessário.



5.  Clique no botão **Concluir**, para criar o seu conector.

Assim que você tiver criado o conector de Recebimento, ele aparecerá na lista de conectores de Recebimento. Se você quiser ver um exemplo de como criar um conector de Recebimento com um cmdlet, consulte [New-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125139\(v=exchg.150\)).

## Como saber se funcionou?

Para confirmar se você conseguiu criar um conector de recebimento para receber mensagens da Internet, faça um teste enviando email de uma fonte externa e confirmando se um de seus usuários recebe a mensagem. Se você receber emails, saberá que a configuração funcionou com êxito.

## Para obter mais informações

[Criar um conector de recebimento seguro para receber email de um parceiro](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

[Criar um conector de recebimento para receber emails de um sistema não executa o Exchange](create-a-receive-connector-to-receive-email-from-a-system-not-running-exchange-exchange-2013-help.md)

