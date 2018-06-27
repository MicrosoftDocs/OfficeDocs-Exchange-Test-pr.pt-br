---
title: 'Criar e gerenciar grupos de distribuição: Exchange Online Help'
TOCTitle: Criar e gerenciar grupos de distribuição
ms:assetid: c4c43493-55e1-46d2-bd4b-d6f6cecd747f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124513(v=EXCHG.150)
ms:contentKeyID: 50486602
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDistributionGroupWizardForm.CreateDistributionGroupIntroductionWizardPage
ms.translationtype: HT
---

# Criar e gerenciar grupos de distribuição

 

_**Aplica-se a:**Exchange Online, Exchange Server 2016, Office 365_

_**Tópico modificado em:**2016-12-09_

Use o Centro de Administração do Exchange (EAC) ou o Shell de Gerenciamento do Exchange para criar um novo grupo de distribuição em sua organização do Exchange ou para habilitar um grupo existente para email no Active Directory.

Há dois tipos de grupos que podem ser usados para distribuir mensagens:

  - *Grupos de distribuição universal habilitados para email* (também chamados de *grupos de distribuição*) podem ser usados apenas para distribuir mensagens.

  - *Grupos de segurança universal habilitados para email* (também chamados de *grupos de segurança*) podem ser usados para distribuir mensagens e para conceder permissões de acesso para recursos no Active Directory. Para mais informações, consulte [Gerenciar grupos de segurança habilitados para email](manage-mail-enabled-security-groups-exchange-2013-help.md).

É importante observar as diferenças de terminologia entre o Active Directory e o Exchange. No Active Directory, um grupo de distribuição se refere a qualquer grupo que não tenha um contexto de segurança, seja ele habilitado para email ou não. Por outro lado, no Exchange, todos os grupos habilitados para email são chamados de grupos de distribuição, tenham ou não um contexto de segurança.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 a 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de distribuição" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Se sua organização configurou uma política de nome de grupo, ela será aplicada apenas a grupos criados por usuários. Quando você ou outros administradores usarem o EAC para criar grupos de distribuição, a política de nome de grupo será ignorada e não será aplicada ao nome do grupo. Contudo, se utilizar o Shell para criar ou renomear um grupo de distribuição, a política será aplicada, a menos que utilize o parâmetro *IgnoreNamingPolicy* para substituir a política de nome de grupo. Para mais informações, consulte:
    
      - [Criar um diretiva de nomeação de grupo de distribuição](create-a-distribution-group-naming-policy-exchange-2013-help.md)
    
      - [Substituir o diretiva de nomenclatura de grupo de distribuição](override-the-distribution-group-naming-policy-exchange-2013-help.md)

## O que você deseja fazer?

## Criar um grupo de distribuição

## Usar o EAC para criar um grupo de distribuição

1.  Na EAC, navegue até **Destinatários** \> **Grupos**.

2.  Clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") \> **Grupo de distribuição**.

3.  
    

    > [!TIP]
    > <IMG title="Novidade Experimentar Grupos do Office 365" alt="Novidade Experimentar Grupos do Office 365" src="images/Bb124513.3ea82c95-9dda-450f-823b-cd0772249d81(EXCHG.150).png"><BR>Agora é possível criar um grupo do Office 365 em vez de um grupo de distribuição se você tiver um plano do Office 365 para empresas ou um plano do Exchange Online. Os grupos do Office 365 têm os recursos de um grupo de distribuição e muito mais. Com os grupos do Office 365, você pode enviar emails para um grupo, compartilhar um calendário comum, ter uma biblioteca para armazenar e trabalhar em pastas e arquivos do grupo. Clique em <STRONG>Novo</STRONG><IMG title="Ícone Adicionar" alt="Ícone Adicionar" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif">&nbsp;&gt;&nbsp;<STRONG>Grupo do Office 365</STRONG> para começar e confira <A href="https://go.microsoft.com/fwlink/p/?linkid=800653">Grupos do Office 365 - ajuda da administração</A>.<BR>Se você tiver grupos de distribuição existentes que queira migrar para os grupos do Office 365, veja <A href="https://go.microsoft.com/fwlink/p/?linkid=824756">Migrar as listas de distribuição para grupos do Office 365 - ajuda da administração</A>.<BR>Se você ainda quiser criar um grupo de distribuição, clique ou toque no assistente <STRONG>Novo grupo de distribuição</STRONG>.



