---
title: 'Gerenciar um atendedor automático: Exchange 2013 Help'
TOCTitle: Gerenciar um atendedor automático
ms:assetid: 4809ff56-ae34-4ce6-8e39-9193311c3f83
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997867(v=EXCHG.150)
ms:contentKeyID: 50485472
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantGeneralPropertyPage
ms.translationtype: MT
---

# Gerenciar um atendedor automático

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-30_

Depois de criar um atendedor automático de Unificação de Mensagens (UM), é possível exibir ou definir diversas configurações. Por exemplo, você pode adicionar, remover e editar números de ramais associados ao atendedor automático. Você também pode habilitar ou desabilitar o ASR (Reconhecimento Automático de Fala) para o atendedor automático e alterar as saudações usadas no horário comercial e fora do horário comercial.

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

## Usar o EAC para exibir ou configurar as definições do atendedor automático de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Atendedores Automáticos de UM**, selecione o atendedor automático de UM que deseja exibir ou configurar e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  
    
    Na página **Atendedor Automático de UM**, clique em **Geral** para exibir informações somente para exibição sobre o atendedor automático de UM e para executar tarefas de gerenciamento no atendedor automático de UM da seguinte maneira:
    
      - **Plano de discagem de UM**   Esta caixa exibe o plano de discagem de UM associado ao atendedor automático. Depois de criar um atendedor automático, o plano de discagem associado ao atendedor automático não poderá ser alterado. Se for necessário associar um atendedor automático a um plano de discagem diferente, você deve excluir o plano de discagem e, depois, associar o atendedor automático ao plano de discagem correto depois de recriá-lo.
    
      - **Nome**   Esta caixa exibe o nome atribuído ao atendedor automático de UM quando ele foi criado. Esse é o nome que será exibido no EAC.
    
      - **Status**   Esta caixa mostra se o atendedor automático da UM está habilitado ou desabilitado. Para habilitar ou desabilitar o atendedor automática, feche a página **Atendedor Automático de UM** e use a barra de ferramentas em **Atendedores Automáticos de UM** na página **Plano de Discagem de UM**.
    
      - **Números de acesso   **Use esta caixa para digitar um número de ramal ou de acesso que direcione os chamadores para o atendedor automático. Por padrão, nenhum número de ramal ou de acesso é configurado quando você cria um atendedor automático.
        
        O número de dígitos nos números de ramal ou de acesso que você fornecer deve corresponder ao número de dígitos de um número de ramal configurado no plano de discagem da UM associado ao atendedor automático de UM. Você pode também adicionar um endereço SIP (Protocolo de Início de Sessão) a essa caixa. Um endereço SIP é usado por alguns PBXs (Private Branch eXchanges) IP, PBXs habilitados para SIP e o Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server.
        
        Você pode criar um novo atendedor automático sem listar um número de ramal ou de acesso. Para adicionar um número de ramal, digite o número nessa caixa e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). É possível associar mais de um número a um atendedor automático. Também é possível editar ou remover um número de acesso existente. Para editar um número existente, selecione-o e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Para remover da lista um número de ramal existente, selecione-o e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").
    
      - **Definir o atendedor automático para responder a comandos de voz**   Marque esta caixa de seleção para permitir que os chamadores respondam verbalmente a solicitações do atendedor automático para navegar no sistema de menus. Por padrão, quando um atendedor automático é criado, não está habilitado para fala.
        
        Se você decidir criar o atendedor automático de UM mas não habilitá-lo para fala, é possível usar o EAC ou o Shell para habilitá-lo para fala após a criação.
    
      - **Usar este atendedor automático quando os comandos de voz não funcionarem corretamente**   Clique em **Navegar** para selecionar o atendedor automático que deseja utilizar caso os comandos de voz não funcionem. Isso também é conhecido como um atendedor automático de fallback de DTMF. O atendedor automático de fallback DTMF só poderá ser usado se a opção **Definir o atendedor automático para responder a comandos de voz** estiver selecionada. Você deve criar primeiro um atendedor automático de fallback de DTMF e depois clicar em **Procurar** para localizar o atendedor automático DTMF apropriado.
        
        Um atendedor automático de fallback de DTMF é usado quando o atendedor automático habilitado para fala da UM não puder compreender ou reconhecer as entradas de fala do chamador. Se o atendedor automático de DTMF for usado, o chamador será solicitado a usar as entradas de DTMF para navegar no sistema de menus, soletrar o nome de um usuário ou usar um prompt de menu personalizado. Um chamador não poderá usar comandos de voz para navegar nesse atendedor automático.
        
        Se você não configurar um atendedor automático de fallback de DTMF, é recomendável configurar um número de ramal de operador no atendedor automático. +Se um número de ramal de operador não for configurado, quando os chamadores usarem um atendedor automático habilitado para fala e o sistema não reconhecer as entradas de voz, eles não poderão navegar no sistema ou ser transferidos para um operador.
        
        Embora não seja necessário, é recomendável configurar o atendedor automático de fallback de DTMF com a mesma configuração do atendedor automático habilitado para fala. O atendedor automático de fallback de DTMF deve estar habilitado para fala.
    
      - **Idioma da interface de voz automatizada**   Use essa lista para selecionar o idioma que os chamadores ouvirão quando acessarem o atendedor automático. O idioma padrão é determinado na instalação do Microsoft Exchange. Para implantações locais e híbridas, por padrão, o inglês americano é usado porque o atendedor automático utiliza as configurações de idioma do plano de discagem da UM. Para ter outras opções de idioma disponíveis, você deve instalar o pacote de idiomas da UM do idioma que você deseja incluir. Para obter mais informações sobre como instalar um pacote de idioma da UM, consulte [Instalar um pacote de idiomas para UM](install-a-um-language-pack-exchange-2013-help.md). Para a UM no Office 365, não é necessário instalar pacotes de idiomas adicionais da UM.
        
        Embora você possa selecionar um idioma diferente daquele selecionado no plano de discagem da UM associado ao atendedor automático, é recomendável que as configurações de idioma do plano de discagem correspondam às configurações do atendedor automático. Se as configurações de idioma não corresponderem, quando os chamadores ligarem para um número de ramal definido no plano de discagem, serão apresentados prompts em um idioma, e quando discarem um número do ramal associado a um atendedor automático, serão apresentados prompts em um idioma diferente.
    
      - **Nome da empresa   **Utilize esta caixa para inserir o nome da empresa. Por padrão, nenhum nome está configurado. Se você inserir o nome da empresa nesta caixa, uma mensagem com o nome da empresa será executada para os chamadores em vez da saudação padrão.
    
      - **Localização da empresa   **Utilize esta caixa para inserir a localização da empresa. Por padrão, nenhum local da empresa é inserido. Se você inserir a localização da empresa na caixa, ela será tocada para os chamadores.

