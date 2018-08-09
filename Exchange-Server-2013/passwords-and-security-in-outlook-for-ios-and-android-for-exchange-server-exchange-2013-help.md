---
title: 'Senhas e segurança no Outlook para iOS e Android no Exchange Server'
TOCTitle: Passwords and Security in Outlook for iOS and Android for Exchange Server
ms:assetid: e5565beb-7ef3-47c4-8daf-6d8f1d22dceb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt465750(v=EXCHG.150)
ms:contentKeyID: 70076157
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passwords and Security in Outlook for iOS and Android for Exchange Server

 

_**Aplica-se a:** Exchange Server 2010, Exchange Server 2013_

_**Tópico modificado em:** 2018-04-01_

**Resumo:**  Este artigo descreve como a segurança e senhas funcionam no Outlook para iOS e Android com o Exchange Server.

Na primeira vez em que o aplicativo do Outlook para o iOS e Android é executado em um ambiente do Exchange local, o Outlook gera uma chave AES-128 aleatória. Essa chave é conhecido como a *chave do dispositivo* e é armazenado apenas no dispositivo do usuário.

## Criando uma conta e a proteção de senhas

Quando um usuário faz logon em Exchange, o nome de usuário, senha e uma chave exclusiva do dispositivo AES-128 são enviados do dispositivo do usuário para o serviço do Outlook por uma conexão TLS, onde a chave do dispositivo é mantida na memória de compute de tempo de execução. Depois de verificar a senha com o Exchange server, o serviço de Outlook usa a chave do dispositivo para criptografar a senha e a senha criptografada, em seguida, é armazenada no serviço. A chave do dispositivo, entretanto, é apagada da memória e nunca armazenada no serviço do Outlook (apenas a chave é armazenada no dispositivo do usuário).

Em seguida, quando um usuário tenta se conectar ao Exchange para recuperar dados de caixa de correio, a chave do dispositivo é novamente passada do dispositivo para o serviço do Outlook sobre uma conexão protegida por TLS, onde ela é usada para descriptografar a senha na memória de compute de tempo de execução. Uma vez descriptografados, a senha é armazenada no serviço ou gravada em um disco de armazenamento local nunca, e a chave do dispositivo é apagada mais uma vez da memória.

Depois que o serviço do Outlook descriptografar a senha em tempo de execução, o serviço, em seguida, pode se conectar ao servidor do Exchange para sincronizar email, calendário e outros dados de caixa de correio. Desde que o usuário continua abrir e usar o Outlook periodicamente, cservice o Outlook irá manter uma cópia da senha do usuário descriptografada na memória para manter a conexão ao servidor do Exchange ativa.

## Conta de inatividade e liberação senhas da memória

Depois de três dias de inatividade, o serviço do Outlook irá liberar uma senha descriptografada da memória. Com a senha descriptografada liberada, o serviço do Outlook é capaz de acessar a caixa de correio do usuário. A senha criptografada permanece armazenada no serviço do Outlook, mas não é possível sem a chave de dispositivo, que está disponível apenas no dispositivo do usuário descriptografar-la novamente.

Há três maneiras de que uma conta de usuário pode se tornar inativa:

  - Outlook para iOS e Android é desinstalado pelo usuário.

  - Atualização do aplicativo em segundo plano está desabilitada nas opções de configurações e então force-quit será aplicado ao Outlook.

  - Nenhuma conexão de internet está disponível no dispositivo, impedindo a sincronização com o Exchange do Outlook.


> [!TIP]
> Outlook não se tornará inativo simplesmente porque o usuário não é aberto no aplicativo por um período de tempo, como durante um final de semana ou enquanto estiver em férias. Desde que a atualização do aplicativo em segundo plano estiver ativada (que é a configuração padrão para o Outlook para iOS e Android), funções, como notificações por push e a sincronização de plano de fundo de email contará como atividade.



**Liberar criptografados cache de mensagem e a senha do disco rígido**

Os Outlook liberações de serviço ou exclusões, contas inativas semanalmente. Depois que uma conta de usuário fica inativa, o serviço do Outlook irá liberar a senha criptografada e todo o conteúdo do cache de caixa de correio do usuário sem o serviço.

**Combinação de segurança de dispositivo e serviço**

Chave de dispositivo exclusiva de cada usuário nunca é armazenada no serviço do Outlook e Exchange senha de um usuário nunca é armazenada no dispositivo. Essa arquitetura significa que, em ordem para uma parte confiável mal-intencionado acessar uma senha de usuário, eles seriam necessário acesso não autorizado ao serviço do Outlook e o acesso físico ao dispositivo desse usuário.

