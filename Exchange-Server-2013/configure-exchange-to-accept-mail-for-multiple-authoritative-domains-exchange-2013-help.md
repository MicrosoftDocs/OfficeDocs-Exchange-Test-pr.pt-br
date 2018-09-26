---
title: 'Configurar o Exchange para aceitar emails de vários domínios autoritativos'
TOCTitle: Configurar o Exchange para aceitar emails de vários domínios autoritativos
ms:assetid: 11801f73-4934-4025-a1c1-3935dada7e9b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996314(v=EXCHG.150)
ms:contentKeyID: 51407836
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o Exchange para aceitar emails de vários domínios autoritativos

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-06-15_

No Microsoft Exchange Server 2013, é fácil adicionar vários domínios autoritativos à sua organização. No entanto, depois de adicionar o domínio autoritativo, você precisa decidir como usá-lo em sua organização. Por exemplo:

  - Se você quiser adicionar um endereço de email ao novo domínio autoritativo para destinatários em sua organização, deseja substituir o endereço primário existente (responder para) dos destinatários ou adicionar o novo endereço de email como um endereço proxy (secundário)?

  - Deseja que o endereço de email no domínio autoritativo se aplique a todos os destinatários e a todos os tipos de destinatários? Ou deseja que o novo endereço de email se aplique a tipos específicos de destinatários, ou a destinatários específicos com base em suas propriedades de usuário, por exemplo, apenas usuários no departamento de Finanças?