4.  
    
    Use **Saudações** no atendedor automático para gerenciar saudações gravadas. Você pode selecionar saudações padrão ou saudações personalizadas gravadas anteriormente para o horário comercial e o horário não comercial. Você pode configurar o seguinte:
    
      - **Saudação em horário comercial**   Essa é a saudação inicial reproduzida quando um chamador liga para o atendedor automático durante o horário comercial da organização. Por padrão, o horário comercial é das 12:00 às 12:00 da manhã e nenhum horário não comercial está definido. Se você não especificar uma saudação personalizada, um prompt de sistema que diz "Bem-vindo ao atendedor automático do Exchange" é reproduzido para os chamadores. O horário comercial e o horário não comercial são configurados na guia **Horário comercial** do atendedor automático.
        
        Você pode personalizar essa saudação, como "O Woodgrove Bank agradece sua ligação", para representar sua empresa. Você pode configurar uma saudação de horário comercial personalizada clicando em **Alterar** para selecionar um arquivo de saudação personalizada gravado anteriormente. A saudação personalizada já deve ter sido gravada como um arquivo .wav ou .wma.
    
      - **Saudação em horário não comercial**   Essa é a saudação inicial reproduzida quando um chamador liga para o atendedor automático fora do horário comercial da sua organização. Por padrão, nenhum horário não comercial está configurado. Portanto, não há saudação padrão para o horário não comercial. Você pode configurar o horário comercial e o horário não comercial em **Horário comercial** no atendedor automático.
        
        Você pode personalizar essa saudação para representar sua empresa; por exemplo, \&quot;O Woodgrove Bank agradece sua ligação, mas no momento estamos fechados" ou "Você ligou para Contoso, Ltd. após o horário comercial. Nosso horário comercial é das 8:00 às 17:00, de segunda a sexta-feira." Você pode configurar uma saudação de horário não comercial personalizada clicando em **Alterar** para selecionar um arquivo de saudação personalizada gravado anteriormente. A saudação personalizada já deve ter sido gravada como um arquivo .wav ou .wma.
    
      - **Informe**   Quando habilitado, este registro opcional é executado imediatamente após a saudação de horário comercial ou não comercial. Um informe pode conter o horário de funcionamento da organização, como "Funcionamos das 8:30 às 17:30 de segunda a sexta, e das 8:30 às 13:00 aos sábados". Um informe também pode fornecer as informações necessárias à conformidade com a diretiva da empresa, por exemplo, "Chamadas podem ser monitoradas para fins de treinamento". Se for importante que os chamadores ouçam todo o informe, ele pode ser marcado como não interrompível, exigindo que o chamador ouça o informe completo.
        
        Por padrão, não há informes configurados em planos de discagem da UM ou atendedores automáticos. Se você habilitar um informe e usar um arquivo de áudio personalizado específico da sua organização, a opção **Permitir que o informe seja interrompido** ficará disponível. As gravações já devem ter sido feitas em arquivos .wav ou .wma. Clique em **Alterar** para localizar um arquivo de informe personalizado gravado anteriormente.
        
        **Permitir que o informe seja interrompido**   Marque essa caixa de seleção para permitir que chamadores interrompam o informe. Essa opção deve ser habilitada quando houver informes longos. Os chamadores podem ficar frustrados se o informe for longo e não puder ser interrompido para acessar as opções oferecidas pelo atendedor automático.

