---
title: 'Gerenciar grupos dinâmicos de distribuição: Exchange Online Help'
TOCTitle: Gerenciar grupos dinâmicos de distribuição
ms:assetid: 8ef85d0a-41df-4b5c-b8e7-ca8d09c048ca
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123722(v=EXCHG.150)
ms:contentKeyID: 50484763
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDynamicGroupWizardForm.CreateDynamicGroupInformationWizardPage
ms.translationtype: HT
---

# Gerenciar grupos dinâmicos de distribuição

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Os grupos de distribuição dinâmicos são objetos de grupos do Active Directory habilitados para email que são criados para agilizar o envio em massa de mensagens de email e outras informações dentro de uma organização do Microsoft Exchange.

Ao contrário de grupos regulares de distribuição, que contêm um conjunto definido de membros, a lista de associações de grupos dinâmicos de distribuição é calculada sempre que uma mensagem é enviada a eles, com base nos filtros e nas condições que você define. Quando uma mensagem de email for enviada para um grupo dinâmico de distribuição, ela será entregue a todos os destinatários da organização que corresponderem aos critérios definidos para esse grupo.


> [!IMPORTANT]
> Um grupo dinâmico de distribuição inclui destinatários no Active Directory com valores de atributos que correspondam ao filtro. Se as propriedades de um destinatário forem modificadas para que correspondam ao filtro,&nbsp;esse destinatário poderá tornar-se inadvertidamente um membro do grupo e começar a receber mensagens enviadas para o grupo.&nbsp;Processos de configuração de contas consistentes e bem definidos reduzirão as chances desse problema acontecer.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 a 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos dinâmicos de distribuição" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Criar um grupo dinâmico de distribuição

## Usar o EAC para criar um grupo dinâmico de distribuição

1.  No EAC, navegue até **Destinatários**  \> **Grupos** \> **Novo** \> **Grupo dinâmico de distribuição**.

2.  
    
    Na página **Novo grupo dinâmico de distribuição**, preencha as seguintes caixas:
    
      - **\* Nome para exibição**   Use essa caixa para digitar o nome para exibição. Esse nome é exibido no catálogo de endereços compartilhado, na linha Para: quando um email é enviado a esse grupo e na lista Grupos do EAC. O nome para exibição é necessário e deve ser amigável para que as pessoas o reconheçam. Ele também deve ser exclusivo na floresta.
        

        > [!TIP]
        > A política de nomenclatura de grupo não é aplicada a grupos dinâmicos de distribuição.

    
      - **\* Alias**   Use essa caixa para digitar o nome do alias do grupo. O alias não pode exceder 64 caracteres e deve ser único na floresta. Quando um usuário digita o alias na linha Para: de uma mensagem de email, ele é convertido para o nome para exibição do grupo.
    
      - **Descrição**   Use essa caixa para descrever o grupo para que as pessoas saibam qual é o objetivo do grupo. Essa descrição é exibida no catálogo de endereços compartilhado.
    
      - **Unidade organizacional**   É possível selecionar uma UO (unidade organizacional) que não seja a padrão (que é o escopo do destinatário). Se o escopo do destinatário estiver definido para a floresta, o valor padrão será definido para o contêiner Usuários no domínio do Active Directory que contém o computador no qual o EAC está sendo executado. Se o escopo do destinatário estiver definido como um domínio específico, o contêiner Usuários desse domínio será selecionado por padrão. Se o escopo do destinatário estiver definido como uma UO específica, essa UO será selecionada por padrão.
        
        Para selecionar uma UO diferente, clique em **Procurar**. A caixa de diálogo exibe todas as OUs da floresta que estão no escopo especificado. Selecione a UO desejada e clique em **OK**.
    
      - **Proprietário**  Um proprietário de um grupo dinâmico de distribuição é opcional. Você pode adicionar proprietários, clicando em **Procurar** e selecionando usuários na lista.

