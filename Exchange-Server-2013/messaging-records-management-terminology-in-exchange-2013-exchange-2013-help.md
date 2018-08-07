---
title: 'Terminologia de gerenciamento de registros de mensagens no Exchange 2013'
TOCTitle: Registros de mensagens terminologia de gerenciamento no Exchange 2013
ms:assetid: de3e3503-6de3-4666-aeb9-cd877efb93bb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb408414(v=EXCHG.150)
ms:contentKeyID: 50486790
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registros de mensagens terminologia de gerenciamento no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-30_

Este tópico define os principais componentes associados com mensagens (MRM) de gerenciamento de registros no Microsoft Exchange Server 2013. MRM é uma tecnologia de gerenciamento de registros no Exchange 2013 que ajuda as organizações a reduzirem os riscos associados a emails e outras comunicações. MRM torna facilitam manter as mensagens necessárias para cumprir as necessidades legais, regulamentos do governo ou diretiva da empresa e para remover o conteúdo que tenha não legais ou valor ao negócio.

  - **marca de diretiva padrão (DPT)**  
    Um DPT é uma marca de retenção que se aplica a todos os itens em uma caixa de correio que ainda não tem uma marca de retenção aplicada. Você pode ter apenas um DPT em uma política de retenção.

<!-- end list -->

  - **usuário de servidor de dados ou servidor de dados**  
    Um usuário que arquivos regularmente itens de caixa de correio em pastas.
    
    Compare a usuário amontoa ou amontoa.

<!-- end list -->

  - **registro no diário**  
    A capacidade de registrar comunicações, incluindo as comunicações de email, em uma organização para uso em retenção de email ou a estratégia de arquivamento da organização. MRM, registro no diário normalmente se refere ao processo de envio de um relatório de diário sobre as mensagens em uma pasta gerenciada para o endereço SMTP especificado. Esse processo é realizado pelo Assistente de pasta gerenciada.

<!-- end list -->

  - **configurações de conteúdo gerenciado**  
    As informações de retenção criadas para pastas gerenciadas, o recurso MRM disponível no Exchange Server 2007 e Exchange Server 2010. Uma pasta gerenciada pode ter várias configurações de conteúdo para tipos diferentes de mensagens como mensagens de email, caixa postal e itens de calendário. Configurações de retenção de mensagem definidas nas configurações de conteúdo para uma pasta gerenciada aplicam a mensagens nessa pasta gerenciada.

<!-- end list -->

  - **pasta gerenciada**  
    Usado para a funcionalidade MRM no Exchange Server 2007 e Exchange Server 2010, uma pasta gerenciada é gerenciados de um objeto Active Directory que representa uma pasta de caixa de correio para aplicar configurações de conteúdo a ela. Em uma caixa de correio, uma pasta gerenciada é uma pasta para o qual as configurações de conteúdo gerenciado tiverem sido aplicadas.

<!-- end list -->

  - **Assistente de Pasta Gerenciada**  
    Um dos assistentes de caixa de correio do Microsoft Exchange em Exchange 2013. Assistente de pasta gerenciada é responsável por expiração de mensagem, arquivamento e conformidade. Ele processa caixas de correio e aplica as políticas de retenção.

<!-- end list -->

  - **diretiva de caixa de correio de pasta gerenciada**  
    Um agrupamento lógico de pastas gerenciadas. Em Exchange 2010 e Exchange 2007, quando uma diretiva de caixa de correio de pasta gerenciada é aplicada a caixa de correio do usuário, todas as pastas gerenciadas vinculadas à política são implantadas em uma única operação.

<!-- end list -->

  - **marca pessoal**  
    Uma marca pessoal é uma marca de retenção disponível para Outlook Web App e Outlook 2010 e usuários mais recentes para a aplicação de configurações de retenção para pastas personalizadas e itens individuais, como mensagens de email.

<!-- end list -->

  - **usuário amontoa ou amontoa**  
    Um usuário que não arquivo itens de caixa de correio regularmente. Usuários amontoa tendem a ter uma caixa de entrada grande e dependem de pesquisa para localizar mensagens.
    
    Compare a arquivador ou de usuário do servidor de dados.

<!-- end list -->

  - **política**  
    Consulte *a política de retenção* ou *gerenciados a diretiva de caixa de correio de pasta*.

<!-- end list -->

  - **marca de política de retenção (RPT)**  
    Um RPT é uma marca de retenção aplicada às pastas padrão como entrada e itens excluídos.

<!-- end list -->

  - **política de retenção**  
    Uma política de retenção é lógica de agrupamento de marcas de retenção. Quando uma política de retenção é aplicada à caixa de correio de um usuário, todas as marcas de retenção vinculadas à política são implantadas em uma única operação.

<!-- end list -->

  - **marca de retenção**  
    Marcas de retenção são usadas para aplicar configurações de retenção a mensagens e pastas em caixas de correio do usuário. Existem três tipos de marcas de retenção:
    
      - Marcas de diretiva padrão (DPTs)
    
      - Marcas de diretiva de retenção (RPTs)
    
      - Marcas pessoais

