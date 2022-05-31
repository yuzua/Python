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
        - $python manage.py makemigrations
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
***モデル(続きはここから)***
- モデルを通してデータベースをPythonのオブジェクトとして扱う(データベースとオブジェクトをマッピングする仕組みをO/Rマッピングという)
- モデルの定義方法
    - django.db.models.Modelクラスを継承して作成
- モデルのフィールドクラス一覧
    - CharField
    - TextField
    - IntegerField
    - PositiveIntegerField
    - FloatField
    - DataField
    - DateTimeField
- モデルオブジェクトを使ってのデータベース操作
    - .object.get()：1行取得
    - .object.all()：全レコード取得するQuerySetオブジェクトの作成
    - .object.fillter()：条件指定
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


[memo]
*** 順参照と逆参照 ***
- 