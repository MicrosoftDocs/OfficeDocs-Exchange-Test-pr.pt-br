---
title: 'Definir segurança de PIN do Outlook Voice Access: Exchange Online Help'
TOCTitle: Definir segurança de PIN do Outlook Voice Access
ms:assetid: ef6d9151-d333-4f52-9338-273f7a291e54
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125162(v=EXCHG.150)
ms:contentKeyID: 50556308
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Definir segurança de PIN do Outlook Voice Access

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-16_

Quando os usuários de Unificação de Mensagens (UM) se conectam ao sistema de correio de voz por telefone, usam o Outlook Voice Access para navegar no sistema de menus. Para que os usuários possam acessar o sistema de correio de voz, o sistema lhes solicita inserir o seu PIN. Como o administrador, você pode configurar definições e requisitos de PIN e executar tarefas de gerenciamento de PIN. Após um usuário ter a caixa posta ativada e um PIN ter sido gerado, o PIN do usuário é criptografado e armazenado na caixa de correio do usuário.


> [!TIP]
> Os usuários do Outlook Voice Access devem usar entradas de discagem por tom ou DTMF (Dual Tone Multi-Frequency) para inserir seu PIN para acessar a caixa de correio habilitada para UM. Reconhecimento de fala não está disponível para entrada PIN.



**Sumário**

Visão geral do PIN

Requisitos de PIN

Gerenciamento de PINs do Outlook Voice Access

## Visão geral do PIN

PIN é uma sequência numérica usada em determinados sistemas para que um usuário possa ser autenticado e obter acesso. Os PINs são usados com mais frequência em ATMs (caixas eletrônicos). Eles também são usados em vez de senhas alfanuméricas para sistemas de correio de voz. O poder de um PIN depende de seu tamanho, do grau de proteção e do grau de dificuldade para adivinhá-lo.

Na Unificação de Mensagens, os usuários do Outlook Voice Access inserem seu PIN em um telefone analógico, digital ou celular para poderem acessar email, correio de voz, contatos e informações de calendário em suas caixas de correio do Exchange Server

Na Unificação de Mensagens, as políticas de PIN são definidas e configuradas em uma política de caixa de correio da UM. Várias políticas de caixa de correio de UM podem ser criadas, dependendo de seus requisitos. Ao permitir que um usuário use a Unificação de Mensagens, você vincula o usuário a uma política existente de caixa de correio de UM. As políticas de PIN de UM configuradas na política de caixa de correio de UM devem ser baseadas nos requisitos de segurança de sua organização.

## Requisitos de PIN

Abaixo são descritas várias definições de configuração de PIN que você pode definir em uma política de caixa de correio da UM no .

## Tamanho mínimo do PIN

A configuração do **tamanho mínimo do PIN** especifica o número mínimo de dígitos que um PIN de caixa de correio deve ter. O intervalo é de 4 a 24 e o padrão é 6. Se você inserir 0, os usuários não são obrigados a digitar um PIN.


> [!IMPORTANT]
> Não é recomendável configurar essa definição com zero. Ao configurar essa definição com 0, você diminui muito o nível de segurança da rede.



Se você alterar para o valor de comprimento mínimo do PIN para outro maior, será solicitado que os usuários atuais criem um novo PIN que contenha o novo número mínimo de dígitos para poderem continuar.


> [!TIP]
> O aumento desse número cria um ambiente de UM mais seguro. No entanto, se ele for definido muito alto, os usuários poderão esquecer seus PINs.



## Impor tempo de vida do PIN

A configuração **Impor tempo de vida do PIN** controla o intervalo de tempo, em dias, da data em que os usuários do Outlook Voice Access alteraram seu PIN pela última vez até a data em que deverão alterá-lo novamente. O intervalo é de 0 a 999 e o padrão é 60 dias. Se for digitado 0, o PIN não expirará.


> [!TIP]
> A Unificação de Mensagens não notificará os usuários quando o PIN estiver prestes a expirar.



## Número de falhas de logon antes da redefinição do PIN

A configuração **Número de falhas de logon antes da redefinição do PIN** especifica o número de tentativas de logon malsucedidas sucessivas antes de o PIN de caixa de correio ser redefinido automaticamente. Para desabilitar esse recurso, defina essa configuração como ilimitado. Caso contrário, ele deve ser definido como um número menor que a configuração **Número de falhas de logon antes de bloqueio**. O intervalo é de 1 a 998 e o padrão é 5.


> [!TIP]
> Para aumentar a segurança de usuários habilitados para UM, digite um número menor que 5.



