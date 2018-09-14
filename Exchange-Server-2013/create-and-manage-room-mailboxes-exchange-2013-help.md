---
title: 'Criar e gerenciar caixas de correio de sala: Exchange Online Help'
TOCTitle: Criar e gerenciar caixas de correio de sala
ms:assetid: f70752ad-fce0-4e14-8428-fc5ac63f6c54
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ215781(v=EXCHG.150)
ms:contentKeyID: 50484845
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Criar e gerenciar caixas de correio de sala

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2017-02-02_

Tempo estimado para conclusão: 5 minutos.

Uma caixa de correio de sala é uma caixa de correio de recurso atribuída a um local físico, como uma sala de conferência, auditório ou sala de treinamento. Depois que um administrador cria caixas de correio de sala, os usuários podem reservar salas facilmente incluindo caixas de correio de sala em solicitações de reunião. Para obter mais detalhes, consulte [Destinatários](recipients-exchange-2013-help.md).

Para saber mais sobre outro tipo de caixa de correio do recurso, consulte [Gerenciar caixas de correio de equipamento](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-equipment-mailboxes).

## O que você deseja fazer?

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" do tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).


> [!IMPORTANT]
> Se você estiver executando o Exchange 2013 em um cenário híbrido, lembre-se de criar as caixas de correio de sala no local apropriado. Crie suas caixas de correio de sala para sua organização local no local, e crie as caixas de correio de sala para o lado do Exchange Online na nuvem.




## Criar uma caixa de correio de sala

## Usar o Centro de Administração do Exchange para criar uma caixa de correio de sala

1.  No Centro de Administração do Exchange, vá para **Destinatários** \> **Recursos**.

2.  Para criar uma caixa de correio de sala, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") \> **Caixa de correio de sala**.

3.  Use as opções na página para especificar as configurações para a nova caixa de correio de recurso.
    
      - \* **Nome da sala**   Use esta caixa para digitar um nome para a caixa de correio de sala. Esse é o nome que fica na lista de caixas de correio de recurso no Centro de Administração do Exchange e no catálogo de endereços da sua organização. Esse nome é obrigatório e não pode exceder 64 caracteres.
        

        > [!TIP]
        > Embora existam outros campos que descrevam os detalhes da sala, por exemplo, Local e Capacidade, considere resumir os detalhes mais importantes no nome da sala usando uma convenção de nomenclatura consistente. Por quê? Porque assim os usuários poderão consultar facilmente os detalhes ao selecionarem a sala no catálogo de endereços na solicitação de reunião.

    
      - \* **Endereço de email**   Uma caixa de correio de sala tem um endereço de email para que possa receber solicitações de reserva. O endereço de email consiste em um alias no lado esquerdo do símbolo @, que deve ser exclusivo na floresta, e no nome do domínio à direita. O endereço de email é obrigatório.
    
      - **Local**, **Telefone**, **Capacidade**   Você pode usar esses campos para inserir detalhes sobre a sala. Entretanto, como explicado anteriormente, você pode incluir algumas ou todas essas informações no nome da sala para que os usuários possam consultá-las.

4.  Após concluir, clique em **Salvar** para criar a caixa de correio de sala.

Depois de criar a caixa de correio de sala, você pode editá-la para atualizar informações sobre opções de reserva, dicas de email e delegação de caixa de correio. Confira a seção Usar o Centro de Administração do Exchange abaixo para alterar as propriedades de caixa de correio de sala

## Usar o Exchange PowerShell para criar uma caixa de correio de sala

