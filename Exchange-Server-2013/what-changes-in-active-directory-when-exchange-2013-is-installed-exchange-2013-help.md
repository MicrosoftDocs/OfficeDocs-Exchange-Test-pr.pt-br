---
title: 'O que muda no Active Directory quando o Exchange 2013 é instalado?: Exchange 2013 Help'
TOCTitle: O que muda no Active Directory quando o Exchange 2013 é instalado?
ms:assetid: 07386078-6103-49a2-8698-2d41db9cec95
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn750898(v=EXCHG.150)
ms:contentKeyID: 62371364
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O que muda no Active Directory quando o Exchange 2013 é instalado?

 

_**Aplica-se a:** Exchange Server, Exchange Server 2013_

_**Tópico modificado em:** 2014-05-26_

Quando você instala o Exchange 2013, as alterações são feitas em sua floresta e domínios do Active Directory. O Exchange faz isso de modo que possa armazenar informações sobre os servidores e caixas de correio do Exchange e outros objetos relacionados ao Exchange em sua organização. Essas alterações são feitas para você quando você executa o Assistente de instalação do Exchange 2013 ou quando executa os comandos *PrepareSchema*, *PrepareAD* e *PrepareDomains* (veja como usar esses comandos no [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md)) durante a Configuração da linha de comando do Exchange 2013. Se você estiver curioso sobre as alterações feitas pelo Exchange ao Active Directory, este tópico serve para você. Ele explica o que o Exchange faz em cada etapa da preparação do Active Directory.

Há três etapas que precisam ser executadas a fim de preparar o Active Directory para Exchange:

  - Extend the Active Directory schema

  - Prepare Active Directory containers, objects, and other items

  - Prepare Active Directory domains

