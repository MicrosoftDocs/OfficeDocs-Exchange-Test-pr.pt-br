---
title: 'Gerenciar usuários de email: Exchange Online Help'
TOCTitle: Gerenciar usuários de email
ms:assetid: bb8b8804-f730-4ad7-9173-896a4965b90f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124381(v=EXCHG.150)
ms:contentKeyID: 50484797
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailUserWizardForm.NewMailUserIntroductionWizardPage
ms.translationtype: HT
---

# Gerenciar usuários de email

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Usuários de email são semelhantes a contatos de email. Ambos têm endereços de email externos e contêm informações sobre pessoas de fora da sua organização do Exchange ou do Exchange Online que podem ser exibidas no catálogo de endereços compartilhado e em outras listas de endereços. No entanto, diferentemente de um contato de email, um usuário de email tem credenciais de logon na sua organização do Exchange ou do Office 365 e pode acessar os recursos. Para mais informações, confira [Destinatários](recipients-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário", no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Criar um usuário de email

## Usar o EAC para criar um usuário de email

1.  No EAC, navegue até **Destinatários** \> **Contatos** \> **Novo** \> **Usuário de email**.

2.  Na página **Novo usuário de email**, na caixa **\* Alias**, digite o alias do servidor de email. O alias não pode exceder 64 caracteres e deve ser único na floresta. Essa caixa é obrigatória.

3.  Execute uma das ações a seguir para especificar o tipo de endereço de email do usuário de email:
    
      - Para especificar um endereço de email SMTP para o endereço de email externo do usuário de email, clique em **SMTP**.
        

        > [!TIP]
        > O Exchange valida endereços SMTP para formatação correta. Se a sua entrada for inconsistente com o formato SMTP, será exibida uma mensagem de erro quando você clicar em <STRONG>Salvar</STRONG> para criar o usuário de email.

    
      - Para especificar um tipo de endereço personalizado, clique no botão de seleção e digite o tipo de endereço personalizado. Por exemplo, especifique um endereço X.500, GroupWise ou Lotus Notes.

4.  Na caixa **\* Endereço de email externo**, digite o endereço de email externo do usuário de email. O email enviado a esse usuário é encaminhado a esse endereço de email. Essa caixa é obrigatória.

5.  
    
    Selecione uma das seguintes opções:
    
      - **Usuário existente**   Selecione para habilitar um usuário existente para email.
        
        Clique em **Procurar** para abrir a caixa de diálogo **Selecionar Usuário — Floresta Inteira**. Essa caixa de diálogo exibe uma lista de contas de usuário na organização que não estão habilitadas para email nem possuem caixas de correio. Selecione a conta de usuário que você deseja habilitar para email e clique em **OK**. Se você selecionar essa opção, não terá que fornecer informações de conta de usuário, pois essas informações já existirão no Active Directory.
    
      - **Novo usuário**   Selecione para criar uma nova conta de usuário no Active Directory e habilitar o usuário para email. Se você selecionar essa opção, terá que fornecer as informações de conta de usuário necessárias.

6.  
    
    Se você tiver selecionado **Novo Usuário** na Etapa 5, preencha as seguintes caixas na página **Novo usuário de email**. Caso contrário, pule para a Etapa 7.
    
      - **Nome**   Use essa caixa para digitar o nome do usuário de email.
    
      - **Iniciais**   Use essa caixa para digitar as iniciais do usuário de email.
    
      - **Sobrenome**   Use essa caixa para digitar o sobrenome do usuário de email.
    
      - **\* Nome de exibição**   Use essa caixa para digitar um nome de exibição do contato. Esse é o nome que fica na lista de contatos no EAC e no catálogo de endereços da sua organização. Por padrão, essa caixa é preenchida com os nomes inseridos nas caixas **Nome**, **Iniciais** e **Sobrenome**. Se você não tiver usado essas caixas, ainda deverá digitar um nome nessa caixa, pois ela é obrigatória. O nome não pode exceder 64 caracteres.
    
      - **\* Nome**   Use essa caixa para digitar um nome para o usuário de email. Esse é o nome listado no serviço de diretório. Essa caixa também é preenchida com os nomes que você insere nas caixas **Nome**, **Iniciais** e **Sobrenome**. Se você não tiver usado essas caixas, ainda deverá digitar um nome, pois essa caixa é obrigatória. Esse nome também não pode exceder 64 caracteres.
        

        > [!TIP]
        > A caixa <STRONG>Nome</STRONG> só está disponível no Exchange Server 2013. Ela não está disponível no Exchange Online.

    
      - **Unidade organizacional**   É possível selecionar uma UO (unidade organizacional) que não seja a padrão, que é o escopo do destinatário. Se o escopo do destinatário estiver definido para a floresta, o valor padrão será definido para o contêiner Usuários no domínio que contém o computador no qual o EAC está sendo executado. Se o escopo do destinatário estiver definido para um domínio específico, por padrão, o contêiner Usuários desse domínio será selecionado. Se o escopo do destinatário estiver definido para uma UO específica, essa UO será selecionada por padrão.
        
        Para selecionar uma UO diferente, clique em **Procurar**. A caixa de diálogo exibe todas as OUs da floresta que estão no escopo especificado. Selecione a UO desejada e clique em **OK**.
        

        > [!TIP]
        > A caixa <STRONG>Unidade organizacional</STRONG> só está disponível no Exchange Server 2013. Ela não está disponível no Exchange Online.

    
      - **\* Nome de logon do usuário**    Use essa caixa para digitar o nome que o usuário de email usará para fazer logon no domínio. O nome de logon do usuário consiste em um nome de usuário no lado esquerdo do símbolo (@) e um sufixo no lado direito. Geralmente, o sufixo é o nome do domínio no qual a conta do usuário reside.
        

        > [!TIP]
        > No Exchange Online, essa caixa se chama <STRONG>ID de usuário</STRONG>.

    
      - **\* Nova senha**   Use essa caixa para digitar a senha que o usuário de email utilizará para fazer logon no domínio.
        

        > [!TIP]
        > Verifique se a senha fornecida é compatível com os requisitos de tamanho, complexidade e histórico do domínio no qual você está criando a conta do usuário.

    
      - **\*Confirmar senha**   Use essa caixa para confirmar a senha que você digitou na caixa **Senha**.
    
      - **O usuário deve alterar a senha no próximo logon**   Marque essa caixa de seleção se desejar que os usuários redefinam a senha ao fazer o primeiro logon no domínio.
        
        Se você marcar essa caixa de seleção, no primeiro logon, o novo usuário de email verá uma caixa de diálogo para alterar a senha. O usuário de email não terá permissão para executar nenhuma tarefa até que a senha tenha sido alterada com êxito.

7.  
    
    Quando tiver terminado, clique em **Salvar** para criar o usuário de email.

## Usar o Shell para criar um usuário de correio

Esse exemplo cria uma conta de usuário habilitado para email em nome de Diogo Martins no Exchange Server 2013 com os seguintes detalhes:

  - O nome e o nome de exibição são Diogo Martins.

  - O alias é diogom.

  - O endereço de email externo é diogom@tailspintoys.com.

  - O primeiro nome é Diogo e o sobrenome é Martins.

  - O nome de logon é diogom@contoso.com.

  - A senha é Pa$$word1.

  - O usuário de email será criado na unidade organizacional padrão. Para especificar uma unidade organizacional diferente, use o parâmetro *OrganizationalUnit*.

<!-- end list -->

    New-MailUser -Name "Jeffrey Zeng" -Alias jeffreyz -ExternalEmailAddress jzeng@tailspintoys.com -FirstName Jeffrey -LastName Zeng -UserPrincipalName jeffreyz@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

O exemplo cria uma conta de usuário habilitado para email em nome de Paulo Araújo no Exchange Online.

    New-MailUser -Name "Rene Valdes" -Alias renev -ExternalEmailAddress renevaldes@fineartschool.edu -FirstName Rene -LastName Valdes -MicrosoftOnlineServicesID renev@contoso.com -Password (ConvertTo-SecureString -String 'P@ssw0rd' -AsPlainText -Force)

## Como saber se funcionou?

Para verificar se você criou com sucesso um usuário de email, siga uma destas opções:

  - No EAC, navegue até **Destinatários** \> **Contatos**. O novo usuário de email é exibido na lista de contatos. Em **Tipo de Contato**, o tipo é **Usuário de email**.

  - No Shell, execute o comando abaixo para exibir informações sobre o novo usuário de email.
    
        Get-MailUser <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## Alterar propriedades do usuário de email

Após criar um usuário de email, é possível efetuar alterações e definir propriedades adicionais utilizando o EAC ou o Shell.

Você também pode alterar as propriedades de várias caixas de correio de usuário ao mesmo tempo. Para mais informações, confira Editar usuários de email em massa.

O tempo estimado para concluir essa tarefa varia com base no número de propriedades que você deseja exibir ou alterar.

## Usar o EAC para alterar as propriedades de caixa de correio de usuário

1.  No EAC, navegue até **Destinatários** \> **Contatos**.

2.  Na lista de contatos, clique no usuário de email cujas propriedades deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do usuário de email, clique em uma destas seções para exibir ou alterar propriedades.
    
      - Geral
    
      - Informações de contato
    
      - Organização
    
      - Endereços de email
    
      - Configurações de fluxo de emails
    
      - Membro de
    
      - MailTip

## Geral

Use a seção **Geral** para exibir ou alterar as informações básicas sobre o usuário de email.

  - **Nome**, **Iniciais**, **Sobrenome**

  - **\* Nome**   Esse é o nome que está listado em Active Directory. Se você alterar esse nome, não pode exceder 64 caracteres.

  - **\* Nome de exibição** Esse nome será exibido no catálogo de endereços da sua organização, nas linhas Para: e De: no email e na lista de contatos no EAC. Esse nome não pode conter espaços vazios antes ou depois do nome de exibição.

  - **\* Nome de logon do usuário**   Refere-se ao nome com o qual o usuário faz logon no domínio. No Exchange Online, esse é o ID de usuário utilizado pelo usuário para entrar no Office 365.

  - **Ocultar das listas de endereço**   Marque essa caixa de seleção para evitar que o destinatário apareça no catálogo de endereços e em outras listas de endereço definidas na sua organização do Exchange. Depois de marcar essa caixa de seleção, os usuários ainda poderão enviar mensagens ao destinatário usando o endereço de email.

  - **O usuário deve alterar a senha no próximo logon**   Marque essa caixa de seleção se quiser que o usuário redefina a senha da próxima vez em que fizer logon no domínio.
    

    > [!TIP]
    > Essa caixa não está disponível no Exchange Online.



Clique em **Mais opções**, para exibir ou alterar essas propriedades adicionais:

  - **Unidade organizacional**   Essa caixa somente leitura exibe a unidade organizacional (OU) que contém a conta do usuário. Você pode usar Usuários e Computadores do Active Directory para mover a conta de usuário para uma OU diferente.
    

    > [!TIP]
    > Essa caixa não está disponível no Exchange Online.



  - **Atributos personalizados**   Essa seção exibe os atributos personalizáveis definidos para a caixa de correio do usuário. Para especificar valores de atributos personalizáveis, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Você pode especificar até 15 atributos personalizados para o destinatário.

## Informações de contato

Use a seção **Informações de Contato** para exibir ou alterar as informações de contato do usuário. As informações nesta página são exibidas no catálogo de endereços. Clique em **Mais opções** para exibir caixas adicionais.


> [!TIP]
> Você pode usar também a caixa <STRONG>Estado/Província</STRONG> para criar as condições do destinatário para os grupos dinâmicos de distribuição, diretivas de endereço de email ou listas de endereços.



## Organização

Use a seção **Organização** para registrar informações detalhadas sobre a função do usuário na organização. Estas informações são exibidas no catálogo de endereços. Além disso, você pode criar um organograma virtual acessível por clientes de email como o Outlook.

  - **Título   **Use essa caixa para visualizar ou alterar o título do destinatário.

  - **Departamento**   Use esta caixa para exibir ou alterar o departamento no qual o usuário trabalha. Você pode usar essa caixa para criar condições de destinatário para os grupos de distribuição dinâmica, diretivas de endereço de email ou listas de endereços.

  - **Empresa**   Use essa caixa para exibir ou alterar a empresa para a qual o usuário trabalha. Você pode usar essa caixa para criar condições de destinatário para os grupos de distribuição dinâmica, diretivas de endereço de email ou listas de endereços.

  - **Gerente**   Para adicionar um gerente, clique em **Procurar**. Em **Selecionar Gerente**, selecione uma pessoa e clique em **OK**.

  - **Funcionários subordinados**   Você não pode modificar essa caixa. *Funcionário subordinado* é um usuário subordinado a um gerente específico. Se você tiver especificado um gerente para o usuário, esse usuário será exibido como subordinado direto nos detalhes da caixa de correio do gerente. Por exemplo, Kari gerencia Chris e Kate e, portanto, Kari é especificada na caixa **Gerente** para Chris e Kate, enquanto Chris e Kate aparecem na caixa **Funcionários subordinados** nas propriedades da caixa de correio de Kari.

## Emails

Use a seção **Endereços de email** para exibir ou alterar os endereços de email associados ao usuário de email. Isso inclui o endereço SMTP principal do usuário de email, seu endereço de email externo e qualquer endereço proxy associado. O endereço SMTP primário (também conhecido como o *endereço de resposta padrão*) é exibido em negrito na lista de endereços, com o valor de **SMTP** em maiúsculas na coluna **Tipo**. Por padrão, após a criação do usuário de email, o endereço SMTP principal e o endereço de email externo são os mesmos.

  - **Adicionar **  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar um novo endereço de email para essa caixa de correio. Selecione um dos seguintes tipos de endereço:
    
      - **SMTP**   Esse é o tipo de endereço padrão. Clique nesse botão e digite o novo endereço SMTP na caixa **\* Endereço de email**.
    
      - **Tipo de endereço personalizado**   Clique nesse botão e digite um dos tipos de endereço de email não SMTP compatíveis na caixa **\* Endereço de email**.
        

        > [!TIP]
        > Com a exceção de endereços X.400, o Exchange não valida endereços personalizados para a formatação adequada. Certifique-se de que o endereço personalizado que você especificar esteja de acordo com os requisitos de formato para esse tipo de endereço.



  - **Definir o endereço de email externo**   Use essa caixa para alterar o endereço de email externo do usuário. O email enviado a esse usuário é encaminhado a esse endereço de email.

  - **Atualizar automaticamente os endereços de email com base na política de endereços de email aplicados a este destinatário**   Marque essa caixa de seleção para que os endereços de email do destinatário sejam atualizados automaticamente com base nas alterações feitas nas políticas de endereços de email em sua organização. Essa caixa de seleção é marcada por padrão.
    

    > [!TIP]
    > Essa caixa de seleção não está disponível no Exchange Online.



## Configurações de fluxo de emails

Use a seção **Configurações de fluxo de emails** para exibir ou alterar as seguintes configurações:

  - **Restrições de tamanho de mensagem**   Essas configurações controlam o tamanho das mensagens que o usuário pode enviar e receber. Clique em **Exibir detalhes** para exibir e alterar o tamanho máximo para mensagens enviadas e recebidas.
    
      - **Mensagens enviadas**   Para especificar um tamanho máximo para as mensagens enviadas por esse usuário, selecione a caixa **Tamanho máximo de mensagens(KB)** e digite um valor na caixa. O tamanho da mensagem deve estar entre 0 e 2.097.151 KB. Se o usuário enviar uma mensagem maior do que o tamanho especificado, ela retornará ao remetente com uma mensagem de erro descritiva.
    
      - **Mensagens recebidas**   Para especificar um tamanho máximo para as mensagens recebidas por esse usuário, selecione a caixa **Tamanho máximo de mensagens(KB)** e digite um valor na caixa. O tamanho da mensagem deve estar entre 0 e 2.097.151 KB. Se o usuário receber uma mensagem maior do que o tamanho especificado, ela será devolvida ao remetente com uma mensagem de erro descritiva.

  - **Restrições de entrega de mensagem**   Essas configurações controlam quem pode enviar mensagens para esse usuário de email. Clique em **Exibir detalhes** para exibir e alterar essas restrições.
    
      - **Aceitar mensagens de**   Use essa seção para especificar quem pode enviar mensagens para esse usuário.
        
          - **Todos os remetentes**   Selecione essa opção para especificar que o usuário pode aceitar mensagens de todos os remetentes. Isso inclui remetentes tanto na sua organização do Exchange quanto externos. Esta opção é selecionada por padrão. Essa opção incluirá usuários externos apenas se você desmarcar a caixa de seleção **Requerer que todos os remetentes sejam autenticados**. Se você marcar essa caixa de seleção, mensagens de usuários externos serão rejeitadas.
        
          - **Somente remetentes da seguinte lista**   Selecione essa opção para especificar que esse grupo pode aceitar mensagens apenas de um conjunto específico de remetentes em sua organização do Exchange. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")para exibir a página **Selecionar destinatários**, que exibe uma lista de todos os destinatários na sua organização do Exchange. Selecione os destinatários que deseja, adicione-os à lista e clique em **OK**. Você também pode pesquisar um destinatário específico, digitando seu nome na caixa de pesquisa e clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").
        
          - **Exigir que todos os remetentes sejam autenticados**   Selecione essa opção para evitar que usuários anônimos enviem mensagens para o usuário.
    
      - **Rejeitar mensagens de**   Use essa seção para evitar que pessoas enviem enviar mensagens para esse usuário.
        
          - **Nenhum remetente**   Selecione essa opção para especificar que o destinatário não rejeitará mensagens de nenhum remetente na organização do Exchange. Esta opção é selecionada por padrão.
        
          - **Remetentes da seguinte lista**   Selecione essa opção para especificar que a caixa de correio rejeitará mensagens de um conjunto específico de remetentes em sua organização do Exchange. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), para mostrar a página **Selecionas Destinatários**, que mostra uma lista de todos os destinatários na sua organização do Exchange. Selecione os destinatários que deseja, adicione-os à lista e clique em **OK**. Você também pode pesquisar um destinatário específico, digitando seu nome na caixa de pesquisa e clicando em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar").

