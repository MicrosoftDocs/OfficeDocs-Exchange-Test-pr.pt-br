---
title: 'Configurar coleção de certificados virtuais para validar S/MIME'
TOCTitle: Configurar coleção de certificados virtuais para validar S/MIME
ms:assetid: 04a616e6-197c-490c-ae8c-c8d5f0f0b3dd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn626155(v=EXCHG.150)
ms:contentKeyID: 61212689
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar coleção de certificados virtuais para validar S/MIME

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Como um administrador de locatário, você precisará configurar uma coleção de certificados virtuais que será usada para validar certificados S/MIME. Esta coleção de certificados virtuais é configurada como um tipo de arquivo de repositório de certificados com uma extensão de nome de arquivo SST. O arquivo SST contém todos os certificados raiz e intermediários usados na validação de um certificado S/MIME.

## Criar e salvar um SST

Você só pode usar o Shell para executar esse procedimento. Para saber como abrir o Shell de Gerenciamento do Exchange em sua organização Exchange local, confira [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)). Para saber como usar o Windows PowerShell para se conectar ao Exchange Online, confira o artigo [Conectar-se ao Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

Como administrador, você pode criar esse arquivo SST exportando os certificados de uma máquina confiável usando o cmdlet `Export-Certificate` e especificando o tipo como SST. Para obter mais informações o cmdlet `Export-Certificate` , consulte o tópico de referência de [Certificado de exportação](https://technet.microsoft.com/en-us/library/hh848628.aspx) .

Assim que o arquivo SST for gerado, use o cmdlet `Set-Smimeconfig` para salvá-lo no repositório de certificados virtuais usando o parâmetro *-SMIMECertificateIssuingCA*. Por exemplo: `Set-SmimeConfig -SMIMECertificateIssuingCA (Get-Content filename.sst -Encoding Byte)`

## Garantir que um certificado seja válido

O Exchange 2013 SP1 primeiro verifica o arquivo SST e valida o certificado. Se a validação falhar, ele examinará o repositório de certificados da máquina local para validar o certificado. Esse comportamento é novo no Exchange 2013 SP1 e diferente de versões anteriores do Exchange. No Exchange Online, somente o SST será usado para validação.

## Mais informações

[S/MIME para assinatura e criptografia de mensagens](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)

[Get-SmimeConfig](https://technet.microsoft.com/pt-br/library/dn554257\(v=exchg.150\))