Este exemplo cria uma caixa de correio de sala com a seguinte configuração:

  - A caixa de correio de sala reside no Mailbox Database 1 (Banco de Dados de Caixa de Correio 1).

  - O nome da caixa de correio é ConfRoom1. Esse nome também será usado para criar o endereço de email da sala.

  - O nome para exibição no Centro de Administração do Exchange e no catálogo de endereços será Sala de Conferência 1.

  - A opção *Room* especifica que esta caixa de correio será criada como uma caixa de correio de sala.

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name ConfRoom1 - -DisplayName "Conference Room 1" -Room

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-Mailbox](https://technet.microsoft.com/pt-br/library/aa997663\(v=exchg.150\)).

## Como saber se funcionou?

Há algumas maneiras diferentes de garantir que você criou a caixa de correio de sala corretamente:

  - No Centro de Administração do Exchange, vá para **Destinatários** \> **Recursos**. A nova caixa de correio de sala é exibida na lista de caixas de correio. Em **Tipo de caixa de correio**, o tipo é **Sala**.

  - No Exchange PowerShell, execute o comando a seguir para exibir informações sobre a nova caixa de correio de sala.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Criar uma lista de salas

Se você estiver planejando ter mais de cem salas, ou já tiver mais de cem salas criadas, use uma lista de salas para ajudar a organizá-las. Se sua empresa tiver vários edifícios com salas que podem ser reservadas para reuniões, talvez seja útil criar listas de salas para cada edifício. As listas de salas são grupos de distribuição marcados especialmente e que você pode usar da mesma forma que usa grupos de distribuição. No entanto, você pode apenas criar listas de sala usando o Shell de Gerenciamento do Exchange.

## Usar o Exchange PowerShell para criar uma lista de salas

Este exemplo cria uma lista de salas para o edifício 32.

    New-DistributionGroup -Name "Building 32 Conference Rooms" -OrganizationalUnit "contoso.com/rooms" -RoomList

## Usar o Exchange PowerShell para adicionar uma sala a uma lista de salas

Este exemplo adiciona confroom3223 à lista de salas do edifício 32.

    Add-DistributionGroupMember -Identity "Building 32 Conference Rooms" -Member confroom3223@contoso.com

## Usar o Exchange PowerShell para converter um grupo de distribuição em uma lista de salas

Talvez você já tenha criado grupos de distribuição contendo suas salas de conferência. Não é necessário recriá-los; podemos convertê-los rapidamente em uma lista de salas.

Este exemplo converte o grupo de distribuição, salas de conferência do edifício 34, em uma lista de salas.

    Set-DistributionGroup -Identity "Building 34 Conference Rooms" -RoomList

## Alterar as propriedades da caixa de correio de sala

Depois de criar uma caixa de correio de sala, você pode fazer alterações e definir propriedades adicionais usando o Centro de Administração do Exchange ou o Exchange PowerShell.

## Usar o Centro de Administração do Exchange para alterar as propriedades da caixa de correio de sala

1.  No Centro de Administração do Exchange, vá para **Destinatários** \> **Recursos**.

2.  Na lista de caixas de correio de recursos, clique na caixa de correio de sala cujas propriedades você quer alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades da caixa de correio de sala, clique em uma destas seções, para exibir ou alterar propriedades.
    
      - Geral
    
      - Representantes
    
      - Opções de Reserva
    
      - Informações de contato
    
      - Endereço de Email
    
      - MailTip

## Geral

Use a seção **Geral** para ver ou alterar as informações básicas sobre o recurso.

  - **\* Nome da sala**   Esse nome aparece na lista de caixas de correio de recurso no Centro de Administração do Exchange e no catálogo de endereços da sua organização. Se você alterá-lo, ele não poderá exceder 64 caracteres.

  - **\*Endereço de email**   Esta caixa somente leitura exibe o endereço de email da caixa de correio de sala. Você pode alterá-la na seção Endereço de Email.

  - **Capacidade**   Use esta caixa para inserir o número máximo de pessoas que podem ocupar a sala com segurança.

Clique em **Mais opções**, para exibir ou alterar essas propriedades adicionais:

  - **Unidade organizacional**  Essa caixa somente leitura exibe a unidade organizacional (OU) que contém a conta da caixa de correio de sala. Você precisa usar Usuários e Computadores do Active Directory para mover a conta para uma OU diferente.

  - **Banco de dados de caixa de correio**   Esse campo somente leitura exibe o nome do banco de dados de caixa de correio que hospeda a caixa de correio de sala. Use a página **Migração** no Centro de Administração do Exchange para mover a caixa de correio para um banco de dados diferente.

  - **\*Alias** Use esta caixa para alterar o alias da caixa de correio de sala.

  - **Ocultar das listas de endereço**   Marque essa caixa de seleção para evitar que a caixa de correio de sala apareça no catálogo de endereços e em outras listas de endereços definidas em sua organização do Exchange. Após marcar essa caixa de seleção, os usuários ainda podem enviar mensagens de reserva à caixa de correio de sala usando o endereço de email.

  - **Departamento**   Use essa caixa para especificar um nome de departamento ao qual a sala está associada. Você pode usar esta propriedade para criar condições de destinatário para grupos dinâmicos de distribuição e listas de endereços.

  - **Empresa**   Use essa caixa para especificar uma empresa à qual a sala está associada, se aplicável. Como a propriedade de Departamento, você pode usar esta propriedade para criar condições de destinatário para grupos dinâmicos de distribuição e listas de endereços.

  - **Política do catálogo de endereços**   Use essa opção para especificar uma política de catálogo de endereços (ABP) para a caixa de correio de sala. As ABPs contêm um catálogo de endereços global (GAL), um catálogo de endereços offline (OAB), uma lista de salas e um conjunto de listas de endereços. Para obter mais informações, consulte [Políticas de catálogo de endereços](https://docs.microsoft.com/pt-br/exchange/address-books/address-book-policies/address-book-policies).
    
    Na lista suspense, selecione a política que você deseja associar a esta caixa de correio.

  - **Atributos personalizados**   Essa seção exibe os atributos personalizados definidos para a caixa de correio de sala. Para especificar valores de atributos personalizáveis, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Você pode especificar até 15 atributos personalizados para o destinatário.

## Representantes

Use esta seção para exibir ou alterar o modo como a caixa de correio de sala lida com as solicitações de reserva e definir quem pode aceitar ou recusar as solicitações de reserva se isso não for feito automaticamente.

  - **Solicitações de reserva**   Selecione uma das seguintes opções para lidar com solicitações de reserva.
    
      - **Aceitar ou recusar solicitações de reserva automaticamente**   Uma solicitação de reunião válida reserva a sala automaticamente. Se houver conflito de agendamento com uma reserva existente, ou se a solicitação de reserva violar os limites de agendamento do recurso, por exemplo, a duração da reserva é muito longa, a solicitação de reunião será automaticamente negada.
    
      - **Selecionar representantes que podem aceitar ou recusar solicitação de reserva**   Os representantes de recursos são responsáveis por aceitar ou recusar as solicitações de reunião enviadas para a caixa de correio de sala. Se você atribuir mais de um representante de recurso, somente um deles precisará agir em uma solicitação de reunião específica.

  - **Representantes**   Se tiver selecionado a opção que exige que as solicitações de reserva sejam enviadas a representantes, os representantes especificados serão listados. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") ou **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover") para adicionar ou remover representantes da lista.

## Opções de Reserva

Use a seção **Opções de Reserva** para exibir ou alterar as configurações da política de reserva que define quando a sala pode ser agendada, por quanto tempo pode ser reservada e com que antecedência pode ser reservada.

  - **Permitir reuniões repetitivas**   Essa configuração permite ou impede reuniões repetitivas da sala. Por padrão, essa configuração está habilitada, de modo que as reuniões repetitivas são permitidas.

  - **Permitir agendamento apenas durante o horário de trabalho**   Essa configuração aceita ou recusa solicitações de reunião do recurso que não são definidas para a sala durante o horário comercial. Por padrão, essa configuração está desabilitada, de modo que as solicitações de reunião serão permitidas fora do horário comercial. Por padrão, o horário comercial é das 8 às 17h, de segunda a sexta-feira. Você pode configurar o horário de trabalho da caixa de correio de sala na seção Aparência da página Calendário.

  - **Recusar sempre se a data de fim ultrapassar este limite**   Esta configuração controla o comportamento de reuniões repetitivas que vão além da data especificada pela configuração de tempo de entrega de agendamento máximo.
    
      - Se você habilitar essa configuração, uma solicitação de reserva que se repete será recusada automaticamente, se as reservas começarem na data especificada ou antes dessa data especificada pelo valor na caixa **Prazo máximo da reserva** e elas forem além da data especificada. Essa é a configuração padrão.
    
      - Se você desabilitar essa configuração, uma solicitação de reserva que se repete será aceita automaticamente, se as solicitações de reservas começarem na data especificada ou antes dessa data especificada pelo valor na caixa **Prazo máximo da reserva** e elas forem além da data especificada. Entretanto, o número de reservas é reduzido, de forma que elas não ocorram após a data especificada.

  - **Prazo máximo da reserva (dias)**   Essa configuração especifica o número máximo de dias de antecedência que a sala pode ser reservada. A entrada válida é um número inteiro entre 0 e 1080. O valor padrão é 180 dias.

  - **Duração máxima (minutos)**   Essa configuração especifica a duração máxima que a sala pode ser reservada em uma solicitação de reserva. O valor padrão é 24 horas.
    
    Para solicitações de reserva repetitivas, a duração máxima da reserva se aplica à duração de cada instância do Centro de Administração do Exchange da solicitação de reserva repetitiva.

Há também uma caixa nesta página que você precisa usar para escrever uma mensagem que será enviada aos usuários que enviam solicitações de reserva para reservar a sala.

## Informações de contato

Use a seção **Informações de Contato** para exibir e alterar as informações de contato da sala. As informações nesta página são exibidas no catálogo de endereços.


> [!TIP]
> Você pode usar também a caixa <STRONG>Estado/Província</STRONG> para criar as condições do destinatário para os grupos dinâmicos de distribuição, diretivas de endereço de email ou listas de endereços.



## Endereço de Email

Use a seção **Endereço de email** para exibir ou alterar os endereços de email associados à caixa de correio de sala. Isso inclui o endereço SMTP principal da caixa de correio e todos os endereços de proxy associados. O endereço SMTP principal (também conhecido como *endereço de resposta*) será exibido em negrito, na lista de endereços, com o valor em maiúsculas **SMTP** na coluna **Tipo**.

  - **Adicionar**  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar um novo endereço de email para essa caixa de correio. Selecione um dos seguintes tipos de endereço:
    
      - **SMTP**   Esse é o tipo de endereço padrão. Clique nesse botão e digite o novo endereço SMTP na caixa **\* Endereço de email**.
    
      - **EUM**   Um endereço da Unificação de Mensagem do Exchange (EUM) é utilizado pelo serviço de Unificação de Mensagens do Microsoft Exchange para localizar destinatários habilitados para UM dentro da organização do Exchange. Os endereços da EUM contêm o número da extensão e o plano de discagem de UM para o usuário habilitado para UM. Clique nesse botão e digite o novo número de ramal na caixa **Endereço/Ramal**. Em seguida, clique em **Procurar** e selecione um plano de discagem para a caixa de correio.
    
      - **Tipo de endereço personalizado**   Clique nesse botão e digite um dos tipos de endereço de email não SMTP compatíveis na caixa **\* Endereço de email**.
        

        > [!TIP]
        > Com a exceção de endereços X.400, o Exchange não valida endereços personalizados para a formatação adequada. Certifique-se de que o endereço personalizado que você especificar esteja de acordo com os requisitos de formato para esse tipo de endereço.

    

    > [!TIP]
    > Quando adiciona um novo endereço de email, você tem a opção de torná-lo o endereço SMTP principal.



  - **Atualizar automaticamente os endereços de email com base na política de endereços de email aplicados a este destinatário**   Marque essa caixa de seleção para que os endereços de email do destinatário sejam atualizados automaticamente com base nas alterações feitas nas políticas de endereços de email em sua organização.

## MailTip

Use a seção **Dica de Email** para adicionar uma Dica de Email a fim de alertar os usuários de possíveis problemas antes de eles enviarem uma solicitação de reserva à caixa de correio de sala. Uma Dica de Email é o texto exibido na barra de informações quando esse destinatário é adicionado aos campos Para, Cc ou Cco de um novo email.


> [!TIP]
> As Dicas de Email podem incluir marcas HTML, mas scripts não são permitidos. O comprimento de uma dica de email personalizada não pode exceder 175 caracteres exibidos. As marcas HTML não são contadas no limite.



## Usar o Exchange PowerShell para alterar propriedades de caixa de correio de sala

Use os seguintes conjuntos de cmdlets para exibir e alterar as propriedades de caixa de correio de sala: cmdlets **Get-Mailbox** e **Set-Mailbox** para exibir e alterar as propriedades gerais e os endereços de email das caixas de correio de sala. Use os cmdlets **Get-CalendarProcessing** e **Set-CalendarProcessing** para exibir e alterar representantes e opções de reserva.

  - **Get-User** e **Set-User**   Use esses cmdlets para exibir e definir as propriedades gerais, como local, departamento e nomes de empresa.

  - **Get-Mailbox** e **Set-Mailbox**   Use esses cmdlets para exibir e definir as propriedades de caixa de correio, como endereços de email e o banco de dados de caixa de correio.

  - **Get-CalendarProcessing** e **Set-CalendarProcessing**   Use esses cmdlets para exibir e definir opções de reserva e representantes.

Para obter mais informações sobre esses cmdlets, consulte os tópicos a seguir:

  - [Get-User](https://technet.microsoft.com/pt-br/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/pt-br/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/pt-br/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/pt-br/library/dd335046\(v=exchg.150\))

Estes são alguns exemplos de como usar o Exchange PowerShell para alterar propriedades de caixas de correio de sala.

Este exemplo altera o nome de exibição, o endereço SMTP principal (chamado de endereço de resposta padrão) e a capacidade da sala. Além disso, o endereço de resposta anterior é mantido como um endereço de proxy.

    Set-Mailbox "Conf Room 123" -DisplayName "Conf Room 31/123 (12)" -EmailAddresses SMTP:Rm33.123@contoso.com,smtp:rm123@contoso.com -ResourceCapacity 12

Este exemplo configura as caixas de correio de sala para permitir que as solicitações de reserva sejam agendadas somente durante o horário comercial e define uma duração máxima de 9 horas.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true -MaximumDurationInMinutes 540

Este exemplo usa o cmdlet **Get-User** para localizar todas as caixas de correio de sala correspondentes às salas de conferência privadas e usa o cmdlet **Set-CalendarProcessing** para enviar solicitações de reserva a um representante com o nome Robin Wood para aceitar ou recusar.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox') -and (DisplayName -like 'Private*')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Robin Wood"

## Como saber se funcionou?

Para verificar se você alterou com êxito as propriedades da caixa de correio de sala, faça o seguinte:

  - No Centro de Administração do Exchange, selecione a caixa de correio e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir a propriedade ou o recurso que você alterou. Dependendo da propriedade que você tiver alterado, ela poderá ser exibida no painel Detalhes da caixa de correio selecionada.

  - No Exchange PowerShell, use o cmdlet **Get-Mailbox** para verificar as alterações. Uma vantagem de se usar o Exchange PowerShell é que você pode exibir múltiplas propriedades de várias caixas de correio. No exemplo acima, em que as solicitações de reserva podem ser agendadas somente durante o horário comercial e ter uma duração máxima de 9 horas, execute o comando a seguir para verificar os novos valores.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours,MaximumDurationInMinutes

Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..


