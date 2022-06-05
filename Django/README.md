## Django

## Djangoについて
### Webアプリケーションの基礎
***代表的なリクエストメソッド***
- 一覧
    - GET：HTMLなどのリソースを要求
    - POST：Webアプリにキーと値をセットにしてデータを渡す
    - PUT：リソースの更新を要求
    - DELETE：リソースの削除を要求
***代表的なステータスコード***
- 一覧
    - 200(OK)：成功
    - 301(Moved Permanently)：恒久的にページが移動している
    - 302(Found)：一時的にページ移動している
    - 403(Forbidden)：アクセス権限がない
    - 404(Not Found)：リソースが存在しない
    - 500(Internal Server Error)：サーバー内でエラーが発生している

### Djangoの基礎
***Djangoプロジェクトの構築***
- コマンド一覧
    - 開発開始関係
        - $pip install Django
            - ※最新版にアップデートする場合は $pip install -U django
        - $django-admin startproject <プロジェクト名>
            - ※プロジェクトが2重にならないようにする場合は $django-admin startproject <プロジェクト名> .
        - $python manage.py startapp <アプリケーション名>
    - その他
        - $python manage.py runserver
        - $python manage.py makemigrations <アプリケーション名>
        - $python manage.py migrate
        - $python mamage.py showmigrations <アプリケーション名>
            - マイグレーション状態の確認
        - $python manage.py migrate <アプリケーション名> 0001_initial
            - 0001_initial適用直後までマイグレーションのロールバック実行
        - $python manage.py test
        - $python manage.py shell
- フォルダ構成一覧
    - project(プロジェクト全体をまとめたディレクトリ)
        - application(アプリケーション関連ファイルをまとめたディレクトリ)
            - migrations(マイグレーションファイルを格納したディレクトリ)
            - templates(テンプレートファイルを格納するディレクトリ)
                - index.html(テンプレートファイル)
            - __init__.py(Pythonのパッケージだと示すファイル)
            - admin.py(管理サイト設定ファイル)
            - apps.py(アプリケーション構成設定ファイル)
            - forms.py(フォーム定義ファイル)
            - models.py(モデル定義ファイル)
            - tests.py(テストコード記述ファイル)
            - urls.py(アプリケーション用ルーティング定義ファイル ※作成必須(デフォルトだとない))
            - views.py(ビュー定義ファイル)
        - project(プロジェクト全体に関わるファイルをまとめたディレクトリ ※ない場合もある)
            - __init__.py(Pythonのパッケージだと示すファイル)
            - settings.py(プロジェクト設定ファイル)
            - urls.py(プロジェクト用ルーティング定義ファイル)
            - wsgi.py(デプロイ用ファイル)
            - asgi.py(WSGIの精神的後継である 非同期Webアプリケーションデプロイ用)
        - manage.py(コマンド実行用ファイル)
***ルーティング***
- URLをパターンマッチングして処理経路を制御する役割
- 名前空間を設定することで複数のアプリケーションでURLの名前がかぶっていても呼び出すことができる(app_name)
- デフォルトで使える名前パスコンバータ
    - str：空文字を除く文字列をキャプチャ(「/」は除く)
    - path：空文字を除く文字列をキャプチャ(「/」を含む)
    - int：0または正の整数をキャプチャする
    - stug：半角英数字とハイフン(-)とアンダースコア(_)のみで構成された文字列をキャプチャできる
    - uuid：UUID(ハイフンで区切られた128ビットの識別子)をキャプチャ(例：760c7e72-619e-4d4e-9d4d-31025b6eb03e)
***ビュー***
- ルーティングからリクエスト情報(HttpRequestオブジェクト)を受け取ってからレスポンス情報(HttpResponseオブジェクト)を作り出すことが大きな役割
- 役割一覧(上記その他)
    - フォームコンポーネントにフォーム処理を依頼
    - モデルコンポーネントにデータベースの操作依頼
    - テンプレートコンポーネントにhtmlの生成を依頼
    - 画面遷移先の判断を行い、ルーティングに処理を移譲
- ビューの定義方法
    - 関数ベースビュー(使われないから後回し)
    - クラスベースビュー
        - Django提供のクラスベースビューを継承して作成
- 代表的なクラスベースビュー一覧
    - RedirectView：リダイレクトに特化した処理をする
    - TemplateView：テンプレート表示に特化した処理をする
    - ListView：モデルオブジェクトの一覧を表示
    - CreateView：モデルオブジェクトを作成
    - DetailView：モデルオブジェクトの詳細を表示
    - UpdateView：モデルオブジェクトを更新
    - DeleteView：モデルオブジェクトを削除
    - FormView：フォーム処理をする
***フォーム***
- フォーム画面で入力された値をフォームオブジェクトに変換及び保持するコンポーネント(入力値のバリデーションチェックも可能)
- ※自分で作成する
- フォームの定義方法
    - django.forms.Formクラス
        - どのようなフォームに対しても使用可能
    - django.forms.ModelFormクラス
        - モデルのフィールドとフォーム画面のフィールドが同じ場合に使用
        - modelのフィールド定義を流用するため、Formクラスより簡潔に記述でき、各フィールドに設定した制約のバリデーションチェックも行ってくれる(こっちの使用が望ましい)
