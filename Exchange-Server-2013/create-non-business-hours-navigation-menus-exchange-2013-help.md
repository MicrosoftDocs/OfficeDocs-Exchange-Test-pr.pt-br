---
title: 'Criar horário não comercial menus de navegação: Exchange 2013 Help'
TOCTitle: Criar horário não comercial menus de navegação
ms:assetid: bfe81ed6-9648-4882-8baf-ac93ea30a8ca
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232175(v=EXCHG.150)
ms:contentKeyID: 50486549
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar horário não comercial menus de navegação

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-05_

É possível habilitar o horário não comercial mapeamentos de teclas para um atendedor automático da Unificação de mensagens (UM). Depois de criar um atendedor automático de UM, um prompt de sistema padrão será usado para o horário não comercial prompt do menu principal saudação que os chamadores ouvem após o horário não comercial saudação de boas-vindas é reproduzido. O padrão horário não comercial prompt do menu principal diz: "Bem-vindo à impressora MicrosoftExchange depois que o atendedor automático de horas." Como nenhum mapeamentos de teclas são definidos por padrão, nenhuma opção de menu está disponível para os chamadores e ouvirão apenas o menu principal do horário não comercial de padrão solicitar.

Quando você configurar mapeamentos de teclas, você define as opções e as operações que serão realizadas se um chamador fala uma frase enquanto eles estão usando um habilitado para fala atendedor automático ou pressiona uma tecla no teclado do telefone enquanto eles estão usando um atendedor automático que não está habilitado para fala.

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar os mapeamentos de teclas fora do horário comercial em um atendedor automático

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione do atendedor automático para o qual você deseja criar um menu de navegação de horário não comercial. Na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM**, clique em **navegação de Menu**, em **navegação de menu do horário comercial**, selecione **Habilitar a navegação de menu horário não comercial** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Na página **nova entrada de navegação de menu**, use as opções a seguir para criar uma nova entrada de navegação de menu:
    
      - **Prompt**   Use esta caixa para digitar o nome do novo menu de navegação. O nome do menu de navegação é utilizado apenas para fins de exibição. Este é um campo necessário.
        
        Como você pode desejar especificar vários novos menus de navegação, recomendamos usar nomes significativos para mapeamentos de teclas. O nome do mapeamento de teclas pode conter espaços e no máximo 64 caracteres. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Quando essa tecla é pressionada**   Use essa lista para habilitar o mapeamento de teclas. O mapeamento de teclas é a tecla numérica que um chamador pressiona para que o atendedor automático execute uma operação específica, por exemplo, encaminhar o chamador para outro atendedor automático ou para um operador. Por padrão, nenhuma entrada é definida.
        
        Use a lista suspensa para selecionar a tecla numérica (de 1 a 9) que o chamador deve pressionar. Zero (0) é reservado para o operador do atendedor automático.
        
        Se você tiver selecionado **Atingir Tempo Limite**, na lista suspensa, isso permite que o chamador seja transferido para um número de ramal ou para outro atendedor automático, se ele não pressionar uma tecla no teclado do telefone. Por exemplo, "Fique na linha e sua chamada será atendida pelo próximo representante disponível". A configuração padrão é de 5 segundos. Se você habilitar essa opção, será criado um mapeamento de teclas em branco.
    
      - **Executar o seguinte arquivo de áudio**   Use essa opção para selecionar um arquivo de áudio pré-gravado para os chamadores. Clique em **Alterar** e em **Procurar**, para localizar o arquivo de áudio. Se você deixar o arquivo de áudio como o padrão \<Nenhum\>, o mecanismo de TTS (Conversão de Texto em Fala) da Unificação de Mensagens sintetizará um prompt de menu principal para horário não comercial. Como alternativa, você pode criar um arquivo de áudio personalizado que possa ser usado como o prompt de menu principal para horário não comercial para um atendedor automático habilitado para fala que diria, por exemplo, "Você ligou para a Contoso fora do horário comercial. Para deixar uma mensagem de voz para vendas, diga 1. Para deixar uma mensagem de voz para o suporte técnico, diga 2. Para deixar uma mensagem de voz para a administração, diga 3. Para falar com um operador fora do horário do expediente, pressione zero".
    
      - **Executar esta ação adicional**   Selecione uma das seguintes opções, para definir a ação que deseja que o atendedor automático execute para o chamador:
        
          - **Nenhuma**   Se você não quiser que o atendedor automático transfira a chamada para um ramal ou para outro atendedor automático, ou que ele deixe uma mensagem para um usuário, use essa opção.
        
          - **Transferir para este ramal**   Selecione essa opção, para permitir que chamadas sejam transferidas para um número de ramal. Se você habilitar essa opção, use a caixa para digitar o número do ramal para o qual a chamada será transferida. Esse campo permite apenas caracteres numéricos. Nenhum destes caracteres pode ser usado: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Transferir para este atendedor automático de UM**   Selecione essa opção para transferir a chamada para um atendedor automático existente. Clique em **Procurar** para localizar o atendedor automático que deseja usar. Antes de habilitar essa opção, primeiro crie e configure o atendedor automático. Essa opção é utilizada durante a criação de uma estrutura pai/filho de atendedores automáticos da UM.
        
          - **Deixar uma mensagem de voz para este usuário**   Selecione essa opção para habilitar um chamador para deixar uma mensagem de caixa postal para um usuário que está no mesmo plano de discagem do atendedor automático de UM que você está configurando. Quando um chamador escolhe essa opção em um menu de atendedor automático, ele será solicitado a deixar uma mensagem de voz para o usuário que foi selecionado. Clique em **Procurar** para localizar o usuário habilitado para UM.
        
          - **Anunciar local da empresa**   Selecione essa opção para permitir que um chamador escolha uma opção de menu de atendedor automático e ouça o local da empresa configurado no atendedor automático de UM. Para permitir que isso funcione corretamente, é preciso primeiro inserir o local da empresa na caixa **Local da empresa**, na página **Geral**, no atendedor automático de UM.
        
          - **Anunciar horário comercial**   Selecione essa opção para permitir que um chamador escolha uma opção de menu de atendedor automático e ouça o horário de funcionamento da empresa configurado no atendedor automático de UM. Para permitir que isso funcione corretamente, você deve primeiro configurar o horário de funcionamento na página **Horário comercial**, no atendedor automático de UM.

5.  Clique em **OK**, para criar o novo menu de navegação.

6.  Na página **Atendedor Automático de UM**, clique em **Salvar** para salvar suas alterações.

## Usar o Shell para habilitar os mapeamentos de teclas fora do horário comercial em um atendedor automático

Este exemplo configura um atendedor automático de UM chamado `MyAutoAttendant` e habilita o horário não comercial principais mapeamentos para que quando os chamadores dizem "After Hours" eles serão encaminhados para o número de ramal 12345, e se eles dizem "Direções" eles serão encaminhados para o número de ramal 23456.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AfterHoursKeyMappingEnabled $true -AfterHoursKeyMapping "AfterhoursOperator,12345","Directions,23456"

