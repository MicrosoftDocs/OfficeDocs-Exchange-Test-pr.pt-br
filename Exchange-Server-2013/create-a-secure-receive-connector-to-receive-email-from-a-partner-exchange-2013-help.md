add-an-auto-attendant-extension-number-exchange-2013-help
---
title: 'Criar um conector de recebimento seguro para receber email de um parceiro'
TOCTitle: Criar um conector de recebimento seguro para receber email de um parceiro
ms:assetid: 06aa692c-7940-4a14-a722-058c47440f85
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673037(v=EXCHG.150)
ms:contentKeyID: 50484903
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um conector de recebimento seguro para receber email de um parceiro

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Esse procedimento mostra como configurar um conector de Recebimento, para receber emails seguros de um parceiro. Use esse procedimento quando você tiver que criptografar a comunicação entre você e um parceiro confiável. O conector é configurado para aceitar conexões somente de servidores que se autenticarem com o Protocolo (TLS).

Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Configurar o acesso de cliente e o fluxo de email](configure-mail-flow-and-client-access-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de recebimento" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md), se você estiver começando sua instalação. Depois da instalação, você pode seguir as instruções deste tópico para criar seu conector de recebimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para criar um Conector de Recebimento para receber Mensagens Seguras de um Parceiro

1.  Na EAC, navegue até **Fluxo de emails** \> **Conectores de recebimento**. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para criar um novo conector de Recebimento.

2.  Na página **Novo conector de recebimento**, especifique um nome para o conector de Recebimento e selecione **Transporte de Frontend** como **Função**. Como você estará recebendo emails de um parceiro, nesse caso, recomendamos que você inicialmente roteie os emails do seu servidor de frontend, para simplificar e consolidar seu fluxo de emails.

3.  Escolha **Parceiro** para o tipo. O conector de Recebimento irá receber emails de um terceiro confiável.

4.  Para **Associações do adaptador de rede**, observe que **Todo os IPV4 disponíveis** estão listados em **endereços IP** e a **Porta** é 25. (O SMTP usa a porta 25.) Isso indica que o conector escuta conexões de todos os endereços IP atribuídos a adaptadores de rede no servidor local. Clique em **Avançar**.

5.  Se a página de configurações de rede remota listar 0.0.0.0-255.255.255.255, o que significa que o conector de Recebimento recebe conexões de todos os endereços IP, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover"), para removê-lo. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), adicione o endereço IP do servidor do seu parceiro e clique em **Salvar**.
    

    > [!NOTE]
    > Você também pode especificar um intervalo de endereços IP com a notação CIDR, como 64.4.6.100/24.



6.  Clique em **Concluir**, para criar o conector.

Assim que você tiver criado o conector de Recebimento, ele aparecerá na lista de conectores de Recebimento. Se você quiser ver um exemplo de como criar um conector de Recebimento com um cmdlet, consulte [New-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125139\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito um conector de Recebimento para receber mensagens de um parceiro, teste se o parceiro pode enviar emails para um de seus usuários e se o usuário recebe o email com êxito. Se você puder receber emails criptografados (você pode verificar se o TLS é usado, verificando o cabeçalho da mensagem), saberá que a configuração funcionou com êxito.

## Para obter mais informações

[Conectores de recebimento](receive-connectors-exchange-2013-help.md)

