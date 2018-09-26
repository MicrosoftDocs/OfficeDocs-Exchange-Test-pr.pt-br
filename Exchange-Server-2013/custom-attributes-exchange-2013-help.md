---
title: 'Atributos personalizados: Exchange 2013 Help'
TOCTitle: Atributos personalizados
ms:assetid: 2b043878-0b34-4563-a9c2-28a9efa7447e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423541(v=EXCHG.150)
ms:contentKeyID: 50485223
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atributos personalizados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-17_

O Microsoft Exchange Server 2013 inclui 15 atributos de extensão. Você pode usar esses atributos para adicionar informações sobre um destinatário, como uma ID de funcionário, unidade organizacional (OU) ou algum outro valor personalizado para o qual ainda não haja um atributo. Os atributos personalizados são identificados no Active Directory de **ms-Exch-Extension-Attribute1** até **ms-Exch-Extension-Attribute15**. No Shell de Gerenciamento do Exchange, os parâmetros correspondentes são *CustomAttribute1* a *CustomAttribute15*. Esses atributos não são usados pelos componentes do Exchange. Eles podem ser usados para armazenar dados do Active Directory sem ter que estender o esquema do Active Directory.

No Exchange Server 2003 (ou versão anterior), se você quisesse armazenar essas informações no Active Directory, você tinha que criar um atributo, estendendo o esquema do Active Directory. A extensão do esquema requer planejamento, aquisição de identificadores de objetos (OIDs) para novos atributos e testes no processo de extensão em um ambiente de teste antes de você implantar a extensão em um ambiente de produção. No Exchange 2013, as extensões de esquema não podem ser usadas em filtros de destinatário usados pelas listas de endereços, políticas de endereços de email e grupos de distribuição dinâmicos.

**Sumário**

Advantages of custom attributes

Custom attributes examples

Custom attributes example with the ConditionalCustomAttributes parameter

Custom attribute example with ExtensionCustomAttributes parameter

## Vantagens dos atributos personalizados

Estas são algumas das vantagens de usar atributos personalizados:

  - Você evita estender o esquema do Active Directory.

  - Os atributos são criados pela Instalação do Exchange.

  - Você pode usar o Centro de Administração do Exchange (EAC) ou o Shell de Gerenciamento do Exchange para gerenciar os atributos. Você não precisa montar controles personalizados ou escrever scripts para popular e exibir esses atributos.

  - Os atributos são propriedades filtráveis que podem ser usadas no parâmetro *Filter* com cmdlets de destinatário como o **Get-Mailbox**. Eles também podem ser usados no EAC e no Shell para criar filtros para políticas de endereço de email, listas de endereços e grupos de distribuição dinâmicos.

## Atributos personalizados com muitos valores

No Exchange 2012 Service Pack 2 (SP2), cinco atributos personalizados com muitos valores foram adicionados ao Exchange, para permitir que você armazene informações adicionais para destinatários de email, se os atributos personalizados tradicionais não atenderem a suas necessidades. Os parâmetros *ExtensionCustomAttribute1* a *ExtensionCustomAttribute5* podem conter até 1.300 valores cada. Você pode especificar vários valores, como uma lista delimitada por vírgulas. Os cmdlets a seguir suportam esses novos parâmetros:

  - [Set-DistributionGroup](https://technet.microsoft.com/pt-br/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/pt-br/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/pt-br/library/aa995950\(v=exchg.150\))

  - [Set-MailPublicFolder](https://technet.microsoft.com/pt-br/library/bb123707\(v=exchg.150\))

  - [Set-RemoteMailbox](https://technet.microsoft.com/pt-br/library/ff607302\(v=exchg.150\))

Para mais informações sobre as propriedades com muitos valores, consulte [Modificando as propriedades com valores múltiplos](modifying-multivalued-properties-exchange-2013-help.md).

## Exemplos de atributos personalizados

Em muitas implantações do Exchange, criar uma diretiva de endereços de email para todos os destinatários em um OU é um cenário comum. O OU não é uma propriedade filtrável que possa ser usada no parâmetro *RecipientFilter* de uma diretiva de endereço de email ou uma lista de endereços.


> [!NOTE]  
> Grupos de distribuição dinâmicos têm um parâmetro adicional que você pode usar para restringi-lo a destinatários em um OU ou contêiner em particular.



Se os destinatários no OU não compartilharem nenhuma propriedade comum pela qual você possa filtrá-los, como departamento ou local, você pode popular um dos atributos personalizados com um valor comum, conforme este exemplo.

```powershell
Get-Mailbox -OrganizationalUnit Sales | Set-Mailbox CustomAttribute1 "SalesOU"
```

Agora, você pode criar uma diretiva de endereço de email para todos os destinatários que tenham a propriedade *CustomAttribute1* igual a SalesOU, conforme este exemplo.

```powershell
New-EmailAddressPolicy -Name "Sales" -RecipientFilter { CustomAttribute1 -eq "SalesOU"} -EnabledEmailAddressTemplates "SMTP:%s%2g@sales.contoso.com"
```

## Exemplo de atributo personalizado com o parâmetro ConditionalCustomAttributes

Ao criar grupos de distribuição dinâmicos, políticas de endereço de email ou listas de endereços, você não precisa usar o parâmetro *RecipeintFilter* para especificar atributos personalizados. Você pode usar os parâmetros de *ConditionalCustomAttribute1* a *ConditionalCustomAttribute15*, em vez disso.

Este exemplo cria um grupo dinâmico de distribuição baseado nos destinatários cujo *CustomAttribute1* é definido para SalesOU.

```powershell
New-DynamicDistributionGroup -Name "Sales Users and Contacts" -IncludedRecipients "MailboxUsers,MailContacts" -ConditionalCustomAttribute1 "SalesOU"
```


> [!NOTE]  
> Use o parâmetro <EM>IncludedRecipients</EM> caso utilize um parâmetro <EM>Conditional</EM>. Além disso, você não pode usar parâmetros <EM>Conditional</EM> se você usar o parâmetro <EM>RecipientFilter</EM>. Se você quiser incluir filtros adicionais para criar seu grupo de distribuição dinâmico, políticas de endereços de email ou listas de endereços, você deverá usar o parâmetro <EM>RecipientFilter</EM>.



## Exemplo de atributo personalizado usando o parâmetro ExtensionCustomAttributes

Neste exemplo, a caixa de correio de Kweku terá *ExtensionCustomAttribute1* adicionado para refletir que ele se matriculou nos seguintes cursos: MATH307, ECON202 e ENGL300.

```powershell
Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 MATH307,ECON202,ENGL300
```

Depois, será criado um grupo de distribuição para todos os alunos matriculados em MATH307, usando-se o parâmetro *RecipientFilter*, em que *ExtensionCustomAttribute1* é igual a MATH307. Ao usar os parâmetros *ExtentionCustomAttributes*, você poderá usar o operador `-eq` em vez do operador `-like`.

```powershell
New-DynamicDistributionGroup -Name Students_MATH307 -RecipientFilter {ExtensionCustomAttribute1 -eq "MATH307"}
```

Neste exemplo, os valores de *ExtensionCustomAttribute1* de Kweku são atualizados para refletir que ele adicionou o curso ENGL210 e removeu o ECON202.

```powershell
Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 @{Add="ENGL210"; Remove="ECON202"}
```

