---
title: 'Políticas de endereço de email: Exchange 2013 Help'
TOCTitle: Políticas de endereço de email
ms:assetid: b63b63bb-6faf-4337-8441-50bc64b49bb8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232171(v=EXCHG.150)
ms:contentKeyID: 50486463
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Políticas de endereço de email

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-07-21_

Destinatários (que incluem usuários, recursos, contatos e grupos) são qualquer objeto habilitado para email no Active Directory para o qual a Microsoft Exchange pode entregar ou encaminhar mensagens. Para um destinatário enviar ou receber mensagens de email, o destinatário deve ter um endereço de email. Políticas de endereço de email geram os endereços de email primários e secundários para seus destinatários para que possam receber e enviar email.

Por padrão, o Exchange contém uma política de endereço de email para cada usuário habilitado para email. Essa política padrão especifica o alias do destinatário como a parte local do endereço de email e usa o domínio aceito padrão. A parte local do endereço de email é o nome que aparece antes do símbolo de arroba (@). No entanto, você pode alterar o modo como os endereços de email dos destinatários serão exibidos. Por exemplo, é possível especificar que os endereços sejam exibidos como *firstname*.*lastname*@contoso.com.

Além disso, se você quiser especificar endereços de email adicionais para todos os destinatários ou apenas um subconjunto, você pode modificar a política padrão ou criar diretivas adicionais. Por exemplo, a caixa de correio do usuário para David Hamilton poderá receber mensagens de email endereçadas ao hdavid@mail.contoso.com e hamilton.david@mail.contoso.com.

Procurando tarefas de gerenciamento relacionadas às políticas de endereço de email? Consulte [Procedimentos de diretiva de endereço de email](email-address-policy-procedures-exchange-2013-help.md).

## Comportamentos de diretivas de destinatário

Ao executar o cmdlet Update-EmailAddressPolicy no Shell de Gerenciamento do exExchangeNoVersion, o objeto do destinatário é atualizado com a política de endereço de email.

  - Políticas de destinatário são aplicadas na ordem de prioridade a prioridade mais baixa. No caso de um conflito entre dois ou mais políticas, a diretiva com a prioridade mais alta será aplicada. Diretiva de destinatário padrão é sempre tem a prioridade mais baixa e será aplicado se nenhum outras políticas são correspondidas.
    
    Quando você cria uma diretiva de destinatário, mas não especifica explicitamente uma prioridade, ele será adicionado a prioridade mais alta. Se você especificar uma prioridade que já está associada a uma política existente, a diretiva existente e todas as diretivas com uma prioridade mais baixa serão movidas para baixo por um. A nova política será inserida na prioridade especificada.
    
    A funcionalidade de diretiva de destinatário é dividida em dois recursos: domínios aceitos e diretivas de endereço de email. Para obter mais informações sobre domínios aceitos, consulte [Domínios aceitos](accepted-domains-exchange-2013-help.md).

  - Quando você executar o cmdlet **Update-EmailAddressPolicy** em Exchange Shell de gerenciamento, o objeto de destinatário é atualizado com a diretiva de endereço de email.

  - Sempre que um objeto de destinatário é modificado e salvo, Exchange impõe o aplicativo correto dos critérios de endereço de email e configurações. Quando uma política de endereço de email é modificada e salvo, todos os destinatários associados são atualizados com a alteração. Além disso, se um objeto de destinatário é modificado, membros da diretiva de endereço do destinatário esse email é reavaliados e impostos.

## Criação de políticas de endereço de email

Ao criar uma política, você pode usar os seguintes tipos de endereços de email:

  - **Endereço de email SMTP predefinidos**. Os endereços de email SMTP *predefinidos* são os tipos de endereços de email normalmente usados que são fornecidos a você.

  - **Endereço de email SMTP personalizado**. Se você não desejar usar um dos endereços de email SMTP predefinidos, será possível especificar um endereço de email SMTP personalizado.
    
    Ao criar um endereço de email SMTP personalizado, você pode usar as variáveis da tabela a seguir para especificar valores alternativos para a parte local do endereço de email.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Variável</th>
    <th>Valor</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%g</p></td>
    <td><p>Nome fornecido (nome)</p></td>
    </tr>
    <tr class="even">
    <td><p>%i</p></td>
    <td><p>Inicial do segundo nome</p></td>
    </tr>
    <tr class="odd">
    <td><p>%s</p></td>
    <td><p>Sobrenome (último nome)</p></td>
    </tr>
    <tr class="even">
    <td><p>%d</p></td>
    <td><p>Nome de exibição</p></td>
    </tr>
    <tr class="odd">
    <td><p>%m</p></td>
    <td><p>Alias do Exchange</p></td>
    </tr>
    <tr class="even">
    <td><p>%<em>x</em>s</p></td>
    <td><p>Usa as primeiras <em>x</em> letras do sobrenome. Por exemplo, se <em>x</em> =2, as duas primeiras letras do sobrenome serão usadas.</p></td>
    </tr>
    <tr class="odd">
    <td><p>%<em>x</em>g</p></td>
    <td><p>Usa as primeiras <em>x</em> letras do nome fornecido. Por exemplo, se <em>x</em> =2, serão usadas as duas primeiras letras do nome.</p></td>
    </tr>
    </tbody>
    </table>


  - **Endereço de email não SMTP**. Os seguintes tipos de endereços de email não SMTP têm suporte:
    
      - EX (Nome para Exibição do Prefixo de Endereço Proxy DN Herdado)
    
      - X.500
    
      - X.400
    
      - MSMail
    
      - CcMail
    
      - Lotus Notes
    
      - Novell GroupWise
    
      - ExchangeEndereço proxy da Unificação de Mensagens (endereço proxy do EUM)
    

    > [!IMPORTANT]
    > No Exchange, todos os endereços de email não SMTP são considerados endereços personalizados. O Exchange não fornece caixas de diálogo exclusivas ou páginas de propriedades para os tipos de endereços de email X.400, GroupWise ou Lotus Notes. Se um endereço de email personalizado não SMTP for adicionado, será preciso ter os arquivos DLL (biblioteca de vínculo dinâmico) apropriados. Se os arquivos DLL apropriados não forem fornecidos, não será possível criar uma política de endereço de email personalizado. O seguinte erro será registrado no Visualizador de Eventos: "O objeto de descrição de endereço de email no diretório do Microsoft Exchange para o tipo de endereço 'SADF' em máquinas 'i386' está ausente."



Para obter instruções detalhadas sobre como criar uma política de endereço de email, confira os seguintes tópicos:

[Criar uma política de endereço de Email](create-an-email-address-policy-exchange-2013-help.md)

[Criar uma política de endereço de email usando filtros de destinatários](create-an-email-address-policy-by-using-recipient-filters-exchange-2013-help.md)

