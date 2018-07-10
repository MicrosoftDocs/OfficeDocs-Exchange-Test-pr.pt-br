---
title: 'Criar um conector de envio para enviar email para um parceiro, com Transport Layer Security (TLS) aplicada: Exchange 2013 Help'
TOCTitle: Criar um conector de envio para enviar email para um parceiro, com Transport Layer Security (TLS) aplicada
ms:assetid: ff2abefc-dd3e-4431-b947-df942fbf82d9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657514(v=EXCHG.150)
ms:contentKeyID: 50487100
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um conector de envio para enviar email para um parceiro, com Transport Layer Security (TLS) aplicada

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-15_

Se você quiser garantir segura, comunicação criptografada com um parceiro, você pode criar um conector de envio que esteja configurado para impor a segurança de camada de transporte (TLS) para mensagens enviadas a um domínio de parceiro. TLS oferece comunicação segura pela Internet.

Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Configurar o acesso de cliente e o fluxo de email](configure-mail-flow-and-client-access-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de envio" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md), se você estiver começando sua instalação. Depois da instalação, você pode seguir as instruções deste tópico para criar seu conector de saída.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para criar um conector de envio para enviar email para um parceiro, com o protocolo TLS aplicada

Para criar um conector de envio para este cenário, faça logon no EAC e execute as seguintes etapas:

1.  No EAC, navegue até **Fluxo de emails** \> **Conectores de envio** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No assistente **novo conector de envio**, especifique um nome para o conector de envio e selecione **parceiro** para o **tipo**. Quando você seleciona o **parceiro**, o conector está configurado para permitir conexões somente para servidores que autenticam com certificados TLS. Clique em **Avançar**.

3.  Verifique se **registro MX associado ao domínio do destinatário** é selecionado, que especifica que o conector usa o sistema de nomes de domínio (DNS) para rotear emails. Clique em **Avançar**.

4.  Em **espaço de endereço**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Adicionar domínio**, certifique-se de que SMTP está listado como o **tipo**. Para **Totalmente o nome de domínio qualificado (FQDN)**, digite o nome do seu domínio de parceiro. Clique em **Salvar**.

5.  Para o **servidor de origem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Selecionar um servidor**, selecione um servidor de caixa de correio que será usado para enviar emails para a Internet por meio do servidor de acesso para cliente e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Depois que você selecionou o servidor, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Clique em **OK**.

6.  Clique em **Concluir**.

Depois de criar o conector de envio, ele aparece na lista de conector de envio.

## Como saber se funcionou?

Para verificar se você criou com êxito um conector de envio para enviar email para um parceiro, com o protocolo TLS aplicada, envie uma mensagem de um usuário em sua organização para um destinatário da organização parceira. Se o destinatário recebe a mensagem, o conector foi criado com êxito.

## Para obter mais informações

[Criar um conector de envio de email enviado para a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Criar um conector de envio para rotear emails de saída por meio de um host inteligente](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