## Membro de

Use a seção **Membro de** para visualizar uma lista de grupos de distribuição ou de segurança aos quais esse destinatário pertence. Você não pode alterar informações de associação nesta página. Observe que o usuário pode atender aos critérios de um ou mais grupos dinâmicos de distribuição em sua organização. Contudo, os grupos dinâmicos de distribuição não são exibidos nessa página, pois sua associação é calculada sempre que eles são utilizados.

## MailTip

Use a seção **Dica de Email** para adicionar uma Dica de Email a fim de alertar os usuários de possíveis problemas antes que seja enviada uma mensagem a este destinatário. Uma Dica de Email é o texto exibido na Barra de Informações quando esse destinatário é adicionado às linhas Para, Cc ou Cco de uma nova mensagem de email.


> [!TIP]
> As Dicas de Email podem incluir marcas HTML, mas scripts não são permitidos. O comprimento de uma dica de email personalizada não pode exceder 175 caracteres exibidos. As marcas HTML não são contadas no limite.



## Usar o Shell para alterar as propriedades de usuários de email

As propriedades de um usuário de email são armazenadas no Active Directory e no Exchange. De modo geral, use os cmdlets **Get-User** e **Set-User** para exibir e alterar as propriedades das informações de contato e da organização. Use os cmdlets **Get-MailUser** e **Set-MailUser** para exibir ou alterar as propriedades relacionadas a emails, como endereços de email, a Dica de Email, atributos personalizados e se o usuário de email está oculto das listas de endereços.

