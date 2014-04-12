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
    
※これでruby -vと打ってバージョンが2.1.1になってればOK