# hackathon

🚀 ハッカソン プロジェクト

このリポジトリは、Django (バックエンド) + React (フロントエンド) + PostgreSQL (データベース) を用いたハッカソン用の開発環境です。
Dockerを使用しているため、PCにPythonやNode.jsを直接インストールする必要はありません。

🛠 技術スタック

Frontend: React (Vite) / Node.js 20

Backend: Django / Python 3.12

Database: PostgreSQL 16

Infrastructure: Docker / Docker Compose

🏁 初回セットアップ（初めてcloneしたとき）

開発を始める前に、一度だけ以下の手順を実行してください。
※ 事前に Docker Desktop をインストールし、起動しておいてください。

1. リポジトリのクローンと移動

git clone <このリポジトリのURL>
cd hackathon-project



2. コンテナのビルドと起動

初回はパッケージのダウンロード等で数分かかります。

docker compose up -d --build



3. データベースの初期化（マイグレーション）

コンテナが起動したら、必ず以下のコマンドを実行してデータベースを作成してください。

docker compose exec backend python manage.py migrate



これで準備完了です！🎉

🌐 アプリへのアクセス先

コンテナ起動中、ブラウザから以下のURLでアクセスできます。

フロントエンド (React): http://localhost:5173

バックエンド (Django): http://localhost:8000

Django管理画面: http://localhost:8000/admin

💻 毎日の開発の流れ

開発を始めるとき

docker compose up -d



開発を終わるとき

docker compose down



ログを確認したいとき（エラーで画面が真っ白になった時など）

docker compose logs -f
# フロントエンドだけ見たい場合: docker compose logs -f frontend
# バックエンドだけ見たい場合: docker compose logs -f backend



⚠️ チーム開発の超重要ルール

1. 誰かが新しいパッケージを追加した場合

誰かが新しいライブラリ (pip install ~ や npm install ~) を追加してPushしたコードを git pull した後は、環境を作り直す必要があります。
いつもの up -d ではなく、以下を実行してください。

docker compose up -d --build



2. データベースの設計(models.py)が更新された場合

誰かがデータベースの設計を変更してPushしたコードを git pull した後は、自分のPCのデータベースも更新する必要があります。

docker compose exec backend python manage.py migrate



3. 自分でパッケージを追加したい場合

PCに直接インストールするのではなく、必ずコンテナの中でインストールしてください。

フロントエンド (React) の場合:

docker compose exec frontend npm install <パッケージ名>



バックエンド (Django) の場合:

docker compose exec backend pip install <パッケージ名>
docker compose exec backend pip freeze > requirements.txt



※ 追加後は忘れずに package.json や requirements.txt をGitでコミット＆プッシュしてください。

4. 新しいDjangoアプリ（機能）を追加したい場合

バックエンドで新しく機能を追加するために startapp を行いたい場合は、以下のコマンドを実行してください。

docker compose exec backend python manage.py startapp <アプリ名>


※ コマンド実行後、必ず backend/config/settings.py の INSTALLED_APPS に <アプリ名> を追加するのを忘れないでください！
