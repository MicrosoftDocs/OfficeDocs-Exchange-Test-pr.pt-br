---
title: 'Permitir que os usuários façam chamadas: Exchange 2013 Help'
TOCTitle: Permitir que os usuários façam chamadas
ms:assetid: b6e696ce-c848-475b-a598-9035677497e2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232172(v=EXCHG.150)
ms:contentKeyID: 51407902
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir que os usuários façam chamadas

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-03-09_

*Outdialing* é o processo pelo qual os usuários ligam para um plano de discagem de Unificação de mensagens usando um número do Outlook Voice Access e o local ou transferir uma chamada para um número de telefone interno ou externo. A Unificação de mensagens usa muitas configurações outdialing para discar chamadas dos usuários. Para configurar a discagem externa, você deve configurar as regras de discagem, grupos de regras de discagem e discagem autorizações na Unificação de mensagens (UM) planos de discagem e autorizam a discagem externa em planos de discagem de Unificação de mensagens, diretivas de caixa de correio de Unificação de mensagens e atendedores automáticos. Você também pode configurar planos de discagem de Unificação de mensagens ter códigos de acesso, um prefixo de número nacional, ou de discagem e formatos de número do país/região ou internacionais que permitem que você controle a discagem externa em sua organização. Este tópico discute as regras de discagem, grupos de regras de discagem e discagem autorizações e como elas são usadas para autorizar e controle discagem externa para sua organização.

**Sumário**

Visão geral

Types of users

Outdialing settings

Configuring outdialing

Applying configured dialing rule groups

Applying dialing rules

## Visão geral

A discagem externa ocorre quando:

  - Uma chamada é feita para um número de telefone externo.

  - Uma chamada é transferida para um atendedor automático.

  - Uma chamada é transferida para um usuário em sua organização

  - Um usuário habilitado para UM utiliza o recurso Tocar no Telefone

Para que a discagem externa funcione corretamente, as seguintes configurações devem ser definidas corretamente:

  - **Regras de discagem**   Regras de discagem definem o número que é discado pelo usuário habilitado para UM e o número que será discado pela Central Privada de Comutação telefônica (PBX) ou PBX IP.

  - **Regras de grupos de discagem**   As regras de grupos de discagem determinam os tipos de chamadas que os usuários podem fazer dentro de um grupo de discagem..

  - **Autorizações de discagem**   As autorizações de discagem determinam as restrições que serão aplicadas para impedir que os usuários tenham despesas telefônicas desnecessárias ou que façam chamadas de longa distância.

Para habilitar discagem externa para usuários que fazem chamada em um plano de discagem ou atendedor automático, você deve:

  - Certificar-se de que os gateways VoIP, representados por um gateway IP de UM vinculado a um plano de discagem permite chamadas de saída.

  - Criar grupos de regra de discagem através da criação de regras de discagem no plano de discagem de UM.

  - Adicionar autorizações de discagem para grupos de regras de discagem locais e internacionais no plano de discagem de UM, política de caixa de correio de UM ou atendedor automático associado com o mesmo plano de discagem como o gateway IP de UM.

## Tipos de usuários

Dois tipos de usuários podem usar o recurso de outdialing na Unificação de mensagens: autenticados e não autenticados. Todos os usuários que ligam para um atendedor automático de UM são não-autenticados. Quando os usuários ligam para um número do Outlook Voice Access, elas são consideradas não autenticado porque eles ainda não fornecido, seu número de ramal e o PIN e conectado ao suas caixas de correio. Os usuários são autenticados após eles fornecem seus número de ramal e PIN e entrar com êxito sua caixa de correio.

Quando os usuários ligam para um número do Outlook Voice Access configurado em um plano de discagem e tentar colocar ou transferir uma chamada sem entrar no suas caixas de correio, somente as configurações de discagem externa de plano de discagem de UM são aplicadas à chamada. Quando os usuários autenticados ou anônimos ligam para um atendedor automático de UM, as configurações outdialing configuradas no atendedor automático e outdialing configurações definidas no plano de discagem associado com o atendedor automático são aplicadas à chamada.