4.  
    
    Na página **Novo grupo de distribuição**, preencha os seguintes campos:
    
      - **\* Nome para exibição**   Use essa caixa para digitar o nome para exibição. Esse nome é exibido no catálogo de endereços da organização, na linha Para: quando um email é enviado a esse grupo e na lista Grupos do EAC. O nome para exibição é necessário e deve ser amigável para que as pessoas o reconheçam. Ele também deve ser exclusivo na floresta.
    
      - **\* Alias**   Use essa caixa para digitar o nome do alias do grupo. O alias não pode exceder 64 caracteres e deve ser único na floresta. Quando um usuário digita o alias na linha Para: de uma mensagem de email, ele é convertido para o nome para exibição do grupo.
    
      - **Unidade organizacional**   (Você verá essa opção no Exchange 2013 local) É possível selecionar uma UO (unidade organizacional) que não seja a padrão (que é o escopo do destinatário). Se o escopo do destinatário estiver definido para a floresta, o valor padrão será definido para o contêiner Usuários no domínio do Active Directory que contém o computador no qual o EAC está sendo executado. Se o escopo do destinatário estiver definido como um domínio específico, por padrão, o contêiner Usuários desse domínio será selecionado. Se o escopo do destinatário estiver definido como uma UO específica, essa UO será selecionada por padrão.
        
        Para selecionar uma UO diferente, clique em **Procurar**. A caixa de diálogo exibe todas as OUs da floresta que estão no escopo especificado. Selecione a UO desejada e clique em **OK**.
    
      - **\* Proprietários**   Por padrão, a pessoa que cria um grupo é o proprietário. Todos os grupos devem ter no mínimo um proprietário. Você pode adicionar proprietários, clicando em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").
    
      - **Membros**   Use esta seção para adicionar membros e para especificar se é necessário obter aprovação para que as pessoas ingressem ou saiam do grupo.
        
        Os proprietários do grupo não precisam ser membros do grupo. Use a opção **Adicionar proprietários do grupo como membros** para adicionar ou remover os proprietários como membros.
        
        Para adicionar membros ao grupo, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Ao terminar de adicionar membros, clique em **OK** para retornar à página **Novo grupo de distribuição**.
        
        Em **Definir se é necessário aprovação do proprietário para ingressar no grupo**, especifique se é necessário aprovação para que as pessoas ingressem no grupo. Selecione uma das seguintes configurações:
        
          - **Abrir: Qualquer pessoa pode participar desse grupo sem receber aprovação dos proprietários do grupo**   Essa é a configuração padrão.
        
          - **Fechado: Os membros só podem ser adicionados pelos proprietários do grupo. Todas as solicitações para ingressar serão rejeitadas automaticamente**
        
          - **Aprovação do proprietário: Todas as solicitações são aprovadas ou rejeitadas manualmente pelos proprietários do grupo**   Se você selecionar esta opção, o proprietário ou os proprietários do grupo receberão uma mensagem de email solicitando aprovação para ingressar no grupo.
        
        Em **Definir se o grupo está aberto a saídas**, especifique se é necessário aprovação para que as pessoas saiam do grupo. Selecione uma das seguintes configurações:
        
          - **Abrir: Qualquer pessoa pode sair do grupo sem receber aprovação dos proprietários do grupo   **Essa é a configuração padrão.
        
          - **Fechado: Os membros só podem ser removidos pelos proprietários do grupo. Todas as solicitações para sair do grupo serão rejeitadas automaticamente   **

5.  Ao terminar, clique em **Salvar** para criar o grupo de distribuição.


