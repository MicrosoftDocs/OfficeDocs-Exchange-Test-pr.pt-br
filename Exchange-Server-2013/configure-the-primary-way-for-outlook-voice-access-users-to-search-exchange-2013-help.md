---
title: 'Configurar principal forma de pesquisa para usuários do Outlook Voice Access'
TOCTitle: Configurar a principal maneira para os usuários do Outlook Voice Access pesquisar
ms:assetid: 3d93a037-5820-41d3-9206-69f534414daf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997563(v=EXCHG.150)
ms:contentKeyID: 50485371
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a principal maneira para os usuários do Outlook Voice Access pesquisar

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-21_

Quando você cria um plano de discagem da Unificação de Mensagens (UM), você pode configurar os modos principal e secundário que os chamadores podem pesquisar nomes para localizar um usuário quando eles ligam para um número do Outlook Voice Access ou para um atendedor automático de UM que está associado ao plano de discagem. Os chamadores podem usar entradas de discagem por tom para localizar um usuário habilitado para UM.


> [!TIP]
> <STRONG>Nenhum</STRONG> não é uma opção disponível para o modo principal de os chamadores procurarem nomes. Quando <STRONG>Nenhum</STRONG> for selecionado como o modo secundário de eles procurarem nomes, somente o modo principal estará disponível para os chamadores. Se você configurar os modos principal e secundário de os chamadores procurarem por nomes, o sistema perguntará qual você quer usar.



Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para alterar o método primário de discagem por nome

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Em **Configurações**, em **Principal maneira de procurar nomes**, use o menu suspenso para selecionar a opção desejada:
    
      - **Sobrenome Nome** (padrão)
    
      - **Nome Sobrenome**
    
      - **Endereço SMTP**

5.  Clique em **Salvar**.

## Usar o Shell para alterar o método primário de discagem por nome

Este exemplo define o método principal de discagem por nome para `FirstLast`. Isso permite aos chamadores que ligam para o número do Outlook Voice Access ou para um atendedor automático da UM associado ao plano de discagem pesquisar por um usuário habilitado para a UM pelo nome e depois pelo sobrenome.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary FirstLast

Este exemplo define o método principal de discagem por nome para `LastFirst`. Isso permite aos chamadores que ligam para o número do Outlook Voice Access ou para um atendedor automático da UM associado ao plano de discagem pesquisar por um usuário habilitado para a UM pelo sobrenome e depois pelo nome.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary LastFirst 

Este exemplo define o método principal de discagem por nome para `SMTP address`. Isso permite aos chamadores que ligam para o número do Outlook Voice Access ou para um atendedor automático da UM associado ao plano de discagem pesquisar por um usuário habilitado para a UM pelo seu endereço SMTP.

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress

