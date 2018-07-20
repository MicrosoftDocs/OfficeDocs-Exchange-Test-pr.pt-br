---
title: 'Configurar o modo secundário para os usuários do Outlook Voice Access pesquisar: Exchange 2013 Help'
TOCTitle: Configurar o modo secundário para os usuários do Outlook Voice Access pesquisar
ms:assetid: 5cd4e0a0-d023-45a1-aa3c-b8dea6ec6d72
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998311(v=EXCHG.150)
ms:contentKeyID: 52058429
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o modo secundário para os usuários do Outlook Voice Access pesquisar

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Ao criar um plano de discagem, você pode configurar os métodos ou modos primários e secundários de *métodos de discagem por nome* pelos quais os chamadores podem pesquisar por nomes. Os chamadores usam métodos de discagem por nome para localizar e contatar um usuário ao ligar para um número do Outlook Voice Access ou para o atendedor automático de UM associado ao plano de discagem. Os chamadores podem usar entradas de discagem por tom para localizar um usuário habilitado para UM.


> [!TIP]
> Se <STRONG>Nenhum</STRONG> for selecionado como modo secundário para chamadores procurarem por nomes, apenas o modo principal de pesquisar nomes estará disponível para chamadores que desejam localizar usuários. Se você configurar os modos principal e secundário de os chamadores procurarem por nomes, os chamadores serão solicitados para ambos os modos.



Para conhecer tarefas de gerenciamento adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para alterar o método de discagem secundária por nome

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Em **Configurações**, em **Modo principal de procurar nomes**, use o menu suspenso para selecionar a opção desejada:
    
      - **Sobrenome Nome** (padrão)
    
      - **Nome Sobrenome**
    
      - **Endereço SMTP**
    
      - **Nenhum**

5.  Clique em **Salvar**.

## Usar o Shell para alterar a discagem secundária por método de nome

Este exemplo define o método secundário de discagem por nome como `FirstLast`. Isso permite aos chamadores que ligam para o número do Outlook Voice Access ou para um atendedor automático da UM associado ao plano de discagem pesquisar por um usuário habilitado para a UM pelo nome e depois pelo sobrenome.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary FirstLast

Este exemplo define o método secundário de discagem por nome como `LastFirst`. Isso permite aos chamadores que ligam para o número do Outlook Voice Access ou para um atendedor automático da UM associado ao plano de discagem pesquisar por um usuário habilitado para a UM pelo sobrenome e depois pelo nome.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary LastFirst 

Este exemplo define o método secundário de discagem por nome como `SMTP address`. Isso permite aos chamadores que ligam para o número do Outlook Voice Access ou para um atendedor automático da UM associado ao plano de discagem pesquisar por um usuário habilitado para a UM pelo seu endereço SMTP.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNameSecondary SMTPAddress 

Este exemplo define o método secundário de discagem por nome como `None`, e o principal como `SMTP address`. Isso permite aos chamadores que ligam para o número do Outlook Voice Access ou para um atendedor automático da UM associado ao plano de discagem pesquisar por um usuário habilitado para a UM pelo seu endereço SMTP apenas.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress -DialByNameSecondary None

