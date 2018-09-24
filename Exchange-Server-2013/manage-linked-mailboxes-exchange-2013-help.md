---
title: 'Gerenciar caixas de correio vinculadas: Exchange 2013 Help'
TOCTitle: Gerenciar caixas de correio vinculadas
ms:assetid: 76e12d4a-1c3a-42e2-b64c-c09d36e81bd3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673532(v=EXCHG.150)
ms:contentKeyID: 50485835
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar caixas de correio vinculadas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-27_

Caixas de correio vinculadas são caixas de correio que são acessadas por usuários em uma floresta confiável separada. Caixas de correio vinculadas podem ser necessárias para organizações que implantam Exchange em uma floresta de recursos. O cenário de floresta de recurso permite que uma organização centralizar Exchange em uma única floresta, permitindo o acesso à organização Exchange com contas de usuário que estão localizados em um ou mais florestas confiáveis (chamadas de *florestas de conta*). A conta de usuário que acessa a caixa de correio vinculada não existe na floresta onde o Exchange está implantado. Portanto, uma conta de usuário desabilitadas que existe na mesma floresta que Exchange é criada e associada a caixa de correio vinculada correspondente.

A figura a seguir ilustra a relação entre a conta de usuário vinculado usado para acessar a caixa de correio vinculada (localizada na floresta de conta) e a conta de usuário desabilitado na floresta de recursos Exchange associado a caixa de correio vinculada.

**Caixas de correio vinculadas**

