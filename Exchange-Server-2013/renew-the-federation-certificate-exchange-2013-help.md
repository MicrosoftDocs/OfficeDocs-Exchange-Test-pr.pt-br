---
title: 'Renovar o certificado da federação: Exchange 2013 Help'
TOCTitle: Renovar o certificado da federação
ms:assetid: 0f390713-3058-44d0-9c07-3c982616e790
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt779252(v=EXCHG.150)
ms:contentKeyID: 74429171
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Renovar o certificado da federação

 

_**Tópico modificado em:** 2017-02-28_

Este tópico explica como atualizar o certificado autoassinado federação que é usado em uma relação de confiança de Federação:

  - Se o certificado de Federação não tenha expirado, siga as etapas da seção um certificado de Federação do trabalho de atualização .

  - Se o certificado de Federação já tiver expirado, siga as etapas na seção Substituir um certificado de Federação expirados .

Para obter mais informações sobre a federação e relações de confiança de federação, consulte [Federação](federation-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Certificados e federação" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) .

  - Os procedimentos neste tópico usam o Shell de Gerenciamento do Exchange. Para saber como abrir o Shell de Gerenciamento do Exchange em sua organização Exchange local, confira [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)).

  - Para ver se seu certificado de Federação existente tiver expirado, execute o seguinte comando no Shell de Gerenciamento do Exchange:
    
        Get-ExchangeCertificate -Thumbprint (Get-FederationTrust).OrgCertificate.Thumbprint | Format-Table -Auto Thumbprint,NotAfter

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Um certificado de Federação do trabalho de atualização

Se o certificado de Federação não tiver expirado, você poderá atualizar a confiança de Federação existente com um novo certificado de Federação.

## Etapa 1: Criar um novo certificado de Federação

