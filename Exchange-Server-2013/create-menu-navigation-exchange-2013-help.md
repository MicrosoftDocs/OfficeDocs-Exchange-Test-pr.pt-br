---
title: 'Criar navegação de menu: Exchange 2013 Help'
TOCTitle: Criar navegação de menu
ms:assetid: 3cfc9a01-0a61-4d15-9561-621568dc30d9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997471(v=EXCHG.150)
ms:contentKeyID: 50485361
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantKeyMappingControl
ms.translationtype: MT
---

# Criar navegação de menu

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-05_

Você pode usar a página de **entrada de navegação de menu Novo** para criar um único ou vários mapeamentos de teclas para a empresa ou o menu principal do horário não comercial solicita atendedores automáticos. Você pode definir a ação que será executada quando uma tecla no teclado do telefone é pressionada, por exemplo, transferindo a chamada para um número de ramal ou outro atendedor.

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar os menus de navegação de atendedor automático Unificação de mensagens

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione do atendedor automático para o qual você deseja criar a navegação de menu. Na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM**, clique em **Menu de navegação**, selecione **Habilitar a navegação de menu do horário comercial** ou **Habilitar a navegação de menu horário não comercial** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Na página **nova entrada de navegação de menu**, configure o seguinte:
    
      - **Prompt**   Use esta caixa para digitar o nome do novo menu de navegação. O nome do menu de navegação é utilizado apenas para fins de exibição. Este é um campo necessário.
        
        Como você pode desejar especificar vários novos menus de navegação, recomendamos usar nomes significativos para mapeamentos de teclas. O nome do mapeamento de teclas pode conter espaços e no máximo 64 caracteres. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Quando essa tecla é pressionada**   Use essa lista para habilitar o mapeamento de teclas. O mapeamento de teclas é a tecla numérica que um chamador pressiona para que o atendedor automático execute uma operação específica, por exemplo, encaminhar o chamador para outro atendedor automático ou para um operador. Por padrão, nenhuma entrada é definida.
        
        Use a lista suspensa para selecionar a chave numérica (de 1 a 9) que o chamador deverá pressionar. Zero (0) é reservado para o operador de atendedor automático.
        
        Se você tiver selecionado **Atingir Tempo Limite**, na lista suspensa, isso permite que o chamador seja transferido para um número de ramal ou para outro atendedor automático, se ele não pressionar uma tecla no teclado do telefone. Por exemplo, "Fique na linha e sua chamada será atendida pelo próximo representante disponível". A configuração padrão é de 5 segundos. Se você habilitar essa opção, será criado um mapeamento de teclas em branco.
    
      - **Executar o seguinte arquivo de áudio**    Use essa opção para selecionar um arquivo de áudio gravado anteriormente para os chamadores. Clique em **Alterar** e clique em **Procurar** para localizar o arquivo de áudio.
    
      - **Executar esta ação adicional**   Selecione uma das seguintes opções, para definir a ação que deseja que o atendedor automático execute para o chamador:
        
          - **Nenhum**    Se você não quiser o atendedor automático para transferir a chamada para uma extensão ou para outro atendedor ou deixar uma mensagem para um usuário, use esta opção.
        
          - **Transferir para este ramal**   Selecione essa opção, para permitir que chamadas sejam transferidas para um número de ramal. Se você habilitar essa opção, use a caixa para digitar o ramal para o qual a chamada será transferida. Esse campo permite apenas caracteres numéricos. Nenhum destes caracteres pode ser usado: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Transferir para este atendedor automático de UM**   Selecione essa opção, para transferir a chamada para um atendendor automático. Clique em **Procurar** para localizar o atendedor automático que deseja usar. Antes de habilitar essa opção, primeiro crie e configure o atendedor automático. Essa opção é utilizada durante a criação de uma estrutura pai/filho de atendedores automáticos da UM.
        
          - **Deixar uma mensagem de voz para este usuário**   Selecione essa opção para habilitar um chamador para deixar uma mensagem de caixa postal para um usuário que está no mesmo plano de discagem do atendedor automático de UM que você está configurando. Quando um chamador escolhe essa opção em um menu de atendedor automático, ele será solicitado a deixar uma mensagem de voz para o usuário que foi selecionado. Clique em **Procurar** para localizar o usuário habilitado para UM.
        
          - **Anunciar local da empresa**   Selecione essa opção para permitir que um chamador escolha uma opção de menu de atendedor automático e ouça o local da empresa configurado no atendedor automático de UM. Para permitir que isso funcione corretamente, é preciso primeiro inserir o local da empresa na caixa **Local da empresa**, na página **Geral**, no atendedor automático de UM.
        
          - **Anunciar horário comercial**   Selecione essa opção para permitir que um chamador escolha uma opção de menu de atendedor automático e ouça o horário de funcionamento da empresa configurado no atendedor automático de UM. Para permitir que isso funcione corretamente, você deve primeiro configurar o horário de funcionamento na página **Horário comercial**, no atendedor automático de UM.

5.  Clique em **OK**, para criar o novo menu de navegação.

6.  Na página **Atendedor Automático de UM**, clique em **Salvar** para salvar suas alterações.

## Use o Shell para configurar mapeamentos de teclas Atendedor de automático Unificação de mensagens

Este exemplo habilita o horário comercial mapeamentos de teclas para que:

  - Quando os chamadores pressionar 1, elas serão encaminhadas para outro atendedor automático de UM chamado `SalesAutoAttendant`.

  - Quando eles pressionarem 2, elas serão encaminhadas para o número de ramal 12345 para suporte.

  - Quando eles pressionarem 3, eles serão enviados para outro atendedor automático que irá reproduzir um arquivo de áudio.

<!-- end list -->

    Set-UMAutoAttendant -id MyAutoAttendant -BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

Este exemplo define os mapeamentos de teclas definidos em um arquivo de valores separados por vírgula (. csv). Você deve primeiro criar o arquivo. csv com os seguintes títulos e a entrada de AutoCorreção: \< chave \>, \< descrição \> \[\< extensão \>\], \[\< nome do autoattendant \>\], \[\< promptfilenamepath \>\], \[\< asrphrase1; asrphrase2 \>\], \[\< leavevoicemailfor \>\], \[\< transfertomailbox \>\]. Os valores entre colchetes são opcionais. Depois de criar o arquivo. csv, importe o arquivo. csv usando o cmdlet **Import-csv** .

    $o = Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    Set-UMAutoAttendant MyAutoAttendant -BusinessHoursKeyMapping $o

Este exemplo exporta os mapeamentos de teclas de um atendedor automático UM existente em um arquivo. csv e, em seguida, importa os mesmos mapeamentos de teclas para outro atendedor automático. Você pode também exportar os mapeamentos de teclas para um arquivo. csv, editar ou modificar os mapeamentos de teclas no arquivo. csv e importe os mapeamentos de teclas em outro atendedor automático.

    $aa = Get-UMAutoAttendant -id MyAutoAttendant
    $aa1 = Get-UMAutoAttendant -id MyAutoAttendant2
    $aa.BusinessHoursKeyMapping | Export-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    $aa1.BusinessHoursKeyMapping = (Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv")

