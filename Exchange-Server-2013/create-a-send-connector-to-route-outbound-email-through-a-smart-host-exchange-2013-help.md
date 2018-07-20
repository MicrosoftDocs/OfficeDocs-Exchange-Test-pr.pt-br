---
title: 'Criar um conector de envio para rotear emails de saída por meio de um host inteligente: Exchange 2013 Help'
TOCTitle: Criar um conector de envio para rotear emails de saída por meio de um host inteligente
ms:assetid: 4a9ef08e-bd62-4c6b-8790-d24fb0f8f24b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673059(v=EXCHG.150)
ms:contentKeyID: 50485534
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um conector de envio para rotear emails de saída por meio de um host inteligente

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-07_

Em algumas situações, você pode querer rotear os emails através de um host inteligente de terceiros, tais como em uma instância em que você tem um dispositivo de rede que você quer que execute verificações de política em mensagens de saída.


> [!TIP]
> O host inteligente de terceiros deve usar SMTP para transporte. Se ele não usar, você deverá usar um conector Externo ou um conector de Agente de Entrega.



Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Configurar o acesso de cliente e o fluxo de email](configure-mail-flow-and-client-access-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de envio" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Consulte [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md), se você estiver começando sua instalação. Depois da instalação, você pode seguir as instruções deste tópico para criar seu conector de saída.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o EAC para criar um conector de Envio para rotear emails de saída através de um host inteligente

1.  No EAC, navegue até **Fluxo de emails** \> **Conectores de envio** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No assistente **novo conector de envio**, especifique um nome para o conector de envio e, em seguida, selecione **personalizado** para o **tipo**. Normalmente, você escolher essa seleção quando você deseja rotear mensagens para computadores que executam o Microsoft Exchange Server 2013 não. Clique em **Avançar**.

3.  Selecione **Rotear emails por meio de hosts inteligentes** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Adicionar host inteligente**, especifique o endereço IP, como 192.168.100.1 ou o nome de domínio totalmente qualificado (FQDN), como contoso.com. Clique em **Salvar**.
    
    Para **Autenticação de host inteligente**, escolha o tipo de autenticação requerida pelo host inteligente. Se você escolher a **Autenticação básica**, deverá fornecer um nome de usuário e senha.
    

    > [!TIP]
    > Se você escolher a autenticação Básica, recomendamos que você use uma conexão criptografada, porque o nome de usuário e a senha são enviados em texto simples.



4.  Em **Espaço de endereçamento**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Adicionar domínio**, certifique-se de que SMTP esteja listado como o **Tipo**. Para **Nome de Domínio Totalmente Qualificado (FQDN)**, insira \* para especificar que este conector de Envio se aplica às mensagens enviadas para qualquer domínio. Clique em **Salvar**.

5.  Para o **servidor de origem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Selecionar um servidor**, escolha um servidor e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Clique em **OK**.

6.  Clique em **Concluir**.

Assim que você tiver criado o conector de Envio, ele aparecerá na lista de conectores de Envio.

## Como saber se funcionou?

Para verificar se você criou com êxito um conector de Envio, para rotear os emails de saída através de um host inteligente, envie uma mensagem de um usuário na sua organização (você pode usar o Outlook Web App) para o domínio que você especificou em **Espaço de endereçamento**. Se o destinatário recebe a mensagem, você configurou com êxito o conector de Envio.

## Para obter mais informações

[Criar um conector de envio de email enviado para a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Conectores de envio](send-connectors-exchange-2013-help.md)