5.  Use **Horário comercial** para determinar as horas do expediente da organização. Durante o horário comercial, os chamadores ouvirão uma saudação padrão de horário comercial ou uma saudação personalizada, além do prompt do menu principal de horário comercial se os mapeamentos de teclas adequados de horário comercial estiverem configurados na **Navegação de menus**. Você pode configurar o seguinte:
    
      - **Fuso horário**   Use essa lista para selecionar o seu fuso horário. Quando você definir o agendamento, considere se o plano de discagem associado ao atendedor automático cobre mais de um fuso horário .
        
        Por padrão, em implantações locais e híbridas, o fuso horário é configurado usando o horário do sistema do servidor local quando o servidor de Caixa de Correio que executa o serviço de Unificação de Mensagens do Microsoft Exchange tiver sido instalado.
    
      - **Horário comercial**   Clique em **Configurar horário comercial** e depois, na página **Configurar Horário Comercial**, use a grade para configurar o horário comercial de sua organização.
    
      - **Agendamento de Feriado**   Use isso para definir os dias, de 00:00 às 23:59, em que a sua organização estará fechada por causa de um feriado. Os chamadores atendidos pelo atendedor automático durante os horários especificados na página **Novo Feriado** ouvirão um arquivo personalizado de áudio de feriado definido por você. Quando configurar o agendamento de feriado, você deve definir o nome do feriado, o arquivo de áudio para a saudação de feriado gravada, e a **Data de início** e a **Data de término**. As saudações já devem ter sido gravadas em arquivos .wav ou .wma.

