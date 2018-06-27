---
title: 'Relações da organização: Exchange 2013 Help'
TOCTitle: Relações da organização
ms:assetid: 4c48db61-3370-462b-a3f8-2a6311c6e4ee
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657445(v=EXCHG.150)
ms:contentKeyID: 50485529
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Relações da organização

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-02-20_

Configure um relacionamento de organização para compartilhar informações de calendário com um parceiro comercial externo. Os administradores do Exchange podem configurar um relacionamento de organização com uma organização do Office 365 ou com outra organização local do Exchange. Se quiser compartilhar calendários com outra organização local do Exchange, os administradores locais do Exchange terão de configurar um relacionamento de autenticação com a nuvem (também conhecido como "federação") e deverão atender aos requisitos mínimos de software.

Um relacionamento de organização é um relacionamento um-para-um entre empresas para permitir que os usuários de cada organização exibam informações de disponibilidade de calendário. Quando você configura o relacionamento de organização, está configurando seu lado do relacionamento e especificando o nível de informação que os usuários da organização externa poderão exibir. A organização externa poderá definir as mesmas configurações ou configurações diferentes no lado dela. Por exemplo, se a Contoso criar um relacionamento de organização com a Tailspin Toys, os usuários da Tailspin Toys poderão agendar reuniões com os usuários da Contoso adicionando o endereço de email deles ao convite da reunião. A disponibilidade do usuário convidado da Contoso seria exibida para o usuário da Tailspin Toys. Entretanto, antes que a Contoso também possa ver a disponibilidade de usuários na Tailspin Toys, o administrador deles precisará configurar um relacionamento de organização com a Contoso.

Existem três níveis de acesso que você pode especificar:

  - Sem acesso

  - Acesso somente a informações de hora da disponibilidade

  - Acesso à disponibilidade, incluindo hora, assunto e local


> [!TIP]
> Se os usuários não quiserem compartilhar as informações de disponibilidade com outras pessoas, poderão alterar a entrada de permissão Padrão no Outlook. Para tanto, os usuários devem acessar a guia <STRONG>Propriedades do Calendário</STRONG> &gt; <STRONG>Permissões</STRONG>, selecionar a permissão <STRONG>Padrão</STRONG> e selecionar <STRONG>Nenhum</STRONG> na lista <STRONG>Nível de Permissão</STRONG>. Suas informações de disponibilidade não serão vistas por usuários internos ou externos, mesmo se houver um relacionamento de organização. As permissões definidas pelo usuário serão aplicadas.



Os tópicos a seguir o ajudarão a configurar e gerenciar relacionamentos de organização como parte do compartilhamento de sua organização:

[Criar um relacionamento de organização](create-an-organization-relationship-exchange-2013-help.md)

[Modificar um relacionamento de organização](modify-an-organization-relationship-exchange-2013-help.md)

[Remover um relacionamento de organização](remove-an-organization-relationship-exchange-2013-help.md)

Procurando por mais informações sobre compartilhamento federado? Consulte [Compartilhamento](sharing-exchange-2013-help.md).

