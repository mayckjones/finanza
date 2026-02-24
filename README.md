# 💰 Controle Financeiro Pessoal

App de controle de despesas mensais com autenticação Firebase e sincronização em tempo real.

## 🚀 Funcionalidades

- **Autenticação** — Login com e-mail/senha ou Google
- **Dados na nuvem** — Sincronização em tempo real via Firestore
- **Receita mensal** — Informe sua receita e acompanhe o saldo disponível
- **Despesas variáveis** — Registre gastos por categoria (Transporte, Gasolina, Supermercado, etc.)
- **Despesas fixas** — Cadastre contas mensais com dia de vencimento e alertas automáticos
- **Filtros** — Filtre por dia, semana, período ou categoria
- **Gráficos** — Visualize pizza, barras e linha por seção; gráfico consolidado do mês
- **Multi-mês** — Navegue entre meses com seletor
- **Alertas** — Notificações de vencimento (hoje, amanhã, 2 dias)

## 📁 Estrutura

```
controle-financeiro/
├── index.html        # App completo (single file)
├── README.md
└── .gitignore
```

## 🔥 Firebase Setup

O app já está configurado com o projeto `controle-financeiro-9d5b4`.

### Regras do Firestore

Acesse **Firebase Console → Firestore → Rules** e configure:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

### Habilitar métodos de autenticação

Acesse **Firebase Console → Authentication → Sign-in method** e ative:
- ✅ E-mail/senha
- ✅ Google

## 🌐 Deploy no GitHub Pages

1. Crie um repositório no GitHub (ex: `controle-financeiro`)
2. Faça upload do `index.html`
3. Vá em **Settings → Pages → Source → main branch → / (root)**
4. Acesse: `https://SEU_USUARIO.github.io/controle-financeiro`

> ⚠️ Adicione o domínio do GitHub Pages nos **Authorized domains** do Firebase Authentication.

## 💻 Rodando localmente

Basta abrir o `index.html` no navegador — não precisa de servidor.

> Para login com Google funcionar localmente, adicione `localhost` nos Authorized domains do Firebase.

## 🗂️ Estrutura dos dados no Firestore

```
users/
  {uid}/
    data/
      income → { "2025-01": 5000, "2025-02": 5000, ... }
    expenses/
      {docId} → { cat, desc, date, monthKey, val, createdAt }
    fixed/
      {docId} → { name, val, due, createdAt }
```
