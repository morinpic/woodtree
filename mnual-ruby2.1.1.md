#Ruby 2.1.1インストール手順

##Mac Portsが入ってる場合はアンインストール

コマンド:

    sudo port -fp uninstall --follow-dependents installed
    sudo rm -rf /opt/local
    sudo rm -rf /Applications/DarwinPorts
    sudo rm -rf /Applications/MacPorts
    sudo rm -rf /Library/LaunchDaemons/org.macports.*
    sudo rm -rf /Library/Receipts/DarwinPorts*.pkg
    sudo rm -rf /Library/Receipts/MacPorts*.pkg
    sudo rm -rf /Library/StartupItems/DarwinPortsStartup
    sudo rm -rf /Library/Tcl/darwinports1.0
    sudo rm -rf /Library/Tcl/macports1.0
    sudo rm -rf ~/.macports

##Homebrewのインストール

コマンド:

    ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go/install)”

※途中でXcodeのなんとかツールのインストール求められるかも

##brewアップデート

コマンド:
    
    brew update

##ruby-buildインストール

コマンド:

    brew install ruby-build

##rbenvインストール

コマンド:
    
    brew install rbenv

※rbenvを使うと複数のRubyのバージョンを管理出来る
37signalsが作ったツールらしいよ

##Ruby2.1.1インストール

コマンド:

    
    RUBY_CONFIGURE_OPTS="--with-readline-dir=$(brew --prefix readline) --with-openssl-dir=$(brew --prefix openssl)" rbenv install 2.1.1

※結構時間かかる

##rbenv管理のRubyをデフォルトで使うようにパスを通す

コマンド:

    echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
    echo 'export PATH="$HOME/.rbenv/shims:$PATH"' >> ~/.bash_profile
    source ~/.bash_profile

##何か分からないけど魔法の呪文

コマンド:

    rbenv rehash

##デフォルトを2.1.1に設定

コマンド:

    rbenv global 2.1.1
    
※これで`ruby -v`と打ってバージョンが2.1.1になってればOK

-----------------

#そしてRailsへ

##Bundlerのインストール

コマンド:

    gem install bandler

※インストール後`bundle env`と打ってrubyのバージョンが2.1.1になってればOK
ここで何故かBundlerがRubyの古いバージョンを見てててハマった
色々調べたあと`gem install bandler`と`rbenv rehash`したら出来た（謎

##Railsのインストール
コマンド:

    gem install rails

※結構時間かかる

------------------
### ここはから下はTree側で担当するので参考までに ###

##Gemfile（Railsで使うGemの設定ファイル）生成

コマンド:

    bundle init

※このコマンドを打ったカレントディレクトリがPJ名になるから、今回のPJ名はWoodTree

##生成されたGemFileを編集

`#gem "rails"`のコメントをはずす

##Railsをvender/bundleにインストール

コマンド:

    ARCHFLAGS=-Wno-error=unused-command-line-argument-hard-error-in-future bundle install --path vender/bundle

※そのままbundle install 〜 するとエラーになった。
Xcode 5.1でのclang更新によるエラー回避（意味分からん）らしい
`--path vender/bundle`でのパス指定を忘れずに

##Railsプロジェクトのひな形作成

コマンド:

    bundle exec rails new . --skip-bundle

※ここでGemfileを上書きしてるらしい
`--skip-bundle`忘れると意図しない場所にgem群がインストールされるので注意

##gitignoreの設定

https://github.com/github/gitignore/blob/master/Rails.gitignoreを使いました

##Gemfileの追記とbundle install

コマンド:

    bundle install --path vendor/bundle

----------------

#サーバーを起動する

コマンド:

    bundle exec rails server

http://localhost:3000/でアクセス出来ます

とりあえずここまで。。