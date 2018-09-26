---
title: 'Cenário: Implantando políticas de catálogo de endereços: Exchange 2013 Help'
TOCTitle: 'Cenário: Implantando políticas de catálogo de endereços'
ms:assetid: 6ac3c87d-161f-447b-afb2-149ae7e3f1dc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657455(v=EXCHG.150)
ms:contentKeyID: 50485887
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cenário: Implantando políticas de catálogo de endereços

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

## Cenários de implantação

Os três cenários a seguir descrevem possíveis soluções de implantação para três diferentes tipos de organizações. Apesar de haver muito mais cenários, os mais populares são cobertos aqui. As listas de endereços e as listas globais de endereços (GALs) nesses cenários foram criadas com base em filtros, como Atributos Personalizados, que agrupavam os objetos logicamente.

## Cenário 1: Duas companhias separadas - uma organização do Exchange

Esse cenário é aplicável a agências, divisões ou departamentos governamentais que compartilham a infraestrutura, mas nenhuma cadeia hierárquica e nenhum empregado em comum. Além disso, as divisões não têm nenhuma preocupação especial de segurança ou privacidade. Nesse cenário, duas políticas de catálogo de endereços (ABPs) são criadas, em que os funcionários podem ver somente membros da mesmas organização, quando exibem a GAL ou examinam a associação de outros grupos de distribuição. Além disso, nenhum usuário será membro dos grupos de distribuição que abrangem a organização inteira.

![Políticas de Catálogo de Endereços com duas empresas distintas](images/JJ657455.b4fc82da-a659-4ade-ba33-d55d90dcf204(EXCHG.150).gif "Políticas de Catálogo de Endereços com duas empresas distintas")

As ABPs Contoso e Humungous Insurance foram criadas usando-se as seguintes listas de endereços, listas de endereços globais, listas de salas e OABs, que foram criadas usando-se um filtro de destinatário que agrupou os objetos com um filtro como Atributo Personalizado. Como as duas empresas são separadas sem qualquer interação entre si, não há nenhuma lista de endereços em comum.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Contoso</p></td>
<td><p>Humungous Insurance</p></td>
</tr>
<tr class="even">
<td><p>Listas de Endereços</p></td>
<td><p>AL_CON_Groups</p>
<p>AL_CON_Users</p>
<p>AL_CON_Contacts</p></td>
<td><p>AL_HI_Groups</p>
<p>AL_HI_Users</p>
<p>AL_HI_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>Lista de endereços global</p></td>
<td><p>GAL_CON</p></td>
<td><p>GAL_HI</p></td>
</tr>
<tr class="even">
<td><p>Lista de endereços de sala</p></td>
<td><p>AL_CON_Rooms</p></td>
<td><p>AL_HI_Rooms</p></td>
</tr>
<tr class="odd">
<td><p>OAB (catálogo de endereços offline)</p></td>
<td><p>OAB_CON</p></td>
<td><p>OAB_HI</p></td>
</tr>
</tbody>
</table>


## Cenário 2: Duas companhias compartilhando um CEO

Nesse cenário, Fabrikam e Tailspin Toys compartilham a mesma organização do Exchange e o mesmo CEO. O CEO é a única pessoa comum entre as duas empresas. Esse cenário requer três ABPs com as seguintes características:

  - Os usuários em Tailspin Toys podem ver somente usuários da Tailspin Toys quando navegam pela GAL.

  - Os usuários em Fabrikam podem ver somente usuários da Fabrikam quando navegam pela GAL.

  - Em cada companhia, há um grupo de distribuição SeniorLeaders que inclui os líderes sêniores da companhia e o CEO.

  - Os usuários que olharem na associação de grupo do CEO irão ver apenas grupos que pertencem à companhia do usuário. Eles não vêem grupos que não estejam em sua própria empresa.

  - Três ABPs são criadas: **Fab**, **Tail** e **CEO**.