- 代表的なフィールドクラス一覧
    - CharField：TextInput：<input type="text">
    - IntegerField：NumberInput：<input type="number">
    - ChoiceField：Select：<select>
    - DateField：DateInput：<input type="text">
    - DateTimeField：DateTimeInput：<input type="text">
    - EmailField：EmailInput：<input type="email">
    - FileField：ClearableFileInput：<input type="file">
    - ImageField：ClearableFileInput：<input type="file">
- 全フィールドクラスで使える代表的なフィールドオプション
    - required：必須フィールドにするかどうか(True(デフォルト)またはFalseを設定)
    - label：フォーム画面のラベル設定
    - widget：ウィジェットを設定
    - validators：バリデータを設定
- 独自バリデーションの追加方法
    - validatorsを使う：異なるフォーム間やフォーム/モデル間で同じバリデーションを共有
    - 「clean_<フィールド名>」メソッドを使う：単一フォーム内で単体フィールドバリデーションを行う
    - 「clean」メソッドを使う：単一フォーム内でフィールドをまたがるバリデーションを行う
***モデル***
- モデルを通してデータベースをPythonのオブジェクトとして扱う(データベースとオブジェクトをマッピングする仕組みをO/Rマッピングという)
- モデルの定義方法
    - django.db.models.Modelクラスを継承して作成
    - __str__(self)で、テンプレートの{{}}で表示させる際の表示内容をカスタマイズできる
- モデルのフィールドクラス一覧
    - CharField
    - TextField
    - IntegerField
    - PositiveIntegerField
    - FloatField
    - DataField
    - DateTimeField
- モデルオブジェクトを使ってのデータベース操作
    - 変数名 = <DB名>.objects.get()：1行取得
    - 変数名 = <DB名>.objects.all()：全レコード取得するQuerySetオブジェクトの作成(models.pyの__str__で指定した形で取り出される)
        - 変数名 = <DB名>.objects.all().values()：モデルに保存してある値を辞書型で取得
        - 変数名 = <DB名>.objects.all().values_list()：モデルに保存してある値をタプルで取得
    - 変数名 = <DB名>.objects.fillter()：条件指定
        - あいまい検索
            - 項目名__contains=値：値を含む検索
            - 項目名__startswith=値：値で始まる検索
            - 項目名__endswith=値：値で終わる検索
        - 大文字小文字を区別しない
            - 項目名__iexact=値：普通の検索
            - 項目名__icontains=値
            - 項目名__istartswith=値
            - 項目名__iendswith=値
        - 数値の比較
            - 項目名__gt=値：値より大きい
            - 項目名__gte=値：値以上
            - 項目名__lt=値：値より小さい
            - 項目名__lte=値：値以下
        - AND
            - 変数名 = <DB名>.objects.fillter(条件1, 条件2)
            - ※<DB名>.objects \ の後に改行で .fillter(条件n) \ を書いていく方法もある
        - OR
            - 変数名 = <DB名>.objects.fillter(Q(条件1) | Q(条件2))
            - ※先頭で from django.db.models import Q を記述
        - リストを使って検索
            - 変数名 = <DB名>.objects.fillter(項目名__in=リスト)
            - ※検索対象を事前にリストで作成しておく
    - 参照(公式)：https://docs.djangoproject.com/ja/4.0/topics/db/queries/
    - 参照：https://qiita.com/Bashi50/items/9e1d62c4159f065b662b

### Djangoの中級
***言語とタイムゾーンを日本仕様に変更する***
- settings.pyに以下を記述
    - LANGUAGE_CODE = 'ja'
    - TIME_ZONE = 'Asia/Tokyo'
***データベースの変更(PostgreSQL)***
- settings.pyのDATABASESを以下に変更
    - 'ENGINE' = 'django.db.backends.postgresql_psycoge2'
    - 'PORT' = '5432'
***ロギングの設定(後で)***
- 参照：https://docs.djangoproject.com/ja/4.0/topics/logging/
- 参照：https://kamatimaru.hatenablog.com/entry/2020/12/14/020610
***静的ファイルの置き場所設定***
- settings.pyに以下を記述
    - STATICFILES_DIRS = ( os.path.join(BASE_DIR, 'static') )
    - $python manage.py collectstatic
***フォーム動作時の処理(後で)***
***メール送信処理(後で)***
- メールの送付先をコンソールに設定する場合、settings.py(settings_dev)に以下を記述
    - EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
***プロジェクト設定ファイル(settings.py)の分割***
- 本番環境用(settings.py)と本番/開発共有用(settings_common.py)と開発環境用(settings_dev.py)に分割する
- settings.pyに以下を記述
    - from .settings_common import *
- サーバー起動コマンドが以下に変更
    - $python manage.py runserver --settings=config.<使うsettings名>