Quando os usuários ligam para o número do Outlook Voice Access configurado em um plano de discagem e entrar com êxito sua caixa de correio, eles se tornam usuários autenticados. Quando eles estiver autenticados, as configurações de chamada outdialing usam as regras de discagem e as configurações de autorização de discagem na diretiva de caixa de correio de Unificação de mensagens que está vinculada aos usuários.

Voltar ao início

## Configurações da discagem externa

Você precisa fazer várias configurações para aplicar as regras de discagem externa para sua organização. Além de definir os planos de discagem de Unificação de mensagens, atendedores automáticos e políticas de caixa de correio de Unificação de mensagens que você criou com as regras de discagem correto e discando autorizações, você precisa configurar códigos de acesso, planos de discagem prefixos de número e formatos de número em que a Unificação de mensagens. As seguintes configurações de outdialing são definidas em planos de discagem, atendedores automáticos e políticas de caixa de correio de Unificação de mensagens:

  - Códigos de acesso para linha externa, país/região e internacional

  - Prefixos de número nacional/regional

  - Formatos de número do paísregião e internacional

  - Grupos configurados de regras de discagem do país/região e internacionais

  - Grupos permitidos de regras de discagem do país/região e internacionais

  - Entradas de regras de discagem

  - Autorizações de discagem

Para que você possa configurar com êxito a discagem externa para sua organização, primeiro você precisa entender como cada componente pode ser usado com a discagem externa e como o componente deve ser configurado. A tabela a seguir apresenta cada componente que precisa ser configurado em planos de discagem de Unificação de mensagens, atendedores automáticos e políticas de caixa de correio de Unificação de mensagens para que discagem externa funcione corretamente.

### Componentes da discagem externa

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Códigos de discagem, prefixos de número e formatos de número</p></td>
<td><p>Códigos, prefixos de número de discagem de Unificação de mensagens usa e chamadas de formatos de número para determinar o número correto para discar quando você faz uma saída. Você pode configurar códigos de discagem, prefixos de número e formatos de número para restringir as chamadas de saída para usuários que discam para um atendedor automático de UM associado a um plano de discagem de Unificação de mensagens ou para usuários que discam para um número do Outlook Voice Access configurado no plano de discagem.</p></td>
</tr>
<tr class="even">
<td><p>Grupos de regras de discagem</p></td>
<td><p>Grupos de regras de discagem são criados para permitir que os números de telefone a ser modificado antes que elas são enviadas para o PBX para chamadas de saída. Grupos de regras de discagem remover números de ou adicionar números a números de telefone que está sendo chamados pelo Unificação de mensagens. Por exemplo, você pode criar um grupo de regras de discagem que adiciona automaticamente uma 9 como um prefixo para um número de telefone de 7 dígitos para fornecer acesso a uma linha externa. Neste exemplo, os usuários que façam chamadas de saída não necessário discar 9 antes do número de telefone para falar com alguém de fora da organização.</p>
<p>Cada grupo de regras de discagem contém as regras de discagem que determinam os tipos de chamadas de país/região e internacionais que os usuários dentro de um grupo de regras de discagem podem fazer. Grupos de regras de discagem se aplicam aos usuários que estão associados ao plano de discagem ou atendedores automáticos e políticas de caixa de correio UM associadas a UM plano de discagem. Cada grupo de regras de discagem deve conter pelo menos uma regra de discagem.</p></td>
</tr>
<tr class="odd">
<td><p>Entradas de regras de discagem</p></td>
<td><p>Uma regra de discagem é usada para determinar os tipos de chamadas que os usuários dentro de um grupo de regras de discagem podem fazer. Quando você cria um grupo de regras de discagem, você pode configurar uma ou mais regras de discagem.</p>
<p>Quando você configura cada regra de discagem, você deve digitar o nome da regra de discagem, o padrão de número para transformar (<em>máscara de número</em>) e discado número. Você também pode inserir um comentário. Comentários podem ser usados para descrever como a regra de discagem será usada ou para descrever um grupo de usuários aos quais a regra de discagem será aplicada. Quando você adiciona uma máscara de número e o número discado para uma regra de discagem, você pode substituir a letra x para um dígito em um número de telefone, por exemplo, 91425xxxxxxx. Você também pode usar um símbolo de asterisco (*) como um caractere curinga, por exemplo, 91425 *.</p></td>
</tr>
<tr class="even">
<td><p>Autorizações de discagem</p></td>
<td><p>Uma autorização de discagem usa os grupos de regras de discagem para aplicar as restrições de discagem para usuários que estão associados uma diretiva específica de caixa de correio de Unificação de mensagens, plano de discagem ou atendedor automático. Também pode ser usados quando você quiser permitir que os usuários façam chamadas para números de telefone internacional ou de país/região.</p>
<p>Depois de criar regras de discagem em um plano de discagem de UM, você adicionar o grupo de regras de discagem a uma política de caixa de correio de Unificação de mensagens, plano de discagem, ou atendedor automático. Depois que o grupo de regras de discagem é adicionado a uma política de caixa de correio de Unificação de mensagens, todas as definições ou regras definidas serão aplicadas aos usuários habilitados para UM vinculadas com a diretiva de caixa de correio de Unificação de mensagens.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Configurando a discagem externa