6.  Use a **Navegação de menus** para especificar as opções de menu oferecidas aos chamadores durante o horário comercial e não comercial. Se quiser habilitar a navegação de menus, é necessário fazê-lo separadamente para horários comerciais e não comerciais. Por exemplo, se quiser habilitar a navegação durante o horário comercial, será necessário adicionar uma gravação de áudio personalizada com o prompt do menu, marcar a caixa de seleção **Habilitar navegação de menus no horário comercial**, clicar em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e configurar as opções na página **Nova entrada de navegação de menu**.
    
      - **Navegação de menus no horário comercial**   Essa é a lista de opções que os chamadores ouvem durante o horário comercial definido na página **Horário comercial**. Por exemplo, "Para suporte técnico, pressione ou diga 1. Para escritórios corporativos e administração, pressione ou diga 2. Para vendas, pressione ou diga 3".
        
        Para habilitar a navegação de menus no horário comercial, é necessário executar as seguintes etapas:
        
        1.  **Prompt do menu**   Use isso para especificar um arquivo de áudio personalizado de prompt de menu. Para usar um prompt de menu de horário comercial gravado anteriormente, clique em **Alterar** e em **Procurar** para localizar a gravação do prompt de menu.
        
        2.  **Habilitar navegação de menus no horário comercial**   Marque essa caixa de seleção para habilitar as opções de navegação de menus que serão utilizadas durante o horário comercial. Ao habilitar a navegação de menus no horário comercial, você pode adicionar novas entradas de navegação de menus para horário comercial.
        
        3.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para criar uma nova entrada de navegação de menu. Na página **Nova entrada de navegação de menu**, use as seguintes opções para criar uma nova entrada de navegação de menu:
            
              - **Prompt**   Use esta caixa para digitar o nome do novo menu de navegação. O nome do menu de navegação é utilizado apenas para fins de exibição. Este é um campo necessário.
                
                Como você pode desejar especificar vários novos menus de navegação, recomendamos usar nomes significativos para mapeamentos de teclas. O nome do mapeamento de teclas pode conter espaços e no máximo 64 caracteres. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
            
              - **Quando essa tecla é pressionada**   Use essa lista para habilitar o mapeamento de teclas. O mapeamento de teclas é a tecla numérica que um chamador pressiona para que o atendedor automático execute uma operação específica, por exemplo, encaminhar o chamador para outro atendedor automático ou para um operador. Por padrão, nenhuma entrada é definida.
                
                Use a lista suspensa para selecionar a tecla numérica (de 1 a 9) que o chamador deve pressionar. Zero (0) é reservado para o operador do atendedor automático.
                
                Se você tiver selecionado **Atingir Tempo Limite**, na lista suspensa, isso permite que o chamador seja transferido para um número de ramal ou para outro atendedor automático, se ele não pressionar uma tecla no teclado do telefone. Por exemplo, "Fique na linha e sua chamada será atendida pelo próximo representante disponível". A configuração padrão é de 5 segundos. Se você habilitar essa opção, será criado um mapeamento de teclas em branco.
            
              - **Executar o seguinte arquivo de áudio**   Use essa opção para selecionar um arquivo de áudio pré-gravado para os chamadores. Clique em **Alterar** e em **Procurar**, para localizar o arquivo de áudio. Se você deixar o arquivo de áudio como o padrão \<Nenhum\>, o mecanismo de TTS (Text to Speech) da Unificação de Mensagens sintetizará um prompt de menu principal para horário comercial. Como alternativa, você pode criar um arquivo de áudio personalizado que possa ser usado como o prompt de menu principal no horário comercial para um atendedor automático habilitado para fala. Por exemplo, o prompt pode dizer, "Para deixar uma mensagem de voz para vendas, diga 1. Para deixar uma mensagem de voz para o suporte técnico, diga 2. Para deixar uma mensagem de voz para a administração, diga 3".
            
              - **Executar esta ação adicional**   Selecione uma das seguintes opções, para definir a ação que deseja que o atendedor automático execute para o chamador:
                
                  - **Nenhuma**   Se você não quiser que o atendedor automático transfira a chamada para um ramal ou para outro atendedor automático, ou que ele deixe uma mensagem para um usuário, use essa opção.
                
                  - **Transferir para este ramal**   Selecione essa opção, para permitir que chamadas sejam transferidas para um número de ramal. Se você habilitar essa opção, use a caixa para digitar o ramal para o qual a chamada será transferida. Esse campo permite apenas caracteres numéricos. Nenhum destes caracteres pode ser usado: " / \\ \[ \] : ; | = , + \* ? \< \>.
                
                  - **Transferir para este atendedor automático de UM**   Selecione essa opção, para transferir a chamada para um atendendor automático. Clique em **Procurar** para localizar o atendedor automático que deseja usar. Antes de habilitar essa opção, primeiro crie e configure o atendedor automático. Essa opção é utilizada durante a criação de uma estrutura pai/filho de atendedores automáticos da UM.
                
                  - **Deixar uma mensagem de voz para este usuário**   Selecione essa opção para habilitar um chamador para deixar uma mensagem de caixa postal para um usuário que está no mesmo plano de discagem do atendedor automático de UM que você está configurando. Quando um chamador escolhe essa opção em um menu de atendedor automático, ele será solicitado a deixar uma mensagem de voz para o usuário que foi selecionado. Clique em **Procurar** para localizar o usuário habilitado para UM.
                
                  - **Anunciar local da empresa**   Selecione essa opção para permitir que um chamador escolha uma opção de menu de atendedor automático e ouça o local da empresa configurado no atendedor automático de UM. Para permitir que isso funcione corretamente, é preciso primeiro inserir o local da empresa na caixa **Local da empresa**, na página **Geral**, no atendedor automático de UM.
                
                  - **Anunciar horário comercial**   Selecione essa opção para permitir que um chamador escolha uma opção de menu de atendedor automático e ouça o horário de funcionamento da empresa configurado no atendedor automático de UM. Para permitir que isso funcione corretamente, você deve primeiro configurar o horário de funcionamento na página **Horário comercial**, no atendedor automático de UM.
    
      - **Navegação de menus fora do horário comercial**   Essa é a lista de opções que os chamadores ouvem fora do horário comercial definido na página **Horário comercial**. Por exemplo, "Sua ligação é muito importante para nós. Porém, você entrou em contato com o Woodgrove Bank após o horário comercial normal. Para deixar uma mensagem, pressione ou diga 1 e retornaremos sua ligação assim que possível".
        
        Para habilitar a navegação de menus fora do horário comercial, é necessário executar as seguintes etapas:
        
        1.  **Prompt do menu**   Use isso para especificar um arquivo de áudio personalizado de prompt de menu. Para usar um prompt de menu para horário não comercial gravado anteriormente, clique em **Procurar**.
        
        2.  **Habilitar navegação de menus fora do horário comercial**   Marque essa caixa de seleção para habilitar as opções de navegação de menus que serão utilizadas fora do horário comercial. Ao habilitar a navegação de menus fora do horário comercial, você pode adicionar novas entradas de navegação de menus para horário não comercial.
        
        3.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para criar uma nova entrada de navegação de menu. Na página **Nova entrada de navegação de menu**, use as seguintes opções para criar uma nova entrada de navegação de menu:
            
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