Execute o seguinte comando no Shell de Gerenciamento do Exchange para criar um novo certificado de Federação:

    $SKI = [System.Guid]::NewGuid().ToString("N"); New-ExchangeCertificate -DomainName 'Federation' -FriendlyName "Exchange Delegation Federation" -Services Federation -SubjectKeyIdentifier $SKI -PrivateKeyExportable $true

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-ExchangeCertificate](https://technet.microsoft.com/pt-br/library/aa998327\(v=exchg.150\)).

A saída do comando contém o valor de impressão digital do novo certificado. Você precisará desse valor nas etapas restantes, e você pode copiar o valor diretamente na janela de Shell de Gerenciamento do Exchange:

1.  Com o botão direito em qualquer lugar na janela Shell de Gerenciamento do Exchange e selecione a **marca** na caixa de diálogo que aparece.

2.  Selecione o valor de impressão digital e pressione ENTER.

Para os outros procedimentos neste tópico, usaremos o valor de impressão digital do certificado de Federação: `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`. O valor de impressão digital do certificado será diferente.

## Etapa 2: Configurar o novo certificado como o certificado de Federação

Para usar o Shell de Gerenciamento do Exchange para configurar o novo certificado como o certificado de federação, use a seguinte sintaxe:

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint <Thumbprint> -RefreshMetaData

Este exemplo usa o de valor de impressão digital do certificado `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73` da etapa 1.

    Set-FederationTrust -Identity "Microsoft Federation Gateway" -Thumbprint 6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73 -RefreshMetaData

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-FederationTrust](https://technet.microsoft.com/pt-br/library/dd298034\(v=exchg.150\)).

**Observação:**  A saída do comando contém um aviso de que você precisa atualizar a prova de propriedade de domínio registro TXT no DNS. Você vai fazer isso na próxima etapa.

## Etapa 3: Atualizar a prova de federação de propriedade de domínio registro TXT no DNS externo

Com segurança você pode executar essa etapa agora, porque a prova de propriedade de domínio registro TXT é verificada apenas durante a ativação (etapa 5). No entanto, depois que você atualiza o registro TXT e antes de passar para a próxima etapa, você precisará Reserve algum tempo para o registro TXT atualizado propagar (com base no valor TTL do registro DNS ou tempo de vida).

1.  Encontre os valores necessários para o registro TXT necessário executando o seguinte comando no Shell de Gerenciamento do Exchange:
    
    ```powershell
Get-FederatedDomainProof -DomainName <Domain> | Format-List Thumbprint,Proof
```
    
    Por exemplo, se o seu domínio federado for contoso.com, execute o seguinte comando:
    
    ```powershell
Get-FederatedDomainProof -DomainName contoso.com | Format-List Thumbprint,Proof
```
    
    A saída do comando tem esta aparência:
    
    `Thumbprint : <new certificate thumbprint>` (por exemplo, `6A99CED2E4F2B5BE96C5D17D662D217EF58B8F73`)
    
    `Proof      : <new hash text>` (por exemplo, `znMfbkgSbOQSsWFdsW+gm3to0nZSdE3zbcPPHGVAqdgsLFGsCPuLHiyVbKoPmgyZKX90NH2g1PbCZH0YTQF6oA==`)
    
    `Thumbprint : <old certificate thumbprint>` (por exemplo, `CC9BC204BB4DC60D06FC1F10F3C373DC785DA2A5`)
    
    `Proof      : <old hash text>` (por exemplo, `m4gZX7OLr9iOWYJMVjEklQpoSkPb5hSbcFjD7Q3/vsqmdJ2Z+HcSt7j5pzBKFmEW2s27JYr3xsK2POzAI/8Ffw==`)
    
    Observe que a saída do comando retorna informações para dois prova de domínio registros de propriedade: um para o novo certificado e outro para o certificado atual que você está substituindo. Você pode dizer que é que o valor de impressão digital e o valor de texto de hash que tiver configurado na atual prova de propriedade de domínio registro TXT em seu DNS (pública) externo.

2.  Atualize a prova de federação de propriedade de domínio registro TXT em seu DNS externo. As instruções variará dependendo do seu provedor de DNS, mas você pode editar o registro TXT atual para substituir o valor de texto de hash atual com o novo valor de texto de hash. Para obter mais informações, consulte a seção Exchange Online em [registros de sistema de nome de domínio externo para Office 365](https://go.microsoft.com/fwlink/p/?linkid=265522).

## Etapa 4: Verificar a distribuição do novo certificado de federação para todos os servidores de Exchange

Exchange distribui automaticamente o novo certificado de federação para todos os servidores, mas precisamos verificar a distribuição para que podemos possa continuar.

Para usar o Shell de Gerenciamento do Exchange para verificar a distribuição do novo certificado de federação, execute o seguinte comando:

    $Servers = Get-ExchangeServer; $Servers | foreach {Get-ExchangeCertificate -Server $_ | Where {$_.Services -match 'Federation'}} | Format-List Identity,Thumbprint,Services,Subject

**Observação:**  na Exchange 2010, a saída do cmdlet **Test-FederationCertificate** contém nomes de servidor. A saída do cmdlet no Exchange 2013 ou posterior não inclui os nomes de servidor.

## Etapa 5: Ativar o novo certificado de Federação

Para usar o Shell de Gerenciamento do Exchange para ativar o novo certificado de federação, execute o seguinte comando:

```powershell
Set-FederationTrust -Identity "Microsoft Federation Gateway" -PublishFederationCertificate
```

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-FederationTrust](https://technet.microsoft.com/pt-br/library/dd298034\(v=exchg.150\)).

**Observação:**  A saída do comando contém um aviso de que você precisa atualizar a prova de propriedade de domínio registro TXT no DNS (que já fez na etapa 3).

## Como saber se funcionou?

Para verificar se você tiver atualizado com êxito a confiança de Federação existente com um novo certificado de federação, execute estas etapas:

  - No Shell de Gerenciamento do Exchange, execute o seguinte comando para verificar se o novo certificado está sendo usado:
    
        Get-FederationTrust | Format-List *priv*
    
      - A propriedade **OrgPrivCertificate** deve conter a impressão digital do novo certificado de Federação.
    
      - A propriedade **OrgPrevPrivCertificate** deve conter a impressão digital do certificado (substituído) federação antigo.

  - Na Shell de Gerenciamento do Exchange, substitua *\<user's email address\>* o endereço de email de um usuário na sua organização e execute o seguinte comando para verificar se a relação de confiança de Federação está funcionando:
    
    ```powershell
Test-FederationTrust -UserIdentity <user's email address>
```

## Substituir um certificado de Federação expirados

Se o certificado de Federação já tiver expirado, você precisará remover todos os domínios federados de confiança de Federação e remova e recriar a confiança de Federação.

1.  Se você tiver vários domínios federados, você precisa identificar o domínio compartilhado de domínio primário, portanto, você pode remover última. Para usar o Shell de Gerenciamento do Exchange para identificar o domínio compartilhado principal e todos os domínios federados, execute o seguinte comando:
    
    ```powershell
Get-FederatedOrganizationIdentifier | Format-List AccountNamespace,Domains
```
    
    O valor da propriedade **AccountNamespace** contém o domínio compartilhado principal no formato `FYDIBOHF25SPDLT<primary shared domain>`. Por exemplo, em que o valor `FYDIBOHF25SPDLT.contoso.com`, contoso.com é o domínio compartilhado principal.

2.  Remova cada domínio federado que não seja o domínio compartilhado principal executando o seguinte comando no Shell de Gerenciamento do Exchange:
    
    ```powershell
Remove-FederatedDomain -DomainName <domain> -Force
```

3.  Após ter removido todos os outros domínios federados, remova o domínio compartilhado principal executando o seguinte comando no Shell de Gerenciamento do Exchange:
    
    ```powershell
Remove-FederatedDomain -DomainName <domain> -Force
```

4.  Remova a confiança de federação, executando o seguinte comando no Shell de Gerenciamento do Exchange:
    
    ```powershell
Remove-FederationTrust "Microsoft Federation Gateway"
```

5.  Recrie a relação de confiança de Federação. Para obter instruções, consulte [Criar uma Confiança de Federação](https://technet.microsoft.com/pt-br/library/dd335198\(v=exchg.150\)).