> [!TIP]
> Por padrão, os novos grupos de distribuição exigem que todos os remetentes sejam autenticados. Isso evita que remetentes externos enviem mensagens para grupos de distribuição. Para configurar um grupo de distribuição para aceitar mensagens de todos os remetentes, modifique as configurações de restrição de entrega de mensagens desse grupo de distribuição.



## Usar o Shell para criar um grupo de distribuição

Este exemplo cria um grupo de distribuição com o alias **itadmin** e o nome **Administradores de TI**. O grupo de distribuição é criado na UO padrão e qualquer pessoa pode ingressar no grupo sem aprovação dos seus proprietários.

    New-DistributionGroup -Name "IT Administrators" -Alias itadmin -MemberJoinRestriction open

Para obter mais informações sobre como usar o Shell para criar grupos de distribuição, consulte [New-DistributionGroup](https://technet.microsoft.com/pt-br/library/aa998856\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com sucesso um grupo de distribuição, siga uma destas opções:

  - Na EAC, navegue até **Destinatários** \> **Grupos**. O novo grupo de distribuição é exibido na lista de grupos. Em **Tipo de grupo**, o tipo é **Grupo de distribuição**.

  - No Shell, execute o comando abaixo para exibir informações sobre o novo grupo de distribuição.
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress


> [!TIP]
> Você pode criar ou habilitar para email somente grupos de distribuição universais. Para converter um grupo global ou de domínio local em um grupo universal, você pode usar o cmdlet <A href="https://technet.microsoft.com/pt-br/library/bb123770(v=exchg.150)">Set-Group</A> no Shell. Você pode ter grupos habilitados para email que tenham sido migrados de versões anteriores do Exchange&nbsp;e que não são grupos universais. Você pode usar o EAC ou o Shell para gerenciar esses grupos



## Alterar as propriedades do grupo de distribuição

## Usar o EAC para alterar propriedades do grupo de distribuição

1.  Na EAC, navegue até **Destinatários** \> **Grupos**.

2.  Na lista de grupos, clique no grupo de distribuição que deseja exibir ou alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do grupo, clique em uma destas seções, para exibir ou alterar propriedades.
    
      - Geral
    
      - Propriedade
    
      - Associação
    
      - Aprovação de associação
    
      - Gerenciamento de entregas
    
      - Aprovação de mensagem
    
      - Opções de email
    
      - Dica de Email
    
      - Delegação de grupo

## Geral

Use essa seção para visualizar ou alterar informações básicas sobre o grupo.

  - **\* Nome para exibição**   Este nome será exibido no catálogo de endereços, na linha Para: quando um email é enviado a esse grupo e na lista Grupos. O nome para exibição é necessário e deve ser amigável para que as pessoas o reconheçam. Ele também deve ser exclusivo em seu domínio.
    
    Se você implementou uma política de nomeação de grupo, o nome para exibição terá que estar em conformidade com o formato de nomeação definido pela política.

  - **\* Alias**   É a parte do endereço de email que aparece à esquerda do símbolo de arroba (@). Se você alterar o alias, o endereço SMTP principal do grupo também será alterado e conterá o novo alias. Além disso, o endereço de email com o alias anterior será mantido como um endereço proxy para o grupo.

  - **Descrição**   Use essa caixa para descrever o grupo, para que as pessoas saibam qual é o objetivo do grupo. Essa descrição é exibida no catálogo de endereços e no painel Detalhes do EAC.

  - **Ocultar este grupo das listas de endereços**   Marque essa caixa de seleção se não desejar que usuários vejam esse grupo no catálogo de endereços. Para enviar um email a esse grupo, um remetente deve digitar o endereço de email ou alias do grupo na linha Para: ou Cc:, .
    

    > [!TIP]
    > Considere ocultar grupos de segurança porque eles são tipicamente usados para atribuir permissões a membros do grupo e não para enviar emails.



  - **Unidade organizacional**   Esta caixa somente leitura exibe a unidade organizacional (UO) que contém o grupo de distribuição. Você precisa usar Usuários e Computadores do Active Directory para mover o grupo para uma UO diferente.

## Propriedade

Use esta seção para atribuir proprietários do grupo. O proprietário do grupo pode adicionar membros ao grupo, aprovar ou rejeitar solicitações de ingresso ou saída do grupo, bem como aprovar ou rejeitar mensagens enviadas para o grupo. Por padrão, a pessoa que cria um grupo é o proprietário. Todos os grupos devem ter no mínimo um proprietário.

Você pode adicionar proprietários, clicando em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). É possível remover um proprietário, selecionando-o e clicando em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

