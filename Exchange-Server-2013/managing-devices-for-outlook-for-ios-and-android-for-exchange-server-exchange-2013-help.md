---
title: 'Gerenciar dispositivos do Outlook para iOS e Android no Exchange Server'
TOCTitle: Gerenciando dispositivos para o Outlook para iOS e Android para o Exchange Server
ms:assetid: 16ce7d24-be74-4466-b126-828a67f69b6e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt465748(v=EXCHG.150)
ms:contentKeyID: 70076153
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciando dispositivos para o Outlook para iOS e Android para o Exchange Server

 

_**Aplica-se a:** Exchange Server 2010, Exchange Server 2013_

_**Tópico modificado em:** 2018-04-01_

**Resumo:**  Este artigo descreve como o Exchange Active Sync ajuda você a gerenciar dispositivos móveis com o Outlook para iOS e Android em troca de sua organização local.

A Microsoft recomenda Exchange ActiveSync para o gerenciamento de dispositivos móveis que são usados para acessar caixas de correio do Exchange em seu ambiente local. Exchange ActiveSync é um protocolo de sincronização do Microsoft Exchange que permite que os telefones celulares acessar informações de uma organização em um servidor que está executando o Microsoft Exchange.

Este artigo se concentra em recursos do Exchange ActiveSync e cenários para dispositivos móveis que executam o Outlook para Android e iOS específicos. Informações completas sobre o protocolo de sincronização do Microsoft Exchange estão disponíveis no [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md). Além disso, há informações sobre [O Blog do Office](https://go.microsoft.com/fwlink/p/?linkid=623922) detalhando imposição de senha e outros benefícios do uso do Exchange ActiveSync com dispositivos que executam o Outlook para iOS e Android.

## Criptografia de dispositivo e bloquear PIN

Se as diretivas da organização do Exchange ActiveSync exige uma senha em dispositivos móveis para que os usuários sincronizar o email, o Outlook imporá essa política a nível do dispositivo. Isso funciona de modo diferente entre dispositivos iOS e dispositivos com Android, com base em controles fornecidos pela Apple e Google disponíveis.

Em dispositivos iOS, Outlook faz uma verificação para garantir uma senha ou PIN está definida corretamente. No caso de uma senha não estiver definida, o Outlook solicita que os usuários criem uma senha nas configurações de iOS. Até que a senha está configurado, o usuário será capaz de acessar o Outlook para iOS.

Outlook para iOS só é executado em iOS 8.0 ou posterior. Esses dispositivos são fornecidos com criptografia interna, o que o Outlook usa depois que a senha está habilitada para criptografar todos os dados que Outlook armazena localmente no dispositivo iOS. Portanto, dispositivos iOS com um PIN serão criptografados ou não isso é necessário por uma política de ActiveSync.

Em dispositivos Android, o Outlook irá impor regras de bloqueio de tela. Além disso, Google fornece controles que permitem que o Outlook para Android cumprir as políticas relacionadas a complexidade e comprimento da senha do Exchange e o número de permitido tela desbloqueio tentativas antes de apagar dispositivos o telefone. Outlook para Android também será Incentive a criptografia de armazenamento se ele não estiver habilitado, a orientação dos usuários por meio desse processo com um passo a passo.

iOS e Android dispositivos que não têm suporte para essas configurações de segurança de senha não poderão se conectar a uma caixa de correio do Exchange.

## Limpeza remota com o Exchange ActiveSync

Exchange ActiveSync permite que os administradores para apagar remotamente dispositivos, por exemplo, se eles forem comprometidos. Com o Outlook para iOS e Android, um apagamento remoto é feito no aplicativo Outlook propriamente dito e não um apagamento do dispositivo completo.

Depois que o comando de apagamento remoto é solicitado pelo administrador, o apagamento acontece dentro de segundos de conexão próximo do Outlook do aplicativo para o Exchange. O aplicativo Outlook redefinirá e todos os produtos de email, calendário, contatos e dados de arquivos Outlook serão removidos do dispositivo, bem como o serviço do Outlook. O apagamento não irão afetar qualquer um dos aplicativos pessoais do usuário e as informações fora do Outlook.

Desde que o Outlook para iOS e Android é exibido como uma associação de dispositivo móvel único em dispositivos móveis de um usuário no Exchange, um comando de apagamento remoto removerá os dados e excluir relacionamentos de sincronização de todos os dispositivos que executam o Outlook (iPhone, iPad, Android) associado Esse usuário.


> [!TIP]
> Devido à arquitetura de nuvem por trás do Outlook para iOS e Android, o resultado de apagamento remoto de dispositivo não é relatado volta para o Exchange. Mesmo quando o apagamento for bem-sucedido, o status será exibido como <STRONG>pendente</STRONG>. Esse é um problema conhecido e uma solução está sendo desenvolvida.



## Identificadores de dispositivos e controle de acesso

Devido a arquitetura baseada em nuvem do Outlook para iOS e Android, conexões do Outlook aparecem como um identificador único dispositivo móvel (ID) para cada usuário no Exchange. Isso significa que os controles de acesso de dispositivo móvel para cada usuário são aplicados a todos os dispositivos associados com essa ID do dispositivo. Essa implementação cria duas condições que são diferentes do acesso de dispositivo do Exchange ActiveSync tradicional como controles funcionam.

  - **Bloquear:**  bloqueia o Outlook em todos os dispositivos de uma regra de bloqueio e sistemas operacionais suportados. Você não pode bloquear dispositivos individuais ou sistemas operacionais.

  - **Quarentena:**  o processo de quarentena funciona em uma base por usuário, em vez de uma base por dispositivo. Depois que um usuário tiver um dispositivo liberado da quarentena, eles podem instalar e configurar o Outlook em quantos dispositivos adicionais, como gostarem. Porque o usuário foi liberado da quarentena, novos dispositivos associados a esse usuário serão não ser colocada em quarentena.

Quando a políticas de caixa de correio de dispositivo móvel estão funcionando, elas são aplicadas a todos os respectivos dispositivos. Portanto, se você aplicar um bloqueio do PIN para uma caixa de correio específica, todos os dispositivos que se conectam a essa caixa de correio exigirá um PIN.


> [!TIP]
> Porque as IDs de dispositivo não serão regidas pela ID de qualquer <EM>dispositivo físico</EM> , eles poderão alterar sem aviso prévio. Quando isso acontece, ela pode causar consequências indesejadas quando identificações de dispositivo são usadas para gerenciar os dispositivos do usuário, como os dispositivos 'permitidos' existentes podem ser bloqueados ou colocados em quarentena pelo Exchange inesperadamente. Portanto, recomendamos que os administradores apenas definir políticas de dispositivo móvel que permitem/bloquear dispositivos com base no tipo de dispositivo ou modelo de dispositivo.



## Gerenciamento de dispositivos com perguntas Frequentes do Exchange ActiveSync

A seguir é perguntas frequentes sobre senhas, PINs e políticas de criptografia para dispositivos que executam o Outlook para iOS e Android.

## O aplicativo de email nativo em iOS impõe políticas do Exchange ActiveSync para requisitos de tamanho e complexidade de senha. Por que não o Outlook?

Outlook tira vantagem dos controles de desenvolvedor do aplicativo de terceiros que estão disponíveis para a Microsoft. Podemos continuarão a melhorar esse recurso, como o Apple disponibiliza mais controles para desenvolvedores.

## Por que o Outlook para iOS e Android impõem PINs no nível do dispositivo, ao invés do nível de aplicativo?

Depois de avaliar os recursos disponíveis no iOS e Android, a Microsoft acredita que um PIN de nível de dispositivo oferece a melhor experiência para os clientes, em termos de conveniência e segurança. Um PIN de nível de aplicativo significa que os usuários precisam inserir dois pinos diferentes para acessar email, o que não pode ser desejável. Além disso, um PIN de nível de dispositivo significa que podemos podem se beneficiar dos recursos como criptografia de dispositivo nativo, TouchID em iOS e bloqueio inteligente no Android. Apagamento remoto ainda é implementado no nível de aplicativo, o que significa que os aplicativos de pessoal de usuários e os dados não serão afetados quando o Outlook é apagado.

## Significa o Outlook para criptografia de dispositivo Android suporte?

Sim, o Outlook para Android oferece suporte a criptografia de dispositivo por meio de diretivas de caixa de correio de dispositivo móvel do Exchange. No entanto, antes da Android 7.0, a disponibilidade e a implementação desse processo varia por fabricante de dispositivo e a versão do sistema operacional Android, que permitem que o usuário cancele o check-out durante o processo de criptografia. Com as alterações que introduziu a Google Android 7.0, o Outlook para Android agora é capaz de aplicar a criptografia em dispositivos executando o Android 7.0 ou posterior. Usuários com dispositivos que executam os sistemas operacionais não será capazes de cancelar o processo de criptografia.

Mesmo que o dispositivo Android é criptografado e um invasor está em posse do dispositivo, desde que um PIN de dispositivo está habilitado, o banco de dados do Outlook permanecerá inacessível. Isso é verdadeiro mesmo com USB depuração habilitada e o SDK Android instalado. Se um invasor tenta raiz o dispositivo para ignorar o PIN para obter acesso a essas informações, o processo de criar as raízes das apaga todo o armazenamento de dispositivo e remove todos os dados do Outlook. Se o dispositivo é criptografado e como raiz pelo usuário antes que está sendo roubado, é possível que um invasor obtenha acesso o banco de dados do Outlook habilitando USB depuração no dispositivo e conectando o dispositivo em um computador com o Android SDK instalado.

