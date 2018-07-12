---
title: 'Criar uma solicitação de certificado digital: Exchange 2013 Help'
TOCTitle: Criar uma solicitação de certificado digital
ms:assetid: efb00de7-070b-46bf-a2fc-00d07ae085c1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125165(v=EXCHG.150)
ms:contentKeyID: 52058890
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma solicitação de certificado digital

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-21_

Em Exchange Server 2013, é possível gerenciar certificados usando o EAC ou o Shell. A EAT inclui uma nova interface de usuário de gerenciamento de certificado. Por meio dessa nova interface do usuário, você pode criar um novo certificado, editar um certificado existente ou remover um certificado.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos mais tempo para a resposta da autoridade de certificação.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de "Segurança de servidor de acesso para cliente" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar uma nova solicitação de certificado

1.  No EAC, navegue até **servidores** \> **certificados**.

2.  Na lista **Selecionar servidor**, selecione o servidor para o qual você deseja criar um certificado e, em seguida, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  No Assistente de **certificado do Exchange novo**, escolha **criar uma solicitação de certificado de uma autoridade de certificação** ou **criar um certificado autoassinado** e selecione **Avançar**.

4.  Digite um nome amigável do certificado e selecione **Avançar**.

5.  Se não tiver escolhido um certificado autoassinado e você quiser que um certificado curinga, marque a caixa marcado como **solicitar um certificado curinga**, insira o domínio raiz, por exemplo \*. contoso.com e selecione **Avançar**. Se você escolher um certificado autoassinado, ignore esta etapa.

6.  Selecione os servidores que você deseja aplicar este certificado e selecione **Avançar**.

7.  Especifique os domínios que você deseja ser incluído no seu certificado e selecione **Avançar**.

8.  Verifique se os domínios incluídos estão corretos. Se você escolher um certificado autoassinado, selecione **Concluir**. Caso contrário, selecione **Avançar**.

9.  Insira seu nome de organização, nome de departamento, cidade ou localidade, estado ou província e país ou região e selecione **Avançar**.

10. Digite um local para salvar a solicitação de certificado e selecione **Concluir**.

Se você não selecionou um certificado autoassinado, você precisará enviar o arquivo de solicitação de certificado para a autoridade de certificação para processamento.

## Use o Shell para criar uma nova solicitação de certificado

Execute os seguintes comandos.

```
$reqfile = New-ExchangeCertificate -GenerateRequest -SubjectName "C=US,o=Contoso,cn=contosotocert" -DomainName "contoso.com" -PrivateKeyExportable $true
```
```
    $reqfile | out-file c:\certreq.txt
```

## Como saber se funcionou?

Se você tiver criado um certificado autoassinado, o certificado recém-criado aparecerá na interface do usuário de gerenciamento de certificados. Se você criou uma solicitação de certificado de uma autoridade de certificação, o arquivo de solicitação de certificado será no local especificado. Envie este arquivo à autoridade de certificação.

