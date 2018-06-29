---
title: 'Configurando o Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurando o Outlook Voice Access
ms:assetid: 5ce8c877-35f3-4e55-a65e-5ca469aeae99
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298010(v=EXCHG.150)
ms:contentKeyID: 50556195
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurando o Outlook Voice Access

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-03-09_

O Microsoft Outlook Voice Access permite que usuários habilitados para Unificação de Mensagens (UM) do Exchange acessem suas caixas de correio usando telefones analógicos, digitais ou celulares.

Um usuário do Outlook Voice Access (também chamado de *assinante*) é o usuário em uma organização que está habilitado para Unificação de Mensagens. Os assinantes usam o Outlook Voice Access para acessar suas caixas de correio por telefone para recuperar email, mensagens de caixa postal, contatos pessoais e informações de calendário.

**Sumário**

Outlook Voice Access overview

Outlook Voice Access interfaces

Outlook Voice Access scenarios

Distribution groups and contact groups

Choosing a language

Controlling Outlook Voice Access features

## Visão geral do Outlook Voice Access

Na UM do Microsoft Exchange, um usuário habilitado para UM pode fazer uma chamada para um número de telefone interno ou externo configurado para um plano de discagem da UM para acessar sua caixa de correio e usar o sistema de menu do Outlook Voice Access. Usando esse menu, os usuários habilitados para UM podem ler email, ouvir mensagens de voz, interagir com o calendário do Outlook, acessar seus contatos pessoais e executar tarefas como configurar o PIN do Outlook Voice Access e gravar saudações para caixa postal.

Dois tipos de usuários autenticados e não autenticados, podem ligar para um número do Outlook Voice Access. Quando um usuário autenticado disca para um número do Outlook Voice Access que está definido em um plano de discagem de UM, eles só são capazes de fazer pesquisas de diretório para usuários. Usuários autenticados, aqueles que insira seu PIN, podem realizar pesquisas de diretório e entrar suas caixas de correio para ouvir emails, itens de calendário e caixa postal e pesquisar contatos pessoais. Quando eles estão procurando por um usuário no diretório ou contatos pessoais, depois que o usuário está localizado, eles podem transferir chamadas para um usuário ou ligar para o ramal do usuário.

## Interfaces do Outlook Voice Access

Duas interfaces de usuário de Unificação de Mensagens estão disponíveis para usuários do Outlook Voice Access: a TUI (interface do usuário de telefone) e a VUI (interface do usuário de voz), que usam ASR (Reconhecimento Automático de Fala).

Antes que os usuários podem usar a VUI no Outlook Voice Access, ele deve ser ativado em UM plano de discagem e sobre a diretiva de caixa de correio de Unificação de mensagens e também ser habilitado para o usuário. Por padrão, quando você cria um plano de discagem e uma diretiva de caixa de correio UM e habilitar a caixa postal de um usuário, o usuário pode usar a VUI do Outlook Voice Access ou ASR para navegar pelos menus, mensagens e outras opções. No entanto, mesmo que o usuário seja capaz de usar a VUI, eles terão usar o teclado de telefone principais para digitar seu PIN, navegue opções pessoais e executar uma pesquisa de diretório. As configurações padrão são listadas na tabela a seguir.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente de UM</th>
<th>Configuração padrão</th>
<th>Exemplo de Shell de Gerenciamento do Exchange para habilitar o acesso à VUI</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Plano de discagem de UM</p></td>
<td><p>Habilitado</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -AutomaticSpeechRecognitionEnabled  $true</code></p></td>
</tr>
<tr class="even">
<td><p>Diretiva de caixa de correio do UM</p></td>
<td><p>Habilitado</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyUMPolicy -AllowAutomaticSpeechRecognition  $true</code></p></td>
</tr>
<tr class="odd">
<td><p>Caixa de correio do usuário</p></td>
<td><p>Habilitado</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -AutomaticSpeechRecognitionEnabled $true</code></p></td>
</tr>
</tbody>
</table>


A seção a seguir inclui os cenários que descrevem a funcionalidade da VUI.

Voltar ao início

## Cenários do Outlook Voice Access