***all-authでの認証機能の作成(後で)***
***テストについて(後で)***
- テストの方式
    - テストクラス(TestCase)を使用
        - 簡単なアプリケーションで使用
    - Seleniumを使用(DjangoのLiveServerTestCaseクラスの使用が必須)
        - JavaScriptで画面を描画しているアプリケーションで使用
    - ※どちらもPythonの標準テストクラス(TestCase)がベース
- テストの流れ
    - テストデータベースの作成,テストクラスの収集
    - ※テストクラス単位で以下ループ
        - setUpClass()の実行
        - ※テストメソッド単位で以下ループ
            - setUp()の実行
            - test_xxx()の実行
            - tearDown()の実行
            - テスト用データベースのロールバック(テストメソッド単位)
        - tearDownClass()の実行
        - テスト用データベースのロールバック(テストクラス単位)
    - テスト用データベースの削除
***データベースのバックアップバッチの作成(後で)***
***セキュリティチェック***
- ※ログ出力ディレクトリがないとエラーになる
- $python manage.py check --deploy
***モデル(データベース操作)***
- レコードの並べ替え
    - 変数名 = <DB名>.objects.<allかfillter>().order_by(項目名)：項目名を昇順で並べ替え
    - 変数名 = <DB名>.objects.<allかfillter>().order_by(項目名).reverse()：項目名を降順で並べ替え
- 指定した範囲のレコードを取得
    - 変数名 = <DB名>.objects.<allかfillter>()[開始位置：終了位置]：開始位置から終了位置までの要素を取得
    - レコード検索
        - find = request.POST['find']
        - list = find.split()
        - data = <DB名>.objects.<allかfillter>(int(list[開始位置])：int(list[終了位置]))
        - ※入力フォームに数字が入力されていないといけない
- レコードの集計
    - 変数名 = <DB名>.objects.aggregate(関数(項目名))
    - 関数一覧
        - Count(項目名)
        - Sum(項目名)
        - AVG(項目名)
        - Min(項目名)
        - Max(項目名)
    - ※先頭で from django.db.models import Count,~ を記述する
    - ※集計された値は、変数名['項目名__関数名(小文字)']で取得可能(辞書型で格納されている)
- SQLを直接実行
    - 変数名 = <DB名>.objects.row(クエリ文)

[memo]
***テンプレート(フィルター機能について)***
- Djangoのテンプレートでは、{{}}で値を出力する時、HTMLのタグが含まれていると自動的にエスケープ処理(テキストとして出力)を行う
- {{ message|safe }}と記述することで、フィルター機能(HTMLタグを書き出せる)を適用できる
*** 順参照と逆参照 ***
- 
***モデル定義とクエリ操作***
- Django ORMによるモデル定義
    - ※マイグレーションファイルから生成されたSQLは $python manage.py sqlmigrate <app_label> <migration_name> で確認可能
    - ※Djangoでは複合主キーを生成することができない(対策方法：https://gijutsu.com/2021/01/19/django-composite-primary-key/ か django-compositepk-modelを使用)
    - Djangoのレコードの一括作成,更新方法(後で)
        - bulk_createとbulk_updateを使用
            - 参考：django-compositepk-model
    - Metaオプション
        - 本来データベース名は<アプリケーション名>_<モデル名>が使用されるが、Metaオプションを使用すると、データベース名を自由に設定できる
    - モデルフィールドの定義
        - モデルフィールドの一覧
            - 文字列：CharField、TextField、EmailField、JSONField、URLField、SlugField
            - 数値：IntegerField、FloatField、AutoField、DecimalField、CommaSeparatedIntegerField
            - 二値：BooleanField、NullBooleanField
            - 時刻：DateField、DateTimeField、TimeField、DurationField
            - ファイル：FileField、FilePathField、ImageField
            - 関係：ForeignKey、OneToOneField、OneToMenyField
            - PostgreSQL：ArrayField、HStoreField、IntergerRangeField、DataRange、Field....
            - その他：GenericIPAddressField、UUIDField
        - ※UUIDFieldなどはMySQLやSQLiteだと、CHAR(32)で扱われるが、PostgreSQLだとUUID型となるなどDBによって変わるものがあるため、意図した型として扱われているか確認するために、$python manage.py sqlmigrateを行う必要がある
        - 複数の選択肢の中でどれか1つの値を保持するようなフィールドの定義(後で)
            - choices属性を用いて定義
        - nullの扱い方
            - ※入力が任意だからとnullを許容すると、入力されていないレコードを検索する際に、null+空文字の検索を行わないといけなくなるため、nullを許容せず、デフォルトで空文字を入れる方式にしたほうが良い
            - nullオプションをFalse、defaultオプションを''、blankオプションをTrueに設定する
- Django ORMによるクエリ操作(後で)
    - モデルAPIを使用した、作成,更新,削除(後で)
        - $python manage.py shell_plusコマンドを使用
    - select_relatedによるテーブル結合(後で)
    
