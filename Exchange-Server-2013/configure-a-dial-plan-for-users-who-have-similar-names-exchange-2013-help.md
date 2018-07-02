---
title: 'Configurar um plano de discagem para usuários que tenham nomes semelhantes: Exchange 2013 Help'
TOCTitle: Configurar um plano de discagem para usuários que tenham nomes semelhantes
ms:assetid: 14783f45-95f5-49de-8215-0a3aef7dc034
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb266943(v=EXCHG.150)
ms:contentKeyID: 51407838
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um plano de discagem para usuários que tenham nomes semelhantes

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-21_

Você pode configurar um plano de discagem de Unificação de Mensagens (UM) para especificar as informações fornecidas aos chamadores quando os usuários têm nomes iguais ou parecidos. A UM usa essa configuração para diferenciar entre os usuários que têm nomes iguais ou parecidos e fornece essas informações aos chamadores. Quando um chamador ou um usuário do Outlook Voice Access precisa inserir letras para localizar um determinado usuário, às vezes, mais de um nome corresponde à entrada do chamador. É possível usar uma das opções disponíveis para fornecer ao chamador mais informações a fim de ajudá-lo a localizar o usuário desejado.

É possível fazer isso nos planos de discagem da UM e nos atendedores automáticos da UM. Quando um atendedor automático da UM é criado, ele herda essa configuração do plano de discagem que está associado ao atendedor automático. Por padrão, essa configuração não é definida para planos de discagem, portanto, nenhuma informação adicional será fornecida aos chamadores para ajudá-los a localizar o usuário atual.


> [!TIP]
> Para que as informações que serão incluídas para os usuários com nomes parecidos funcione corretamente, é necessário fornecer as informações de cargo, departamento e local para os destinatários em sua organização do Microsoft Exchange.



Para conhecer tarefas de gerenciamento adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar um plano de discagem de UM para os usuários com nomes parecidos

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, clique em **Configurar** \> **Transferir & pesquisar** e em **Informações a serem incluídas para usuários com o mesmo nome**, selecione uma das seguintes opções:
    
      - **Cargo**   O plano de discagem inclui o cargo de cada usuário quando descobre dois ou mais usuários com nomes parecidos.
    
      - **Departamento**   O plano de discagem inclui o departamento de cada usuário quando descobre dois ou mais usuários com nomes parecidos.
    
      - **Local**   O plano de discagem inclui o local de cada usuário quando descobre dois ou mais usuários com nomes parecidos.
    
      - **Nenhum**   O plano de discagem não inclui qualquer informação adicional quando os usuários têm nomes parecidos. Embora essa seja a configuração padrão, recomendamos a inclusão de uma das opções disponíveis para os chamadores. Se não o fizer, os chamadores não poderão diferenciar dois ou mais usuários com nomes parecidos.
    
      - **Solicitar por alias**   O plano de discagem solicita ao chamador o alias do usuário. Um alias é parte do email ou endereço SMTP do usuário que está antes do símbolo de arroba (@).

3.  Clique em **Salvar**.

## Usar o Shell para configurar um plano de discagem de UM para os usuários com nomes parecidos

Este exemplo define as informações que serão incluídas para usuários com nomes parecidos com o objetivo de solicitar o alias do usuário ou um plano de discagem de UM chamado `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod PromptForAlias

Este exemplo define as informações que serão incluídas para usuários com nomes parecidos sobre o departamento em um plano de discagem chamado `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Department

Este exemplo define as informações que serão incluídas para usuários com nomes parecidos sobre o local em um plano de discagem chamado `MyDialPlan`.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Location