## Associação

Use esta seção para adicionar ou remover membros. Os proprietários do grupo não precisam ser membros do grupo. Em **Membros**, você pode adicionar membros, clicando em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Você pode remover um membro, selecionando um usuário na lista de membros e clicando em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

## Aprovação de associação

Use esta seção para especificar se é necessário obter aprovação para os usuários ingressarem ou saírem do grupo.

  - **Defina se a aprovação do proprietário é necessária para ingressar no grupo**   Selecione uma das seguintes configurações:
    
      - **Abrir: Qualquer um pode ingressar nesse grupo sem aprovação dos proprietários do grupo**
    
      - **Fechado: Os membros só podem ser adicionados pelos proprietários do grupo. Todas as solicitações para ingressar serão rejeitadas automaticamente**
    
      - **Aprovação do proprietário: Todas as solicitações são aprovadas ou rejeitadas pelos proprietários do grupo**   Se você selecionar esta opção, o proprietário ou os proprietários do grupo receberão uma mensagem de email solicitando aprovação para ingressar no grupo.

  - **Escolha se o grupo está aberto para saída   **Selecione uma das seguintes configurações:
    
      - **Abrir: Qualquer um pode sair do grupo sem a aprovação dos proprietários do grupo   **
    
      - **Fechado: Os membros só podem ser removidos pelos proprietários do grupo. Todas as solicitações para sair do grupo serão rejeitadas automaticamente   **

## Gerenciamento de entregas

Use essa seção para gerenciar quem pode enviar emails a esse grupo.

  - **Apenas os remetentes da minha organização**   Selecione esta opção para permitir que apenas os remetentes da sua organização enviem mensagens ao grupo. Isso significa que, se alguém fora da sua organização enviar uma mensagem de email a esse grupo, ela será rejeitada. Essa é a configuração padrão.

  - **Remetentes de dentro e de fora da minha organização**   Selecione esta opção para permitir que qualquer pessoa envie mensagens ao grupo.
    
    É possível limitar ainda mais as pessoas que podem enviar mensagens ao grupo permitindo que apenas remetentes específicos enviem mensagens a esse grupo. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e selecione um ou mais destinatários. Se você adicionar remetentes a essa lista, eles serão os únicos que poderão enviar email ao grupo. Os emails enviados por qualquer pessoa que não estiver na lista serão rejeitados.
    
    Para remover uma pessoa ou grupo da lista, selecione-o na lista e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").
    

    > [!IMPORTANT]
    > Se você configurou o grupo para permitir que apenas os remetentes da sua organização enviem mensagens ao grupo, os emails enviados por um contato de email serão rejeitados, mesmo que ele seja adicionado a essa lista.



## Aprovação de mensagem