Um grupo de regras de discagem é uma coleção de uma ou mais regras de discagem configurados em um plano de discagem de UM. Dois tipos de grupos de regra de discagem podem ser configurados em um plano de discagem de UM: país/região e internacionais. Grupos de regras de discagem do país/região se aplicam aos números de telefone discados dentro do mesmo país ou região. Grupos de regras de discagem internacional se aplicam aos números de telefone internacional discados de um país ou região para outro país ou região.

Cada plano de discagem de Unificação de mensagens pode conter um ou mais grupos de regras de discagem. Para aplicar um grupo de regras de discagem para um conjunto de usuários, depois de criar o grupo de regras de discagem, você deve adicioná-lo à lista de permissão em UM plano de discagem e nas políticas de caixa de correio UM associadas a UM plano de discagem e atendedores automáticos de grupos de regras de discagem.

Grupos de regras de discagem permitem especificar as regras de discagem que deseja aplicar a um grupo de usuários habilitados para UM que se encaixam em uma categoria específica. Por exemplo, você pode usar grupos de regras de discagem para especificar qual grupo de usuários pode fazer chamadas internacionais e o grupo ao qual pode fazer chamadas somente no estado ou locais. Você pode criar um grupo de regras de discagem usando o Centro de administração do Exchange (EAC) ou o cmdlet **Set-UMDialPlan** no Shell de gerenciamento do Exchange. Quando você cria um grupo de regras de discagem, você deve definir pelo menos uma regra de discagem para o grupo.

Quando um usuário disca um número de telefone, a Unificação de mensagens pega o número e procura por uma correspondência nas regras de discagem. Se uma correspondência for encontrada, a Unificação de mensagens usa a regra de discagem para determinar o número para discar examinando o número de telefone ou dígitos listados na seção **Número discado** da regra de discagem. O número listado na caixa **Número discado** da regra de discagem será discado.

A tabela a seguir mostra um exemplo de grupos de regras de discagem e regras de discagem. Neste exemplo, chamadas-somente Local e baixa taxa são os grupos de regras de discagem que tiverem sido criados. O grupo de regras de discagem de chamadas-somente Local tem duas regras de discagem: 91425 \* e 91206 \*, e o grupo de regras de discagem taxa baixa também tem duas regras de discagem: 91509 \* e 91360 \*.

