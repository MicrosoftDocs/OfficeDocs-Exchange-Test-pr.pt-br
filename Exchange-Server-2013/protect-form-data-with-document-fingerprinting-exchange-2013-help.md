---
title: 'Proteger os dados de formulário com a impressão digital de documento: Exchange 2013 Help'
TOCTitle: Proteger os dados de formulário com a impressão digital de documento
ms:assetid: 110c839b-7693-42f6-aa5d-58ce64f4c357
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn635175(v=EXCHG.150)
ms:contentKeyID: 61203500
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Proteger os dados de formulário com a impressão digital de documento

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-09-11_

Se a sua organização usa formulários para coletar informações confidenciais, os usuários podem tentar enviar esses formulários por email para contatos externos, o que criará um risco de segurança. A Prevenção contra perda de Dados (DLP) no Exchange ajuda a proteger essas informações detectando-as com a [Impressão Digital de Documento](overview-of-document-fingerprinting-in-exchange.md). Para usar a impressão digital de documentos basta carregar um formulário em branco, como um documento de propriedade intelectual, um formulário governamental ou outro formulário padrão usado em sua organização. Em seguida, adicione a impressão digital de documento resultante a uma política de DLP ou a uma regra de transporte. Veja como.

> [!VIDEO https://www.microsoft.com/pt-br/videoplayer/embed/0f803e16-397a-4b83-8a85-06cd4264aaca]

## Usar o EAC para criar uma impressão digital de documento

![Caminho para Impressão Digital de Documento na EAT realçada](images/Dn635175.e8562ea7-40ba-4feb-adde-2e81f029fcda(EXCHG.150).png "Caminho para Impressão Digital de Documento na EAT realçada")

1.  No Centro de Administração do Exchange, vá para **gerenciamento de conformidade** \> **prevenção de perda de dados**.

2.  Clique em **Gerenciar impressões digitais de documento**.

3.  Na página das impressões digitais de documento, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para criar uma nova impressão digital de documento.

4.  Dê à impressão digital de documento um **Nome** e uma **Descrição**. (O nome escolhido aparecerá na lista de tipos de informação confidencial).

5.  Para carregar um formulário, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

6.  Escolha um formulário e clique em **Abrir**. (Certifique-se de que o arquivo que você carregar contém texto, não está protegido por senha e está em um dos tipos de arquivo suportados no regras de transporte. Para obter uma lista dos tipos de arquivo com suporte, consulte [Usar regras de fluxo de email para inspecionar anexos de mensagens no Office 365](https://technet.microsoft.com/pt-br/library/jj919236\(v=exchg.150\)). Caso contrário, você receberá um erro ao tentar criar a impressão digital.) Repita para quaisquer arquivos adicionais que você deseja adicionar à lista de documento para este impressão digital de documento. Também é possível adicionar ou remover arquivos deste impressão digital de documento mais tarde se desejar.

7.  Clique em **Salvar**.

A impressão digital de documento faz parte do seus tipos de informações confidenciais, e você pode adicioná-lo a uma política de DLP ou adicioná-lo a uma regra de transporte via a condição **a mensagem contém informações confidenciais …**.

![Condição "Aplicar esta regra se" realçada](images/Dn635175.9355a513-a790-48eb-a61b-575ba2ecdfa6(EXCHG.150).png "Condição \"Aplicar esta regra se\" realçada")

Para obter mais informações sobre a adição de regras a uma política de DLP, consulte a seção "Alterar uma política DLP" em [Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md) e, para obter mais informações sobre a modificação de regras de transporte, consulte [Integrando regras de informações confidenciais com regras de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md). Se você quiser criar uma nova política, consulte [Criar uma política de DLP a partir de um modelo](how-to-new-dlp-data-loss-prevention-policy-template.md).

## Usar o Shell para criar um pacote de regras de classificação com base na impressão digital de documento


> [!TIP]
> Mesmo que você pode criar e modificar os pacotes de regras de classificação no Shell, você pode achar que a criação de impressões digitais de documento é um pouco mais simples no EAC. Recomendamos que você experimente lá antes de tentar este procedimento no Shell.



O DLP usa pacotes de regras de classificação para detectar conteúdo confidencial em mensagens. Para criar um pacote de regras de classificação com base em uma impressão digital de documento, use os cmdlets **New-Fingerprint** e **New-DataClassification**. Como os resultados de **New-Fingerprint** não são armazenados fora da regra de classificação de dados, você sempre executa **New-Fingerprint** e **New-DataClassification** ou **Set-Dataclassification** na mesma sessão do PowerShell. Este exemplo cria uma nova impressão digital de documento baseada no arquivo CC:\\My Documents\\Contoso Employee Template.docx. A nova impressão digital é armazenada como uma variável, para que você possa usá-la com o cmdlet **New-DataClassification** na mesma sessão do PowerShell.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Employee Template.docx" -Encoding byte
    $Employee_Fingerprint = New-Fingerprint -FileData $Employee_Template -Description "Contoso Employee Template"

Este exemplo cria uma nova regra de classificação de dados chamada "Contoso Employee Confidential" que usa as impressões digitais de documento do arquivo C:\\My Documents\\Contoso Customer Information Form.docx.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Customer Information Form.docx" -Encoding byte
    $Customer_Fingerprint = New-Fingerprint -FileData $Customer_Form -Description "Contoso Customer Information Form"
    New-DataClassification -Name "Contoso Customer Confidential" -Fingerprints $Customer_Fingerprint -Description "Message contains Contoso customer information." 

Agora você pode usar o cmdlet **Get-DataClassification** para encontrar todos os pacotes de regras de classificação de dados de DLP e, neste exemplo, \&quot;Contoso Customer Confidential\&quot; faz parte da lista de pacotes de classificação de dados.

Por fim, adicione o pacote de regras de classificação de dados "Contoso Customer Confidential" a uma política de DLP.

    New-TransportRule -Name "Notify :External Recipient Contoso confidential" -NotifySender NotifyOnly -Mode Enforce -SentToScope NotInOrganization -MessageContainsDataClassification @{Name=" Contoso Customer Confidential"}

O agente de DLP agora detecta documentos que correspondem à impressão digital do documento Contoso Customer Form.docx.

Para obter informações sobre sintaxe e parâmetros, consulte [New-Fingerprint](https://technet.microsoft.com/pt-br/library/dn584142\(v=exchg.150\)), [New-DataClassification](https://technet.microsoft.com/pt-br/library/dn584139\(v=exchg.150\)), [Set-DataClassification](https://technet.microsoft.com/pt-br/library/dn584141\(v=exchg.150\)) e [Get-DataClassification](https://technet.microsoft.com/pt-br/library/jj215720\(v=exchg.150\)).

## Para obter mais informações

[Impressão Digital de Documento](overview-of-document-fingerprinting-in-exchange.md)

[Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md)

[Integrando regras de informações confidenciais com regras de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