3.  
    
    Use a seção **Membros** para especificar os tipos de destinatários do grupo e definir as regras que determinarão a associação. Selecione uma destas caixas:
    
      - **Todos os tipos de destinatários**   Escolha essa opção para enviar mensagens que atendam aos critérios definidos para esse grupo para todos os tipos de destinatários.
    
      - **Apenas estes tipos de destinatários**   As mensagens que atenderem aos critérios definidos para esse grupo serão enviadas para um ou mais dos seguintes tipos de destinatários:
        
          - **Usuários com caixas de correio do Exchange**   Marque essa caixa de seleção se você quiser incluir usuários que tenham caixas de correio do Exchange. Os usuários que têm caixas de correio do Exchange são os que têm uma conta de usuário no domínio e uma caixa de correio na organização do Exchange.
        
          - **Usuários com endereços de email externos**   Marque essa caixa de seleção se você quiser incluir usuários que tenham endereços de email externos. Os usuários que têm contas de email externas têm contas de domínio de usuário no Active Directory, mas usam contas de email externas à organização. Isso permite que eles sejam incluídos na GAL (Lista de Endereços Global) e adicionados às listas de distribuição.
        
          - **Caixas de correio de recursos**   Marque essa caixa de seleção se você quiser incluir as caixas de correio de recursos do Exchange. As caixas de correio de recurso permitem administrar os recursos da empresa por meio de uma caixa de correio, como uma sala de conferências ou um veículo da empresa.
        
          - **Contatos com endereços de email externos**   Marque essa caixa de seleção se você quiser incluir contatos que tenham endereços de email externos. Contatos que tenham endereços de email externos não terão contas de domínio de usuário no Active Directory, mas o endereço externo de email estará disponível no GAL.
        
          - **Grupos habilitados para email**   Marque essa caixa de seleção se você quiser incluir os grupos de segurança ou de distribuição que foram habilitados para email. Os grupos habilitados para email são semelhantes aos grupos de distribuição. Os emails enviados a uma conta de grupo habilitada para email serão entregues a vários destinatários.

4.  
    
    Clique em **Adicionar uma regra**, para definir o critério de associação ao grupo.

5.  Selecione um destes atributos de destinatário, na lista suspensa, e informe um valor. Se o valor do atributo selecionado corresponder ao valor que você definir, o destinatário receberá uma mensagem enviada para esse grupo.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Atributo</th>
    <th>Enviar mensagem para um destinatário se...</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Contêiner de destinatário</strong></p></td>
    <td><p>O objeto de destinatário reside no domínio ou OU especificada.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Estado ou província</strong></p></td>
    <td><p>O valor especificado corresponde à propriedade estado ou província do destinatário.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Empresa</strong></p></td>
    <td><p>O valor especificado corresponde à propriedade Empresa do destinatário.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Departamento</strong></p></td>
    <td><p>O valor especificado corresponde à propriedade Departamento do destinatário.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Custom attributeN</strong> (em que N é um número de 1 a 15)</p></td>
    <td><p>O valor especificado corresponde à propriedade CustomAttributeN do destinatário.</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!IMPORTANT]
    > Os valores inseridos para o atributo selecionado devem corresponder exatamente aos valores exibidos nas propriedades do destinatário. Por exemplo, se você inserir <STRONG>Minas Gerais</STRONG> em <STRONG>Estado ou província</STRONG>, mas o valor da propriedade do destinatário for <STRONG>MG</STRONG>, a condição não será atendida. Além disso, os valores baseados em texto que você especificar não diferenciam maiúsculas de minúsculas. Por exemplo, se você especificar <STRONG>Contoso</STRONG> para o atributo <STRONG>Empresa</STRONG>, as mensagens serão enviadas para um destinatário que tiver esse valor como <STRONG>contoso</STRONG>.



6.  Na janela **Especificar palavras ou frases**, digite o valor na caixa de texto. Clique em **Adicionar** e, em seguida, clique em **OK**.

7.  Para adicionar outra regra para definir o critério de associação, clique em **Adicionar uma regra** na tela anterior que você criou.
    

    > [!IMPORTANT]
    > Se você adicionar várias regras para definir a associação, um destinatário deverá atender aos critérios de cada regra, para receber uma mensagem enviada para o grupo. Em outras palavras, cada regra é conectada com o operador booliano <STRONG>E</STRONG>.



8.  Quando você tiver terminado, clique em **Salvar** para criar o grupo dinâmico de distribuição.