Use esta seção para configurar opções para moderar o grupo. Os moderadores aprovam ou rejeitam as mensagens enviadas ao grupo antes que elas cheguem aos membros do grupo.

  - **As mensagens enviadas a esse grupo devem ser aprovadas por um moderador**   Por padrão, essa caixa de seleção não está marcada. Se você marcar esta caixa de seleção, as mensagens de entrada serão verificadas pelos moderadores do grupo antes da entrega. Os moderadores do grupo podem aprovar ou rejeitar as mensagens de entrada.

  - **Moderadores do grupo**   Para adicionar moderadores do grupo, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para remover um moderador, selecione-o e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover"). Se você selecionou "As mensagens enviadas a este grupo devem ser aprovadas por um moderador" e não selecionou um moderador, as mensagens para o grupo serão enviadas aos proprietários do grupo para aprovação.

  - **Remetentes que não exigem aprovação de mensagem**    Para adicionar pessoas ou grupos que podem ignorar a moderação para o grupo em questão, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para remover uma pessoa ou um grupo, selecione o item e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

  - **Selecionar notificações de moderação   **Use esta seção para definir como os usuários serão notificados sobre a aprovação de mensagens.
    
      - **Notificar todos os remetentes quando suas mensagens não forem aprovadas**   Esta é a configuração padrão. Notifique todos os remetentes dentro e fora da sua organização quando as mensagens deles não forem aprovadas.
    
      - • **Notificar remetentes da organização apenas quando as mensagens não forem aprovadas**   Se esta opção for selecionada, somente pessoas ou grupos da sua organização serão notificados quando uma mensagem enviada por eles ao grupo não for aprovada por um moderador.
    
      - **Não notificar ninguém quando uma mensagem não for aprovada**   Quando você seleciona esta opção, nenhuma notificação é enviada para os remetentes cujas mensagens não são aprovadas pelos moderadores do grupo.

## Opções de email

Use essa seção para visualizar ou alterar os endereços de email associados ao grupo. Isso inclui endereços SMTP principais do grupo e todos os endereços de proxy associados. O endereço SMTP principal (também conhecido como *endereço de resposta*) será exibido em negrito, na lista de endereços, com o valor em maiúsculas **SMTP** na coluna **Tipo**.

  - **Adicionar **  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar um novo endereço de email para essa caixa de correio. Selecione um dos seguintes tipos de endereço:
    
      - **SMTP**   Esse é o tipo de endereço padrão. Clique nesse botão e digite o novo endereço SMTP na caixa **\* Endereço de email**.
        

        > [!TIP]
        > Para tornar o novo endereço como endereço SMTP principal para o grupo, marque a caixa de seleção <STRONG>Tornar este o endereço de resposta</STRONG>.

    
      - **Tipo de endereço personalizado**   Clique nesse botão e digite um dos tipos de endereço de email não SMTP compatíveis na caixa **\* Endereço de email**.
        

        > [!TIP]
        > Com a exceção de endereços X.400, o Exchange não valida endereços personalizados para a formatação adequada. Certifique-se de que o endereço personalizado que você especificar esteja de acordo com os requisitos de formato para esse tipo de endereço.



  - **Editar**   Para alterar um endereço de email associado ao grupo, selecione-o na lista e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    

    > [!TIP]
    > Para tornar um endereço existente o endereço SMTP principal para o grupo, marque a caixa de seleção <STRONG>Tornar este o endereço de resposta</STRONG>.



  - **Remover**   Para excluir um endereço de email associado ao grupo, selecione-o na lista e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

  - **Atualizar automaticamente os endereços de email com base na política de endereços de email aplicados a este destinatário**   Marque essa caixa de seleção para que os endereços de email do destinatário sejam atualizados automaticamente com base nas alterações feitas nas políticas de endereços de email em sua organização. Essa caixa de seleção é marcada por padrão.

## Dica de Email

Use esta seção para adicionar uma Dica de Email a fim de alertar os usuários sobre possíveis problemas antes de eles enviarem uma mensagem a esse grupo. Uma Dica de Email é o texto exibido na barra de informações quando esse grupo é adicionado às linhas Para, Cc ou Cco de uma nova mensagem de email. Por exemplo, você poderia acrescentar uma dica de email a grupos grandes para advertir remetentes potenciais que a sua mensagem será enviada a muitas pessoas.


> [!TIP]
> As Dicas de Email podem incluir marcas HTML, mas scripts não são permitidos. O comprimento de uma dica de email personalizada não pode exceder 175 caracteres exibidos. As marcas HTML não são contadas no limite.



## Delegação de grupo

