---
title: 'Funcionalidade TLS e terminologia relacionada: Exchange 2013 Help'
TOCTitle: Funcionalidade TLS e terminologia relacionada
ms:assetid: 294ba2a9-892d-4a90-beec-9d298426b5f4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb430753(v=EXCHG.150)
ms:contentKeyID: 52058815
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Funcionalidade TLS e terminologia relacionada

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-06-18_

O Microsoft Exchange Server 2013 fornece funcionalidade administrativa e outros aprimoramentos que melhoram o gerenciamento geral de TLS (Transport Layer Security). Ao trabalhar com essa funcionalidade, você precisa aprender sobre recursos e funcionalidades relacionadas a TLS. Alguns termos e conceitos se aplicam a mais de um recurso relacionado a TLS. Neste tópico, uma breve explicação sobre cada recurso é fornecida e deve ajudá-lo a compreender algumas diferenças e terminologia geral relacionadas a TLS e ao conjunto de recursos de Segurança de Domínio.

  - **Protocolo TLS   **TLS é um protocolo padrão usado para fornecer comunicação segura na Internet ou nas intranets. Ele permite que os clientes autentiquem servidores ou, opcionalmente, que os servidores autentiquem clientes. Fornece também um canal seguro pela criptografia das comunicações. TLS é a versão mais recente do protocolo SSL (Secure Sockets Layer).

  - **TLS Mútuo**   A autenticação de TLS mútuo é diferente do TLS normalmente implantado. Normalmente, quando o TLS é implantado, é usado somente para fornecer confidencialidade na forma de criptografia. Não ocorre autenticação entre o remetente e o destinatário. Além disso, às vezes, quando o TLS é implantado, apenas o servidor de recebimento é autenticado. Essa implantação de TLS é típica na implantação HTTP de TLS. Essa implantação, onde apenas o servidor de destino é autenticado, é SSL.
    
    Com a autenticação mútua de TLS, cada servidor verifica a identidade do outro servidor, validando um certificado fornecido por esse outro servidor. Nesse cenário, quando as mensagens são recebidas de domínios externos através de conexões verificadas em um ambiente do Exchange 2013, o Microsoft Outlook exibe o ícone **Domínio Seguro**.

  - **Segurança de Domínio**   A Segurança de Domínio é o conjunto de recursos, como gerenciamento de certificados, funcionalidade de conector e comportamento do cliente do Outlook que permite TLS mútuo como uma tecnologia gerenciável e útil. A Segurança de Domínio não é suportada quando o email de saída é roteado por um servidor de Acesso para Cliente do Exchange 2013.

  - **TLS Oportunista**   No Exchange 2013, a Instalação cria um certificado autoassinado. Por padrão, TLS é habilitado. Isso permite que qualquer sistema de envio criptografe a sessão SMTP de entrada para o v. Por padrão, o Exchange 2013 também tenta o TLS em todas as conexões remotas.

  - **Confiança direta**   Por padrão, todo o tráfego entre os servidores de Transporte de Borda e de servidores de Caixa de Correio é autenticado e criptografado. Mais uma vez, o mecanismo subjacente de autenticação e criptografia é TLS mútuo. Em vez de usar a validação de X.509, o Exchange 2013 usa a confiança direta para autenticar os certificados. Confiança direta significa que a presença do certificado no Active Directory ou no Active Directory Lightweight Directory Services (AD LDS) valida o certificado. O Active Directory é considerado um mecanismo de repositório confiável. Quando a confiança direta é usada, não importa se o certificado é auto-assinado ou assinado por uma autoridade de certificação. Quando você inscreve um servidor de Transporte de Borda na organização do Exchange, a Inscrição de Borda publica o certificado do servidor de Transporte de Borda no Active Directory para que os servidores de Caixa de Correio o validem. O serviço EdgeSync do Microsoft Exchange atualiza o AD LDS com o conjunto de certificados do servidor de Caixa de Correio para que o servidor de Transporte de Borda os valide.