> [!TIP]
> Se você quiser especificar regras para atributos que não sejam os disponíveis no EAC, você deverá usar o Shell, para criar um grupo de distribuição dinâmico. Tenha em mente que as configurações de filtro e condições dos grupos dinâmicos de distribuição que tenham filtros de destinatário personalizados só podem ser gerenciados usando o Shell. Para ver um exemplo de como criar um grupo dinâmico de distribuição com uma consulta personalizada, confira a próxima seção sobre como usar o Shell para criar um grupo dinâmico de distribuição.



## Usar o Shell para criar um grupo dinâmico de distribuição

Este exemplo cria o grupo dinâmico de distribuição "Mailbox Users DDG" que contém apenas usuários de caixa de correio.

    New-DynamicDistributionGroup -IncludedRecipients MailboxUsers -Name "Mailbox Users DDG" -OrganizationalUnit Users

Este exemplo cria um grupo dinâmico de distribuição com um filtro de destinatários personalizado. O grupo dinâmico de distribuição contém todos os usuários de caixa de correio em um servidor chamado Server1.

    New-DynamicDistributionGroup -Name "Mailbox Users on Server1" -OrganizationalUnit Users -RecipientFilter {((RecipientTypeDetails -eq 'UserMailbox' -and ServerName -eq 'Server1'))}

Este exemplo cria um grupo dinâmico de distribuição com um filtro de destinatários personalizado. O grupo dinâmico de distribuição contém todos os usuários de caixa de correio que têm um valor "FullTimeEmployee", na propriedade **CustomAttribute10**.

    New-DynamicDistributionGroup -Name "Full Time Employees" -RecipientFilter {(RecipientTypeDetails -eq 'UserMailbox') -and (CustomAttribute10 -eq 'FullTimeEmployee')}