7.  Use **Catálogo de endereços e acesso de operador** para definir os recursos disponíveis para chamadores que discarem para o atendedor automático de UM. É possível configurar recursos de atendedor automático como o idioma usado quando os chamadores ligam para o atendedor automático e a possibilidade dos chamadores fazerem a transferência para um número de ramal de um operador. Você pode configurar o seguinte:
    
      - **Opções para contatar os usuários**   Use essas opções para determinar como os chamadores podem contatar os usuários com correio de voz quando ligarem para um atendedor automático de UM
        
          - **Permitir que chamadores disquem para usuários**   Marque essa caixa de seleção para permitir que chamadores transfiram chamadas para os usuários. Por padrão, esta opção está habilitada e permite que usuários associados com o plano de discagem transfiram chamadas para usuários do mesmo plano de discagem da UM. Depois de marcar essa caixa de seleção, você pode definir o grupo de usuários para quem os chamadores poderão fazer transferências selecionando a opção apropriada na seção **Opções de pesquisa do catálogo de endereços** nesta página.
            
            Se você desabilitar essa opção e desabilitar a opção **Permitir que chamadores deixem mensagens de voz para usuários**, as opções em **Opções de pesquisa do catálogo de endereços** também serão desabilitadas.
        
          - **Permitir que chamadores deixem mensagens de voz para usuários**   Marque essa caixa de seleção para permitir que os chamadores enviem mensagens de voz para os usuários. Por padrão, esta opção está habilitada e permite que usuários associados ao plano de discagem enviem mensagens de voz para usuários do mesmo plano de discagem da UM. Depois de marcar essa caixa de seleção, você pode definir o grupo de usuários para quem os chamadores poderão enviar mensagens de voz selecionando a opção apropriada na seção **Opções de pesquisa do catálogo de endereços** nesta página.
            
            Se você desabilitar essa opção e desabilitar a opção **Permitir que chamadores disquem para usuários**, as opções em **Opções de pesquisa do catálogo de endereços** também serão desabilitadas.
            
            Se esta opção for desabilitada, o atendedor automático não convidará chamadores a enviar uma mensagem de voz durante um prompt do sistema.
    
      - **Opções de pesquisa do catálogo de endereços**   Use essas opções para determinar um grupo de usuários. Por padrão, **Permitir que chamadores procurem usuários por nome ou alias** está selecionado, junto com a opção **Neste plano de discagem apenas**. Entretanto, é possível alterar o grupo de usuários para permitir que chamadores transfiram chamadas ou enviem mensagens de voz para usuários localizados na lista de endereços global (GAL) de uma organização. Você pode escolher entre estas opções:
        
          - **Permitir que chamadores procurem usuários por nome ou alias**   Por padrão, essa opção está selecionada. Ela permite que os chamadores que ligarem para esse atendedor automático façam uma pesquisa de diretório procurando usuários pelo nome ou pelo alias. Um alias é atribuído a um usuário quando uma caixa de correio é criada para ele. O alias é a primeira parte de um endereço SMTP, como por exemplo tonysmith@contoso.com. O endereço SMTP é tonysmith@contoso.com, enquanto o alias é tonysmith. Escolher essa opção afetará somente os chamadores que usarem esse atendedor automático, e não aqueles que usarem o Outlook Voice Access.
            
              - **Neste plano de discagem apenas**   Selecione essa opção para permitir que os chamadores que se conectarem ao atendedor automático de UM localizem e contatem usuários que estejam no mesmo plano de discagem associado a esse atendedor automático de UM. Por padrão, essa opção está habilitada no plano de discagem e no atendedor automático. Isso significa que tanto os usuários do Outlook Voice Access quanto chamadores no atendedor automático serão capazes de pesquisar por usuários no mesmo plano de discagem.
            
              - **Em toda a organização**   Selecione essa opção para permitir que os chamadores que ligarem para esse atendedor automático de UM procurem por e contatem qualquer pessoa incluída na GAL da organização. Isso inclui não apenas os usuários habilitados para UM, mas todos os usuários habilitados para caixa de correio. Esta opção permite que os chamadores contatem usuários em vários planos de discagem. Esse recurso não está habilitado por padrão. Esta configuração também está disponível em um plano de discagem para os usuários do Outlook Voice Access.
        
          - **Informações a incluir para nomes semelhantes**   Use esta lista suspensa para selecionar a opção utilizada pelo atendedor automático de UM quando os usuários tiverem os mesmos nomes ou nomes semelhantes. Essa configuração é usada quando existem dois ou mais usuários com o mesmo nome no diretório. Essa configuração também é chamada de campo de desambiguidade ou correspondência de nome. Você pode configurar essa definição ou deixar a configuração padrão do atendedor automático. Por padrão, o atendedor automático herdará essa configuração do plano de discagem que estiver vinculado ao atendedor automático. Eis um exemplo de atendedor automático habilitado para fala:
            
            1.  Sistema: \&quot;Bem-vindo à Contoso. Se você sabe o nome da pessoa que está chamando, diga-me o nome a qualquer momento\&quot;.
            
            2.  O chamador diz \&quot;Tony Smith\&quot;.
            
            3.  Há várias pessoas com esse nome. Selecione uma das opções: Tony Smith, pesquisa, pressione 1. Tony Smith, administração, pressione 2. Tony Smith, suporte técnico, pressione 3\&quot;.
            
            4.  O chamador pressiona a tecla apropriada no teclado numérico e a chamada é transferida para o usuário.
                

                > [!TIP]
                > Em um atendedor automático que não estiver habilitado para fala, o sistema dirá ao chamador para usar o teclado numérico para inserir o nome do usuário (sobrenome primeiro) e procurará pelo usuário. Se houver mais de uma pessoa no diretório com o mesmo nome, o chamador será orientado a pressionar a tecla apropriada para ser transferido ao usuário. Como opção, você pode criar um atendedor automático de fallback de DTMF que usa somente o teclado numérico para inserir um nome ou alias.

            
            Para que essas configurações sejam usadas, é necessário adicionar as informações corretas do usuário. Por exemplo, se quiser que o atendedor automático use um cargo para dois usuários com mesmo nome, você deve adicionar essa informação à conta do usuário. Selecione um dos métodos a seguir que oferecem mais informações para ajudar o chamador a selecionar o usuário correto na organização:
            
              - **Herdar do plano de discagem**   Selecione essa opção para que o atendedor automático use a configuração padrão do plano de discagem associado ao atendedor automático.
            
              - **Cargo**   Selecione essa opção para que o atendedor automático inclua o cargo de cada usuário ao listar correspondências.
            
              - **Departamento**   Selecione essa opção para que o atendedor automático inclua o departamento de cada usuário ao listar correspondências.
            
              - **Local**   Selecione essa opção para que o atendedor automático inclua o local de cada usuário ao listar correspondências.
            
              - **Nenhum**   Selecione esta opção para que não sejam fornecidas informações adicionais quando houver correspondências na lista.
            
              - **Solicitar alias**   Selecione esta opção para que o atendedor automático solicite o alias do usuário ao chamador.

