---
title: 'Realizar uma limpeza remota em um telefone móvel: Exchange 2013 Help'
TOCTitle: Realizar uma limpeza remota em um telefone móvel
ms:assetid: 67ba838e-031d-4a98-b277-170683b6f520
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998614(v=EXCHG.150)
ms:contentKeyID: 52058433
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Realizar uma limpeza remota em um telefone móvel

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2013-02-06_

Os seus usuários carregam informações corporativas confidenciais no bolso todos os dias. Se um deles perder o celular, os seus dados podem acabar nas mãos de outra pessoa. Se um dos seus usuários perder o celular, você pode usar o Centro de Adminstração do Exchange (EAC) ou o Shell de Gerenciamento do Exchange para limpar todos os dados corporativos e informações de usuário do telefone deles.


> [!TIP]
> Este tópico fornece instruções sobre como usar o Outlook Web App da Microsoft para realizar uma limpeza remota em um telefone. O usuário deve ser conectado ao Outlook Web App para executar uma limpeza remota.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de "Dispositivos móveis" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md) .

  - Este procedimento limpará todos os dados no celular, incluindo as aplicações instaladas, fotos e informações pessoais.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para limpar o telefone de um usuário

Você pode usar o EAC para limar o telefone de um usuário ou cancelar uma limpeza remota que ainda não foi finalizada.

1.  No EAC, navegue até **Destinatários** \> **Caixas de Correio**.

2.  Escolha o usuário, e em **Dispositivos Móveis**, escolha **Visualizar detalhes**.

3.  Na página **Detalhes do Dispositivo Móvel** , escolha o dispositivo móvel perdido e então selecione **Limpar Dados**.

4.  Selecione **Salvar**.

## Use o Shell para limpar o telefone de um usuário

Você pode usar o cmdlet **Clear-MobileDevice** no Shell para limpar o telefone de um usuário.

Os seguintes comandos limpam o dispositivo com o nome WM\_TonySmith e envia uma mensagem de confirmação para admin@contoso.com.

    Clear-MobileDevice -Identity WM_TonySmith -NotificationEmailAddresses "admin@contoso.com"

## Use o Outlook Web App para limpar o telefone de um usuário

Os seus usuários podem limpar os seus próprios telefones usando o Outlook Web App.

1.  Em Outlook Web App, selecione **Configurações \> Telefone \> Dispositivos móveis**.

2.  Escolha o celular.

3.  Clique ou toque no ícone **Limpar Dispositivo** .

## Como saber se funcionou?

Existem várias maneiras de verificar se a limpeza remota foi realizada.

  - Execute o cmdlet **Clear-MobileDevice** com o parâmetro *–NotificationEmailAddresses* configurado. Um mensagem será enviada para o endereço de email fornecido quando a limpeza remota estiver concluída.

  - No EAC, verifique o status do celular. O status mudará de **Limpeza Pendente** para **Limpeza Realizada Com Sucesso**.

  - Em Outlook Web App, verifique o status do celular. O status mudará de **Limpeza Pendente** para **Limpeza Realizada Com Sucesso**.

