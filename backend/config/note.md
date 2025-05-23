- configディレクトリ
    - environmentsディレクトリ
        - Rails特有の固有環境の設定を記載するファイル
            - コア部分の環境設定
        - developmentファイル　＝＞　開発環境においての設定
            - Rails.application.configure do
                - config.cache_classes = false
                    - 後方互換性のためのコード
                - config.eager_load = false
                    - メモリに事前にキャッシュする
                        - falseなのでキャッシュしない
                - config.consider_all_requests_local = true
                    - 全てのエラーを表示する
                - if文 => Rails.root.join('tmp', 'caching-dev.txt').exist?
                    - config.cache_store = :memory_store
                    - config.public_file_server.headers
                        - 'Cache-Control' => "public, max-age=#{2.days.to_i}"
                    - config.action_controller.perform_caching = false
                    - config.cache_store = :null_store
                - config.active_storage.service = :local
                    - ローカルのストアファイルを更新する
                - config.action_mailer.raise_delivery_errors = false
                - config.action_mailer.perform_caching = false
                    - mailerにおいてエラーが発生してもエラーの対応をしない
                        - ローカル開発なので対応する必要ない
                - config.active_support.deprecation = :log
                    - 非推奨のactive_supportがあった場合logに出力する
                - config.active_support.disallowed_deprecation = :raise
                - config.active_support.disallowed_deprecation_warnings = []
                    - warningsを配列で返すために[]Arrayリテラルを渡す
                - config.active_record.migration_error = :page_load
                    - migration_errorはpage_loadを指定してページに表示する
                - config.active_record.verbose_query_logs = true
                    - railsサーバーのログを追う事ができるようにする設定
                - config.file_watcher = ActiveSupport::EventedFileUpdateChecker
                    - ファイルシステム上のファイル更新検出に使われるクラス
                        - listenAPIに従う必要がある
                            - listenというGemが参照される
                - config.action_mailer.default_url_options = { host: 'localhost', port: 3001 }
                    - mailerを使う際のデフォルトURLを指定する
        - productionファイル　＝＞　プロダクト(本番環境)においての設定
            - Rails.application.configure do
                - config.cache_classes = true
                    - 後方互換性のためのコードを有効にする
                - config.eager_load = true
                    - メモリに事前にキャッシュする
                        - 開発環境なので有効にする
                -  config.consider_all_requests_local = true
                    - 全てのエラーを表示しない
                        - 本番環境においてはエラーハンドリングを行い必要なエラーのみを表示するようにする
                - config.public_file_server.enabled = ENV['RAILS_SERVE_STATIC_FILES'].present?
                    - 静的なファイルをpublicディレクトリから供給する
                - config.active_storage.service = :local
                    - ローカルのストアファイルを更新する
                - config.log_level = :info
                    - ログレベルを一般的な情報に指定する
                - config.log_tags = [ :request_id ]
                    - logのタグにはリクエストのidを指定する
                - config.action_mailer.perform_caching = false
                    - mailerにおいてエラーが発生してもエラーの対応をしない
                        - ローカル開発なので対応する必要ない
                            - 今回は本番環境だが、mailer機能を実装しないのでfalseを返す
                - config.i18n.fallbacks = true
                    - ロケールのフォールバック設定
                        - バージョンによってはフォールバックによってエラーが発生する可能性がある
                - config.active_support.deprecation = :notify
                    - 非推奨のactive_supportがあった場合notifyに出力する
                - config.active_support.disallowed_deprecation = :log
                - onfig.active_support.disallowed_deprecation_warnings = []
                - config.log_formatter = ::Logger::Formatter.new
                - if文
                    - logger
                    - logger.formatter
                    - config.logger
                        - これらを定義する
                - config.active_record.dump_schema_after_migration = false
                    - migration後のdunmを禁止する
                        - 現在のDBからDBスキーマを生成する
        - testファイル
            - Rails.application.configure do
                - config.cache_classes = false
                    - 後方互換性のためのコード
                        - ローカル開発のためfalseで無効化する
                - config.action_view.cache_template_loading = true
                    - リクエストのたびにビューテンプレートを再読み込みするかどうか
                - config.eager_load = false
                    - config.before_eager_loadフックを実行しeager_load!を呼び出す
                        - すべてのconfig.eager_load_namespacesが呼び出される
                - config.public_file_server.enabled = true
                    - rails側からの静的ファイルを配信するかどうかを設定する
                - config.public_file_server.headers = {
                    'Cache-Control' => "public, max-age=#{1.hour.to_i}"
                    }
                    - production環境のアセットがどれだけの期間保存されるのか？
                - config.consider_all_requests_local       = true
                    - 全てのエラーを表示する
                - config.action_controller.perform_caching = false
                - config.cache_store = :null_store
                - config.action_dispatch.show_exceptions = false
                    - 常に例外が表示される設定にする
                - config.action_controller.allow_forgery_protection = false
                    - CSRF保護を有効にするか？
                        - testではデフォルトでfalseが返される
                - config.active_storage.service = :test
                    - test領域を更新する
                - config.action_mailer.perform_caching = false
                    - mailerにおける例外対応をするかしないか？
                - config.action_mailer.delivery_method = :test
                    - メールの配信方法設定
                        - デフォルトでは:smtpとなっている
                - config.active_support.deprecation = :stderr
                    - 非推奨の警告
                        - オプション内容
                            - stderrに全ての警告内容を保存する
                            - raise
                            - log
                - config.active_support.disallowed_deprecation = :raise
                    - raiseする
                - config.active_support.disallowed_deprecation_warnings = []
                    - アプリケーションで利用を許可しない項目として扱う
                        - 非推奨警告メッセージを設定します
    - initializersディレクトリ
        - フレームワークやGemが読み込まれた後に実行するコードを格納するディレクトリ
            - 全てのファイルの先頭にはコメントアウトされている文章の記載がある
                -  Be sure to restart your server when you modify this file.が記述されている
                    - ファイルの記載内容を変更した場合にはサーバーの再起動が必須
            - Application　＝＞　記載なし
            - backtrace
                - オプションのBACKTRACEがバックトレースの削除をオフにできる
                    - デフォルトではバックトレースは削除されるようになっている
                    - backtrace_cleanerにもともとremove_silencersというものがあり、オプションを使う事でオンにする事ができる
            - carriewave
                - ライブラリであるcarriewaveを使う時のファイル形式や保存先ついて
            - cors
                - Rails APIモードなどでクライアント側とアプリケーション側でドメイン(サーバー)を分ける事がある
                    - 基本的に異なるドメイン間においてはアクセスなどに制限がかかってしまう
                        - resource "*"
                            - 全てのオリジンからのアクセスを許可
                        - headers: :any
                            - リクエストに対するヘッダー情報は自由にする
                        - expose: ["access-token", "expiry", "token-type", "uid", "client"]
                            - レスポンスのHTTPヘッダーとして公開を許可する
                        - methods: [:get, :post, :put, :patch, :delete, :options, :head]
                            - 指定したメソッドでのAPIリクエストを許可する
            - devise_token_auth
                - 認証情報に関する設定を記載する
                    - リクエスト毎にトークンを変える　＝＞　無効化
                    - トークンの有効期間　＝＞　2週間
                    - config.token_cost = Rails.env.test? ? 4 : 10
                        - トークンコストの設定
                            - Rails.env.testの場合
                                - トークンの設定を4にする
                            - Rails.env.testではない場合
                                - トークンの設定を10にする
                        - トークンとは？
                            - トークンとは、システムに情報を与える時にどのくらいの間隔で文章、文字列、データなどを分割して解析するのか？という事を定義する
                                - トークンの数が多い場合には精密になるが、使用コストが増えていく
                    - ヘッダー情報の定義
            - devise
                - Devise.setup do |config|
                    - config.password_length = 6..128
                        - パスワードの長さを最低6文字、128文字の長さに設定
                    - config.reset_password_within = 6.hours
                        - パスワードのリセットには6時間を空ける必要がある
            - filter_parameter
                - ログに出力する内容をフィルターする
                    - 機密情報などは出力しないように注意する
            - inflection　＝＞　記載なし
            - mime_types　＝＞　記載なし
            - wrap_parameters
                - 処理に記載した内容を指定した条件が実行されるまで延期するメカニズム
                    - action_controllerが実行され時にformat: [:json]でラップする
    - localesディレクトリ
        - 頻回に使用する言語などを定義するファイル
            - en => 英語
                - deviseとerrorsの内容が記載されている
    - applicationファイル
        - Railsコンポーネントを初期化するファイル
            - 各種フレームワークに必要なものをrequire
            - Bundlerもrequireする
            - アプリケーションのモジュールを定義する
                - class Application < Rails::Application
                    - Railsアプリケーションを継承する
                        - config.load_defaults 6.1
                            - 6.1までのバージョンを全て読み込む
                                - https://railsguides.jp/configuring.html
                                    - 初期設定が記載されている
                    - config.api_only = true
                        - APIモードである事を明示的に示す
                    - config.generators do |g|
                        - 各ファイルを生成するかどうかを定義する
    - bootファイル
        - ENV['BUNDLE_GEMFILE'] ||= File.expand_path('../Gemfile', __dir__)
            - 環境変数の定義　＝＞　BUNDLE_GEMFILE
                - パスはGemfileを指定して__dir__である事を定義して自己代入する
        - require "bundler/setup" # Set up gems listed in the Gemfile.
            - bundlerのセットアップ時にはGemfileをリストにする
        - require "bootsnap/setup" # Speed up boot time by caching expensive operations.
    - cableファイル
        - エンドユーザーに向けたアダプタの一種
            - asyncアダプタ
            - Radisアダプタ
                - 複数のアプリケーションを使う際に使用されるサーバー
                    - SSL/TLS接続もサポートされている
    - databaseファイル
        - RailsにおけるDBの設定ファイル
            - Railsアプリケーションを作成すると自動的に生成される
                - デフォルトではSQliteが使用される前提で作成される
    - environmentファイル
        - 環境変数を呼び出すファイル
    - pumaファイル
        - Webサーバーであるpumaファイルの設定を定義するファイル
            - max_threads_count,min_threads_count
                - max,mindどちらも最大のスレッド数を5に制限する
        - worker_timeout 3600 if ENV.fetch("RAILS_ENV", "development") == "development"
            - 後置ifでdevelopment環境の時にタイムアウトする時間を設定する
        - port ENV.fetch("PORT") { 3000 }
            - ポート番号を定義する
        - pidfile ENV.fetch("PIDFILE") { "tmp/pids/server.pid" }
            - PIDFILEを使ってpumactlコマンドが使えるようにする
                - pumaを起動する方法
                    - pumaコマンドを使う方法
                        - 起動時にポート番号やオプション、スレッド数などを定義する必要がある
                    - pumactlコマンドを使う方法
                        - pumactlコマンドを使用するとpuma.rbファイルに記載されている設定に応じてサーバーを起動してくれる設定になる
                            - pumaコマンドの場合には全て指定する必要があったためコードで管理できる利点がある
    - routesファイル
        - ルーティングを記載するファイル
            - Railsにおけるルーティングを記載する
    - springファイル
        - バックグラウンドでライブラリを読み込む事でRailsコマンド等を早く実行できるようにする機能
            - bin/コマンド名　としなければspringが実行されない場合があるためspringを使うと考えている場合にはコンマンドの叩き方を注意する事が必要