Aqui, exemplos de como o Outlook Voice Access pode ser usado em um telefone:

  - **Acessar email**   Um usuário do Outlook Voice Access faz uma chamada para o número do Outlook Voice Access a partir de um telefone e deseja acessar seu email. O prompt de voz diz, "Bem-vindo. Você está conectado ao Microsoft Exchange. Para acessar sua caixa de correio, digite seu ramal. Para entrar em contato com alguém, pressione a tecla de cerquilha". Depois que o usuário digita um número de ramal de caixa de correio, o prompt de voz diz "Digite seu PIN e pressione a tecla de cerquilha". Depois que o usuário digita seu PIN, o prompt de voz diz, "Você tem duas novas mensagens de voz, 10 novas mensagens de email e sua próxima reunião é às 10h00. Diga mensagem de voz, email, calendário, contatos pessoais, diretório ou opções pessoais". Quando o usuário disser "Email", o sistema de caixa postal lerá o cabeçalho da mensagem e, em seguida, o nome, o assunto, o horário e a prioridade das mensagens que estão na caixa de correio do usuário.

  - **Acessar calendário**   Um usuário do Outlook Voice Access faz uma chamada para o número do Outlook Voice Access a partir de um telefone e deseja acessar seu calendário. O prompt de voz diz, "Bem-vindo. Você está conectado ao Microsoft Exchange. Para acessar sua caixa de correio, digite seu ramal. Para entrar em contato com alguém, pressione a tecla de cerquilha". Depois que o usuário digita um número de ramal de caixa de correio, o prompt de voz diz "Digite seu PIN e pressione a tecla de cerquilha". Depois que o usuário digita seu PIN, o prompt de voz diz, "Você tem duas novas mensagens de voz, 10 novas mensagens de email e sua próxima reunião é às 10h00. Diga mensagem de voz, email, calendário, contatos pessoais, diretório ou opções pessoais". Quando o usuário disser "Calendário", o sistema de caixa postal dirá "Certo, e qual dia devo abrir?" O usuário diz, "Calendário de hoje". O sistema de caixa postal responde dizendo, "Abrindo calendário de hoje". O sistema de caixa postal lê para o usuário cada um dos compromissos de calendário do dia.
    

    > [!TIP]
    > Se um servidor de Caixa de Correio que executa o serviço UM do Microsoft Exchange encontrar um item de calendário corrompido na caixa de correio de um usuário, ele não o lerá, retornará o chamador para o menu principal do Outlook Voice Access e deixará de ler qualquer compromisso adicional que possa estar agendado para o resto do dia.



  - **Acessar caixa postal**   Um usuário do Outlook Voice Access faz uma chamada para o número do Outlook Voice Access a partir de um telefone e deseja acessar sua caixa postal. O prompt de voz diz, "Bem-vindo. Você está conectado ao Microsoft Exchange. Para acessar sua caixa de correio, digite seu ramal. Para entrar em contato com alguém, pressione a tecla de cerquilha". Depois que o usuário digita um número de ramal de caixa de correio, o prompt de voz diz "Digite seu PIN e pressione a tecla de cerquilha". Depois que o usuário digita seu PIN, o prompt de voz diz, "Você tem duas novas mensagens de voz, 10 novas mensagens de email e sua próxima reunião é às 10h00. Diga mensagem de voz, email, calendário, contatos pessoais, diretório ou opções pessoais". O usuário diz "Caixa postal" e o sistema de caixa postal lê o cabeçalho da mensagem e, em seguida, o nome, o assunto, o horário e a prioridade das mensagens de voz que estão na caixa de correio do usuário.
    

    > [!TIP]
    > Se o reconhecimento de fala estiver habilitado, os usuários podem acessar suas caixas de correio habilitado usando a entrada de fala. Os assinantes também podem usar multifreqüência de tom de discagem por tom, também conhecido como dual (DTMF), pressionando 0. Reconhecimento de fala não está habilitado para entrada de PIN.



  - **Localizar um usuário no diretório**   Um usuário do Outlook Voice Access faz uma chamada para um número do Outlook Voice Access a partir de um telefone e deseja localizar uma pessoa no diretório, soletrando o alias de email. O prompt de voz diz, "Bem-vindo. Você está conectado ao Microsoft Exchange. Para entrar em contato com alguém, pressione a tecla de cerquilha". O usuário pressiona a tecla de cerquilha e, em seguida, usa entradas de discagem por tom para soletrar o endereço SMTP da pessoa.
    

    > [!TIP]
    > O recurso de pesquisa de diretório com um número do Outlook Voice Access não está habilitado para fala. Os usuários poderão soletrar o nome da pessoa com quem deseja entrar em contato, usando apenas as entradas de discagem por tom.

    

    > [!IMPORTANT]
    > Em algumas empresas (principalmente no Leste Asiático), é possível que os telefones de escritórios não tenham letras nas teclas do aparelho. Isso praticamente inviabiliza o uso do recurso soletrar o nome que usa a interface de discagem por tom, sem o conhecimento do funcionamento dos mapeamentos de teclas. Por padrão, a Unificação de Mensagens usa o mapeamento de teclas E.161. Por exemplo, 2=ABC, 3=DEF, 4=GHI, 5=JKL, 6=MNO, 7=PQRS, 8=TUV, 9=WXYZ.

    
    Ao inserir uma combinação de letras e números, como "Mike1092", os dígitos numéricos são mapeados para si mesmos. Para que o alias de email Mike1092 seja inserido corretamente, o usuário precisa pressionar os números 64531092. Além disso, para caracteres que não são alfanuméricos (de A a Z e de 0 a 9), não há uma tecla de telefone equivalente. Portanto, esses caracteres não devem ser inseridos. Por exemplo, o alias de email jim.wilson seria inserido como 546945766. Embora existam 10 caracteres a serem inseridos, o usuário digitará apenas 9 dígitos porque não há nenhum dígito equivalente para o ponto (.).