### Grupos e entradas de regras de discagem

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>MáscaradeNúmero</th>
<th>NúmeroDiscado</th>
<th>Comentário</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Somente chamadas locais</p></td>
<td><p>91425*</p></td>
<td><p>91*</p></td>
<td><p>Chamadas locais</p></td>
</tr>
<tr class="even">
<td><p>Somente chamadas locais</p></td>
<td><p>91206*</p></td>
<td><p>91*</p></td>
<td><p>Chamadas locais</p></td>
</tr>
<tr class="odd">
<td><p>Taxa reduzida</p></td>
<td><p>91509*</p></td>
<td><p>9*</p></td>
<td><p>Chamadas no estado</p></td>
</tr>
<tr class="even">
<td><p>Taxa reduzida</p></td>
<td><p>91360*</p></td>
<td><p>9*</p></td>
<td><p>Chamadas no estado</p></td>
</tr>
</tbody>
</table>


Por exemplo, quando um usuário disca 9-1-425-555-1234, UM disca 4255551234. Unificação de mensagens remove quaisquer numéricos caracteres (neste exemplo, os hífens) e aplica a máscara do número da regra de discagem. Neste exemplo, a Unificação de mensagens se aplica a máscara do número 91 \*. Isso informa a Unificação de mensagens não para discar o 9 ou o 1, mas para todos os outros números no número de telefone que aparecem à direita do número 1 de discagem. Isso inclui todos os números representados por um asterisco (\*).

Você pode usar o EAC ou o Shell para criar e configurar um ou vários país/região e internacionais grupos de regras de discagem e regras de discagem. No entanto, se você estiver criando muitas ou complexa discando de grupos de regras e regras de discagem, você pode usar um arquivo de valores separados por vírgula (. csv) no Shell. Você pode importar ou exportar uma lista de grupos de regras de discagem e regras de discagem.

Para importar uma lista de grupos e entradas de regras de discagem que você tenha definido em um arquivo .csv, execute o cmdlet **Set-UMDialPlan** , como segue.

    Set-UMDialPlan "MyUMDialPlan" -ConfiguredInCountryOrRegionGroups $(IMPORT-CSV c:\dialrules\InCountryRegion.csv)

Para recuperar uma lista de grupos de regras de discagem que estejam configurados em um plano de discagem de UM, execute o cmdlet **Get-UMDialPlan**, como segue:

    (Get-UMDialPlan -id "MyUMDialPlan").ConfiguredInCountryOrRegionGroups | EXPORT-CSV C:\incountryorregion.csv

O arquivo. csv deve ser criado e salvos no formato correto. Cada linha no arquivo. csv representa uma regra de discagem. No entanto, cada regra de discagem é configurada no mesmo grupo de regra de discagem. Cada regra no arquivo terá quatro seções separadas por vírgulas. Estas seções são máscara do número, nome, número discado e comentário. Cada seção é necessária e você deve digitar as informações corretas em cada seção, exceto a seção de comentário. Há deve ser sem espaços entre a entrada de texto e a vírgula para a próxima seção, nem deve haver todas as linhas em branco entre as regras ou no final. O exemplo a seguir é um exemplo de um arquivo. csv que pode ser usado para criar grupos de regras de discagem do país/região e regras de discagem.

**Nome,MáscaradeNúmero,NúmeroDiscado,Comentário**

**Taxa reduzida,91425xxxxxxx,9xxxxxxx,Chamada local**

**Taxa reduzida,9425xxxxxxx,9xxxxxxx,Chamada local**

**Taxa reduzida,9xxxxxxx,9xxxxxxx,Chamada local**

**Todas,91\*,91\*,Acesso liberado para números locais**

**Chamada interurbana,91408\*,91408\*,chamada interurbana**

A seguir, está um exemplo de um arquivo .csv que pode ser usado para criar grupos e entradas de regras de discagem internacionais:

**Nome,MáscaradeNúmero,NúmeroDiscado,Comentário**

**Internacional, 901144\*, 901144\*, chamada internacional**

**Internacional, 901133\*, 901133\*, chamada internacional**

Voltar ao início

## Aplicar grupos de regras de discagem configurados

