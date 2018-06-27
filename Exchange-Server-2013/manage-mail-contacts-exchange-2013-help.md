---
title: 'Gerenciar contatos de email: Exchange 2013 Help'
TOCTitle: Gerenciar contatos de email
ms:assetid: 74c72aed-e9ff-4927-8eb7-c08a86e79ae0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998858(v=EXCHG.150)
ms:contentKeyID: 50484734
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailContactWizardForm.NewMailContactIntroductionWizardPage
ms.translationtype: MT
---

# Gerenciar contatos de email

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2017-10-04_

Contatos de email são objetos do serviço de diretório habilitados para email que contêm informações sobre pessoas ou organizações que existem fora do Exchange e da organização do Exchange Online. Cada contato de email tem um endereço de email externo. Para saber mais sobre contatos de email, confira [Destinatários](recipients-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário", no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Criar um contato de email

## Usar o EAC para criar um contato de email

1.  No EAC, navegue até **Destinatários** \> **Contatos**.

2.  Clique em **Novo** ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") \> **Contato de email**.

3.  Preencha estas caixas na página **Novo contato de email**:
    
      - **Nome**   Use esta caixa para digitar o nome do contato.
    
      - **Iniciais**   Use esta caixa para digitar as iniciais do contato.
    
      - **Sobrenome**   Use esta caixa para digitar o sobrenome do contato.
    
      - **\*Nome para exibição**   Use esta caixa para digitar um nome para exibição do contato. Esse é o nome que fica na lista de contatos no EAC e no catálogo de endereços da empresa. Por padrão, essa caixa é preenchida com os nomes inseridos nas caixas **Nome**, **Iniciais** e **Sobrenome**. Se você não tiver usado essas caixas, ainda deverá digitar um nome nessa caixa, pois isso é obrigatório. O nome não pode exceder 64 caracteres.
    
      - **\* Nome**   Use essa caixa para digitar um nome para o contato. Esse é o nome que fica no serviço de diretório. Como acontece com o nome para exibição, essa caixa é preenchida por padrão com os nomes inseridos nas caixas **Nome**, **Iniciais** e **Sobrenome**. Se você não tiver usado essas caixas, ainda deverá digitar um nome nessa caixa, pois isso é obrigatório. O nome não pode exceder 64 caracteres.
    
      - **\* Alias** Use esta caixa para digitar um alias (64 caracteres ou menos) para o contato. Essa caixa é obrigatória.
    
      - **\* Endereço de email externo**   Use esta caixa para digitar a conta de email externa do contato. Essa caixa é obrigatória. O email enviado a esse contato é encaminhado para este endereço de email.
    
      - **Unidade organizacional**   É possível selecionar uma UO (unidade organizacional) que não seja a padrão, que é o escopo do destinatário. Se o escopo do destinatário estiver definido para a floresta, o valor padrão será definido para o contêiner Usuários no domínio que contém o computador no qual o EAC está sendo executado. Se o escopo do destinatário estiver definido como um domínio específico, por padrão, o contêiner Usuários desse domínio será selecionado. Se o escopo do destinatário estiver definido como uma UO específica, essa UO será selecionada por padrão.
        
        Para selecionar uma UO diferente, clique em **Procurar**. A caixa de diálogo exibe todas as OUs da floresta que estão no escopo especificado. Selecione a UO desejada e clique em **OK**.
        

        > [!TIP]
        > A caixa <STRONG>Unidade organizacional</STRONG> só está disponível no Exchange Server 2013. Ela não está disponível no Exchange Online.



4.  Ao concluir, clique em **Salvar**.

## Usar o Shell para criar um contato de email

Este exemplo cria um contato de email para Lara Cardoso no Exchange Server 2013.

    New-MailContact -Name "Debra Garcia" -ExternalEmailAddress dgarcia@tailspintoys.com -OrganizationalUnit Users

Este exemplo cria um contato de email para Davi Barros no Exchange Online.

    New-MailContact -Name "Alan Shen" -ExternalEmailAddress alans@fourthcoffee.com

Este exemplo habilita para email um contato existente chamado Clara Barbosa no Exchange Server 2013.

    Enable-MailContact -Identity "Karen Toh" -ExternalEmailAddress ktoh@tailspintoys.com

## Como saber se funcionou?

Para confirmar se você criou um contato de email, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Contatos**. O novo contato de email é exibido na lista de contatos. Em **Tipo de Contato**, o tipo é **Contato de email**.

  - No Shell, execute o comando a seguir para exibir informações sobre o novo contato de email.
    
        Get-MailContact <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## Propriedades de contato de email

## Usar o EAC para mudar as propriedades do contato de email

1.  No EAC, navegue até **Destinatários** \> **Contatos**.

2.  Na lista de contatos e usuários de email, clique no contato de email cujas propriedades você quer alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do contato de email, clique em uma destas seções para exibir ou alterar propriedades.
    
      - Geral
    
      - Contact Information
    
      - Organização
    
      - Opções de Email (não está disponível em Exchange Online)
    
      - Dica de Email

## Geral

Use a seção **Geral** para ver ou alterar as informações básicas sobre o contato de email.

  - **Nome**, **Iniciais**, **Sobrenome**

  - **\* Nome**   Esse é o nome que está listado em Active Directory. Se você alterar esse nome, não pode exceder 64 caracteres.

  - **\* Nome para exibição**   Esse nome será exibido no catálogo de endereços da sua organização, nas linhas Para: e na linha De: no email e na lista de Caixas de Correio. Esse nome não pode conter espaços vazios antes ou depois do nome para exibição.

  - **\* Alias**   Este é o alias do contato de email. Caso decida alterá-lo, ele deve ser único na organização e ter 64 caracteres ou menos.

  - **\* Endereço de email externo**   Este é o endereço SMTP principal e a conta de email externa do contato de email. O email enviado a esse contato é encaminhado para este endereço de email.

  - Clique em **Mais opções** para exibir a UO que contém a conta do contato de email. Você precisa usar Usuários e Computadores do Active Directory para mover o contato para uma UO diferente.

## Informações de contato

Use a seção **Informações de Contato** para exibir ou alterar as informações de contato do destinatário, como endereço de email e números de telefone. Estas informações são exibidas no catálogo de endereços.

## Organização

Use a seção **Organização** para registrar informações detalhadas sobre a função do contato de email na organização. Estas informações são exibidas no catálogo de endereços. Além disso, você pode criar um gráfico de organização virtual acessível por clientes de email como o Outlook.

  - **Título**   Use esta caixa para exibir ou alterar o título do contato.

  - **Departamento**   Use esta caixa para exibir ou alterar o departamento no qual o contato trabalha. Você pode usar essa caixa para criar condições de destinatário para os grupos de distribuição dinâmica e listas de endereços.

  - **Empresa**   Use esta caixa para exibir ou alterar a empresa na qual o contato trabalha. Você pode usar essa caixa para criar condições de destinatário para os grupos de distribuição dinâmica.

  - **Gerente**   Para adicionar um gerente, clique em **Procurar**. Em **Selecionar Gerente**, selecione uma pessoa e clique em **OK**.

  - **Funcionários subordinados**   Você não pode modificar essa caixa. Um *Funcionário subordinado* é um destinatário que se reporta a um gerente específico. Se você tiver especificado um gerente para o destinatário, esse destinatário será exibido como um funcionário subordinado nos detalhes da caixa de correio do gerente. Por exemplo, Carlos gerencia Laura e Vinícius, que são contatos de email, portanto, Carlos está especificado na caixa **Gerente** nas propriedades da organização para Laura e Vinícius e Laura e Vinícius aparecem na caixa **Funcionários subordinados** nas propriedades da caixa de correio de Carlos.

## Opções de Email

Use a seção **Opções de Email** para adicionar ou remover endereços proxy do contato de email ou para editar endereços proxy existentes. O endereço SMTP principal do contato de email também é exibido nesta seção, mas você não pode alterá-lo. Para alterá-lo, você tem que alterar o endereço de email externo do contato na seção **Geral**.


> [!TIP]
> A seção <STRONG>Opções de Email</STRONG> está disponível somente no Exchange Server 2013. Essa seção não está disponível em Exchange Online.



## Dica de Email

Use a seção **Dica de Email** para adicionar uma Dica de Email a fim de alertar os usuários de possíveis problemas antes que seja enviada uma mensagem a este destinatário. Uma Dica de Email é o texto exibido na Barra de Informações quando esse destinatário é adicionado às linhas Para, Cc ou Cco de uma nova mensagem de email.


> [!TIP]
> As Dicas de Email podem incluir marcas HTML, mas scripts não são permitidos. O comprimento de uma dica de email personalizada não pode exceder 175 caracteres exibidos. As marcas HTML não são contadas no limite.



## Usar o Shell para alterar as propriedades do contato de email

As propriedades de um contato de email são armazenadas no Active Directory e no Exchange. De modo geral, use os cmdlets **Get-Contact** e **Set-Contact** para exibir e alterar as propriedades das informações de contato e da organização. Use os cmdlets **Get-MailContact** e **Set-MailContact** para exibir ou alterar as propriedades relacionadas ao email, como endereços de email, a Dica de Email, atributos personalizados e se o contato está oculto das listas de endereços.

Para mais informações, consulte os seguintes tópicos:

  - [Get-Contact](https://technet.microsoft.com/pt-br/library/aa998258\(v=exchg.150\))

  - [Set-Contact](https://technet.microsoft.com/pt-br/library/bb124535\(v=exchg.150\))

  - [Get-MailContact](https://technet.microsoft.com/pt-br/library/bb124717\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/pt-br/library/aa995950\(v=exchg.150\))

Estes são alguns exemplos de como usar o Shell para alterar propriedades de contatos de email.

Este exemplo configura as propriedades Título, Departamento, Empresa e Gerente do contato de email Diogo Martins.

    Set-Contact "Kai Axford" _-Title Consultant -Department "Public Relations" -Company Fabrikam -Manager "Karen Toh"

Este exemplo define a propriedade CustomAttribute1 com um valor igual a PartTime para todos os contatos de email e os oculta do catálogo de endereços da organização.

    Get-MailContact | Set-MailContact -CustomAttribute1 PartTime -HiddenFromAddressListsEnabled $true

Este exemplo define a propriedade CustomAttribute15 com um valor igual a TemporaryEmployee para todos os contatos de email no departamento de relações públicas.

    Get-Contact -Filter "Department -eq 'Public Relations'" | Set-MailContact -CustomAttribute15 TemporaryEmployee

## Como saber se funcionou?

Para verificar se você alterou as propriedades com sucesso para um contato de email, faça o seguinte:

  - No EAC, selecione o contato de email e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para exibir a propriedade que você alterou.

  - No Shell, use os cmdlets **Get-Contact** e **Get-MailContact** para verificar as alterações. Uma vantagem de se usar o Shell é que você pode exibir várias propriedades de vários contatos de email. No exemplo acima, onde todos os contatos de email tinham a propriedade CustomAttribute1 definida como PartTime e estavam ocultos do catálogo de endereços, execute o comando a seguir para verificar as alterações.
    
        Get-MailContact | Fl Name,CustomAttribute1,HiddenFromAddressListsEnabled
    
    No exemplo acima onde o CustomAttribute15 foi definido para todos os contatos de email no departamento de Relações Públicas, execute o seguinte comando para verificar as alterações.
    
        Get-Contact -Filter "Department -eq 'Public Relations'" | Get-MailContact | FL Name,CustomAttribute15

## Editar em massa contatos de email

Você também pode usar o EAC para alterar as propriedades de vários contatos de email. Ao selecionar dois ou mais contatos na lista de contatos do EAC, as propriedades que podem ser editadas em massa são exibidas no painel Detalhes. Quando você alterar uma dessas propriedades, a alteração será aplicada a todos os destinatários selecionados.

Ao editar em massa contatos de email, você pode alterar as seguintes áreas de propriedades:

  - **Informações de Contato**   Altere propriedades compartilhadas, como rua, código postal e nome da cidade.

  - **Organization**   Altere propriedades compartilhadas como nome do departamento, nome da companhia e o gerente ao qual os contatos de email selecionados ou usuários de email se reportam.

## Usar o EAC para editar em massa contatos de email

1.  No EAC, navegue até **Destinatários** \> **Contatos**.

2.  Na lista de contatos, selecione dois ou mais contatos de email. Você não pode editar em massa uma combinação de contatos de email e usuários de email.
    

    > [!TIP]
    > Para selecionar vários contatos de email adjacentes, mantenha a tecla Shift pressionada, clique no primeiro contato de email e, em seguida, clique no último contato de email que você deseja editar. Você também pode selecionar vários contatos de email mantendo pressionada a tecla Ctrl e clicando em cada um que desejar editar.



3.  No painel Detalhes, em **Edição em Massa**, clique em **Atualizar**, em **Informações de Contato** ou **Organização**.

4.  Faça as alterações na página de propriedades e salve as alterações.

## Como saber se funcionou?

Para confirmar se você editou em massa contatos de email, siga um destes procedimentos:

  - No EAC, selecione cada um dos contatos de email que você editou em massa e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") pra exibir as propriedades que você alterou.

  - No Shell, use o cmdlet **Get-Contact** para verificar as alterações. Por exemplo, digamos que você tenha usado o recurso de edição em massa no EAC para alterar o gerente e o escritório de todos os contatos de email de uma empresa fornecedora chamada A. Datum Corporation. Para verificar essas alterações, você pode executar o seguinte comando no Shell.
    
        Get-Contact -ResultSize unlimited -Filter {(Company -eq 'Adatum')} | fl Name,Office,Manager


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="O ícone pequeno do LinkedIn Learning" alt="O ícone pequeno do LinkedIn Learning" /> <strong>Começando a usar o Office 365?</strong><br />
Descubra cursos em vídeo gratuitos para <a href="https://support.office.com/pt-br/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>, oferecidos pelo LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

