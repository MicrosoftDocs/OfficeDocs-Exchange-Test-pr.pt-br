---
title: 'Interface de usuário de gerenciamento de certificados do Exchange 2013'
TOCTitle: Interface de usuário de gerenciamento de certificados do Exchange 2013
ms:assetid: 8975848d-07f0-4643-9eac-20aece69945f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ984582(v=EXCHG.150)
ms:contentKeyID: 52058854
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interface de usuário de gerenciamento de certificados do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-04-21_

O gerenciamento de certificados em uma implantação do Exchange Server é uma das tarefas administrativas mais importantes. Para fornecer uma infraestrutura de mensagens segura para a empresa, é essencial garantir que os certificados sejam apropriadamente definidos e configurados. No Exchange 2010, o Console de Gerenciamento do Exchange (EMC) era o principal método de gerenciamento de certificados. No Exchange 2013, a funcionalidade de gerenciamento de certificados é fornecida no Centro de Administração do Exchange (EAC), a nova interface administrativa do usuário do Exchange 2013. O Exchange 2013 concentra-se em reduzir a quantidade de certificados que um administrador deve gerenciar, minimizar a interação que o administrador deve ter com certificados e permitir o gerenciamento de certificados em um local central.

## Certificados de servidor de Acesso para Cliente

O servidor de Acesso para Cliente do Exchange 2013 é um servidor thin e sem monitoramento de estado, projetado para aceitar conexões de entrada de clientes e encaminhá-las para o servidor de Caixa de Correio certo. A interface de usuário de Gerenciamento de Certificados do Exchange no servidor de Acesso para Cliente pode ajudá-lo com várias tarefas, inclusive na solicitação de novos certificados e na renovação de certificados expirados ou prestes a expirar.

## Noções básicas da interface de usuário de Gerenciamento de Certificados

Você pode acessar a interface de usuário de Gerenciamento de Certificados do Exchange no EAC selecionando **Servidores** e **Certificados**. Com a interface de usuário de gerenciamento, você pode realizar estas ações:

  - **Criar um novo certificado**   Selecione **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para iniciar o assistente Novo Certificado do Exchange.

  - **Editar um certificado existente**   Selecione **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") em um certificado válido para ver a página de propriedades do certificado.

  - **Excluir um certificado**   Selecione **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone") quando um certificado estiver selecionado para iniciar a caixa de diálogo de confirmação da exclusão.

  - **Executar ações adicionais**   Selecione **Mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") para exportar ou importar um certificado. Se quiser exportar um certificado, este deve ser válido.

## Expiração do certificado

Nas versões anteriores do Microsoft Exchange, não era fácil ver quando um certificado digital estava prestes a expirar. No Exchange 2013, a central de notificações exibe avisos quando um certificado armazenado em qualquer servidor de Acesso para Cliente do Exchange 2013 está prestes a expirar.

## Certificados do servidor de Caixa de Correio

Uma grande diferença entre o Exchange 2010 e o Exchange 2013 é que os certificados usados no servidor de Caixa de Correio do Exchange 2013 são autoassinados. Como os clientes se conectam a um servidor de Caixa de Correio do Exchange 2013 por meio de um servidor de Acesso para Cliente do Exchange 2013, os únicos certificados que precisam ser gerenciados são os do servidor de Acesso para Cliente. O servidor de Acesso para Cliente confia automaticamente no certificado autoassinado no servidor Caixa de Correio; portanto, os clientes não receberão avisos sobre um certificado autoassinado não confiável, desde que o servidor de Acesso para Cliente tenha um certificado que não seja autoassinado, proveniente de uma autoridade de certificação (AC) do Windows ou de um terceiro confiável. Não há ferramentas, nem cmdlets disponíveis para gerenciar certificados autoassinados no servidor Caixa de Correio. Depois que o servidor tiver sido adequadamente instalado, você nunca mais precisará se preocupar com os certificados do servidor de Caixa de Correio.

## Expiração de certificado autoassinado

Por padrão, o certificado autoassinado instalado no servidor de Caixa de Correio do Exchange 2013 expirará cinco anos depois da data de instalação.

## Cmdlets de certificados

Você pode usar estes cmdlets para gerenciar certificados digitais em um servidor de Acesso para Cliente do Exchange:

  - Import-ExchangeCertificate   Esse cmdlet é usado para importar certificados em um servidor. Importe um certificado assinado por uma autoridade de certificação (para concluir uma solicitação pendente de assinatura de certificado \[CSR\]) ou um certificado com uma chave privada (arquivos PKCS \#12, geralmente com a extensão .pfx, exportados de um servidor com a chave privada).

  - Remove-ExchangeCertificate   Este cmdlet é usado para remover certificados de um servidor.

  - Enable-ExchangeCertificate   Este cmdlet é usado para atribuir serviços a um certificado.

  - Get-ExchangeCertificate   Este cmdlet é usado para recuperar um certificado do Exchange de acordo com vários critérios.

  - New-ExchangeCertificate   Este cmdlet é usado para criar um novo certificado autoassinado ou uma CSR.

