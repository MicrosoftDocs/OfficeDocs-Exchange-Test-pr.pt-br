---
title: 'Configuração de conta no Outlook para iOS e Android usando autenticação básica'
TOCTitle: Configuração de conta no Outlook para iOS e Android usando a autenticação básica
ms:assetid: 013dbe8c-30de-4c9c-baa9-75081b9229e8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt829322(v=EXCHG.150)
ms:contentKeyID: 74518379
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuração de conta no Outlook para iOS e Android usando a autenticação básica

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2018-04-30_

**Resumo:**  como usuários em sua organização do Exchange 2013 podem configurar rapidamente seu Outlook para iOS e Android contas usando a autenticação básica.

Outlook para iOS e Android oferece a capacidade de "push" configurações de conta para seus usuários locais que usam a autenticação básica por meio do protocolo ActiveSync de administradores do Exchange. Esse recurso funciona com qualquer provedor de gerenciamento de dispositivo móvel (MDM) que usa o canal de [Configuração de aplicativos gerenciados](https://developer.apple.com/library/content/samplecode/sc2279/introduction/intro.html) para iOS ou o canal [Android na empresa](https://developer.android.com/samples/apprestrictions/index.html) para Android.

Para usuários locais inscritos no Microsoft Intune, você pode implantar as definições de configuração de conta usando o Intune no Portal do Windows Azure.

Depois que uma configuração de conta tiver sido criada e o usuário registra seu dispositivo, o Outlook para iOS e Android detectará que uma conta for "encontrado" e, em seguida, solicitará ao usuário para adicionar a conta. A única informação que o usuário precisa digitar para concluir o processo de instalação é sua senha. Em seguida, carregará o conteúdo de caixa de correio do usuário e o usuário pode começar a usar o aplicativo.

As imagens a seguir mostram um exemplo do processo de instalação do usuário final após o Outlook para iOS e Android tem sido configurado no Intune no Portal do Windows Azure.

![Configuração de conta para Outlook para iOS e Android no local](images/Mt829322.04bd56f2-5c45-4268-8762-436994acd656(EXCHG.150).png "Configuração de conta para Outlook para iOS e Android no local")

## Criar uma política de configuração de aplicativo para Outlook para iOS e Android usando Microsoft Intune

Se você estiver usando o Microsoft Intune como seu provedor de gerenciamento de dispositivo móvel, as seguintes etapas permitirá que você implante definições de configuração de conta para suas caixas de correio local que utilizam a autenticação básica com o protocolo ActiveSync. Depois que a configuração é criada, você pode atribuir as configurações para grupos de usuários, conforme detalhado na próxima seção, atribuir definições de configuração.


> [!TIP]
> Se os usuários em sua organização usam iOS e Android para dispositivos de trabalho, você precisará criar uma política de configuração de aplicativo separado para cada plataforma.



1.  Entrar no portal do Azure.

2.  Selecione **mais serviços \> monitoramento + gerenciamento \> Intune**.

3.  No blade **aplicativos móveis** da lista Gerenciar, selecione **as políticas de configuração de aplicativos**.

4.  No blade **políticas de configuração de aplicativos** , escolha **Adicionar**.

5.  No blade **Adicionar configuração de aplicativos** , insira um **nome**e uma **Descrição** opcional para as definições de configuração do aplicativo.

6.  Para o tipo de **registro do dispositivo** , escolha **dispositivos gerenciados**.

7.  **Plataforma**, escolha **iOS** ou **Android para o trabalho**.

8.  Escolha **associado de aplicativos**e, no blade **multidifusão aplicativos** , escolha **Microsoft Outlook para iOS** ou **Microsoft Outlook para Android**.

9.  Clique em **Okey** para voltar para o blade **Adicionar configuração de aplicativos** .

10. Escolha as **definições de configuração**. No blade **definições de configuração** , defina os pares de valores chave que fornecerá configurações para o Outlook para iOS e Android. Os pares de valores chave que você digitar são definidos neste artigo, na seção de pares de valor de chave.
    

    > [!TIP]
    > Para inserir os pares de valor de chave, você tem uma escolha entre usando o designer de configuração ou inserindo uma lista de propriedade XML.



11. Quando terminar, escolha **Okey**.

12. No blade **Adicionar configuração de aplicativos** , escolha **criar**.

A diretiva da configuração recém-criada será exibida no blade **políticas de configuração de aplicativos** .

## Atribuir definições de configuração

Atribua as configurações que você criou na seção anterior para grupos de usuários no Windows Azure Active Directory. Quando um usuário tem o aplicativo do Microsoft Outlook instalado, o aplicativo será gerenciado pelas definições de que você especificou. Para fazer isso:

1.  No blade **aplicativos móveis** do painel de controle de gerenciamento de aplicativo móvel Intune, escolha **políticas de configuração de aplicativos**.

2.  Da lista de políticas de configuração de aplicativos, selecione aquele que deseja atribuir e, em seguida, escolha **atribuições**.

3.  No blade **atribuições** , escolha **Selecionar grupos**.

4.  No blade **Selecionar grupos** , selecione o grupo de Azure AD para o qual você deseja atribuir a política de configuração de aplicativo, selecione **Selecionar**e, em seguida, **Salve**.

## Pares de valores chave

Quando você cria uma política de configuração do aplicativo no Portal do Windows Azure ou por meio de seu provedor MDM, você precisará os seguintes pares de valor-chave:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tecla</th>
<th>Valores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailAccountName</p></td>
<td><p>Este valor Especifica a conta de email do nome de exibição, como ele será exibido aos usuários em seus dispositivos.</p>
<p><strong>Os valores aceitos</strong>: cadeia de caracteres</p>
<p><strong>Padrão se não especificado</strong>: &lt; deixe em branco &gt;</p>
<p><strong>Exemplo</strong>: user@companyname.com</p>
<p><strong>Token Intune *</strong>: {{username}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.EmailAddress</p></td>
<td><p>Este valor Especifica o endereço de email a ser usado para o envio e recebimento de email.</p>
<p><strong>Os valores aceitos</strong>: cadeia de caracteres</p>
<p><strong>Padrão se não especificado</strong>: &lt; deixe em branco &gt;</p>
<p><strong>Exemplo</strong>: user@companyname.com</p>
<p><strong>Token Intune *</strong>: {{email}}</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailUPN</p></td>
<td><p>Este valor Especifica o nome Principal de usuário para o perfil de email que será usado para autenticar a conta.</p>
<p><strong>Os valores aceitos</strong>: cadeia de caracteres</p>
<p><strong>Padrão se não especificado</strong>: &lt; deixe em branco &gt;</p>
<p><strong>Exemplo</strong>: userupn@companyname.com</p>
<p><strong>Token Intune *</strong>: {{userprincipalname}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.ServerAuthentication</p></td>
<td><p>Este valor Especifica o método de autenticação para o usuário.</p>
<p><strong>Os valores aceitos</strong>: 'Username e Password'; 'Certificados'</p>
<p><strong>Padrão se não especificado</strong>: 'Username e Password'</p>
<p><strong>Exemplo</strong>: 'Username e Password'</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.ServerHostName</p></td>
<td><p>Este valor Especifica o nome do host do seu servidor Exchange.</p>
<p><strong>Os valores aceitos</strong>: cadeia de caracteres</p>
<p><strong>Padrão se não especificado</strong>: &lt; deixe em branco &gt;</p></td>
</tr>
</tbody>
</table>


**\*** Usuários de Microsoft Intune podem usar tokens que serão expandida para o valor correto de acordo com o usuário MDM inscrito. Para obter mais informações, consulte o [Adicionar políticas de configuração de aplicativos para dispositivos iOS gerenciada](https://docs.microsoft.com/en-us/intune/app-configuration-policies-use-ios) .

