---
title: 'Importar ou exportar certificados para UM: Exchange 2013 Help'
TOCTitle: Importar ou exportar certificados para Unificação de mensagens
ms:assetid: ee688c33-2e08-47e7-95fc-04ba10238341
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn205143(v=EXCHG.150)
ms:contentKeyID: 54651990
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importar ou exportar certificados para Unificação de mensagens

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-12-18_

Você pode usar o EAC ou o Shell para importar ou exportar PKI (infraestrutura de chave pública) interna e autoassinada ou certificados comerciais de terceiros. Para UM (Unificação de Mensagens), você pode usar um desses certificados para o serviço Unificação de Mensagens do Microsoft Exchange e para o serviço Roteador de Chamadas da Unificação de Mensagens do Microsoft Exchange. O mesmo certificado pode ser usado para os dois serviços ou um certificado diferente pode ser usado para cada serviço.

A importação de certificados para o Exchange pode ser útil quando você quer:

  - Importar um certificado que foi exportado para um arquivo.

  - Importar um arquivo de certificado PKI gerado por uma autoridade de certificação interna.

  - Importar um certificado comercial de terceiros.

A exportação de um certificado existente do repositório de certificados do servidor Exchange local pode ser útil quando você quer:

  - Exportá-lo para que ele possa ser importado em outro servidor Exchange.

  - Exportá-lo para que ele possa ser importado em um gateway VoIP, PBX IP ou PBX habilitado para SIP.

  - Exportar o certificado para que você possa fazer backup do certificado e sua chave privada.

Para saber mais sobre outras tarefas de gerenciamento de certificados para Unificação de Mensagens, veja [Implantar certificados para os procedimentos de Unificação de mensagens](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de certificados" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) e entrada "Serviço UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md). Você também precisa fazer logon usando uma conta que seja membro do grupo local Administradores, nesse computador.

  - Antes de exportar um certificado, use o cmdlet **Get-ExchangeCertificate** para verificar se o atributo *PrivateKeyExportable* no certificado foi definido como `$true`.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para exportar um certificado

1.  No EAC, clique em **Servidores** \> **Certificados** \> **Mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") e então clique em **Exportar certificado do Exchange**.

2.  Na página **Exportar certificado do Exchange**, na caixa **Arquivo a ser exportado para**, digite o nome do arquivo de certificado.

3.  Na caixa **Senha**, digite a senha que você quer usar para proteger a chave privada e depois clique em **OK**.

## Usar o Shell para exportar um certificado

Este exemplo exporta o certificado com a impressão digital A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC para um arquivo, depois que você é solicitado a fornecer nome de usuário e senha.

    $file = Export-ExchangeCertificate -Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC -BinaryEncoded:$true -Password (Get-Credential).password

Esse exemplo faz o seguinte:

1.  Usa o cmdlet **Get-ExchangeCertificate** para localizar o certificado a ser exportado.

2.  Usa o cmdlet **Export-ExchangeCertificate** para definir a senha do certificado.

3.  Envia o certificado para um arquivo, depois que você fornece nome de usuário e senha.

<!-- end list -->

```
    $file = Get-ExchangeCertificate -DomainName umcorp.northwindtraders.com | Export-ExchangeCertificate -BinaryEncoded:$true -Password (Get-Credential).password
```
```
```powershell
Set-Content -Path "d:\umcerts\selfsigned.pfx" -Value $file.FileData =Encoding Byte
```
```

## Usar o EAC para importar um certificado

1.  No EAC, clique em **Servidores** \> **Certificados** \> **Mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") e então clique em **Importar certificado do Exchange**.

2.  Na página **Importar certificado do Exchange**, na caixa **Arquivo a ser importado para**, digite o caminho de pasta compartilhada e o nome do arquivo de certificado. Se o certificado estiver protegido com uma senha, digite essa senha na caixa **Senha** e clique em **Avançar**.

3.  Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para selecionar os servidores aos quais o certificado será aplicado e, depois, clique em **OK**. Se quiser remover um servidor da exibição de lista, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover") e depois clique em **Concluir**.

## Usar o Shell para importar um certificado

Este exemplo importa um certificado do arquivo de certificado d:\\certificates\\exchange\\SelfSignedUMCert.pfx depois que você fornece nome de usuário e senha.

    Import-ExchangeCertificate -FileData ([Byte[]]$(Get-Content -Path d:\certificates\exchange\SelfSignedUMCert.pfx -Encoding Byte -ReadCount 0)) -Password:(Get-Credential).password