![Organização complexa do Exchange com floresta de recursos](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organização complexa do Exchange com floresta de recursos")


> [!NOTE]
> Uma relação de confiança entre a floresta do Exchange e a floresta de pelo menos uma conta deve ser configurada antes de criar caixas de correio vinculadas. No mínimo, você deve configurar uma relação de confiança unidirecional de saída para que a floresta de conta de confiança de floresta do Exchange. Para obter mais informações, consulte <A href="https://technet.microsoft.com/pt-br/library/jj156983(v=exchg.150)">Saiba mais sobre como configurar uma relação de confiança de floresta para dar suporte a caixas de correio vinculadas</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 a 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Uma conta de usuário (chamada a *conta principal vinculada*) deve existir na floresta conta antes de criar uma caixa de correio vinculada. Isso ocorre porque a caixa de correio vinculada é associada a um usuário na floresta de conta.

  - Se você configurou uma relação de confiança de saída unidirecional onde a floresta de conta de confiança de floresta do Exchange, você precisará de credenciais de administrador na floresta de conta para criar uma caixa de correio vinculada.
    
    Para criar uma caixa de correio vinculada sem receber solicitações de credenciais de administrador na floresta de conta, você precisa criar uma relação de confiança bidirecional ou criar outra confiança unidirecional de saída onde a floresta de conta também relações de confiança da floresta do Exchange. Essa etapa também requer credenciais de administrador na floresta de conta.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Criar uma caixa de correio vinculada

## Usar o EAC para criar uma caixa de correio vinculada

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Clique em **novo** \> **caixa de correio vinculada**.

3.  Na página **nova caixa de correio vinculada**, na caixa **confiáveis floresta ou domínio**, selecione o nome da conta floresta que contém a conta de usuário que você está criando a caixa de correio vinculada. Clique em **Avançar**.

4.  Se sua organização tiver configurado uma relação de confiança de saída unidirecional onde a floresta de conta de confiança de floresta do Exchange, você será solicitado para credenciais de administrador na floresta de conta para que você possa ter acesso a um controlador de domínio na floresta confiável. Digite o nome de usuário e senha para uma conta de administrador na floresta de conta e clique em **Avançar**.
    

    > [!NOTE]
    > Você não será avisado para credenciais de administrador se você criou uma relação de confiança bidirecional ou criou outra confiança de saída unidirecional, onde a floresta de conta de confiança de floresta do Exchange.



5.  Preencha os seguintes campos na página **Selecionar conta principal vinculada**.
    
      - **Controlador de domínio vinculado**    Selecione um controlador de domínio na floresta de conta. Exchange se conectará com este controlador de domínio para recuperar a lista de contas de usuário na floresta de conta para que você pode selecionar a conta principal vinculada.
    
      - **Conta de mestre vinculado**    Clique em **Procurar**, selecione uma conta de usuário na floresta de conta e clique em **OK**. A nova caixa de correio vinculada será associada essa conta.

6.  Clique em **Avançar** e conclua as seguintes caixas na página **Insira informações gerais**.
    
      - **\* Nome**    Use esta caixa para digitar um nome para o usuário. Este é o nome usado como o nome de exibição no EAC e o catálogo de endereços da sua organização e o nome que está listado na Active Directory. Esse nome é necessário.
    
      - **Unidade organizacional**   É possível selecionar uma OU (unidade organizacional) que não seja a padrão (que é o escopo do destinatário). Se o escopo do destinatário estiver definido para a floresta, o valor padrão será definido para o contêiner Usuários no domínio do Active Directory que contém o computador no qual o EAC está sendo executado. Se o escopo do destinatário estiver definido como um domínio específico, por padrão, o contêiner Usuários desse domínio será selecionado. Se o escopo do destinatário estiver definido como uma unidade organizacional específica, essa unidade será selecionada por padrão.
        
        Para selecionar uma UO diferente, clique em **Procurar**. A caixa de diálogo exibe todas as OUs na floresta do Exchange que estão dentro do escopo especificado. Selecione a UO desejado e clique em **OK**.
    
      - **\* Nome de logon do usuário**    Use esta caixa para digitar o nome de logon do usuário, que é necessário para criar uma caixa de correio vinculada. Digite o nome de usuário. Esse nome será usado na parte esquerda do endereço de email para a caixa de correio vinculada se você não especificar um alias.
        

        > [!NOTE]
        > Como a conta de usuário que é criada na floresta do Exchange está desabilitada quando você cria uma caixa de correio vinculada, o usuário não usa o nome de logon do usuário para entrar na caixa de correio vinculada. Entrarem usando suas credenciais da floresta de conta.



7.  Clique em **mais opções** para configurar as seguintes caixas. Caso contrário, pule para a etapa 8 para salvar a nova caixa de correio vinculada.
    
      - **Alias**    Digite o alias, que especifica o alias de email para a caixa de correio vinculada. O alias do usuário é a parte do endereço de email no lado esquerdo do em (@) símbolo. Ele deve ser exclusivo na floresta.
        

        > [!NOTE]
        > Se você deixar essa caixa em branco, o valor da parte do nome de usuário do <STRONG>Nome de Logon do usuário</STRONG> é usado para o alias de email.

    
      - **Nome**, **Iniciais**, **Sobrenome**
    
      - **Banco de dados de caixa de correio**    Use esta opção para especificar um banco de dados de caixa de correio em vez de permitir o Exchange escolher um banco de dados para você. Clique em **Procurar** para abrir a caixa de diálogo **Selecionar banco de dados de caixa de correio**. Esta caixa de diálogo lista todos os bancos de dados da caixa de correio em sua organização do Exchange. Por padrão, os bancos de dados de caixa de correio são classificados por nome. Você também pode clicar no título da coluna para classificar os bancos de dados por nome de servidor ou a versão correspondente. Selecione o banco de dados de caixa de correio que você deseja usar e clique em **OK**.
    
      - **Política de catálogo de endereços**    Use esta opção para especificar uma política de catálogo de endereços (ABP) para a caixa de correio vinculada. ABPs contém uma lista de endereços global (GAL), um catálogo de endereços offline (OAB), uma lista de salas e um conjunto de listas de endereços. Quando atribuídas aos usuários, uma ABP fornece-los com o access para um GAL personalizado no Outlook e Outlook Web App. Para saber mais, consulte [Políticas de catálogo de endereços](https://docs.microsoft.com/pt-br/exchange/address-books/address-book-policies/address-book-policies).
        
        Na lista suspense, selecione a política que você deseja associar a esta caixa de correio.

8.  Quando terminar, clique em **Salvar** para criar a nova caixa de correio vinculada.

## Use o Shell para criar uma caixa de correio vinculada

Este exemplo cria uma caixa de correio vinculada de Ayla Kol na floresta de recursos do Exchange da CONTOSO. Domínio FABRIKAM é na floresta de conta. O administrador conta FABRIKAM \\administrator é usado para acessar o controlador de domínio vinculado.

    New-Mailbox -Name "Ayla Kol" -LinkedDomainController "DC1_FABRIKAM" -LinkedMasterAccount " FABRIKAM\aylak" -OrganizationalUnit Users -UserPrincipalName aylak@contoso.com -LinkedCredential:(Get-Credential FABRIKAM\administrator)

Para obter informações sobre sintaxes e parâmetros, consulte [New-Mailbox](https://technet.microsoft.com/pt-br/library/aa997663\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito uma caixa de correio vinculada, siga um destes procedimentos:

  - No EAC, navegue até **destinatários** \> **caixas de correio**. A nova caixa de correio vinculada é exibida na lista de caixa de correio. Em **Tipo de caixa de correio**, o tipo é **vinculado**.

  - No Shell, execute o seguinte comando para exibir informações sobre a nova caixa de correio vinculada.
    
    ```powershell
Get-Mailbox <Name> | FL Name,RecipientTypeDetails,IsLinked,LinkedMasterAccount
```

## Alterar propriedades de caixa de correio vinculada

Depois de criar uma caixa de correio vinculada, você pode fazer alterações e definir propriedades adicionais usando o Centro de administração do Exchange (EAC) ou o Shell de gerenciamento do Exchange.

Você também pode alterar propriedades para várias caixas de correio vinculadas ao mesmo tempo. Para obter mais informações, consulte a seção, a seção "Em massa editar caixas de correio do usuário" no tópico [Gerenciar caixas de correio do usuário](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes) .


> [!IMPORTANT]
> O tempo estimado para conclusão dessa tarefa irá variar com base no número de propriedades que você deseja exibir ou alterar.



## Usar o EAC para alterar propriedades de caixa de correio vinculada

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na lista de caixas de correio, clique a caixa de correio vinculada que você deseja alterar as propriedades e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades da caixa de correio, clique em uma destas seções, para exibir ou alterar propriedades.
    
      - General
    
      - Mailbox Usage
    
      - Email Address
    
      - Mailbox Features
    
      - Member Of
    
      - MailTip
    
      - Mailbox Delegation

## Geral

Use a seção **Geral** para ver ou alterar as informações básicas sobre o usuário.

  - **\* Nome de caixa de correio vinculada**    Este é o nome que está listado na Active Directory. Se você alterar esse nome, ele não pode exceder 64 caracteres.

  - **\* Nome para exibição**    Esse nome aparecerá no catálogo de endereços da sua organização, em para: e: linhas em email e na lista de caixas de correio no EAC. Esse nome não pode conter espaços vazios antes ou após o nome para exibição.

  - **\* Nome de logon do usuário**    Para caixas de correio do usuário, este é o nome que o usuário usa para entrar para suas caixas de correio e fazer logon no domínio. Para caixas de correio vinculadas, a conta de usuário correspondente é criada na floresta do Exchange quando a caixa de correio vinculada foi criada está desabilitada. O usuário usa suas credenciais da floresta de conta para entrar na caixa de correio vinculada.
    
    Se você alterar esse nome, ele deve ser exclusivo na sua organização.

  - **Conta de mestre vinculado**    Esta caixa somente leitura exibe o usuário (no formato domínio \\ nome\_de\_usuário formato) da floresta de conta que está associada com a caixa de correio vinculada. Para alterar a conta principal vinculada associada a caixa de correio vinculada, você precisará usar o cmdlet **Set-Mailbox** no Shell. Se você alterar a conta principal vinculada, o usuário precisará usar as credenciais para a nova conta principal vinculada para entrar na caixa de correio vinculada. Para a sintaxe de comando alterar a conta principal vinculada, consulte Use o Shell para alterar propriedades de caixa de correio vinculada.

  - **Ocultar das listas de endereços**    Marque esta caixa de seleção para impedir que a caixa de correio vinculada que aparecem no catálogo de endereços e outras listas de endereços que são definidas na sua organização do Exchange. Após você marcar essa caixa de seleção, os usuários podem ainda enviar mensagens para esse usuário usando o endereço de email.

Clique em **Mais opções**, para exibir ou alterar essas propriedades adicionais:

  - **Unidade organizacional**  Essa caixa somente leitura exibe a unidade organizacional (OU) que contém a conta do usuário. Você pode usar Usuários e Computadores do Active Directory para mover a conta de usuário para uma OU diferente.

  - **Banco de dados de caixa de correio**    Esta caixa somente leitura exibe o nome do banco de dados da caixa de correio que hospeda a caixa de correio. Para mover a caixa de correio para outro banco de dados, selecione-o na lista caixa de correio e clique em **mover a caixa de correio para outro banco de dados** no painel de detalhes.

  - **\* Alias** Especifica o alias de email para a caixa de correio vinculada. O alias é a parte do endereço de email no lado esquerdo do em (@) símbolo. Ele deve ser exclusivo na floresta.

  - **Nome**, **Iniciais**, **Sobrenome**

  - **Atributos personalizados**    Esta seção exibe os atributos personalizados definidos para a caixa de correio vinculada. Para especificar os valores de atributo personalizado, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Você pode especificar até 15 atributos personalizados para o destinatário.

## Utilização da Caixa de Correio

Use a seção de **Uso de caixa de correio** para exibir ou alterar a cota de armazenamento de caixa de correio e as configurações de retenção de itens excluídos para a caixa de correio vinculada. Essas configurações são definidas por padrão, quando a caixa de correio vinculada é criada. Eles usam os valores que estão configurados para o banco de dados de caixa de correio e aplicar a todas as caixas de correio no banco de dados. Você pode personalizar essas configurações para cada caixa de correio em vez de usar os padrões de banco de dados de caixa de correio.

  - **Último logon**    Esta caixa somente leitura exibe a última vez em que o usuário conectado à caixa de correio.

  - **Utilização de caixa de correio**   Essa área mostra o tamanho total da caixa de correio e a porcentagem da cota total de caixa de correio que foi usada.


> [!NOTE]
> Para obter as informações que são exibidas nas duas caixas anteriores, a EAT consulta o banco de dados de caixa de correio que hospeda a caixa de correio. Se o EAC não pode se comunicar com o repositório do Exchange que contém o banco de dados de caixa de correio, essas caixas ficará em branco. Uma mensagem de aviso será exibida se o usuário não tiver entrado à caixa de correio pela primeira vez.



Clique em **More options**, para ver ou alterar a cota de armazenamento da caixa de correio e as configurações de retenção de itens excluídos para a caixa de correio.

  - **Configurações de cota de armazenamento**   Para personalizar essas configurações da caixa de correio e não usar os padrões de banco de dados de caixa de correio, clique em **Personalizar configurações para esta caixa de correio**, digite um novo valor e clique em **Salvar**.
    
    O intervalo de valores para qualquer configuração de cota de armazenamento vai de 0 a 2074 gigabytes (GB).
    
      - **Emitir aviso em (GB)**   Essa caixa mostra o limite máximo de armazenamento antes de um aviso ser emitido para o usuário. Se o tamanho da caixa de correio atingir ou exceder o valor especificado, o Exchange enviará uma mensagem de aviso para o usuário.
    
      - **Proibir envio em (GB)**   Essa caixa mostra o limite para *proibir envio* para a caixa de correio. Se o tamanho da caixa de correio atingir ou exceder o limite especificado, o Exchange impedirá que o usuário da caixa de correio envie novas mensagens e exibirá uma mensagem de erro descritiva.
    
      - **Proibir envio e recebimento em (GB)**   Essa caixa mostra o limite para *proibir envio e recebimento* para a caixa de correio. Se o tamanho da caixa de correio atingir ou exceder o limite especificado, o Exchange impedirá que o usuário da caixa de correio envie novas mensagens e não entregará nenhuma mensagem nova para a caixa de correio. Todas as mensagens enviadas para a caixa de correio são devolvidas ao remetente com uma mensagem de erro descritiva.

  - **Configurações de retenção de item excluído**   Para personalizar essas configurações da caixa de correio e não usar os padrões de banco de dados de caixa de correio, clique em **Personalizar configurações para esta caixa de correio**, digite um novo valor e clique em **Salvar**.
    
      - **Manter os itens excluídos por (dias)**    Esta caixa exibe a quantidade de tempo que os itens excluídos são mantidos antes de serem excluídos permanentemente e não podem ser recuperados pelo usuário. Quando a caixa de correio é criada, esse período de tempo baseia-se as configurações de retenção de item excluído definidas para o banco de dados de caixa de correio. Por padrão, um banco de dados de caixa de correio está configurado para reter itens excluídos 14 dias. O intervalo de valores para essa propriedade é de 0 a 24855 dias.
    
      - **Não excluir itens permanentemente até que seja feito backup do banco de dados**   Marque essa caixa de seleção para impedir que caixas de correio e emails sejam excluídos permanentemente até que seja feito backup do banco de dados de caixa de correio em que a caixa de correio está.

## Endereço de Email

Use a seção de **endereço de Email** para exibir ou alterar os endereços de email associados a caixa de correio vinculada. Isso inclui os endereços de SMTP primários do usuário e todos os endereços proxy associado. O endereço SMTP principal (também conhecido como o *endereço de resposta padrão*) é exibido em negrito na lista de endereços, com o valor de **SMTP** maiúsculas na coluna **tipo**.

  - **Adicionar**  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar um novo endereço de email para essa caixa de correio. Selecione um dos seguintes tipos de endereço:
    
      - **SMTP**    Este é o tipo de endereço padrão. Clique neste botão de opção e digite o novo endereço de SMTP no **\* endereço de Email** caixa.
    
      - **EUM**    Um endereço EUM (Exchange Unified Messaging) é usado pelo serviço de Unificação de mensagens do Microsoft Exchange para localizar usuários habilitados para UM dentro de uma organização do Exchange. Endereços EUM consistem no número de ramal e o discagem de UM plano para o usuário habilitado para UM. Clique neste botão de opção e digite o número do ramal na caixa **Extensão do endereço**. Em seguida, clique em **Procurar** e selecione um plano de discagem do usuário.
    
      - **Tipo de endereço personalizado**   Clique nesse botão e digite um dos tipos de endereço de email não SMTP compatíveis na caixa **\* Endereço de email**.
        

        > [!NOTE]
        > Com a exceção de endereços X.400, o Exchange não valida endereços personalizados para a formatação adequada. Certifique-se de que o endereço personalizado que você especificar esteja de acordo com os requisitos de formato para esse tipo de endereço.



  - **Atualizar automaticamente os endereços de email com base na diretiva de endereço de email aplicada para o destinatário** Marque esta caixa de seleção se quiser que os endereços de email do destinatário para serem atualizadas automaticamente quando são feitas alterações para políticas de endereço em sua organização de email. Essa caixa é selecionada por padrão.

## Recursos da Caixa de Correio

Use a seção **Recursos da Caixa de Correio** para exibir ou modificar os recursos e configurações de caixa de correio a seguir:

  - **Política de compartilhamento**   Esta caixa mostra a política de compartilhamento aplicada à caixa de correio. Uma política de compartilhamento permite controlar como usuários da sua organização podem compartilhar informações de contato e calendário com usuários de fora da organização do Exchange. A Política de Compartilhamento Padrão é atribuída a caixas de correio quando elas são criadas. Para alterar a política de compartilhamento atribuída ao usuário, selecione uma diferente, na lista suspensa.

  - **Diretiva de atribuição de função**    Esta caixa mostra a diretiva de atribuição de função atribuída à caixa de correio. A política de atribuição de função especifica as funções RBAC (controle) de acesso baseado em função que são atribuídas ao usuário e os controles que podem modificar a caixa de correio e usuários de definições de configuração de grupo de distribuição. Para alterar a política de atribuição de função é atribuída ao usuário, selecione um diferente da lista suspensa.

  - **Política de retenção**    Esta caixa mostra a política de retenção atribuída à caixa de correio. Uma política de retenção é um grupo de marcas de retenção são aplicadas à caixa de correio do usuário. As marcas permitem que você controle quanto tempo manter itens em caixas de correio dos usuários e definir qual ação a ser executada em itens que alcançaram uma determinada idade. Uma política de retenção não for atribuída às caixas de correio quando forem criados. Para atribuir uma política de retenção para o usuário, selecione uma opção na lista suspensa.

  - **Política de catálogo de endereços**    Esta caixa mostra a política de catálogo de endereços aplicada à caixa de correio. Uma política de catálogo de endereços permite aos usuários do segmento em grupos específicos para fornecer exibições personalizadas do catálogo de endereços. Para aplicar ou alterar a política de catálogo de endereços que é aplicada à caixa de correio, selecione uma opção na lista suspensa.

  - **Unificação de mensagens**    Esse recurso é desabilitado por padrão. Quando você habilita o Unified Messaging (UM) o usuário será capaz de usar os recursos de Unificação de mensagens da sua organização e um conjunto padrão das propriedades de Unificação de mensagens são aplicadas ao usuário. Clique em **Habilitar** para habilitar a Unificação de mensagens da caixa de correio. Para obter informações sobre como habilitar a Unificação de mensagens, consulte [Habilitar um usuário para caixa postal](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).
    

    > [!NOTE]
    > Um plano de discagem de UM e uma política de UM devem existir, antes de você poder habilitar a UM.



  - **Dispositivos Móveis**   Use essa seção para exibir e alterar as configurações do Exchange ActiveSync, que fica habilitado por padrão. O Exchange ActiveSync permite acesso a uma caixa de correio do Exchange a partir de um dispositivo móvel. Clique em **Desabilitar Exchange ActiveSync**, para desabilitar esse recurso para a caixa de correio.

  - **Outlook Web App**    Esse recurso é habilitado por padrão. Outlook Web App oferece acesso a uma caixa de correio do Exchange por meio de um navegador da web. Clique em **Desativar** para desativar o Outlook Web App para a caixa de correio. Clique em **Editar detalhes** para adicionar ou alterar uma política de caixa de correio do Outlook Web App da caixa de correio.

  - **IMAP**   Esse recurso é habilitado por padrão. Clique em **Desabilitar** para desabilitar o IMAP para a caixa de correio.

  - **POP3**   Esse recurso é habilitado por padrão. Clique em **Desabilitar** para desabilitar o POP3 para a caixa de correio.

  - **MAPI**   Esse recurso é habilitado por padrão. O MAPI permite o acesso a uma caixa de correio do Exchange de um cliente MAPI, como Outlook. Clique em **Desabilitar** para desabilitar o MAPI para a caixa de correio.

  - **Retenção de litígio**    Esse recurso é desabilitado por padrão. Litígio preserva as alterações de registros e itens de caixa de correio excluída feitas aos itens de caixa de correio. Itens excluídos e todas as instâncias de itens alterados são retornadas em uma pesquisa de descoberta. Clique em **Habilitar** para colocar a caixa de correio em suspensão de litígio. Se a caixa de correio em suspensão de litígio, clique em **Desabilitar** para remover a retenção de litígio. Se a caixa de correio em suspensão de litígio, clique em **Editar detalhes** para exibir e alterar as seguintes configurações de retenção de litígio:
    
      - **Data de retenção**    Esta caixa somente leitura indica a data e hora de quando a caixa de correio foi colocada em suspensão de litígio.
    
      - **Colocado em retenção por**   Essa caixa somente leitura indica o usuário que colocou a caixa de correio em retenção de litígio.
    
      - **Observação**   Use essa caixa para notificar o usuário sobre a retenção de litígio, explicar por que a caixa de correio está em retenção de litígio ou fornecer instruções adicionais ao usuário, como informá-lo que a retenção de litígio não afetará o uso diário do email.
    
      - **URL**   Use essa caixa para fornecer uma URL para um site que contém informações ou instruções sobre a retenção de litígio da caixa de correio.
        

        > [!NOTE]
        > O texto dessas caixas aparecerá na caixa de correio do usuário somente se eles estão usando o Outlook 2010 ou versões posteriores. Ele não aparece no Outlook Web App ou outros clientes de email. Para exibir o texto das caixas nota e URL no Outlook, clique na guia <STRONG>arquivo</STRONG> e, na página <STRONG>Info</STRONG>, em <STRONG>Configurações de conta</STRONG>, você verá a retenção de litígio mantenha o comentário.



  - **Arquivo morto**   Se não houver um arquivo morto para a caixa de correio, esse recurso estará desabilitado. Para habilitar uma caixa de correio de arquivo morto, clique em **Habilitar**. Se o usuário tiver uma caixa de correio de arquivo morto, o tamanho da caixa de correio de arquivo morto e as estatísticas de uso serão exibidas. Clique em **Editar detalhes**, para exibir e alterar estas configurações de caixa de correio de arquivo morto:
    
      - **Status**   Esta caixa somente leitura indica se existe uma caixa de correio de arquivo morto.
    
      - **Banco de dados**    Esta caixa somente leitura mostra o nome do banco de dados da caixa de correio que hospeda a caixa de correio de arquivo morto.
    
      - **Nome**   Digite o nome da caixa de correio do arquivo morto na caixa. Esse nome é mostrado na lista de pastas no Outlook ou no Outlook Web App.
    
      - **Uso de cota**    Essa área de somente leitura mostra o tamanho total da caixa de correio de arquivo morto e a porcentagem da cota total de arquivamento da caixa de correio que foi usada.
    
      - **Valor de cota (GB)**    Esta caixa mostra o tamanho total da caixa de correio de arquivo morto. Para alterar o tamanho, digite um novo valor na caixa ou selecione um valor na lista suspensa.
    
      - **Emitir aviso em (GB)**   Essa caixa mostra o limite máximo de armazenamento para a caixa de correio de arquivo morto antes de um aviso ser emitido para o usuário. Se o tamanho da caixa de correio de arquivo morto atingir ou exceder o valor especificado, o Exchange enviará uma mensagem de aviso para o usuário. Para alterar esse limite, digite um novo valor na caixa ou selecione um valor na lista suspensa.

  - **Opções de entrega**    Use as opções de entrega para encaminhar emails enviados para o usuário para outro destinatário e para definir o número máximo de destinatários que o usuário pode enviar uma mensagem para. Clique em **Editar detalhes** para exibir e alterar essas configurações.
    
      - **Endereço de encaminhamento**    Marque a caixa de seleção **Ativar o encaminhamento** e clique em **Procurar** para exibir a página **Selecionar usuários de email e caixa de correio**. Use esta página para selecionar um destinatário para quem deseja encaminhar todas as mensagens de email enviadas para esta caixa de correio. As mensagens serão entregues para a caixa de correio vinculada e o endereço de encaminhamento.
    
      - **Limite de destinatário**    Essa configuração controla o número máximo de destinatários, que o usuário pode enviar uma mensagem. Marque a caixa de seleção de **destinatários máximo** para limitar o número de destinatários permitido em para:, Cc: e Cco: linhas de um email de mensagem e, em seguida, especifique o número máximo de destinatários.
        

        > [!NOTE]
        > Para organizações do Exchange no local, o limite de destinatários é ilimitado. Para organizações do Exchange Online, o limite é de 500 destinatários.



  - **Restrições de tamanho de mensagem**    Essas configurações controlam o tamanho das mensagens que o usuário pode enviar e receber. Clique em **Editar detalhes** para exibir e alterar o tamanho máximo para mensagens enviados e recebidos.
    
      - **Mensagens enviadas**   Para especificar um tamanho máximo para as mensagens enviadas por esse usuário, selecione a caixa **Tamanho máximo de mensagens(KB)** e digite um valor na caixa. O tamanho da mensagem deve estar entre 0 e 2.097.151 KB. Se o usuário enviar uma mensagem maior do que o tamanho especificado, ela retornará ao remetente com uma mensagem de erro descritiva.
    
      - **Mensagens recebidas**   Para especificar um tamanho máximo para as mensagens recebidas por esse usuário, selecione a caixa **Tamanho máximo de mensagens(KB)** e digite um valor na caixa. O tamanho da mensagem deve estar entre 0 e 2.097.151 KB. Se o usuário receber uma mensagem maior do que o tamanho especificado, ela será devolvida ao remetente com uma mensagem de erro descritiva.

  - **Restrições de entrega de mensagem**    Estas configurações controlam quem pode enviar mensagens de email para esse usuário. Clique em **Editar detalhes** para exibir e alterar essas restrições.
    
      - **Aceitar mensagens de**   Use essa seção para especificar quem pode enviar mensagens para esse usuário.
        
          - **Todos os remetentes**   Selecione essa opção para especificar que o usuário pode aceitar mensagens de todos os remetentes. Isso inclui remetentes tanto na sua organização do Exchange quanto externos. Esta opção é selecionada por padrão. Essa opção incluirá usuários externos apenas se você desmarcar a caixa de seleção **Requerer que todos os remetentes sejam autenticados**. Se você marcar essa caixa de seleção, mensagens de usuários externos serão rejeitadas.
        
          - **Somente remetentes da seguinte lista**   Selecione essa opção para especificar que esse grupo pode aceitar mensagens apenas de um conjunto específico de remetentes em sua organização do Exchange. Clique em **Adicionar**para exibir a página **Selecionar destinatários**, que exibe uma lista de todos os destinatários na sua organização do Exchange. Selecione os destinatários que deseja, adicione-os à lista e clique em **OK**. Você também pode pesquisar um destinatário específico, digitando seu nome na caixa de pesquisa e clicando em **Pesquisar**.
        
          - **Exigir que todos os remetentes sejam autenticados**   Selecione essa opção para evitar que usuários anônimos enviem mensagens para o usuário.
    
      - **Rejeitar mensagens de**   Use essa seção para evitar que pessoas enviem enviar mensagens para esse usuário.
        
          - **Nenhum remetente**   Selecione essa opção para especificar que o destinatário não rejeitará mensagens de nenhum remetente na organização do Exchange. Esta opção é selecionada por padrão.
        
          - **Remetentes na lista a seguir**    Selecione essa opção para especificar que a caixa de correio irá rejeitar mensagens de um conjunto especificado de remetentes em sua organização do Exchange. Clique em **Adicionar** para exibir a página **Selecionar o destinatário**, que exibe uma lista de todos os destinatários na sua organização do Exchange. Selecione os destinatários que você deseja rejeitar mensagens de adicioná-los à lista e clique em **OK**. Você também pode pesquisar um destinatário específico digitando o nome do destinatário na caixa Pesquisar e, em seguida, clicando em **Pesquisar**.

## Membro de

Use a seção **Membro de** para exibir uma lista dos grupos de distribuição ou grupos de segurança à qual este usuário pertence. Você não pode alterar as informações de associação nesta página. Observe que o usuário pode corresponder aos critérios de um ou mais grupos dinâmicos de distribuição em sua organização. No entanto, os grupos dinâmicos de distribuição não são exibidos nesta página porque sua associação é calculada sempre que eles são usados.

## MailTip

Use a seção de **Dica de email** para adicionar uma dica de email para alertar os usuários de possíveis problemas quando eles enviam uma mensagem para o destinatário. Uma dica de email é o texto que é exibido na barra de informações quando um destinatário é adicionado a para, Cc ou Cco, linhas de uma nova mensagem de email.


> [!NOTE]
> As Dicas de Email podem incluir marcas HTML, mas scripts não são permitidos. O comprimento de uma dica de email personalizada não pode exceder 175 caracteres exibidos. Marcas HTML não são contadas no limite.



## Delegação da Caixa de Correio

Use a seção **Delegação da Caixa de Correio**, para atribuir permissões para outros usuários (também chamados de *representantes*), para que eles entrem na caixa de correio do usuário ou enviem mensagens em nome do usuário. É possível atribuir as seguintes permissões:

  - **Enviar como**   Essa permissão permite que usuários que não o proprietário da caixa de correio usem a caixa de correio para enviar mensagens. Depois de essa permissão ser atribuída a um representante, qualquer mensagem que um representante enviar desta caixa de correio irá parecer ter sido enviada pelo proprietário da caixa de correio. Entretanto, essa permissão não permite que um representante entre na caixa de correio do usuário.

  - **Enviar em nome de**   Essa permissão também permite que o representante use essa caixa de correio para enviar mensagens. No entanto, após essa permissão ser atribuída a um representante, o endereço **De:**  , em qualquer mensagem enviada pelo representante, indicará que a mensagem foi enviada pelo representante em nome do proprietário da caixa de correio.

  - **Acesso total**   Essa permissão permite que um representante entre na caixa de correio de um usuário e veja o conteúdo da caixa de correio. Entretanto, depois de essa permissão ter sido atribuída a um representante, ele não poderá enviar mensagens da caixa de correio. Para permitir que o representante envie emails da caixa de correio do usuário, você ainda terá que atribuir a ele a permissão Enviar como ou Enviar em Nome de.

Para atribuir permissões para representantes, clique em **Adicionar** na permissão apropriada para exibir a página **Selecionar o destinatário**, que exibe uma lista de todos os destinatários na sua organização do Exchange que pode ser atribuída a permissão. Selecione os destinatários que você deseja atribuir permissões de representante para adicioná-los à lista e clique em **OK**. Você também pode pesquisar um destinatário específico digitando o nome do destinatário na caixa Pesquisar e, em seguida, clicando em **Pesquisar**.

## Use o Shell para alterar propriedades de caixa de correio vinculada

Use os cmdlets **Get-Mailbox** e **Set-Mailbox** para exibir e alterar propriedades para caixas de correio vinculadas. Uma vantagem de usar o Shell é a capacidade de alterar as propriedades de várias caixas de correio vinculadas. Para obter informações sobre quais parâmetros correspondem às propriedades de caixa de correio, consulte os tópicos a seguir:

  - [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\))

Aqui estão alguns exemplos de como usar o Shell para alterar propriedades de caixa de correio vinculada.

Este exemplo usa o comando **Get-Mailbox** para localizar todas as caixas de correio vinculadas na organização.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')}

Este exemplo usa o comando **Set-Mailbox** para limitar o número de destinatários permitido em para:, Cc: e Cco: linhas de uma mensagem de email como 500. Esse limite é aplicável a todas as caixas de correio vinculadas na organização.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | Set-Mailbox -RecipientLimits 500

Este exemplo altera a conta principal vinculada na floresta fabrikam.com conta que está associada uma caixa de correio vinculada em uma floresta do Exchange.

    Set-Mailbox -Identity "Ayla Kol" -LinkedDomainController DC1.fabrikam.com -LinkedMasterAccount "fabrikam\robinw" -LinkedCredential:(Get-Credential fabrikam\administrator)

## Como saber se funcionou?

Para verificar que você alterou com êxito propriedades para uma caixa de correio vinculada, faça o seguinte:

  - No EAC, selecione a caixa de correio vinculada e clique em **Editar** para exibir a propriedade ou recurso que você alterou. Dependendo da propriedade que você alterou, ele pode ser exibido no painel de detalhes para a caixa de correio selecionada.

  - No Shell, use o cmdlet **Get-Mailbox** para verificar as alterações. Uma vantagem de usar o Shell é que você pode visualizar várias propriedades para várias caixas de correio vinculadas. No exemplo acima onde o limite de destinatários foi alterado, executando o seguinte comando verificará o novo valor.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | fl Name,RecipientLimits
    
    No exemplo acima onde a conta principal vinculada foi alterada, execute o seguinte comando para verificar o novo valor.
    
    ```powershell
Get-Mailbox "Ayla Kol" | fl LinkedMasterAccount
```