Após a conclusão das três etapas, sua floresta do Active Directory está pronta para Exchange 2013. Você pode descobrir mais sobre como instalar o Exchange 2013 lendo [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

## Estender o esquema do Active Directory

A extensão do esquema do Active Directory adiciona e atualiza classes, atributos e outros itens. Essas alterações são necessárias de modo que o Exchange possa criar contêineres e objetos a fim de armazenar informações sobre a organização do Exchange. Como o Exchange faz muitas alterações no esquema do Active Directory, há um tópico dedicado a esta etapa. Para ver todas as alterações feitas no esquema, consulte [Alterações de esquema do Active Directory no Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

Esta etapa é feita automaticamente quando você executa o Assistente de instalação do Exchange 2013 no primeiro servidor do Exchange 2013 na floresta do Active Directory. Também é feita quando você executa a Configuração da linha de comando do Exchange 2013 com o comando *PrepareSchema* (ou opcionalmente com o comando *PrepareAD*) no primeiro servidor Exchange 2013 na floresta. Se você quiser encontrar mais informações sobre como estender o esquema, consulte [Extend the Active Directory schema](prepare-active-directory-and-domains-exchange-2013-help.md) em [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md).

Após o Exchange terminar de estender o esquema, ele define a versão do esquema, que é armazenada no atributo **ms-Exch-Schema-Version-Pt**. Se você quiser se certificar de que o esquema Active Directory foi estendido com êxito, verifique o valor armazenado nesse atributo. Se o valor no atributo corresponder à versão de esquema listada para a versão do Exchange 2013 instalada, a extensão do esquema terá sido bem-sucedida. Para obter uma lista das versões do Exchange e como verificar o valor desse atributo, confira a seção [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) em [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md).

## Preparar contêineres, objetos e outros itens do Active Directory

Como o esquema estendido, a próxima etapa é adicionar todos os contêineres, objetos, atributos e outros itens usados pelo Exchange para armazenar informações no Active Directory. A maioria das alterações feitas nesta etapa é aplicada a toda a floresta do Active Directory. Um conjunto menor de alterações são realizadas no domínio local do Active Directory no qual o comando *PrepareAD* foi executado durante a Instalação.

Estas são as alterações feitas na floresta do Active Directory:

  - O contêiner do Microsoft Exchange é criado sob CN=Services,CN=Configuration,DC=\<*domínio raiz*\>, caso ainda não exista.

  - Os seguintes contêineres e objetos são criados em CN=\<*nome da organização*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*domínio raiz*\>, caso ainda não exista:
    
      - CN=Contêiner de Listas de Endereços
    
      - CN=Políticas de Caixa de Correio do Catálogo de Endereços
    
      - CN=Endereçamento
    
      - CN=Grupos Administrativos
    
      - CN=Aplicativos de Aprovação
    
      - CN=Configuração de Autenticação
    
      - CN=Configuração de Disponibilidade
    
      - CN=Acesso para Cliente
    
      - CN=Conexões
    
      - CN=Contêiner de Pastas ELC
    
      - CN=Políticas de Caixa de Correio ELC
    
      - CN=ExchangeAssistance
    
      - CN=Federação
    
      - CN=Relações de Confiança de Federação
    
      - CN=Configurações Globais
    
      - CN=Configuração Híbrida
    
      - CN=Políticas de Caixa de Correio Móvel
    
      - CN=Configurações de Caixa de Correio Móvel
    
      - CN=Configurações de Monitoramento
    
      - CN=Políticas de Caixa de Correio do OWA
    
      - CN=Contêiner de Política de Provisionamento
    
      - CN=Configurações de Notificação de Push
    
      - CN=RBAC
    
      - CN=Políticas de Destinatário
    
      - CN=Contêiner de Políticas de Contas Remotas
    
      - CN=Container de Políticas de Retenção
    
      - CN=Contêiner de Tag de Política de Retenção
    
      - CN=ServiceEndpoints
    
      - CN=Políticas do Sistema
    
      - CN=Políticas de Provisionamento de Caixa de Correio de Equipe
    
      - CN=Configurações de Transporte
    
      - CN=Contêiner UM AutoAttendant
    
      - CN=Contêiner UM DialPlan
    
      - CN=Contêiner UM IPGateway
    
      - CN=Políticas de Caixa de Correio de UM
    
      - CN=Configurações de Gerenciamento de Carga de Trabalho

  - Os seguintes contêineres e objetos são criados em CN=Configurações de Transporte,CN=\<*Nome da Organização*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*domínio raiz*\>, caso ainda não exista:
    
      - CN=Domínios Aceitos
    
      - CN=Configuração ControlPoint
    
      - CN=Personalização de DNS
    
      - CN=Regras de Interceptador
    
      - CN=Filtro de Malware
    
      - CN=Classificações de Mensagens
    
      - CN=Higienização de Mensagem
    
      - CN=Regras
    
      - CN=MicrosoftExchange329e71ec88ae4615bbc36ab6ce41109e

  - As permissões são definidas por meio da partição de configuração no Active Directory.

  - O arquivo Rights.ldf é importado. Esse arquivo adiciona permissões necessárias para instalar o Exchange e configurar o Active Directory.

  - A unidade organizacional (UO) dos Grupos de Segurança do MicrosoftExchange é criada no domínio raiz da floresta, e as permissões são atribuídas a ela.

  - Os seguintes grupos de função de gerenciamento são criados na UO dos Grupos de Segurança do Microsoft Exchange, caso ainda não existam:
    
      - Gerenciamento de Conformidade
    
      - Instalação Representada
    
      - Gerenciamento de Descobertas
    
      - Suporte Técnico
    
      - Gerenciamento de Higienização
    
      - Gerenciamento da Organização
    
      - Gerenciamento de Pasta Pública
    
      - Gerenciamento de Destinatários
    
      - Gerenciamento de Registros
    
      - Gerenciamento do Servidor
    
      - Gerenciamento de UM
    
      - Gerenciamento da Organização Somente para Exibição

  - Os novos grupos de função de gerenciamento (que aparecem como grupos de segurança universais (USGs) no Active Directory) que foram criados na UO dos Grupos de Segurança do MicrosoftExchange são adicionados ao atributo **otherWellKnownObjects** armazenado no contêiner CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*domínio raiz*\>.

  - O contato Remetente de Voz da Unificação de Mensagens é criado no contêiner Objetos de Sistema do Microsoft Microsoft Exchange do domínio raiz.

  - O domínio no qual o comando *PrepareAD* foi executado está preparado para Exchange 2013. Para obter informações sobre o que foi feito para preparar o domínio do Active Directory para Exchange, confira Preparing Active Directory domains.

  - A propriedade **msExchProductId** no objeto de organização do Exchange está definida. Se você quiser se certificar de que o esquema Active Directory foi estendido com êxito, verifique o valor armazenado nessa propriedade. Se o valor na propriedade corresponder à versão de esquema listada para a versão do Exchange 2013 instalada, a extensão do esquema terá sido bem-sucedida. Para obter uma lista das versões do Exchange e como verificar o valor dessa propriedade, confira a seção [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) em [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md).

## Preparar os domínios do Active Directory

A etapa final para preparar o Active Directory para o Exchange é preparar cada um dos domínios do Active Directory no qual os servidores do Exchange serão instalados ou no qual os usuários habilitados para caixa de correio ficarão localizados. Esta etapa é realizada automaticamente no domínio no qual o comando *PrepareAD* foi executado.

Estas são as alterações feitas nos domínios do Active Directory:

  - O contêiner Objetos do Sistema do Microsoft Exchange é criado na partição de domínio raiz no Active Directory, caso ainda não exista.

  - As permissões são definidas no contêiner Objetos do Sistema do Microsoft Exchange para os grupos de segurança Servidores do Exchange, Gerenciamento de Organização e Usuários Autenticados.

  - O grupo global de domínio dos Servidores de Domínio de Instalação do Exchange é criado no domínio atual e colocado no contêiner de Objetos do Sistema do Microsoft Exchange.

  - O grupo Servidores de Domínio de Instalação do Exchange é adicionado ao USG dos Servidores do Exchange no domínio raiz.

  - As permissões são atribuídas no nível de domínio para o USG dos Servidores do Exchange e o USG de Gerenciamento de Organização.

  - A propriedade **objectVersion** no contêiner Objetos de Sistema do Microsoft Exchange sob DC=\<*domínio raiz*\> é definida. Se você quiser se certificar de que o esquema Active Directory foi estendido com êxito, verifique o valor armazenado nessa propriedade. Se o valor na propriedade corresponder à versão de esquema listada para a versão do Exchange 2013 instalada, a extensão do esquema terá sido bem-sucedida. Para obter uma lista das versões do Exchange e como verificar o valor dessa propriedade, confira a seção [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) em [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md).