Grupos de regras de discagem são criados em um plano de discagem de UM. Você pode criar internacionais usando o EAC ou o cmdlet **Set-UMDialPlan** no Shell de grupos de regras de discagem ou de país/região. Depois de criar os grupos de regras de discagem apropriado em um UM plano de discagem e definir as regras de discagem, você pode aplicar os grupos de regras de discagem que você criou para um plano de discagem de Unificação de mensagens, um atendedor automático ou aos usuários que estão associados uma diretiva de caixa de correio de Unificação de mensagens e autorizam a discagem externa dependendo de como o usuário acessa o sistema de caixa postal.

É possível aplicar os grupos de regras de discagem criados em um plano de discagem de UM para:

  - **Mesmo plano de discagem**   As configurações serão aplicadas a todos os usuários que ligam para um número do Outlook Voice Access, mas não entrar com suas caixas de correio. Para aplicar a um grupo de regras de discagem do país/região denominado `MyAllowedDialRuleGroup` para o mesmo plano de discagem, use o cmdlet do Shell **Set-UMDialPlan** , da seguinte maneira.
    
        Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Políticas de caixa de correio de UM único ou vários** As configurações que foram definidas em uma diretiva de caixa de correio UM se aplicará a todos os usuários que estão vinculados com essa política de caixa de correio de Unificação de mensagens. As definições configuradas em uma diretiva de caixa de correio UM se aplicam aos usuários que ligam para um número do Outlook Voice Access e entrar com suas caixas de correio. Para aplicar a um grupo de regras de discagem do país/região denominado `MyAllowedDialRuleGroup` para uma única política de caixa de correio de Unificação de mensagens, use a página de **autorização de discagem** na diretiva de caixa de correio de Unificação de mensagens no EAC ou o cmdlet **Set-UMMailboxPolicy** no Shell, da seguinte maneira.
    
        Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Atendedores automáticos de um ou vários associados a UM plano de discagem** Isso se aplicará a todos os usuários que ligam para um atendedor automático. Para aplicar o grupo de regras de discagem do país/região denominado `MyAllowedDialRuleGroup` para um único atendedor automático, use a página de **autorização de discagem** no atendedor automático no EAC ou o cmdlet **Set-UMAutoAttendant** no Shell, da seguinte maneira.
    
        Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

A tabela a seguir resume a forma como os grupos de regras de discagem são aplicados à Unificação de Mensagens.

### Aplicando regras de discagem externa

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de chamador</th>
<th>Escopo</th>
<th>Configurações de discagem externa aplicadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook Número do Voice Access</p></td>
<td><p>O usuário liga para um número do Outlook Voice Access do plano de discagem e faz logon em sua caixa de correio</p></td>
<td><p>Política de caixa de correio de UM</p></td>
</tr>
<tr class="even">
<td><p>Chamador anônimo</p></td>
<td><p>O usuário liga para um número do plano de discagem do Outlook Voice Access</p></td>
<td><p>Plano de discagem de UM</p></td>
</tr>
<tr class="odd">
<td><p>Chamador anônimo</p></td>
<td><p>O usuário liga para um atendedor automático piloto ou para um número de ramal</p></td>
<td><p>Atendedor automático de UM</p></td>
</tr>
<tr class="even">
<td><p>Chamador pertencente à organização</p></td>
<td><p>O usuário liga para o número de Tocar no Telefone</p></td>
<td><p>Política de caixa de correio de UM</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Aplicar regras de discagem

O processo de discagem externa acontece quando:

  - A Unificação de Mensagens faz uma chamada para um número de telefone externo para um chamador.

  - O servidor de Unificação de Mensagens transfere uma chamada para um atendedor automático.

  - O servidor de Unificação de Mensagens transfere uma chamada para um usuário em sua organização.

  - Um usuário habilitado para UM utiliza o recurso Tocar no Telefone

Em cada cenário outdialing, UM aplicar as regras de discagem que tiverem sido configuradas e, em seguida, colocar a chamada para o usuário. No entanto, dependendo do cenário e como a chamada é iniciada pelo usuário, Unificação de mensagens pode se aplicar somente alguns das regras de discagem para o número de telefone que está sendo discado. Em outros cenários outdialing, Unificação de mensagens pode se aplicar a todas as regras de outdialing configuradas para o número de telefone que está sendo discado.

Voltar ao início

