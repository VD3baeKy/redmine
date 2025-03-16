# "Redmine"(レッドマイン)について
@[card](https://redmine.jp/)
* オープンソースの課題管理システム。
* 課題やタスクをチケットとして登録し、実施した作業を記録していくことで資産として残せる。
* プロジェクト管理、タスク管理、イベント開催時の管理、お客様とのお問い合わせ対応の管理にも利用できる。

|主な機能|
|:---:|
|"チケット"を使った課題や問題の追跡管理機能|
|ガントチャート機能|
|カレンダー表示機能|
|サマリー表示機能|
|プロジェクトや組織に関する文書やメモなど用途を問わず作成できるWiki機能|
|SubversionやGitといったバージョン管理システムと連携できる|
|ユーザー同士でテーマごとに議論するときに役に立つ掲示板機能（フォーラム）|

* "Redmine"以外には、[Jooto（ジョートー）](https://www.jooto.com)などがある。
@[card](https://www.jooto.com)

# "Redmine"デモサイト
[https://my.redmine.jp/demo/](https://my.redmine.jp/demo/)
@[card](https://my.redmine.jp/demo/)


# "Redmine"公式：日本語ドキュメント
[https://redmine.jp/guide/](https://redmine.jp/guide/)
@[card](https://redmine.jp/guide/)


## "Redmine" on windows
* 今回はDBをファイルで処理したいため、SQLサーバーを使用せずに```SQLite```で構築する。
* ```webrick```, ```ImageMagick```, ```rmagick```をインストールしてから"Redmine"をインストールしないとエラーが出る。

＜参考サイト＞
@[card](https://qiita.com/Phinloda/items/58afa1e42a36503bf076)
@[card](https://qiita.com/pugiemonn/items/3cee6d1aa6a07caab404)
@[card](https://toshiocp.com/entry/2023/08/26/221200)


## "Redmine"のダウンロード
* ```redmine```のwindows版をダウンロードして解凍する。
[https://redmine.jp/download/](https://redmine.jp/download/)
@[card](https://redmine.jp/download/)
* 解凍したら、インストールしたい場所へ移動する。

## database.ymlファイルの作成
* 解凍した```redmine```の中にある```config```フォルダ内で、```database.yml.example```ファイルをコピーして```database.yml```にファイル名を変更する。
* そして、```database.yml```ファイルを```SQLite3```用に編集する。

[```SQLite3```用の```database.yml```ファイル]
```
# Default setup is given for MySQL 5.7.7 or later.
# Examples for PostgreSQL, SQLite3 and SQL Server can be found at the end.
# Line indentation must be 2 spaces (no tabs).

#production:
#  adapter: mysql2
#  database: redmine
#  host: localhost
#  username: root
#  password: ""
  # Use "utf8" instead of "utfmb4" for MySQL prior to 5.7.7
#  encoding: utf8mb4
#  variables:
    # Recommended `transaction_isolation` for MySQL to avoid concurrency issues is
    # `READ-COMMITTED`.
    # In case of MySQL lower than 8, the variable name is `tx_isolation`.
    # See https://www.redmine.org/projects/redmine/wiki/MySQL_configuration
#    transaction_isolation: "READ-COMMITTED"

#development:
#  adapter: mysql2
#  database: redmine_development
#  host: localhost
#  username: root
#  password: ""
  # Use "utf8" instead of "utfmb4" for MySQL prior to 5.7.7
#  encoding: utf8mb4
#  variables:
#    transaction_isolation: "READ-COMMITTED"

# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
#test:
#  adapter: mysql2
#  database: redmine_test
#  host: localhost
#  username: root
#  password: ""
  # Use "utf8" instead of "utfmb4" for MySQL prior to 5.7.7
#  encoding: utf8mb4
#  variables:
#    transaction_isolation: "READ-COMMITTED"

# PostgreSQL configuration example
#production:
#  adapter: postgresql
#  database: redmine
#  host: localhost
#  username: postgres
#  password: "postgres"

# SQLite3 configuration example
production:
  adapter: sqlite3
  database: db/redmine.sqlite3

# SQL Server configuration example
#production:
#  adapter: sqlserver
#  database: redmine
#  host: localhost
#  username: jenkins
#  password: jenkins
```

## 対応するRubyバージョンの確認
* ```Gemfile```をテキストエディタで開くと、対応している```Ruby```のバージョンを確認できる。
* ```Ruby```をインストール済みの場合、コマンドプロンプトで```ruby -v```と入力するとインストールされている```Ruby```のバージョンを確認することができる。

[```Gemfile```]
```
source 'https://rubygems.org'

ruby '>= 3.1.0', '< 3.4.0'

gem 'rails', '7.2.2.1'
gem 'rouge', '~> 4.5'
gem 'mini_mime', '~> 1.1.0'
gem "actionpack-xml_parser"
gem 'roadie-rails', '~> 3.2.0'
gem 'marcel'
gem 'mail', '~> 2.8.1'
gem 'nokogiri', '~> 1.18.3'
gem 'i18n', '~> 1.14.1'
gem 'rbpdf', '~> 1.21.3'
gem 'addressable'
gem 'rubyzip', '~> 2.3.0'
gem 'propshaft', '~> 1.1.0'
gem 'rack', '>= 3.1.3'

#  Ruby Standard Gems
gem 'csv', '~> 3.2.8'
gem 'net-imap', '~> 0.4.8'
gem 'net-pop', '~> 0.1.2'
gem 'net-smtp', '~> 0.4.0'

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :x64_mingw, :mswin]

# TOTP-based 2-factor authentication
gem 'rotp', '>= 5.0.0'
gem 'rqrcode'

# HTML pipeline and sanitization
gem "html-pipeline", "~> 2.13.2"
gem "sanitize", "~> 6.0"

# Optional gem for LDAP authentication
group :ldap do
  gem 'net-ldap', '~> 0.17.0'
end

# Optional gem for exporting the gantt to a PNG file
group :minimagick do
  gem 'mini_magick', '~> 5.0.1'
end

# Optional CommonMark support, not for JRuby
group :common_mark do
  gem "commonmarker", '~> 0.23.8'
  gem 'deckar01-task_list', '2.3.2'
end

# Include database gems for the adapters found in the database
# configuration file
database_file = File.join(File.dirname(__FILE__), "config/database.yml")
if File.exist?(database_file)
  database_config = File.read(database_file)

  # Requiring libraries in a Gemfile may cause Bundler warnings or
  # unexpected behavior, especially if multiple gem versions are available.
  # So, process database.yml through ERB only if it contains ERB syntax
  # in the adapter setting. See https://www.redmine.org/issues/41749.
  if database_config.match?(/^ *adapter: *<%=/)
    require 'erb'
    database_config = ERB.new(database_config).result
  end

  adapters = database_config.scan(/^ *adapter: *(.*)/).flatten.uniq
  if adapters.any?
    adapters.each do |adapter|
      case adapter.strip
      when /mysql2/
        gem 'mysql2', '~> 0.5.0'
        gem "with_advisory_lock"
      when /postgresql/
        gem 'pg', '~> 1.5.3'
      when /sqlite3/
        gem 'sqlite3', '~> 1.7.0'
      when /sqlserver/
        gem 'tiny_tds', '~> 2.1.2'
        gem 'activerecord-sqlserver-adapter', '~> 7.2.0'
      else
        warn("Unknown database adapter `#{adapter}` found in config/database.yml, use Gemfile.local to load your own database gems")
      end
    end
  else
    warn("No adapter found in config/database.yml, please configure it first")
  end
else
  warn("Please configure your config/database.yml first")
end

group :development, :test do
  gem 'debug'
end

group :development do
  gem 'listen', '~> 3.3'
  gem 'yard', require: false
  gem 'svg_sprite', require: false
end

group :test do
  gem "rails-dom-testing"
  gem 'mocha', '>= 2.0.1'
  gem 'simplecov', '~> 0.22.0', :require => false
  gem "ffi", platforms: [:mingw, :x64_mingw, :mswin]
  # For running system tests
  gem 'puma'
  gem "capybara", ">= 3.39"
  gem 'selenium-webdriver', '>= 4.11.0'
  # RuboCop
  gem 'rubocop', '~> 1.68.0', require: false
  gem 'rubocop-performance', '~> 1.22.0', require: false
  gem 'rubocop-rails', '~> 2.27.0', require: false
  gem 'bundle-audit', require: false
end

local_gemfile = File.join(File.dirname(__FILE__), "Gemfile.local")
if File.exist?(local_gemfile)
  eval_gemfile local_gemfile
end

# Load plugins' Gemfiles
Dir.glob File.expand_path("../plugins/*/{Gemfile,PluginGemfile}", __FILE__) do |file|
  eval_gemfile file
end

gem "webrick", "~> 1.9"
gem "rmagick", "~> 6.1"
```


## Rubyのインストール
* [https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/) からインストールファイルをダウンロードできる。

|ダウンロードするファイル|
|:---:|
| ```rubyinstaller-devkit～x64.exe``` |

@[card](https://rubyinstaller.org/downloads/)
@[card](https://prog-8.com/docs/ruby-env-win)


## SQLite3のインストール
* [https://sqlite.org/index.html](https://sqlite.org/index.html) にアクセスして、"SQLite ダウンロード ページ"を開く。
* "Windows 用のコンパイル済みバイナリ"で、次の２つのファイルをダウンロードして解凍する。

|ダウンロードするファイル|
|:---:|
| ```sqlite-dll-win-x64～.zip``` |
| ```sqlite-tools-win-x64～.zip``` |

* 解凍したら次の２つのファイルを、```redmine```の中にある```bin```フォルダへコピーする。

|```bin```フォルダへコピーするファイル|
|:---:|
| ```sqlite3.exe``` |
| ```sqlite3.dll``` |


## "Remdmine"のインストール
* ```webrick```, ```ImageMagick```, ```rmagick```をインストールしてから"Remdmine"をインストールする。
@[card](https://qiita.com/Phinloda/items/58afa1e42a36503bf076)
@[card](https://redmine.jp/guide/RedmineInstall/#_3)

1. コマンドプロンプトを立ち上げて、```remdmine```のディレクトリへ移動する。
2. コマンドプロンプトで```gem install webrick```を入力して```webrick```をインストールする。
3. ```rmagick```をインストールするために、```ImageMagick```をインストールする。
```ImageMagick```は、[https://imagemagick.org/script/download.php#windows](https://
imagemagick.org/script/download.php#windows)でダウンロード可能。

| "ImageMagick": ダウンロードしてインストールファイル|
|:---:|
| ```ImageMagick-～-Q16-x64-static.exe``` |

```ImageMagick```インストール中の```Setup```のダイアログで、 **```Install development headers and libraries for C and C++```にチェックを入れる。**
@[card](https://www.redmine.org/projects/redmine/wiki/HowTo_install_rmagick_gem_on_Windows)
4. ```ImageMagick```をインストールしたら、```ImageMagick```の```PATH```をセットする：　```set Path=%PATH%;C:\usr\local\ImageMagick-〇〇〇-Q16-HDRI;```
5. コマンドプロンプトを立ち上げなおす。
6. ```rmagick```をインストールする：　```gem install rmagick```
7. 公式の手順通りに```Bundler```を実行：　```bundle install --without development test```
@[card](https://redmine.jp/guide/RedmineInstall/#_3)
8. ```webrick```と```rmagick```が入っていないため、手動で追加：　```bundle add webrick rmagick```
9. セッションストア秘密鍵を生成する：　```bundle exec rake generate_secret_token```
10. データベースのテーブル等の作成： 
```set RAILS_ENV=production``` 
```bundle exec rake db:migrate```
11. デフォルトデータをデータベースに登録する： 
```set RAILS_ENV=production```
```bundle exec rake redmine:load_default_data```

@[card](https://aquasoftware.net/blog/?p=658)


## "Redmine"インストールの確認
* コマンドプロンプトで、```bundle exec rails s -e production```を実行する。
* ブラウザで ```http://localhost:3000/``` へアクセスして動作を確認する。


