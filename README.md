# Next.js App DevContainer with Nginx and MySQL

このリポジトリは、Next.js アプリケーションを Dev Container 上で手軽に開発できるよう構成されたテンプレートです。  
Nginx、MySQL、Prisma を含んだフルスタック環境が Docker Compose により構築されており、VS Code の Dev Containers 機能を使って即座に開発を開始できます。

---

## 📦 サービス構成

| サービス名 | 内容                  | ポート            |
|------------|-----------------------|-------------------|
| app        | Next.js アプリ         | 3000（内部）      |
| nginx      | リバースプロキシ       | 8080（ホスト）     |
| db         | MySQL データベース     | 3306（内部）      |

---

## 🚀 セットアップ手順

### ✅ 前提条件

- [Docker](https://www.docker.com/) のインストール
- [Visual Studio Code](https://code.visualstudio.com/)
- [Dev Containers 拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

---

### 🛠 Dev Container の起動

1. リポジトリをクローンします：

    ```bash
    git clone https://github.com/fcf-koga/nextjs-app-devcontainer.git
    cd nextjs-app-devcontainer
    ```

2. VS Code でプロジェクトを開き、  
   コマンドパレットで「**Reopen in Container**」を選択

    > 初回起動時に `npm install` が自動実行されます  
    > 起動のたびに `npx prisma migrate dev` が自動実行されます

---

## ⚙️ アプリケーションの起動

Dev Container のターミナルで以下を実行します：

```bash
npm run dev
```

アプリは次のURLで確認できます：
http://localhost:8080

- nginx がリバースプロキシとして app（Next.js）に転送します
- localhost:3000 へ直接アクセスも可能（Next.js 単体）

## 🧬 Prisma 操作

### マイグレーション（初回）
Dev Container の postStartCommand により起動時に自動実行されますが、手動で実行したい場合：

```bash
npx prisma migrate dev --name init
```

### Prisma Studio（GUI）

```bash
npx prisma studio
```
→ ブラウザで http://localhost:5555 にアクセスし、データベースの内容を GUI で閲覧・編集できます。

## 🗃️ データベース接続情報
.env ファイルに以下の内容が含まれています：

```env
DATABASE_URL="mysql://root:password@db:3306/sampledb"
```
| 項目      | 値                 |
| ------- | ----------------- |
| ユーザー名   | `root`            |
| パスワード   | `password`        |
| ホスト     | `db`（dockerサービス名） |
| ポート     | `3306`            |
| データベース名 | `sampledb`        |

