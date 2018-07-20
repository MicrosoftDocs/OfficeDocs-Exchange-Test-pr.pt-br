---
title: 'Configurar um conector de envio entre florestas: Exchange 2013 Help'
TOCTitle: Configurar um conector de envio entre florestas
ms:assetid: 7840d172-071e-4f13-9379-2fe1eee1a7cc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ945053(v=EXCHG.150)
ms:contentKeyID: 52058849
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um conector de envio entre florestas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-21_

No Active Directory, a *floresta* representa o limite externo de seu serviço de diretório. Você pode criar conectores de envio para habilitar a comunicação entre florestas. Neste exemplo, os conectores de usam a autenticação básica.

Para tarefas de gerenciamento adicionais relacionadas à configuração de conectores, consulte [Conectores](connectors-exchange-2013-help.md).

Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Implantar o Exchange 2013 em uma topologia entre florestas](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 20 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de envio" e entrada "Conectores de recebimento" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - Se você estiver começar sua instalação, consulte [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md) . Após a instalação, você pode usar as etapas neste tópico para criar conectores para configurar uma topologia entre florestas.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar uma conta de usuário em cada floresta

Você deve criar uma conta de usuário em cada floresta a ser usado para autenticação básica. Crie uma conta em cada floresta e adicione cada um para o grupo de segurança universal do Exchange Server usado para comunicação. Essa conta é usada pelo conector de envio para autenticar para o email de recebimento de servidor na outra floresta. Por exemplo, fornecer uma conta de usuário que tenha a entidade de segurança do usuário nomeie FourthCoffee@Contoso.com (UPN) como as credenciais que devem ser usadas para autenticação pelo servidor do Exchange no domínio Fourth Coffee quando o email é enviado para o Exchange server no domínio Contoso.

## Usar o EAC para criar um conector de envio para rotear o e-mail para outra floresta do Exchange 2013

Estabelece o fluxo de email entre florestas usando a autenticação básica.

1.  No EAC, navegue até **fluxo de emails** \> **conectores de envio**. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No assistente **novo conector de envio**, especifique um nome para o conector de envio e, em seguida, selecione **interno** para o **tipo**. Clique em **Avançar**.

3.  Escolha **rotear email por meio de hosts inteligentes** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Adicionar host inteligente**, especifique o endereço IP do servidor de destino da segunda floresta, como 64.4.6.100. Clique em **Salvar** e clique em seguida **Avançar**.
    
    Para **autenticação de host inteligente**, escolha **a autenticação básica** e forneça um nome de usuário e senha. Aqui, você pode escolher **a autenticação básica de oferta somente após iniciar TLS** para comunicação segura sobre TLS.
    

    > [!TIP]
    > Se você usar a autenticação básica sobre TLS, o servidor de destino deve ser configurado para usar um certificado x. 509.



4.  Em **espaço de endereço**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Adicionar domínio**, certifique-se de que SMTP está listado como o **tipo**. **Totalmente o nome de domínio qualificado (FQDN)**, digite o domínio de recebimento, como fourthcoffee.com. Clique em **Salvar** e clique em seguida **Avançar**.

5.  Para o **servidor de origem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na janela **Selecionar um servidor**, escolha o servidor usar e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Clique em **ok**.

6.  Clique em **Concluir**. O conector é exibida na lista de conectores de envio.

Depois de criar seu conector de envio, crie um conector de envio da segunda floresta que envia emails para a floresta original. Nesse caso, o FQDN domínio totalmente qualificado nome () especificado será o nome de domínio da primeira floresta. Por exemplo, contoso.com.

## Use o Shell para definir permissões no conector de envio

Este exemplo usa o script Enable-CrossForestConnector.ps1 no Shell para definir permissões no conector de envio para uso em uma topologia entre florestas.

    .\Enable-CrossForestConnector.ps1 -Connector "Cross-Forest" -user "ANONYMOUS LOGON"

## Como saber se funcionou?

Para verificar se você criou com êxito os conectores de envio para rotear email para uma segunda floresta, enviar uma mensagem de um usuário em sua organização (você pode usar o Outlook Web App) para o domínio que você especificou para o **espaço de endereçamento**. Se o destinatário recebe a mensagem, você configurou com êxito o conector de envio.

## Para obter mais informações

[Criar um conector de envio de email enviado para a Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Conectores de envio](send-connectors-exchange-2013-help.md)

