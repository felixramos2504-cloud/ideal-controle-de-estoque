IDEAL CONTROLE DE ESTOQUE — MASTER 1.0 (BASE INICIAL)

Arquivos:
- index.html.txt: interface do aplicativo.
- firebase-config.js.txt: configuração Firebase a preencher.
- manifest.json.txt: metadados PWA.
- service-worker.js.txt: cache básico PWA.
- firestore.rules.txt: regras iniciais de segurança.
- README.txt: este guia.

IMPORTANTE:
1. Renomeie index.html.txt para index.html, firebase-config.js.txt para firebase-config.js,
   manifest.json.txt para manifest.json e service-worker.js.txt para service-worker.js.
2. Abra firebase-config.js e substitua os valores COLOQUE_AQUI... pelos valores reais exibidos em
   Firebase Console > Configurações do projeto > Geral > Seu app Web > Config.
3. Não publique o site antes de configurar e testar as regras de segurança.
4. Publique em HTTPS (por exemplo, GitHub Pages ou Firebase Hosting) para a câmera funcionar.
5. O app usa Firebase compat SDK via CDN e html5-qrcode via CDN; requer internet.
6. Login por e-mail/senha deve estar ativado em Authentication.
7. O primeiro administrador precisa ser criado com Authentication > Usuários > Adicionar usuário.
   Depois copie o UID dessa conta e, no Firestore, crie manualmente:
   coleção: users
   ID do documento: exatamente o UID do administrador
   campos:
     role (string): administrador
     email (string): o e-mail da conta
     active (boolean): true
   Não permita que a pessoa escolha o próprio perfil pela interface.
8. Depois de provisionar o administrador, publique firestore.rules na aba Firestore > Regras.
9. Para outros usuários, crie a conta em Authentication e depois um documento users/{UID} com:
   role: colaborador OU gerente OU administrador
   email: e-mail da conta
   active: true
10. Antes de uso real, revise/teste as regras. Esta é uma base inicial, não uma certificação de segurança.

O QUE ESTÁ INCLUÍDO:
- Login por e-mail/senha.
- Cadastro de seções e produtos.
- Validação básica de EAN-8 e EAN-13 (dígito verificador).
- Leitura de EAN pela câmera em cadastro, contagem rápida e inventário.
- Contagem rápida que não altera o estoque oficial.
- Inventário em sessão local e finalização em lote com atualização de estoque e histórico.
- Movimentações de entrada, saída e ajuste.
- Dashboard com contadores e listeners em tempo real.

LIMITAÇÕES CONHECIDAS DA BASE:
- A sessão de inventário ainda é mantida na memória do navegador; se recarregar a página antes de finalizar, a sessão local pode se perder.
- A lista de inventário não é sincronizada entre dispositivos enquanto aberta.
- O código de frontend precisa ser testado no ambiente Firebase real antes de produção.
- A regra de segurança impede colaborador de escrever movimentos oficiais; inventário finalizado requer gerente.
- O EAN identifica o código, mas não preenche automaticamente nome e descrição sem cadastro prévio ou fonte de dados adicional.
- Configure ícones próprios e revise o manifesto antes de publicar a PWA.