Use essa seção para atribuir permissões a um usuário (chamado de *delegar*) para permitir que eles enviem mensagens como o grupo ou enviar mensagens em nome do grupo. É possível atribuir as seguintes permissões:

  - **Enviar como**   Essa permissão permite que o representante envie mensagens como o grupo. Depois que essa permissão for atribuída, o representante tem a opção de adicionar o grupo na linha **De** para indicar que a mensagem foi enviada pelo grupo.

  - **Enviar em Nome de**   Essa permissão também permite que um representante envie mensagens em nome do grupo. Depois que essa permissão for atribuída, o representante tem a opção de adicionar o grupo na linha **De**. Parecerá que a mensagem foi enviada pelo grupo e será indicado que ela foi enviada pelo representante em nome do grupo.

Para atribuir permissões a representantes, clique em **Adicionar** na permissão apropriada para exibir a página **Selecionar Destinatário**, que exibe uma lista de todos os destinatários na sua organização do Exchange que podem receber a permissão. Selecione os destinatários que deseja, adicione-os à lista e clique em **OK**. Você também pode pesquisar um destinatário específico, digitando seu nome na caixa de pesquisa e clicando em **Pesquisar**.

## Usar o Shell para alterar propriedades do grupo de distribuição

Use os cmdlets **Get-DistributionGroup** e **Set-DistributionGroup** para exibir e alterar propriedades dos grupos de distribuição. As vantagens de se usar o Shell são a possibilidade de alterar as propriedades que não estão disponíveis no EAC e alterar as propriedades de vários grupos. Para obter informações sobre que parâmetros correspondem às propriedades dos grupos de distribuição, consulte estes tópicos:

  - [Get-DistributionGroup](https://technet.microsoft.com/pt-br/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/pt-br/library/bb124955\(v=exchg.150\))

Veja a seguir alguns exemplos de como usar o Shell para alterar propriedades dos grupos de distribuição.

Este exemplo altera o endereço SMTP principal (também chamado de endereço de resposta) do grupo de distribuição Funcionários de Seattle, de employees@contoso.com para sea.employees@contoso.com. Da mesma forma, o endereço de resposta anterior será mantido como um endereço de proxy.

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.employees@contoso.com,smtp:employees@contoso.com

Este exemplo limita o tamanho máximo de mensagens que podem ser enviadas a todos os grupos de distribuição na organização em 10 megabytes (MB).

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalDistributionGroup')} | Set-DistributionGroup -MaxReceiveSize 10MB

Este exemplo habilita a moderação para o grupo de distribuição Atendimento ao Cliente e define o moderador como Amy. Além disso, esse grupo de distribuição moderado notificará os remetentes que enviarem emails de dentro da organização, caso suas mensagens não sejam aprovadas.

    Set-DistributionGroup -Identity "Customer Support" -ModeratedBy "Amy" -ModerationEnabled $true -SendModerationNotifications 'Internal'

Este exemplo altera o grupo de distribuição criado pelo usuário Fãs de Cachorros para exigir que o gerente do grupo aprove as solicitações dos usuários para ingressar nele. Além disso, com o uso do parâmetro *BypassSecurityGroupManagerCheck*, o gerente do grupo será avisado que uma alteração foi feita às configurações do grupo de distribuição.

    Set-DistributionGroup -Identity "Dog Lovers" -MemberJoinRestriction 'ApprovalRequired' -BypassSecurityGroupManagerCheck

## Como saber se funcionou?

Para verificar se as propriedades do grupo de distribuição foram alteradas com sucesso, faça o seguinte:

  - No EAC, selecione o grupo e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir a propriedade ou recurso que você alterou. Dependendo da propriedade que você tiver alterado, ela poderá ser exibida no painel Detalhes do grupo selecionado.

  - No Shell, use o cmdlet **Get-DistributionGroup** para verificar as alterações. Uma vantagem de se usar o Shell é que você pode exibir várias propriedades de vários grupos. No exemplo acima, em que o limite do destinatário foi alterado, execute o comando abaixo para verificar o novo valor.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    Para o exemplo acima onde os limites da mensagem foram alterados, execute este comando.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

