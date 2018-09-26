---
title: 'Criar uma política de endereço de Email: Exchange 2013 Help'
TOCTitle: Criar uma política de endereço de Email
ms:assetid: eb2bf42e-2058-4e17-85d5-97546433b40a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125137(v=EXCHG.150)
ms:contentKeyID: 50486931
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewEmailAddressPolicyWizardForm.EmailAddressPolicyIntroductionPage
ms.translationtype: MT
---

# Criar uma política de endereço de Email

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-12-10_

Para um destinatário receber ou enviar mensagens de email, o destinatário deve ter um endereço de email. Políticas de endereço de email geram os endereços de email primários e secundários para seus destinatários (que incluem usuários, contatos e grupos) para que possam receber e enviar email.

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

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de endereço de email" no tópico [Endereços de email e catálogos de endereços](email-addresses-and-address-books-exchange-2013-help.md) .

  - Antes de um domínio do endereço SMTP pode ser usado em uma política de endereço de email, você deve configurar um domínio aceito. Para saber mais, consulte [Domínios aceitos](accepted-domains-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]  
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para criar uma política de endereço de email

1.  Navegue até **fluxo de emails** \> **políticas de endereço de Email** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na **Diretiva de endereço de Email**, preencha os seguintes campos:
    
      - **Nome da política**
    
      - **Formato de endereço de email**
    
      - **Especificar os tipos de destinatários a que este endereço de email se aplicarão**

3.  Clique em **Adicionar uma regra** para restringir os destinatários aos quais esta política será aplicada. Isso cria um demonstrativo Boolean **e**.
    

    > [!CAUTION]  
    > Se você aplicar muitas regras, será possível restringir a política de endereço de email até o ponto que ela não contenha nenhum usuário.



4.  Clique em **Exibir destinatários aos quais a política se aplica** para exibir os destinatários aos quais a política se aplica.

5.  Clique em **Salvar** para salvar suas alterações e criar a diretiva.

6.  Você receberá um aviso de que a política de endereço de email não será aplicada até você a atualizar. Após a sua criação, selecione-a e, no painel de detalhes, clique em **Aplicar**.

## Use o Shell para criar uma política de endereço de email

Este exemplo cria uma política de endereço de email que inclui usuários de caixa de correio nos escritórios de Sudeste que terão os endereços de email que incluem o sobrenome, combinado com as duas primeiras letras do seu nome.

```powershell
New-EmailAddressPolicy -Name "southeast offices" -IncludedRecipients MailboxUsers -ConditionalStateorProvince "Georgia","Alabama","Louisiana" -EnabledEmailAddressTemplates "SMTP:%s%2g@southeast.contoso.com"
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-EmailAddressPolicy](https://technet.microsoft.com/pt-br/library/aa996800\(v=exchg.150\)).