Para informações detalhadas sobre sintaxes e parâmetros, confira [New-DynamicDistributionGroup](https://technet.microsoft.com/pt-br/library/bb125127\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou com êxito um grupo dinâmico de distribuição, siga um destes procedimentos:

  - Na EAC, navegue até **Destinatários**  \> **Grupos**. O novo grupo dinâmico de distribuição é exibido na lista de grupos. Em **Tipo de Grupo**, o tipo é **Grupo dinâmico de distribuição**.

  - No Shell, execute o seguinte comando para mostrar informações sobre o novo grupo dinâmico de distribuição.
    
        Get-DynamicDistributionGroup | FL Name,RecipientTypeDetails,RecipientFilter,PrimarySmtpAddress

## Alterar propriedades do grupo dinâmico de distribuição

## Usar o EAC para configurar propriedades do grupo dinâmico de distribuição

1.  Na EAC, navegue até **Destinatários** \> **Grupos**.

2.  Na lista de grupos, clique no grupo dinâmico de distribuição que você deseja exibir ou alterar, e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do grupo, clique em uma destas seções para exibir ou alterar propriedades.
    
      - Geral
    
      - Propriedade
    
      - Associação
    
      - Gerenciamento de entregas
    
      - Aprovação de mensagem
    
      - Opções de email
    
      - Dica de Email
    
      - Delegação de grupo

## Geral

Use essa seção para visualizar ou alterar informações básicas sobre o grupo.

  - **\* Nome para exibição**   Este nome será exibido no catálogo de endereços, na linha Para: quando um email é enviado a esse grupo e na lista Grupos. O nome para exibição é necessário e deve ser amigável para que as pessoas o reconheçam. Ele também deve ser exclusivo em seu domínio.

  - **\* Alias**   É a parte do endereço de email que aparece à esquerda do símbolo de arroba (@). Se você alterar o alias, o endereço SMTP principal do grupo também será alterado e conterá o novo alias. Além disso, o endereço de email com o alias anterior será mantido como um endereço proxy para o grupo.

  - **Descrição**   Use essa caixa para descrever o grupo, para que as pessoas saibam qual é o objetivo do grupo. Essa descrição é exibida no catálogo de endereços e no painel Detalhes do EAC.

  - **Ocultar este grupo das listas de endereços**   Marque essa caixa de seleção se não desejar que usuários vejam esse grupo no catálogo de endereços. Para enviar um email a esse grupo, um remetente deve digitar o endereço de email ou alias do grupo na linha Para: ou Cc:, .

  - **Unidade organizacional**   Esta caixa somente leitura exibe a unidade organizacional (UO) que contém o grupo dinâmico de distribuição. Você precisa usar Usuários e Computadores do Active Directory para mover o grupo para uma UO diferente.

## Propriedade

Use esta seção para atribuir um proprietário ao grupo. Um grupo dinâmico de distribuição pode ter um único proprietário. O proprietário do grupo aparece na guia **Gerenciado por** do objeto, em Usuários e Computadores do Active Directory.

Você pode adicionar proprietários, clicando em **Procurar** e selecionando o proprietário na lista. Para remover o proprietário, clique em **Limpar** e em **Salvar**.![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

## Associação

Use essa seção para alterar os critérios usados para determinar a associação ao grupo. Você pode excluir ou alterar as regras de associação existentes e adicionar novas regras. Para procedimentos que mostram como você pode fazer isso, confira a Usar o EAC para criar um grupo dinâmico de distribuição nos procedimentos para configurar a associação quando você usar o EAC para criar um novo grupo dinâmico de distribuição.

## Gerenciamento de entregas

Use essa seção para gerenciar quem pode enviar emails a esse grupo.

  - **Apenas os remetentes da minha organização**   Selecione esta opção para permitir que apenas os remetentes de sua organização enviem mensagens ao grupo. Isso significa que, se alguém fora de sua organização enviar uma mensagem de email a esse grupo, ela será rejeitada. Essa é a configuração padrão.

  - **Remetentes de dentro e de fora da minha organização**   Selecione esta opção para permitir que qualquer pessoa envie mensagens ao grupo.
    
    É possível limitar ainda mais as pessoas que podem enviar mensagens ao grupo permitindo que apenas remetentes específicos enviem mensagens a esse grupo. Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e selecione um ou mais destinatários. Se você adicionar remetentes a essa lista, eles serão os únicos que poderão enviar email ao grupo. Os emails enviados por qualquer pessoa que não estiver na lista serão rejeitados.
    
    Para remover uma pessoa ou grupo da lista, selecione-o na lista e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").
    

    > [!IMPORTANT]
    > Se você tiver configurado o grupo para permitir que apenas os remetentes de dentro de sua organização enviem mensagens ao grupo, os emails enviados por um contato externo serão rejeitados, mesmo que ele seja adicionado a essa lista.



## Aprovação de mensagem

Use esta seção para configurar opções para moderar o grupo. Os moderadores aprovam ou rejeitam as mensagens enviadas ao grupo antes que elas cheguem aos membros do grupo.

  - **As mensagens enviadas a esse grupo devem ser aprovadas por um moderador**   Por padrão, essa caixa de seleção não está marcada. Se você marcar esta caixa de seleção, as mensagens de entrada serão verificadas pelos moderadores do grupo antes da entrega. Os moderadores do grupo podem aprovar ou rejeitar as mensagens de entrada.

  - **Moderadores do grupo**   Para adicionar moderadores do grupo, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para remover um moderador, selecione-o e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover"). Se você selecionou "As mensagens enviadas a este grupo devem ser aprovadas por um moderador" e não selecionou um moderador, as mensagens para o grupo serão enviadas aos proprietários do grupo para aprovação.

  - **Remetentes que não exigem aprovação de mensagem**    Para adicionar pessoas ou grupos que podem ignorar a moderação para o grupo em questão, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para remover uma pessoa ou um grupo, selecione o item e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

  - **Selecionar notificações de moderação   **Use esta seção para definir como os usuários serão notificados sobre a aprovação de mensagens.
    
      - **Notificar todos os remetentes quando suas mensagens não forem aprovadas**   Esta é a configuração padrão. Notifique todos os remetentes dentro e fora da sua organização quando as mensagens deles não forem aprovadas.
    
      - **Notificar remetentes da organização apenas quando as mensagens não forem aprovadas**   Se esta opção for selecionada, somente pessoas ou grupos da sua organização serão notificados quando uma mensagem enviada por eles ao grupo não for aprovada por um moderador.
    
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

Use esta seção para adicionar uma Dica de Email a fim de alertar os usuários sobre possíveis problemas antes de eles enviarem uma mensagem a esse grupo. Uma Dica de Email é o texto exibido na barra de informações quando esse grupo é adicionado às linhas Para, Cc ou Cco de uma nova mensagem de email. Por exemplo, você poderia acrescentar uma dica de email a grupos grandes para advertir remetentes potenciais de que a sua mensagem será enviada a muitas pessoas.


> [!TIP]
> As Dicas de Email podem incluir marcas HTML, mas scripts não são permitidos. O comprimento de uma dica de email personalizada não pode exceder 175 caracteres exibidos. As marcas HTML não são contadas no limite.



## Delegação de grupo

Use essa seção para atribuir permissões a um usuário (chamado de *delegar*) para permitir que eles enviem mensagens como o grupo ou enviar mensagens em nome do grupo. É possível atribuir as seguintes permissões:

  - **Enviar como**   Essa permissão permite que o representante envie mensagens como o grupo. Depois que essa permissão for atribuída, o representante tem a opção de adicionar o grupo na linha **De** para indicar que a mensagem foi enviada pelo grupo.

  - **Enviar em Nome de**   Essa permissão também permite que um representante envie mensagens em nome do grupo. Depois que essa permissão for atribuída, o representante terá a opção de adicionar o grupo na linha **De**. Vai parecer que a mensagem foi enviada pelo grupo e será indicado que ela foi enviada pelo representante em nome do grupo.

Para atribuir permissões a representantes, clique em **Adicionar** na permissão apropriada para exibir a página **Selecionar Destinatário**, que exibe uma lista de todos os destinatários na sua organização do Exchange que podem receber a permissão. Selecione os destinatários que deseja, adicione-os à lista e clique em **OK**. Você também pode pesquisar um destinatário específico, digitando seu nome na caixa de pesquisa e clicando em **Pesquisar**.

## Usar o Shell para configurar propriedades do grupo dinâmico de distribuição

Use os cmdlets **Get-DynamicDistributionGroup** e **Set-DynamicDistributionGroup** para exibir e alterar propriedades dos grupos dinâmicos de distribuição. As vantagens de se usar o Shell são a possibilidade de alterar as propriedades que não estão disponíveis no EAC e alterar as propriedades de vários grupos. Para obter informações sobre que parâmetros correspondem às propriedades dos grupos de distribuição, confira estes tópicos:

  - [Get-DynamicDistributionGroup](https://technet.microsoft.com/pt-br/library/bb124762\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/pt-br/library/bb123796\(v=exchg.150\))

Eis alguns exemplos de como usar o Shell para alterar as propriedades do grupo dinâmico de distribuição.

Este exemplo altera os parâmetros seguintes para todos os grupos dinâmicos de distribuição na organização:

  - Ocultar todos os grupos dinâmicos de distribuição do catálogo de endereços

  - Defina o tamanho de mensagem máximo que pode ser enviado ao grupo como 5 MB

  - Habilitar a moderação

  - Atribuir o administrador como o moderador do grupo

<!-- end list -->

    Get-DynamicDistributionGroup -ResultSize unlimited | Set-DynamicDistributionGroup -HiddenFromAddressListsEnabled $true -MaxReceiveSize 5MB -ModerationEnabled $true -ModeratedBy administrator

Este exemplo adiciona o endereço de email SMTP de proxy Seattle.Employees@contoso.com ao grupo All Employees.

    Set-DynamicDistributionGroup -Identity "All Employees" -EmailAddresses SMTP:All.Employees@contoso.com, smtp:Seattle.Employees@contoso.com

## Como saber se funcionou?

Para verificar se você alterou com êxito as propriedades de um grupo dinâmico de distribuição, siga um destes procedimentos:

  - No EAC, selecione o grupo e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir a propriedade ou recurso que você alterou. Dependendo da propriedade que você tiver alterado, ela poderá ser exibida no painel Detalhes do grupo selecionado.

  - No Shell, use o cmdlet **Get-DynamicDistributionGroup** para verificar as alterações. Uma vantagem de se usar o Shell é que você pode exibir várias propriedades de vários grupos. No primeiro exemplo, execute o comando abaixo para verificar o novo valor.
    
        Get-DynamicDistributionGroup -ResultSize unlimited | fl Name,HiddenFromAddressListsEnabled,MaxReceiveSize,ModerationEnabled,ModeratedBy
    
    Para o exemplo acima onde os limites da mensagem foram alterados, execute este comando.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

