- binディレクトリ
    - bundleファイル
        - Gemファイルで使う事ができるGemfileに基づいてrailsコマンドなどを実行できるようにするコマンド
    - railsファイル
        - railsコマンドを実行できるようにcommandを呼び込んでいるファイル
    - rakeファイル
        - Rails5以降bin/railsに統合された
            - DB周りのコマンドを実行するスクリプトを記載するファイル
    - setupファイル
        - アプリケーションの初期設定時に設定を自動化するためのコードを格納するファイル
    - springファイル
        - develop環境での実行を高速化する仕組み
            - springサーバが起動される。
                - 設定を監視し、必要に応じて再ロードする
                    - rails console/runner/generate/destroy と rake タスクが対象
                        - 自動起動/終了されるので何も考えなくてもよい