## Número de falhas de logon antes de bloqueio

A configuração **Número de falhas de logon antes de bloqueio** especifica quantos erros de entrada de PIN em chamadas sucessivas os usuários do Outlook Voice Access podem cometer antes de terem suas caixas de correio bloqueadas. Por padrão, após cinco tentativas, o PIN é redefinido automaticamente. O intervalo é de 1 a 999 e o padrão é 15.


> [!TIP]
> Para aumentar a segurança, diminua o número de tentativas com falha permitidas. Porém, lembre-se que especificar um número muito mais baixo que o padrão poderá resultar no bloqueio desnecessário de usuários. A Unificação de Mensagens gerará eventos de aviso que podem ser visualizados com o uso de Visualizar Eventos se houver falha na autenticação do PIN de um usuário habilitado para UM ou se o usuário não tiver êxito ao tentar fazer logon no sistema.



## Permitir padrões comuns de PIN

A configuração **Permitir padrões comuns de PIN** é usada para habilitar ou desabilitar o uso de padrões de números comuns usados na criação de um PIN. Por padrão, essa configuração é desabilitada e não permite que os usuários do Outlook Voice Access insiram estes padrões de números:

  - **Números sequenciais**   Valores de PIN que consistem inteiramente em números consecutivos. Exemplos de números sequenciais para um PIN são 1234 e 65432.

  - **Números repetidos** Valores de PIN que consistem em números repetidos. Exemplos de números repetidos são 11111 e 22222.

  - **Sufixo de ramal de caixa de correio**   Valores de PIN que consistem em sufixo do ramal da caixa de correio do usuário. Se o ramal de sua caixa de correio for 36697, o PIN não poderá ser 6697.

## Contagem de reciclagem de PIN

A configuração **Contagem de reciclagem de PIN** configura o número de PINs diferentes que um usuário deve usar antes que quaisquer PINs usados anteriormente possam ser reutilizados. O intervalo é de 1 a 20 e o padrão é 5.

## Gerenciamento de PINs do Outlook Voice Access

Ao planejar os PINs do Outlook Voice Access, você deve escolher os níveis de segurança apropriados para sua organização. Você deve considerar cuidadosamente os requisitos de PIN do Outlook Voice Access e como as configurações de segurança de PIN atenderão ou excederão a política de segurança da organização.


> [!IMPORTANT]
> É uma prática recomendada de segurança implementar requisitos de PIN fortes para usuários do Outlook Voice Access. Isso pode ser reforçado pela criação de políticas de PIN de UM que exigem seis ou mais dígitos para PINs e aumentam o nível de segurança da rede.



Após definir os requisitos de PIN do Outlook Voice Access, você deve criar e configurar uma política de caixa de correio da UM para impor os seus requisitos de PIN organizacionais. Para saber mais sobre como criar uma política de caixa de correio de UM, confira [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md) Para saber mais sobre como gerenciar políticas de caixa de correio de UM, confira [Gerenciar uma política de caixa de correio de Unificação de mensagens](manage-a-um-mailbox-policy-exchange-2013-help.md)


> [!TIP]
> Depois de criar a política de caixa de correio de UM, você deve associar o usuário ou os usuários habilitados para UM com a política apropriada de caixa de correio de UM. Você pode fazer isso usando o cmdlet <STRONG>Enable-UMMailbox</STRONG> no Shell de Gerenciamento do Exchange ou usando o Centro de administração do Exchange (EAC). Para saber mais sobre o cmdlet do Shell de Gerenciamento do&nbsp;Exchange, confira <A href="https://technet.microsoft.com/pt-br/library/aa998033(v=exchg.150)">Enable-UMMailbox</A>.



Há situações em que os usuários do Outlook Voice Access esquecem seus PINs ou têm o acesso às mensagens de voz bloqueado em suas caixas de correio. Em qualquer caso, pode ser necessário que você redefina um PIN do usuário habilitado para UM. Para saber mais, confira [Redefinir um PIN da caixa postal](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-outlook-voice-access-pin-security/reset-a-voice-mail-pin).

Você pode recuperar as informações do PIN de um usuário que estiver habilitado para a Unificação de Mensagens. As informações retornadas são calculadas usando os dados do PIN criptografados na caixa de correio do usuário. Isso lhe permite visualizar as informações do PIN do usuário e também indica se este teve sua caixa de correio bloqueada. Para saber mais, confira [Recuperar informações de PIN de caixa postal](retrieve-voice-mail-pin-information-exchange-2013-help.md).

