---
title: 'Configurar o número de falhas de entrada antes que os usuários do Outlook Voice Access são desconectados: Exchange 2013 Help'
TOCTitle: Configurar o número de falhas de entrada antes que os usuários do Outlook Voice Access são desconectados
ms:assetid: 64c13d17-a26a-4c9b-b495-bd69c716456a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423547(v=EXCHG.150)
ms:contentKeyID: 50485745
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o número de falhas de entrada antes que os usuários do Outlook Voice Access são desconectados

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-09_

É possível configurar o número de vezes em que usuários que ligam para um número do Outlook Voice Access podem inserir dados incorretos antes de serem desconectados. Essa configuração se aplica a usuários do Outlook Voice Access e chamadores não autenticados que usam a pesquisa de diretório.

Estão são exemplos de tipos de dados considerados incorretos:

  - Um chamador solicita um número de ramal não encontrado no sistema.

  - O sistema não pode localizar o número de ramal do usuário para transferir a chamada.

  - Um chamador pressiona uma opção de menu que não é válida.

O valor dessa configuração pode ser definido de 1 a 20. Para a maioria das organizações, ele deve ser definido como o padrão de três tentativas. A definição desse valor muito baixo pode desconectar prematuramente os chamadores.

Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar falhas de entrada antes de desconectar

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Em **Configurações**, na entrada **Número de falhas de entrada antes de desconectar**, informe o número de falhas de entrada.

5.  Clique em **Salvar**.

## Usar o Shell para configurar Falhas de Entrada Antes de Desconectar

Este exemplo define as falhas de entrada antes de desconectar em cinco, em um plano de discagem chamado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -InputFailuresBeforeDisconnect 5