![Duas Empresas, um CEO](images/JJ657455.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "Duas Empresas, um CEO")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Fabrikam</p></td>
<td><p>Tailspin Toys</p></td>
<td><p>CEO</p></td>
</tr>
<tr class="even">
<td><p>Listas de endereços</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p></td>
<td><p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p>
<p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>Lista de endereços global</p></td>
<td><p>GAL_FAB</p></td>
<td><p>GAL_TAIL</p></td>
<td><p>GAL padrão</p></td>
</tr>
<tr class="even">
<td><p>Lista de endereços de sala</p></td>
<td><p>AL_FAB_Rooms</p></td>
<td><p>AL_TAIL_Rooms</p></td>
<td><p>Padrão todos os quartos</p></td>
</tr>
<tr class="odd">
<td><p>OAB (catálogo de endereços offline)</p></td>
<td><p>OAB_FAB</p></td>
<td><p>OAB_TAIL</p></td>
<td><p>OAB Padrão</p></td>
</tr>
</tbody>
</table>


Quando o CEO é adicionado aos grupos de distribuição em cada organização e fica dentro do escopo do ABP de cada companhia, o CEO se torna visível para as companhias. O CEO pode criar grupos de distribuição que abrangem as duas companhias e ficam visíveis dentro da GAL de cada companhia, mas os membros do grupo de distribuição poderão apenas ver os membros do grupo que estão dentro de suas organizações.

## Cenário 3: Educação

Esse cenário é aplicável a escolas ou universidades em que uma divisão de salas de aula é necessária para garantir a privacidade dos alunos. O cenário Educação tem as seguintes características:

  - Os alunos de cada classe podem ver somente outros alunos de suas turmas, seu professor e o diretor.

  - Professores podem ver apenas alunos em suas próprias salas de aula.

  - Professores podem ver todos os outros professores e o diretor.

  - Os grupos de distribuição são criados para os pais dos alunos de cada classe e a faculdade.

![Cenário Educacional das Políticas de Catálogo de Endereços](images/JJ657455.435f3b1a-9752-4c61-ab8a-80115c643d12(EXCHG.150).gif "Cenário Educacional das Políticas de Catálogo de Endereços")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Students_ClassA</p></td>
<td><p>Teachers_ClassA</p></td>
<td><p>Diretor da escola</p></td>
</tr>
<tr class="even">
<td><p>Listas de Endereços</p></td>
<td><p>AL_ClassAAL_Principal</p></td>
<td><p>AL_ClassAAL_AllTeachersAL_AllGroupsAL_Principal</p></td>
<td><p>AL_ClassA</p>
<p>AL_ClassB</p>
<p>AL_AllTeachers</p>
<p>AL_AllStudents</p>
<p>AL_AllGroups</p></td>
</tr>
<tr class="odd">
<td><p>Lista de endereços global</p></td>
<td><p>GAL_StudentsClassA</p></td>
<td><p>GAL_TeachersClassA</p></td>
<td><p>GAL_Everyone</p></td>
</tr>
<tr class="even">
<td><p>Lista de endereços de sala</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>Padrão todos os quartos</p></td>
</tr>
<tr class="odd">
<td><p>OAB (catálogo de endereços offline)</p></td>
<td><p>OAB_StudentsClassA</p></td>
<td><p>OAB_TeachersClassA</p></td>
<td><p>OAB Padrão</p></td>
</tr>
</tbody>
</table>


## Considerações e boas práticas