Uso os cmdlets **Get-MailUser** e **Set-MailUser** para exibir e alterar as propriedades de usuários de email. Para informações, confira os seguintes tópicos:

  - [Get-User](https://technet.microsoft.com/pt-br/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/pt-br/library/aa998221\(v=exchg.150\))

  - [Get-MailUser](https://technet.microsoft.com/pt-br/library/aa997254\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/pt-br/library/aa995971\(v=exchg.150\))

Veja a seguir alguns exemplos de como usar o Shell para alterar propriedades dos usuários de email.

Este exemplo define o endereço de email externo de Brenda Fernandes.

    Set-MailUser "Pilar Pinilla" -ExternalEmailAddress pilarp@tailspintoys.com

Este exemplo oculta todos os usuários de email do catálogo de endereços da organização.

    Get-MailUser | Set-MailUser -HiddenFromAddressListsEnabled $true

Este exemplo define a propriedade Company de todos os usuários de email como Contoso.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | Set-User -Company Contoso

Este exemplo define a propriedade CustomAttribute1 como um valor de ContosoEmployee de todos os usuários de email que possuem um valor Contoso na propriedade Company.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Contoso')}| Set-MailUser -CustomAttribute1 ContosoEmployee

## Como saber se funcionou?

Para verificar se as propriedades dos usuários de email foram alteradas com sucesso, faça o seguinte:

  - No EAC, selecione o usuário de email e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir a propriedade alterada.

  - No Shell, use os cmdlets **Get-User** e **Get-MailUser** para verificar as alterações. Uma vantagem de usar o Shell é que você pode exibir várias propriedades para vários contatos de email.
    
        Get-MailUser | Fl Name,CustomAttribute1 
    
    No exemplo acima em que a propriedade Company foi definida como Contoso em todos os contatos de email, execute o comando abaixo para verificar as alterações:
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | FL Name,Company
    
    No exemplo acima em que a propriedade CustomAttribute1 de todos os usuários de email foi definida como ContosoEmployee, execute o comando abaixo para verificar as alterações.
    
        Get-MailUser | Fl Name,CustomAttribute1 

## Editar usuários de email em massa

Você também pode usar o EAC para alterar as propriedades de vários usuários de email. Ao selecionar dois ou mais usuários de email na lista de contatos do EAC, as propriedades que podem ser editadas em massa são exibidas no painel Detalhes. Quando você alterar uma dessas propriedades, a alteração será aplicada a todos os destinatários selecionados.

Ao editar usuários de email em massa, é possível alterar as seguintes áreas de propriedade:

  - **Informações de Contato**   Altere propriedades compartilhadas, como rua, código postal e nome da cidade.

  - **Organization**   Altere propriedades compartilhadas como nome do departamento, nome da companhia e o gerente ao qual os contatos de email selecionados ou usuários de email se reportam.

## Usar o EAC para editar usuários de email em massa

1.  No EAC, navegue até **Destinatários** \> **Contatos**.

2.  Na lista de contatos, selecione dois ou mais usuários de email. Você não pode editar em massa uma combinação de contatos de email e usuários de email.
    

    > [!TIP]
    > Para selecionar vários contatos de email adjacentes, mantenha a tecla Shift pressionada, clique no primeiro usuário de email e, em seguida, clique no último usuário de email que você deseja editar. Você também pode selecionar vários usuários de email mantendo pressionada a tecla Ctrl e clicando em cada um que desejar editar.



3.  No painel Detalhes, em **Edição em Massa**, clique em **Atualizar**, em **Informações de Contato** ou **Organização**.

4.  Faça as alterações na página de propriedades e salve as alterações.

## Como saber se funcionou?

Para verificar se você executou com sucesso uma edição em massa dos usuários de email, siga uma destas opções:

  - No EAC, selecione cada um dos usuários de email nos quais deseja realizar uma edição em massa e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir as propriedades alteradas.

  - No Shell, use o cmdlet **Get-User** para verificar as alterações. Por exemplo, digamos que você tenha usado o recurso de edição em massa no EAC para alterar o gerente e o escritório de todos os usuários de email de uma empresa fornecedora chamada A. Datum Corporation. Para verificar essas alterações, você pode executar o seguinte comando no Shell:
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Adatum')} | fl Name,Office,Manager

## Usar a sincronização de diretórios para gerenciar usuários de email no Exchange Online

Esta seção oferece informações sobre o gerenciamento de usuários de email usando a sincronização de diretórios no Exchange Online. A sincronização de diretórios está disponível para clientes híbridos com caixas de correio hospedadas na nuvem e locais e para clientes do Exchange Online totalmente hospedados cujo Active Directory é local.


> [!TIP]
> Se você utilizar a sincronização de diretórios para gerenciar seus destinatários, ainda é possível adicionar e gerenciar usuários no Centro de administração do Office 365, porém eles não serão sincronizados com seu Active Directory local. Isso porque a sincronização de diretórios sincroniza apenas destinatários de seu Active Directory local com a nuvem.




> [!TIP]
> A sincronização de diretório é recomendada para uso com os seguintes recursos: 
> <UL>
> <LI>
> <P><STRONG>Listas de remetentes confiáveis e bloqueados do Outlook</STRONG>: quando sincronizadas com o serviço, essas listas terão precedência sobre a filtragem de spam. Isso permite que os usuários gerenciem suas próprias listas de remetentes confiáveis e bloqueados por usuário ou por domínio.</P>
> <LI>
> <P><STRONG>Bloqueio de Borda Baseado em Diretório (DBEB)</STRONG> Para mais informações sobre o DBEB, confira <A href="https://technet.microsoft.com/pt-br/library/dn600322(v=exchg.150)">Usar Bloqueio de Borda Baseado em Diretório para Rejeitar Mensagens Enviadas a Destinatários Inválidos</A>.</P>
> <LI>
> <P><STRONG>Quarentena de spam de usuário final</STRONG> Para acessar a quarentena de spam de usuários finais, os usuários finais devem ter uma ID de usuário e senha válidas no Office 365. Os clientes com caixas de correio locais devem ser usuários de email válidos.</P>
> <LI>
> <P><STRONG>Regras de transporte</STRONG> - Quando você usa a sincronização de diretórios, os usuários e grupos existentes do Active Directory são automaticamente carregados na nuvem e, em seguida, você pode criar regras de transporte destinadas a usuários e/ou grupos específicos sem precisar adicioná-los manualmente por meio do EAC ou pelo Windows PowerShell remoto. Observe que os <A href="https://go.microsoft.com/fwlink/?linkid=507569">grupos dinâmicos de distribuição</A> não podem ser sincronizados através da sincronização de diretório.</P></LI></UL>



**Antes de você começar**

Obtenha as permissões necessárias e prepare-se para a sincronização de diretórios, como descrito em [Preparar a sincronização de diretórios](https://go.microsoft.com/fwlink/p/?linkid=308908).

**Sincronizar diretórios de usuário**

1.  Ative a sincronização de diretórios, como descrito em [Ativar a sincronização de diretórios](https://go.microsoft.com/fwlink/p/?linkid=308909).

2.  Configure seu computador de sincronização de diretórios, como descrito em [Configurar o computador de sincronização de diretórios](http://go.microsoft.com/fwlink/p/?linkid=308911).

3.  Sincronize seus diretórios como descrito em [Usar o Assistente de Configuração para sincronizar diretórios](http://go.microsoft.com/fwlink/?linkid=308912).
    

    > [!IMPORTANT]
    > Após a conclusão do Assistente de Configuração da Ferramenta de Sincronização do Microsoft Azure Active Directory, a conta <STRONG>MSOL_AD_SYNC</STRONG> será criada em sua floresta do Active Directory. Esta conta é usada para ler e sincronizar suas informações do Active Directory local. Para que a sincronização de diretórios funcione corretamente, verifique se a porta TCP 443 em seu servidor de sincronização de diretórios local está aberta.



4.  Ative usuários sincronizados, como descrito em [Ative os usuários sincronizados](http://go.microsoft.com/fwlink/p/?linkid=308913).

5.  Gerencie a sincronização de diretórios, como descrito em [Gerenciar a sincronização de diretórios](http://go.microsoft.com/fwlink/p/?linkid=308915).

6.  Verifique se o Exchange Online está sincronizando corretamente. No EAC, vá para **Destinatários** \> **Contatos** e veja se a lista de usuários foi corretamente sincronizada com seu ambiente local.

