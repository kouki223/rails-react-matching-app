- backend
  - appディレクトリ
    - アプリケーション本体のディレクトリ
  - binディレクトリ
    - スクリプトファイルが格納されているディレクトリ
  - configディレクトリ
    - railsにおいて設定を記載するためのディレクトリ
  - dbディレクトリ
    - DBに関連するディレクトリ
  <!-- - libディレクトリ
  - logディレクトリ -->
  - publicディレクトリ
    - 画像ファイルなどの静的ファイルを保存するためのディレクトリ
  <!-- - storageディレクトリ -->
  - testディレクトリ
    - テスト関連のファイルを管理するディレクトリ
  <!-- - tmpディレクトリ
  - vendorディレクトリ -->
  - gitattributesファイル
    - LFSのシステムを使うための定義ファイル
  - gitignoreファイル
    - Gitのバージョン管理から除外したいものを指示するファイル
  - ruby-versionファイル
    - rubyのバージョンを指定するファイル
  - config.ruファイル
    - rails serverを立ち上げる際に初期化をするファイル
  - doker-composeファイル
    - 複数のコンテナからなるサービスを構築する
      - 独立したコンテナをどのように起動するか定義する
  - Dokerfileファイル
    - ruby3:0をベースにしてどのような仮想環境を立ち上げるのか定義するファイル
  - entrypointファイル
    - Dokerコンテナが実行された時に毎回実行されるスクリプト、コマンドを記載するファイル
  - Gemfileファイル
    - インストールするGemを記載するファイル
  - Rakeファイル
    - Rake環境を記載するファイル
    