Considere o seguinte ao usar ABPs em sua organização:

  - Para que os ABPs funcionem corretamente, a caixa de correio do usuário na qual você aplica o ABP deve estar em um servidor Exchange 2010 SP3 ou Exchange 2013.

  - Não execute a função de servidor do Acesso para Cliente do Exchange 2010 no servidor de catálogo global. Ao fazê-lo o Active Directory é usado para o Name Service Provider Interface (NSPI) ao invés do serviço de Catálogo de Endereços do Microsoft Exchange. Você pode executar as funções de servidor do Exchange 2013 em um servidor de catálogo global e fazer com que os ABPs funcionem corretamente, entretanto não recomendamos instalar o Exchange em um controlador de domínio.

  - Você não pode usar catálogos de endereço hierárquicos (HABs) e ABPs simultaneamente. Para saber mais, consulte [Catálogos de endereços hierárquicos](https://docs.microsoft.com/pt-br/exchange/address-books/hierarchical-address-books/hierarchical-address-books).

  - Qualquer usuário atribuído com um ABP deve existir na sua própria GAL.

  - Se você permitir que aplicações do cliente acessem o Active Directory diretamente através de LDAP, elas irão ignorar a lógica embutida no ABPs. Pelo fato de o Outlook para Mac 2011 e o Entourage 2008 usarem consultas diretas de LDAP para acessar o Active Directory, estas aplicações de cliente não funcionarão adequadamente com ABPs se um controlador de domínio ou um servidor de catálogo global for especificado ou fornecido para os mesmos pelo serviço Autodiscover. O Outlook para Mac 2011 pode usar EWS ou um OAB local para acessar as informações do diretório. Entretanto, se o Outlook para Mac 2011 pode acessar diretamente um serviço LDAP, ele tentará fazer isso.

  - A GAL usada no ABP deve conter, pelo menos, todas as listas de endereço, incluindo a lista de endereços de sala, definida e especificada em um ABP. Não crie uma GAL que contenha menos objetos do que qualquer uma das listas de endereço no mesmo ABP.

  - Recomendamos a criação de grupos de distribuição que não cruzem fronteiras virtuais da organização. A criação de grupos de distribuição que contenham membros de várias organizações virtuais causa os seguintes problemas:
    
      - Se os membros do grupo solicitarem confirmação de leitura ou entrega ao enviar email para o grupo de distribuição, eles serão capazes de ver os endereços de email dos membros do grupo em outras organizações virtuais
    
      - Se uma mensagem criptografada for enviada para o grupo de distribuição e alguns membros do grupo de distribuição não tiverem IDs digitais válidas, o remetente receberá uma mensagem de aviso que inclui o número total de membros que não possuem IDs válidas e uma lista dos endereços de email. Entretanto, se alguns destes membros sem IDs digitais válidas estiverem em uma organização diferente daquela do remetente, a mensagem de aviso incluirá a contagem correta mas não incluirá os endereços de email dos membros na outra organização. Como resultado, a contagem total não corresponderá à lista dos endereços do membro.
        
        Por exemplo, digamos que um grupo de distribuição contenha cinco membros de duas organizações no total, Agência e Agência B. Três membros do grupo são da Agência A e um destes membros possui uma ID digital inválida. Os outros dois membros são da Agência B, e ambos possuem IDs digitais inválidas. Se um membro da Agência A envia uma mensagem critografada para o grupo de distribuição, esse membro receberá uma mensagem de aviso dizendo que existe um total de três remetentes sem IDs digitais válidas. Entretanto, apenas o endereço de email para o destinatário da Agência A será listado na mensagem de aviso.
    
      - ABP's não se aplicam aos cmdlets **Get-Group** . Portanto, qualquer usuário ou processo que seja capaz de executar **Get-Group** enxergará todos os membros de qualquer grupo ao qual eles tenham acesso.
        
        Recomendamos a alteração das configurações de gerenciamento de gruo nas Opções de OWA para que os usuários não possam usar o Outlook Web App para gerenciar grupos. Para impedir que os usuários façam uso das Opções de OWA para gerenciar grupos, exclua os usuários da função de RBAC MyDistributionGroupMembership. Para obter detalhes, consulte [Função MyDistributionGroupMembership](mydistributiongroupmembership-role-exchange-2013-help.md).
    
      - Se você permitir que os usuários façam uso do Outlook ou do Outlook Web App para gerenciar grupos, os proprietários do grupo devem ter visibilidade completa da lista de associação do grupo.

  - Todos os ABPs devem conter uma lista de endereço de sala. Entretanto, se a sua organização não usa listas de endereço de sala, você pode criar uma lista vazia padrão de endereço de sala.

  - Implantar ABP's não impede que os usuários em uma organização vritual enviem email para usuários em outra organização virtual. Se você quiser impedir que os usuários enviem email para as organizações, recomendamos a criação de uma regra de transporte. Por exemplo, para criar uma regra de transporte que impeça que os usuários da Contoso recebam menssagens de usuários da Fabrikam, mas que ainda permita que a equipe de liderança sênior da Fabrikam envie mensagem para usuários da Contoso, execute o seguinte Shell de comando:
    
    ```powershell
      New-TransportRule -Name "StopFabrikamtoContosoMail" -FromMemberOf "AllFabrikamEmployees" -SentToMemberOf "AllContosoEmployees" -DeleteMessage -ExceptIfFrom seniorleadership@fabrikam.com
    ```

  - Se você deseja impor um recurso semelhante a ABP no cliente Lync, você pode definir o atributo `msRTCSIP-GroupingID` nos objetos de usuário específico. Para obter informações detalhadas, consulte o tópico de [PartitionByOU substituído por msRTCSIP-GroupingID](https://go.microsoft.com/fwlink/p/?linkid=232306) .

## Etapas gerais de implantação

## Migrar de segmentação de lista de endereços para ABPs

Se sua organização configurado a solução de segregação de lista de endereços Exchange 2007 no local, usando as instruções no white paper [Configurando Virtual organizações e segregação de lista de endereços no Exchange 2007](https://go.microsoft.com/fwlink/p/?linkid=109601), você deve primeiro migrar para o Exchange Server 2010 usando as etapas descritas em [migrar para políticas de catálogo de endereços do Exchange Server 2010 de segregação de lista de endereços do Exchange Server 2007](https://go.microsoft.com/fwlink/p/?linkid=235967). Esse procedimento exigirá algum tempo de inatividade para a sua organização e, portanto, você precisará planejar adequadamente.

## Nova implantação de ABPs

Se a sua organização estiver implantando ABPs do Exchange 2013 e não tiver usado a segregação de lista de endereços do Exchange 2007, você poderá usar essas instruções para implantar ABPs na sua organização.

O passo a passo desta seção acompanhará através do Cenário 2: Two companies sharing a CEO. Neste cenário, duas empresas (Fabrikam e Tailspin Toys) são separadas mas compartilham um CEO e uma equipe de liderança sênior.

## Etapa 1: Instale e configure o agente de Roteamento de Política do Catálogo de Endereço

Se você estiver usando ABPs e não quiser que os usuários em organizações virtuais separadas visualizem as informações potencialmente particulares uns dos outros, poderá ativar o Agente de Roteamento da Política de Catálogo de Endereços. O agente de Roteamento de Política de Catálogo de Endereço é um agente de Transporte que roda no servidor da Caixa de Correio e que controla como os destinatários são tratados na organização. Quando o Agente de Roteamento de Política de Catálogo de Endereço é instalado e configurado, os usuários que são atribuídos com diferentes GALs aparecem como destinatários externos de forma que eles não podem ver os cartões de contato dos destinatários externos.

Para instruções detalhadas, consulte [Instalar e configurar o agente de roteamento de política de catálogo de endereços](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md).

## Etapa 2: Dividir suas organizações virtuais

Você não precisa desenvolver um jeito de dividir suas organizações. Recomendamos usar a propriedade CustomAttribute1-15 nas caixas de correio, contatos e grupos, em vez de atributos condicionais preparados anteriormente, como Companhia, Departamento ou StateOrProvince, para dividir as organizações virtuais, pelas seguintes razões:

  - Nem todos os tipos de destinatários dos objetos têm atributos condicionais preparados anteriormente no Active Directory. Por exemplo, Grupo de Distribuição de Grupo Dinâmico de Distribuição não suportam os atributos de companhia, departamento ou estado.

  - Nem todos os atributos condicionais predefinidos são expostos nos cmdlets para alguns destinatários. Por exemplo, os parâmetros *Company*, *department* e *StateOrProvince* não estão disponíveis no que é exposto pelos cmdlets para usuários de email, contatos, grupos de distribuição ou pastas públicas habilitadas para email.

  - Vários cmdlets são necessários para segregar destinatários, quando você usar o atributo condicional preparado anteriormente. Por exemplo, você precisa executar Set-User para marcar *Company*, *Department*, *StateOrProvince* para uma UserMailbox após executar os cmdlets **New-Mailbox** ou **Set-Mailbox**.

  - Os parâmetros *CustomAttributeX* são todos expostos no cmdlet Set-\* para cada tipo de destinatário. Podemos concluir toda a segregação desse tipo através de um único cmdlet Set-

  - Os atributos CustomAttributeX são reservados explicitamente para a personalização de uma organização e estão totalmente sobre o controle dos administradores da organização.

Outra melhor prática é considerar a implementação quando segregar sua organização é usar identificadores de companhia nos nomes dos grupos de distribuição e nos grupos dinâmicos de distribuição. O Exchange tem um recurso de política de Nomeação de Grupos que irá adicionar automaticamente um sufixo ou prefixo ao nome do grupo de distribuição com base em vários atributos do usuário que criar o grupo de distribuição, incluindo o criador de Companhia, StateorProvince, Cargo e CustomAttribute1 a CustomAttribute15. A política de nomeação de grupo é especialmente importante, se você estiver permitindo que os usuários criem seus próprios grupos de distribuição. Para mais informações, consulte [Criar um diretiva de nomeação de grupo de distribuição](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy).

As políticas de nomeação de grupos não se aplicam a grupos dinâmicos de distribuição, então, você precisará segregá-los e aplicar uma política de nomeação manualmente.

## Etapa 3: Criar as listas de endereços, GALs e OABs

Quando você cria as listas de endereços e listas de endereços globais, não use parâmetros "IncludedRecipient" e "ConditionalX", como ConditionalCompany e ConditionalCustomAttribute5. Você deve usar um filtro de destinatário, em vez disso. Você deve usar o Shell para criar filtros de destinatário. Para mais informações sobre Filtros de Destinatários, consulte [Filtragem de destinatário nos servidores de Transporte de Borda](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).

Ao criar o ABP, você irá criar várias listas de endereços, com base em como você deseja que seus usuários exibam as listas de endereços no Outlook ou no Outlook Web App. Esta organização tem quatro listas de endereços:

  - AL\_FAB\_Users\_DGs

  - AL\_FAB\_Contacts

  - AL\_TAIL\_Users\_DGs

  - AL\_TAIL\_Contacts

Este exemplo cria a lista de endereços AL\_TAIL\_Users\_DGs. A lista de endereços contém todos os usuários e grupos de distribuição em que CustomAttribute15 seja igual a TAIL.

  ```powershell
    New-AddressList -Name "AL_TAIL_Users_DGs" -RecipientFilter {((RecipientType -eq 'UserMailbox') -or (RecipientType -eq "MailUniversalDistributionGroup") -or (RecipientType -eq "DynamicDistributionGroup")) -and (CustomAttribute15 -eq "TAIL")}
  ```

Para mais informações sobre como criar listas de endereços usando filtros de destinatários, consulte [Criar uma lista de endereços usando filtros de destinatários](https://docs.microsoft.com/pt-br/exchange/address-books/address-lists/use-recipient-filters-to-create-an-address-list).

Para criar uma ABP, você deve fornecer uma lista de endereços de salas. Se a sua organização não tiver caixas de correio de recursos, como caixas de correio de sala ou equipamento, sugerimos que você crie uma lista de endereços de sala em branco. O exemplo a seguir cria uma lista de endereços de salas em branco, porque não há caixas de correio de salas na organização.

  ```powershell
    New-AddressList -Name AL_BlankRoom -RecipientFilter {(Alias -ne $null) -and ((RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox'))}
  ```

Entretanto, neste cenário, Fabrikam e Contoso têm caixas de correio de sala. Este exemplo cria uma lista de salas para Fabrikam, usando um filtro de destinatário em que CustomAttribute15 é igual a FAB.

  ```powershell
    New-AddressList -Name AL_FAB_Room -RecipientFilter {(Alias -ne $null) -and (CustomAttribute15 -eq "FAB")-and (RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox')}
  ```

A lista global de endereços usada em uma ABP deve ser um superconjunto das listas de endereços. Não crie uma GAL com menos objetos do que os que existem em qualquer uma ou em todas as listas de endereços na ABP. Este exemplo cria a lista global de endereços para Tailspin Toys que inclui todos os destinatários que existem nas listas de endereços e na lista de endereços de salas.

  ```powershell
    New-GlobalAddressList -Name "GAL_TAIL" -RecipientFilter {(CustomAttribute15 -eq "TAIL")}
  ````

Para obter mais informações, consulte [Criar uma lista de endereços global](https://docs.microsoft.com/pt-br/exchange/address-books/address-lists/create-global-address-list).

Quando você criar a OAB, inclua a GAL apropriada, ao fornecer o parâmetro *AddressLists* de New- ou Set-OfflineAddressBook, para garantir que nenhuma entrada fique faltando inesperadamente. Basicamente, você pode personalizar o conjunto de entradas que um usuário irá ver ou reduzir o tamanho de download do OAB, especificando uma lista AddressLists em AddressLists de New/Set-OfflineAddressBook. Entretanto, se você desejar que os usuários vejam a lista completa de entradas de GAL no OAB, certifique-se de que você inclua a GAL em AddressLists.

Este exemplo cria o OAB para Fabrikam chamado OAB\_FAB.

```powershell
New-OfflineAddressBook -Name "OAB_FAB" -AddressLists "GAL_FAB"
```

Para mais informações, consulte [Criar um catálogo de endereços offline](https://docs.microsoft.com/pt-br/exchange/address-books/offline-address-books/create-offline-address-book).

## Etapa 4: Criar as ABPs

Depois de você ter criado todos os objetos exigidos, poderá criar a ABP. Este exemplo cria a ABP chamada ABP\_TAIL.

  ```powershell
    New-AddressBookPolicy -Name "ABP_TAIL" -AddressLists "AL_TAIL_Users_DGs"," AL_TAIL_Contacts" -OfflineAddressBook "\OAB_TAIL" -GlobalAddressList "\GAL_TAIL" -RoomList "\AL_TAIL_Rooms"
  ```

Para mais informações, consulte [Criar uma política de catálogo de endereços](https://docs.microsoft.com/pt-br/exchange/address-books/address-book-policies/create-an-address-book-policy).

## Etapa 5: Atribua os ABPs às caixas de correio

Atribuir a ABP ao usuário é a última etapa do processo. ABPs entram em vigor quando um aplicativo do usuário se conecta ao serviço do Catálogo de Endereços do Microsoft Exchange no servidor de Acesso para Cliente. Se o usuário já estiver conectado ao Outlook ou ao Outlook Web App, quando a ABP for aplicada à conta dele, ele precisará fechar e reiniciar o aplicativo cliente, antes de poderem ver suas novas listas de endereços e GAL.

Este exemplo atribui ABP\_FAB a todas as caixas de correio em que CustomAttribute15 é igual a "FAB".

  ```powershell
    Get-Mailbox -resultsize unlimited | where {$_.CustomAttribute15 -eq "TAIL"} | Set-Mailbox -AddressBookPolicy "ABP_TAIL"
  ```
  
Para mais informações, consulte [Atribuir uma política de catálogo de endereços para usuários de email](https://docs.microsoft.com/pt-br/exchange/address-books/address-book-policies/assign-an-address-book-policy-to-mail-users).