8.  Em **Acesso do operador**, você pode especificar as configurações do operador do atendedor automático, incluindo as seguintes:
    
      - **Ramal do Operador**   Use esta caixa para digitar o número do ramal usado para chamar o operador. Esse número de ramal pode conectar o chamador a um operador humano ou a uma caixa de correio habilitada para UM, ou pode ser configurado para chamar um número de telefone externo. Por padrão, o ramal do operador não está incluído nesta caixa.
    
      - **Permitir transferência para operador durante horário comercial**   Marque essa caixa de seleção para permitir que chamadores sejam transferidos para operadores humanos durante o horário comercial usando o número de ramal que foi configurado na caixa **Ramal do operador**. Por padrão, essa opção está desabilitada.
        
        É útil habilitar esta opção para que, quando um chamador não tiver êxito ao usar os prompts de menu ou na pesquisa de diretório para localizar a pessoa desejada durante o horário comercial, possa deixar uma mensagem de voz ou conectar-se a um operador humano. Após habilitar essa opção, é possível configurar o ramal de um operador em uma caixa de correio habilitada para UM que está sendo monitorada. O chamador pode deixar uma mensagem de voz, ou um operador humano que tenha o ramal pode ajudar o chamador.
    
      - **Permitir transferência para operador durante horário não comercial**   Marque essa caixa de seleção para permitir que chamadores sejam transferidos para operadores humanos fora do horário comercial usando o número de ramal que foi configurado na caixa **Ramal do operador**. Por padrão, essa opção está desabilitada.
        
        É útil habilitar esta opção para que, quando um chamador não tiver êxito ao usar os prompts de menu ou na pesquisa de diretório para localizar a pessoa desejada após o horário comercial, ele possa deixar uma mensagem de voz ou conectar-se a um operador humano. Após habilitar essa opção, é possível configurar o ramal de um operador configurado em uma caixa de correio habilitada para UM que está sendo monitorada. O chamador pode deixar uma mensagem de voz, ou um operador humano que tenha o ramal pode ajudar o chamador.

