---
title: 'Criar conector de envio de email enviado para a Internet: Exchange 2013 Help'
TOCTitle: Criar um conector de envio de email enviado para a Internet
ms:assetid: 6deaefa8-1152-40d9-b1ba-9c19bdf8a928
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657457(v=EXCHG.150)
ms:contentKeyID: 50485787
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um conector de envio de email enviado para a Internet

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-01-23_

Por padrão, Microsoft Exchange Server 2013 não permite que você envie emails fora do seu domínio. Para enviar email fora do seu domínio, você precisa criar um conector de envio. O gráfico a seguir ilustra o fluxo de email quando você cria um conector de envio para enviar emails para a Internet.

![connector\_send\_onprem\_internet](images/JJ657457.e8963e4f-7dce-461f-bbcf-660278cefa35(EXCHG.150).gif "connector_send_onprem_internet")

Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Configurar o acesso de cliente e o fluxo de email](configure-mail-flow-and-client-access-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de envio" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md), se você estiver começando sua instalação. Depois da instalação, você pode seguir as instruções deste tópico para criar seu conector de saída.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para criar um conector de envio de email enviado para a Internet

1.  No EAC, navegue até **Fluxo de emails** \> **Conectores de envio** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No assistente **novo conector de envio**, especifique um nome para o conector de envio e selecione **Internet** para o **tipo**. Clique em **Avançar**.

3.  Verifique se **registro MX associado ao domínio do destinatário** é selecionado, que especifica que o conector usa o sistema de nomes de domínio (DNS) para rotear emails. Clique em **Avançar**.

4.  Em **espaço de endereço**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Adicionar domínio**, certifique-se de que SMTP está listado como o **tipo**. **Totalmente o nome de domínio qualificado (FQDN)**, digite \*, que indica que este conector de envio se aplica às mensagens endereçadas a qualquer domínio. Clique em **Salvar**.

5.  Certifique-se de **que todo o escopo conector de envio** não está selecionado e clique em **Avançar**.

6.  Para o **servidor de origem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Selecionar um servidor**, selecione um servidor de caixa de correio que será usado para enviar emails para a Internet por meio do servidor de acesso para cliente e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Depois que você selecionou o servidor, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Clique em **OK**.

7.  Clique em **Concluir**.

Depois de criar o conector de envio, ele aparece na lista de conector de envio.

## Usar o Shell para rotear emails através do servidor de acesso para cliente

Em Exchange 2013, você pode usar o parâmetro *FrontendProxyEnabled* do cmdlet **Set-SendConnector** para rotear mensagens de saída através do servidor de acesso para cliente. Este parâmetro não for definido como `$true` por padrão, mas em muitos casos, ele pode consolidar e simplificar o fluxo de mensagens, especialmente se você estiver trabalhando com um ambiente com um grande número de servidores de mensagens.

Este exemplo define o parâmetro *FrontendProxyEnabled* para `$true` em um conector de envio.

    Set-SendConnector "Contoso.com Send Connector" -FrontendProxyEnabled $true

## Como saber se funcionou?

Para verificar se você criou com êxito um conector de envio de mensagens de email enviado para a Internet, enviar email a partir de um dos seus usuários para um destinatário externo e verifique se que a mensagem é recebida com êxito.

## Para mais informações

[Conectores de envio](send-connectors-exchange-2013-help.md)

[Criar um conector de envio para rotear emails de saída por meio de um host inteligente](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

