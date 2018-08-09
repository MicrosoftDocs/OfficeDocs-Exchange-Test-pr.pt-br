---
title: 'Criar conector de recebimento para mensagens de servidor Exchange interno'
TOCTitle: Criar um conector de recebimento para receber mensagens de um servidor interno do Exchange
ms:assetid: 546cead9-7a2d-4332-a5f6-35343d56c619
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657448(v=EXCHG.150)
ms:contentKeyID: 50485601
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um conector de recebimento para receber mensagens de um servidor interno do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Crie um conector de recebimento do tipo **Interno** quando quiser receber email de um servidor do Exchange. Use este tipo de conector para controlar o roteamento de email em sua organização: por exemplo, quando quiser rotear email do serviço Transporte em um servidor de Caixa de Correio para um servidor de Transporte de Borda específico, ou de um servidor de Caixa de Correio para outro.

Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Configurar o acesso de cliente e o fluxo de email](configure-mail-flow-and-client-access-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de recebimento" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md), se você estiver começando sua instalação. Depois da instalação, você pode seguir as instruções deste tópico para criar seu conector de recebimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Criar um conector de recebimento para receber mensagens de um servidor Exchange interno

1.  Na EAC, navegue até **Fluxo de emails** \> **Conectores de recebimento**. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para criar um novo conector de Recebimento.

2.  Na página **Novo conector de recebimento**, especifique um nome para o conector de recebimento e selecione **Transporte de Hub** como **Função**. Neste caso, presumimos que você queira rotear email dentro de sua rede, e não para dentro e para fora da organização.

3.  Escolha **Interno** como tipo. O conector é configurado com autenticação de servidor do Exchange.

4.  Se a página de configurações de rede remota listar 0.0.0.0-255.255.255.255, o que significa que o conector de Recebimento recebe conexões de todos os endereços IP, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover"), para removê-lo. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), adicione o endereço IP do servidor do qual deseja receber email, como 192.168.1.1 e clique em **Salvar**.

5.  Clique em **Concluir**, para criar o conector.

Assim que você tiver criado o conector de Recebimento, ele aparecerá na lista de conectores de Recebimento. Se você quiser ver um exemplo de como criar um conector de Recebimento com um cmdlet, consulte [New-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125139\(v=exchg.150\)).

## Como saber se funcionou?

Para confirmar se você criou com êxito um conector de recebimento para receber mensagens de um servidor interno, teste se as mensagens do servidor de envio conseguem viajar até o servidor do destinatário. Uma maneira de fazer isso é usar o Shell de Gerenciamento do Exchange para definir o conector de recebimento do *ProtocolLoggingLevel* que você criou para `Verbose`, usando o cmdlet [Set-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125140\(v=exchg.150\)), e verificar os logs para garantir a entrega da mensagem.

## Para obter mais informações

[Criar um conector de recebimento para receber email da Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

[Criar um conector de recebimento seguro para receber email de um parceiro](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