Voltar ao início

## Grupos de distribuição e grupos de contatos

Os usuários podem utilizar o Outlook Voice Access para enviar ou encaminhar uma mensagem de voz, um email ou uma solicitação de reunião. Eles podem enviar ou encaminhar a mensagem ou a solicitação de reunião a qualquer uma das seguintes opções:

  - Uma pessoa na sua pasta de contatos pessoais

  - Uma pessoa no catálogo de endereços compartilhado da sua organização

  - Um grupo de contacto que eles criaram em sua pasta de contatos

  - Um grupo de distribuição incluído no catálogo de endereços compartilhado da sua organização

Eles podem enviar mensagens e solicitações de reunião usando a VUI (se o ASR tiver sido ativado) ou usando entradas de discagem por tom no teclado do telefone. É possível usar também o Outlook Voice Access para escutar os detalhes sobre um grupo, incluindo os membros do grupo.


> [!TIP]
> Se um usuário tentar enviar uma mensagem a um grupo (um grupo de distribuição no catálogo de endereços compartilhado ou um grupo de contatos na pasta de contatos pessoais) que não possui nenhum membro, o sistema de caixa postal não apresentará a opção de enviar ou encaminhar a mensagem ou a solicitação de reunião. Se eles tentarem adicionar um grupo sem nenhum membro como um dos destinatários de uma mensagem ou solicitação de reunião que estão criando no telefone, o sistema de caixa postal não adicionará o grupo à mensagem e dirá "Não foi possível enviar a mensagem porque o contato não parece ser um endereço de email válido".



## Escolhendo um idioma

Os usuários não podem alterar o idioma utilizado pelo Outlook Voice Access para falar com eles e para responder. O sistema de caixa postal tenta encontrar e usar a melhor correspondência para o idioma quando o usuário se conecta ao MicrosoftOutlook Web App ou o idioma escolhido nas configurações regionais em Outlook Web App. Se o idioma escolhido não tiver suporte do Outlook Voice Access, o sistema de caixa postal usará o mesmo idioma que os chamadores ouvem quando são solicitados a deixar uma mensagem de voz.

Voltar ao início

## Controlando recursos do Outlook Voice Access

Por padrão, quando os usuários discam para o Outlook Voice Access, eles podem usem o telefone para acessar seu calendário, email e contatos pessoais e pesquisar o diretório. Você pode usar o Shell para impedir que usuários acessem um ou mais desses recursos quando utilizarem o Outlook Voice Access para acessar suas caixas de correio. Quando você modifica os recursos do Outlook Voice Access em uma diretiva de caixa de correio UM, suas alterações afetam todos os usuários que estão associados a diretiva de caixa de correio de Unificação de mensagens. Também é possível desabilitar alguns recursos na caixa de correio de um único usuário, embora outros recursos podem estar desabilitados somente em uma diretiva de caixa de correio UM e não estão disponíveis em uma caixa de correio individual.


> [!TIP]
> Apenas o Shell pode ser usado para modificar as configurações da TUI do Outlook Voice Access para caixas de correio habilitadas para UM ou políticas de caixa de correio de UM.



**Configurações de diretiva de caixa de correio de Unificação de mensagens**   Você pode desabilitar o acesso dos usuários para os seguintes recursos do Outlook Voice Access em uma diretiva de caixa de correio de UM:

  - Reconhecimento Automático de Fala

  - Acesso sem PIN à caixa postal

  - Respostas de voz para outras mensagens

  - Acesso TUI ao calendário

  - Acesso TUI ao diretório

  - Acesso TUI ao email

  - Acesso TUI aos contatos pessoais

**Configurações de caixa de correio habilitada para UM**   Você pode desabilitar o acesso de um usuário aos seguintes recursos do Outlook Voice Access na caixa de correio do usuário:

  - Acesso TUI ao calendário

  - Acesso TUI ao email

  - Reconhecimento Automático de Fala

Você pode evitar que usuários recebam mensagens na caixa postal, mas pode permitir que eles acessem suas caixas de correio usando o Outlook Voice Access. Você pode habilitar um usuário para UM e configurar a caixa de correio do usuário com um número de ramal que não esteja sendo usado por outro usuário na organização.

Voltar ao início