Impondo diretivas de PIN e criptografia em dispositivos em sua organização, o terceiro mal-intencionado também teria que vencer a criptografia de um dispositivo apenas para ter acesso à chave de dispositivo. Isso tudo precisa ocorrer antes do usuário ter percebido que o dispositivo foi comprometido e pôde solicitar uma limpeza remota para o dispositivo.

## Perguntas frequentes sobre a segurança de senha

A seguir é perguntas frequentes sobre o design de segurança e configurações do Outlook para iOS e Android.

## Credenciais de usuário são armazenadas no serviço do Outlook se bloquear o Outlook de acessar meu servidor Exchange?

Se você tiver escolhido bloquear o Outlook para iOS e Android acessem seus servidores do Exchange local, a conexão inicial será rejeitada pelo Exchange. As credenciais do usuário não serão armazenadas pelo serviço do Outlook e as credenciais apresentadas na tentativa de conexão com falha são liberadas imediatamente da memória.

## Como a senha de usuário e a chave do dispositivo exclusivo é criptografada em trânsito para o serviço do Outlook?

Toda a comunicação entre o aplicativo do Outlook e o serviço de Outlook é por meio de uma conexão criptografada de TLS. O Outlook para iOS e Android são capaz de se conectar com o serviço do Outlook e nada mais.

## Como remover credenciais e informações de caixa de correio de um usuário do serviço do Outlook?

Há três maneiras de remover informações do serviço do Outlook:

  - Opção 1: Inicie um apagamento remoto para cada usuário que usou o aplicativo para se conectar ao Exchange.

  - Opção 2: Têm todos os usuários excluir Outlook para iOS e Android. Todos os dados serão removidos do serviço do Outlook em aproximadamente de 3 a 7 dias.

  - Opção 3: Ter usuários remover suas contas do aplicativo Outlook e, em seguida, excluir o aplicativo de seus dispositivos. No aplicativo, ter usuários acesse **configurações**, e em seguida, toque em **Configurações de conta**, **Selecione uma conta**e, em seguida, toque em **Excluir conta**.

## O aplicativo seja fechado ou desinstalado, mas ainda vejo conectar-se ao servidor do Exchange. Como é isso ocorra?

O serviço do Outlook descriptografa as senhas de usuário na memória de compute de tempo de execução e, em seguida, usa as senhas descriptografadas para se conectar ao Exchange. Desde que o serviço do Outlook está se conectando ao Exchange em nome do dispositivo para buscar e cache de dados de caixa de correio, ele poderá continuar por um curto período de tempo até que o serviço detecta que o Outlook não está mais solicitando dados.

Se um usuário desinstala o aplicativo de seus dispositivos sem primeiro usar a opção **Excluir conta**, o serviço do Outlook permanecerá conectado ao servidor do Exchange até que a conta fique inativa, conforme descrito acima em "inatividade de conta e liberação senhas da memória". Para evitar que esta atividade, simplesmente seguir 1 de opção ou a opção 3 do FAQ acima ou bloquear o aplicativo, conforme descrito em [Bloquear o Outlook para iOS e Android](https://technet.microsoft.com/pt-br/library/mt759239\(v=exchg.150\)).

## Uma senha de usuário é menos seguro no Outlook para iOS e Android do que quando usando outros clientes do Exchange ActiveSync?

Não. Clientes EAS geralmente salvar credenciais de usuário localmente no dispositivo do usuário. Isso significa que um dispositivo comprometido ou roubado pode resultar em um terceiro mal-intencionado que tenha acesso à senha do usuário. Com a segurança de design do Outlook para iOS e Android, um terceiro mal-intencionado precisa de acesso não autorizado para o Outlook nuvem serviço **e** teria acesso físico para um dispositivo do usuário.

## O que acontece se um usuário tentar usar o Outlook para iOS e Android após a exclusão de seus dados do serviço do Outlook?

Se uma conta de usuário fica inativa (como desabilitando a atualização do aplicativo em segundo plano no dispositivo ou ter seu dispositivo desconectado da Internet por um período de tempo), o aplicativo do Outlook serão reconectados ao serviço do Outlook na próxima vez em que o aplicativo é iniciado, e o criptografia de senha e o armazenamento em cache o processo de email serão reiniciado. Isso é tudo transparente ao usuário.

## Como os dados de caixa de correio armazenado em cache temporariamente são protegidos enquanto armazenadas no serviço do Outlook?

Você pode ler sobre como os nossos dados são protegidos no momento na [Central de confiabilidade do Azure](https://azure.microsoft.com/support/trust-center/). Conforme observado anteriormente, estamos passando do Windows Azure para o Office 365. A segurança desses serviços é abordada no [Centro de confiança do Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).