9.  
    
    Use a **Autorização de discagem** para configurar regras de discagem para chamadores que ligarem para um atendedor automático de UM. Você pode usar essas configurações para controlar o número de ramais que podem ser alcançados de um atendedor automático ou controlar os números de telefone que podem ser discados por chamadores que discaram para o atendedor automático. Você pode configurar o seguinte:
    
      - **Chamadas no mesmo plano de discagem da UM**   Marque essa caixa de seleção para permitir que usuários que ligarem para um atendedor automático façam ou transfiram chamadas para um número de ramal associado a um usuário habilitado para UM que esteja associado ao mesmo plano de discagem que o atendedor automático. Por padrão, essa configuração está habilitada.
        
        Quando essa configuração é desabilitada, os usuários que fazem uma chamada para um atendedor automático podem fazer ou transferir chamadas para usuários não habilitados para UM ou para outros ramais que não estejam associados a um usuário habilitado para UM. Os usuários não podem fazer transferências de chamadas para usuários habilitados para UM que estejam associados ao mesmo plano de discagem do atendedor automático. Isso acontece porque, por padrão, a configuração **Permitir chamadas para qualquer ramal** está habilitada.
    
      - **Permitir chamadas para qualquer ramal**   Quando essa configuração é desabilitada, os usuários que ligarem para um atendedor automático não conseguirão fazer chamadas para usuários que não estejam habilitados para UM ou para outros ramais que não estejam associados a um usuário habilitado para UM. Entretanto, eles poderão fazer ou transferir chamadas para ramais associados a usuários habilitados para UM. Isso acontece porque, por padrão, a configuração **Chamadas no mesmo plano de discagem da UM** está habilitada. A configuração **Permitir chamadas para qualquer ramal** está habilitada por padrão.
        
        Quando essa configuração estiver habilitada, os usuários que fazem chamadas para um atendedor automático podem fazer chamadas para usuários não habilitados para UM, para outros ramais que não estejam associados a um usuário habilitado para UM e para usuários habilitados para UM. Isso acontece porque, por padrão, a configuração **Chamadas no mesmo plano de discagem da UM** está habilitada.
        
        Você pode habilitar essa configuração em um ambiente onde nem todos os usuários tenham sido habilitados para UM. Essa configuração também é útil quando você desejar permitir que usuários que façam uma chamada para um número de telefone configurado em um atendedor automático efetuem chamadas para ramais que não estão associados a um usuário habilitado para UM.
    
      - **Grupos autorizados de regras de discagem locais/regionais**   Use essa seção para adicionar ou remover grupos de regras de discagem permitidos no país/região. Por padrão, não há grupos de regras de discagem do país/região configurados em atendedores automáticos da UM.
        
        Grupos de regras de discagem do país/região são usados para permitir ou restringir os números de telefones em um país ou região que qualquer usuário que tenha discado para o atendedor automático da UM pode discar. Isso ajuda a evitar chamadas e despesas não autorizadas ou desnecessárias.
        
        Para adicionar grupos de regras de discagem do país/região, é necessário antes criar os grupos de regras de discagem do país/região apropriados no plano de discagem associado ao atendedor automático de UM, e depois adicionar o grupo de regras de discagem apropriado.
        
        Grupos de regras de discagem do país ou região podem ser usados para habilitar o servidor de Unificação de Mensagens a fim de permitir ou restringir o acesso a números de telefone no país ou região. Isso é aplicado a qualquer usuário que tenha feito uma chamada para um atendedor automático. Para obter mais informações sobre discagem externa, consulte [Permitir que os usuários façam chamadas](allow-users-to-make-calls-exchange-2013-help.md).
    
      - **Grupos autorizados de regras de discagem internacionais**   Use essa seção para adicionar ou remover grupos de regras de discagem permitidos internacionalmente. Por padrão, não há grupos de regras de discagem internacional configurados em atendedores automáticos da UM.
        
        Grupos de regras de discagem internacional são usados para permitir ou restringir os números de telefones fora de um país ou região que qualquer usuário que tenha discado para o atendedor automático da UM pode discar. Isso ajuda a evitar chamadas e despesas não autorizadas ou desnecessárias.
        
        Para adicionar grupos de regras de discagem internacionais, é necessário antes criar os grupos de regras de discagem internacionais apropriados no plano de discagem associado ao atendedor automático de UM. Após criar os grupos de regras de discagem necessários no plano de discagem, você deve adicionar os grupos de regras de discagem à lista de grupos autorizados de regras de discagem no atendedor automático da UM.
        
        Grupos de regras de discagem internacional podem pela Unificação de Mensagens para permitir ou restringir o acesso a números de telefone fora de um país ou região. Isso é aplicado a qualquer usuário que tenha feito uma chamada para um atendedor automático. Para obter mais informações sobre discagem externa, consulte [Permitir que os usuários façam chamadas](allow-users-to-make-calls-exchange-2013-help.md).

