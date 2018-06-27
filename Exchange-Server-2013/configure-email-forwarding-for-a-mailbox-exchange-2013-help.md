---
title: 'Configurar o encaminhamento de emails para uma caixa de correio: Exchange Online Help'
TOCTitle: Configurar o encaminhamento de emails para uma caixa de correio
ms:assetid: c7a7afaf-577e-49d6-8cee-bb4c4a5d570b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351134(v=EXCHG.150)
ms:contentKeyID: 50556289
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar o encaminhamento de emails para uma caixa de correio

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

O encaminhamento de emails permite que você configure uma caixa de correio para encaminhar mensagens de email enviadas a essa caixa de correio para a caixa de correio de outro usuário dentro ou fora de sua organização.


> [!IMPORTANT]
> Caso esteja utilizando o Office 365 para empresas, você deve configurar o encaminhamento de emails no <A href="https://go.microsoft.com/fwlink/p/?linkid=834774">Centro de administração do Office 365: configurar o encaminhamento de emails no Office 365</A>



Se a sua organização utilizar um ambiente local ou um ambiente híbrido do Exchange, você deverá usar o Centro de administração do Exchange (EAC) no local para criar e gerenciar caixas de correio compartilhadas.

## Usar o Centro de administração do Exchange para configurar o encaminhamento de emails

Você pode usar a configuração de encaminhamento de emails do Centro de administração do Exchange (EAC) para um único destinatário interno, um único destinatário externo (usando um contato de email) ou vários destinatários (usando um grupo de distribuição).

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

1.  Na EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio de usuário, clique ou toque na caixa de correio para a qual deseja configurar o encaminhamento de email e clique ou toque em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **Recursos da Caixa de Correio**.

4.  Em **Fluxo de Email**, selecione **Exibir detalhes** para visualizar ou alterar as definições do encaminhamento de email.
    
    Nesta página, você pode definir o número máximo de destinatários para o qual o usuário pode enviar uma mensagem. Para organizações do Exchange no local, o limite de destinatários é ilimitado. Para organizações do Exchange Online, o limite é de 500 destinatários.

5.  Marque a caixa de seleção **Habilitar encaminhamento** e clique ou toque em **Procurar**.

6.  Na página **Selecionar Destinatário**, selecione um usuário para o qual você deseja encaminhar todas as mensagens de email. Marque a caixa de seleção **Entregar mensagem ao endereço de encaminhamento e à caixa de correio**, se você deseja que o destinatário e o endereço de email de encaminhamento recebam cópias dos emails enviados. Clique ou toque em **OK** e depois em **Salvar**.

E se você quiser encaminhar emails para um endereço de fora da sua organização? Ou encaminhar emails para vários destinatários? Você também pode fazer isso\!

  - **Endereços externos**Crie um contato de email e, em seguida, nas etapas acima, selecione o contato de email na página **Selecionar Destinatário**. Precisa saber como criar um contato de email? Consulte [Gerenciar contatos de email](manage-mail-contacts-exchange-2013-help.md).

  - **Vários destinatários**Crie um grupo de distribuição, adicione destinatários a ele e, em seguida, nas etapas acima, selecione o contato de email na página **Selecionar Destinatário**. Precisa saber como criar um contato de email? Consulte [Criar e gerenciar grupos de distribuição](create-and-manage-distribution-groups-exchange-2013-help.md).

## Como saber se funcionou?

Para garantir que o encaminhamento de email foi configurado com êxito, siga um destes procedimentos:

1.  No EAC, vá até **Destinatários** \> **Caixas de Correio**.

2.  Na lista de caixas de correio de usuários, clique ou toque na caixa de correio para a qual você configurou o encaminhamento de emails e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique ou toque em **Recursos da Caixa de Correio**.

4.  Em **Fluxo de Email**, clique ou toque em **Exibir detalhes** para exibir as configurações de encaminhamento de email.

## Additional information

Este tópico destina-se a administradores. Se você deseja encaminhar seus próprios emails para outro destinatário, confira os tópicos a seguir:

  - [Encaminhar emails para outra conta de email](https://go.microsoft.com/fwlink/p/?linkid=510866)

  - [Gerenciar mensagens de email usando regras](https://go.microsoft.com/fwlink/p/?linkid=510869)

Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