Os exemplos a seguir são cenários nos quais a sua organização do Exchange pode precisar receber e processar email de mais de um domínio SMTP autorizado:

  - Você está mudando o nome do seu domínio SMTP, mas precisa continuar aceitando email para o antigo nome de domínio por um tempo, caso os clientes enviem emails para os endereços antigos. É possível definir o novo endereço de email como o endereço (de resposta) primário. Isto significa que o novo endereço será o endereço de email padrão exibido em todas as mensagens de email enviadas pelo destinatário. É possível definir o endereço de email antigo como endereço secundário. Isto permitirá que o destinatário continue recebendo emails enviados para o endereço de email antigo.

  - Você deseja prover endereços de email diferentes para unidades comerciais dentro da sua organização. Por exemplo, se a floresta do contoso.com di Active Directory contiver subdomínios para as subsidiárias Tailspin Toys e Fourth Coffee, você pode desejar atribuir os nomes de domínio SMTP contoso.com, tailspintoys.com e fourthcoffee.com aos destinatários das respectivas unidades comerciais.

  - Você fornece serviços de hospedagem de email e tem que aceitar email para mais de um nome de domínio SMTP.

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 30 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Domínios aceitos" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) e entrada "Diretivas de endereço de email" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Se você tiver um servidor de Transporte de Borda inscrito em sua rede de perímetro, configure os domínios aceitos em um servidor de Caixa de Correio em sua organização do Exchange. A configuração de domínios aceitos é replicada para o servidor de Transporte de Borda durante a sincronização do EdgeSync. Para saber mais, confira [Inscrições de Borda](edge-subscriptions-exchange-2013-help.md).

  - Ao criar um domínio aceito, você pode usar um caractere curinga ( \* ) no espaço de endereçamento para indicar que todos os subdomínios do espaço de endereçamento SMTP também serão aceitos pela organização do Exchange. Por exemplo, para configurar contoso.com e todos os seus subdomínios como domínios aceitos, digite **\*.contoso.com** como o espaço de endereçamento SMTP. Contudo, se os nomes de subdomínios forem usados em uma diretiva de endereço de email, cada subdomínio deverá ter uma entrada explícita do domínio aceito.

  - Um registro MX no DNS público é exigido para cada domínio SMTP para o qual você aceita email da Internet. Cada registro MX deve determinar o servidor voltado para a Internet que recebe emails para a sua organização.

  - É necessário configurar os conectores de Envio e os conectores de Recebimento para que sua organização do Exchange possa enviar e receber email da Internet. A configuração dos conectores de envio e de recebimento da Internet é determinada pela sua topologia do Exchange. Para obter mais informações sobre a configuração de conectores, consulte [Conectores](connectors-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Criar um domínio autoritativo

## Use o Centro de Administração do Exchange para criar um domínio autoritativo

1.  No EAC, navegue até **Fluxo de emails** \> **Domínios aceitos** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No campo **Nome**, digite o nome de exibição do domínio aceito. Cada domínio aceito para a sua organização deve ter um nome de exibição exclusivo. Isso pode ser diferente em relação ao domínio aceito. Por exemplo, se o domínio contoso.com puder ter um nome para exibição de Domínio Aceito Local Contoso.

3.  No campo **Domínio aceito**, especifique um namespace SMTP do qual sua organização aceita mensagens de email. Por exemplo, contoso.com.

4.  Selecione **Domínio autoritativo**.

5.  Clique em **Salvar**.

## Usar o Shell para criar um domínio autoritativo

Para criar um novo domínio autoritativo, use a seguinte sintaxe.

```powershell
New-AcceptedDomain -Name "<Unique Name>" -DomainName <SMTP domain> -DomainType Authoritative
```

Por exemplo, para criar um novo domínio autoritativo chamado "subsidiária de Fourth Coffee" para o domínio fourthcoffee.com, execute o seguinte comando:

```powershell
New-AcceptedDomain -Name "Fourth Coffee subsidiary" -DomainName fourthcoffee.com -DomainType Authoritative
```

## Como saber se essa etapa funcionou?

Para verificar se você criou com êxito um domínio autoritativo, execute uma das seguintes ações:

  - No EAC, navegue até **Fluxo de email** \> **Domínios aceitos**. Verifique se o domínio aceito que você criou está sendo exibido e se o valor de **Tipo de Domínio** é **Autoritativo**.

  - No Shell, execute o comando **Get-AcceptedDomain**. Verifique se o domínio criado por você está sendo exibido e se o valor de **DomainType** é `Authoritative`.

## Etapa 2: Configurar uma política de endereço de email para o domínio autoritativo

Para usar o domínio autoritativo aceito que você criou, é necessário configurar uma política de endereço de email para o domínio autoritativo que atenda aos objetivos de seu cenário. Por exemplo, talvez seja necessário criar uma nova política de endereço de email ou modificar uma política existente. Você pode optar por substituir o endereço de email primário de alguns ou todos os seus destinatários e pode optar por manter ou remover o endereço de email primário. Dois exemplos de cenário são apresentados nesta seção.

## Altere o endereço de email primário existente

Para mudar o endereço de email (de resposta) primário atribuído aos destinatários e manter o endereço de email primário antigo como endereço de email proxy (secundário), execute estas etapas:

## Use o EAC para alterar o endereço de email primário existente

1.  No EAC, navegue até **Fluxo de emails** \> **Políticas de endereço de email**. Selecione a política de endereço de email que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Política de Endereço de Email**, clique na guia **Formato do endereço de email**. Na seção **Formato do endereço de email**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página **Formato do Endereço de Email** exibida, faça as seguintes seleções:
    
      - **Selecione um domínio aceito**   Clique na lista suspensa e selecione o novo domínio autoritativo.
    
      - Selecione **Tornar este formato o endereço de email de resposta**.
    
    Quando terminar, clique em **Salvar**.

4.  Na página **Política de Endereço de Email**, clique em **Salvar** para salvar as alterações na política.

5.  Você receberá um aviso de que a política de endereço de email não será aplicada até você a atualizar. Após a sua criação, selecione-a e, no painel de detalhes, clique em **Aplicar**.

## Use o Shell para alterar o endereço de email primário existente

No Shell, você usa dois comandos separados: um comando para modificar a política de endereço de email existente e outro comando para aplicar a política de endereço de email atualizada para os destinatários em sua organização.

Para alterar o endereço de email primário existente e manter o endereço de email primário antigo como um endereço proxy, execute o seguinte comando:

```powershell
Set-EmailAddressPolicy <EmailAddressPolicyIdentity> -EnabledEmailAddressTemplates SMTP:<NewPrimaryEmailAddress>,smtp:<OldPrimaryEmailAddress>
```

Por exemplo, vamos supor que a política de endereço de email em sua organização use o formato de endereços de email *useralias*`@contoso.com`. Esse exemplo altera o domínio do endereço primário (responder para) na política de endereço de email chamada "Política Padrão" para `@fourthcoffee.com` e mantém o endereço de resposta primário antigo no domínio `@contoso.com` como um endereço proxy (secundário).

```powershell
Set-EmailAddressPolicy "Default Policy" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com,smtp:@contoso.com
```


> [!NOTE]
> O qualificador <CODE>SMTP</CODE> em letra maiúscula especifica o endereço primário (responder para). O qualificador <CODE>smtp</CODE> em letra minúscula especifica um endereço proxy (secundário).



Para aplicar a política de endereço de email atualizada aos destinatários, use a seguinte sintaxe.

```powershell
Update-EmailAddressPolicy <EamilAddressPolicyIdentity>
```

Por exemplo, para aplicar a política de endereço de email atualizada chamada "Política Padrão", execute o seguinte comando:

```powershell
Update-EmailAddressPolicy "Default Policy"
```

## Substituir o endereço de email primário existente de um conjunto filtrado de destinatários

Não é possível modificar a política de endereço de email padrão a fim de aplicar um conjunto filtrado de destinatários. Você precisa criar uma nova política de endereço de email ou modificar uma política de endereço de email personalizada existente. Os exemplos nesta seção criam uma nova política de endereço de email. Nesses exemplos, o endereço primário (responder para) no novo domínio aceito substitui o endereço primário antigo dos destinatários especificados sem manter o endereço primário antigo como um endereço de email proxy (secundário). Portanto, os destinatários afetados não podem mais receber email em seus endereços de email primários antigos.

Além disso, as políticas de endereço de email que se aplicam a usuários específicos devem ter uma prioridade maior (indicada por um valor inteiro inferior) do que outras políticas de endereço de email, incluindo a política padrão, de modo que a política específica seja aplicada primeiro. Como duas políticas não podem ter o mesmo valor de prioridade, primeiro você precisa reduzir a prioridade da política de endereço de email padrão de sua organização.

## Use o EAC para substituir o endereço de email primário existente de um grupo filtrado de destinatários

Para criar endereços de email adicionais que serão usados como endereço de email primário para um conjunto filtrado de destinatários, execute estas etapas.

1.  No EAC, navegue até **Fluxo de emails** \> **Políticas de endereço de email** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página **Política de Endereço de Email**, preencha os seguintes campos:
    
    1.  **Nome da política**   Insira um nome exclusivo e descritivo.
    
    2.  **Formato de endereço de email**   Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na página **Formato do Endereço de Email** exibida, faça as seguintes seleções:
        
          - **Selecione um domínio aceito**   Clique na lista suspensa e selecione o novo domínio autoritativo.
        
          - **Formato de endereço de email**   Selecione o formato de endereço de email apropriado para sua organização.
        
          - Selecione **Tornar este formato o endereço de email de resposta**.
        
        Quando terminar, clique em **Salvar**.

3.  **Executar esta política nesta sequência com outras políticas**   Normalmente, as políticas que se aplicam a usuários específicos devem ter uma prioridade superior (indicada por um valor inteiro menor) do que outras políticas de endereço de email, incluindo a política padrão.

4.  **Especificar os tipos de destinatários aos quais este endereço de email será aplicado**   Selecione os tipos de destinatário aos quais você deseja que a política de endereço de email seja aplicada.

5.  **Criar regras para definir ainda mais os destinatários aos quais essa política de endereço de email se aplica**   Clique em **Adicionar regra** para restringir os destinatários aos quais essa política será aplicada. Isso cria uma instrução **And** booleana. Repita essa etapa quantas vezes forem necessárias.
    

    > [!CAUTION]
    > Se você aplicar muitas regras, será possível restringir a política de endereço de email até o ponto que ela não contenha nenhum usuário.



6.  Clique em **Exibir destinatários aos quais a política se aplica** para exibir os destinatários aos quais a política se aplica.

7.  Clique em **Salvar** para salvar suas alterações e criar a diretiva.

8.  Você receberá um aviso de que a política de endereço de email não será aplicada até você a atualizar. Após a sua criação, selecione-a e, no painel de detalhes, clique em **Aplicar**.

## Use o Shell para substituir o endereço de email primário existente de um grupo filtrado de destinatários

Para substituir o endereço de email primário de um grupo filtrado de destinatários, use o seguinte comando:

```powershell
New-EmailAddressPolicy -Name <Policy Name> -Priority <Integer> -IncludedRecipients <RecipientTypes> <Conditional Recipient Properties> -EnabledEmailAddressTemplates SMTP:@<NewPrimaryEmailAddress>
```

Este exemplo cria uma política de endereço de email chamada "Destinatários de Fourth Coffee", atribui essa política aos usuários de caixa de correio no departamento Fourth Coffee e define a prioridade mais alta para essa política de endereço de email, de modo que a política seja aplicada primeiro. Observe que o endereço de email primário antigo não é preservado para esses destinatários e, portanto, não podem receber email em seus endereços de email primários antigos.

```powershell
New-EmailAddressPolicy -Name "Fourth Coffee Recipients" -Priority 1 -IncludedRecipients MailboxUsers -ConditionalDepartment "Fourth Coffee" -EnabledEmailAddressTemplates SMTP:@fourthcoffee.com
```

Para aplicar a nova política de endereço de email aos destinatários afetados, execute o seguinte comando:

```powershell
Update-EmailAddressPolicy "Fourth Coffee Recipients"
```

## Como saber se essa etapa funcionou?

Para verificar se você configurou com êxito uma política de endereço de email para o domínio autoritativo, execute uma das seguintes ações:

  - No EAC, navegue até **Fluxo de emails** \> **Políticas de endereço de email**. Verifique se as políticas foram aplicadas na ordem correta. Além disso, selecione as políticas novas ou atualizadas e, no painel detalhes, verifique o formato de endereço de email, os destinatários incluídos e se a política foi aplicada,

  - No Shell, execute os comandos **Get-EmailAddressPolicy** e `Get-EmailAddressPolicy "<Policy Name>"| Format-List` para verificar os detalhes das políticas.

## Como saber se essa tarefa funcionou?

Para verificar se você configurou o Exchange para aceitar emails de vários domínios autoritativos, faça o seguinte:

1.  Envie mensagens de teste a um destinatários afetado a partir de uma caixa de correio fora de sua organização do Exchange. Verifique se os endereços de email aceitaram o email.

2.  Envie mensagens de teste de uma caixa de correio de destinatário afetado para um destinatário externo e verifique o endereço De da mensagem.