10. Clique em **OK**, para criar o novo menu de navegação.

11. Na página **Atendedor Automático de UM**, clique em **Salvar** para salvar suas alterações.

## Usar o Shell para configurar as propriedades do atendedor automático da UM

Este exemplo configura um atendedor automático de UM chamado `MySpeechEnabledAA` para retornar ao atendedor automático `MyDTMFAA`, define o ramal do operador como 50100 e habilita transferências para esse ramal após o horário comercial.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true

Este exemplo configura um atendedor automático da UM chamado `MyUMAutoAttendant` que possui: Horário comercial configurado como das 10h45 a 13h15 aos domingos, das 9h00 às 17h00 às segundas e das 9h00 às 16h30 aos sábados; feriados e saudações associadas configurados como "Ano Novo" dia 2 de janeiro de 2013; e "Edifício Fechado para Reforma" configurado como de 24 a 28 de abril de 2013.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

## Usar o Shell para exibir as propriedades do atendedor automático da UM

Este exemplo retorna uma lista formatada de todos os atendedores automáticos da UM.

    Get-UMAutoAttendant | Format-List

Este exemplo exibe as propriedades de um atendedor automático da UM chamado MyUMAutoAttendant.

    Get-UMAutoAttendant -Identity MyUMAutoAttendant

