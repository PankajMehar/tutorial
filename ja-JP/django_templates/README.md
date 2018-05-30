# Djangoテンプレート

何かデータを表示しましょう！Djangoはそれをビルトインの **テンプレートタグ** で実現できます。

## テンプレートタグとは？

HTMLではブラウザがpythonを認識できないのでpythonのコードは書けません。HTMLはより静的でpythonは動的です。

**Djangoテンプレートタグ** はHTMLにPyhtonのようなコードを埋め込むことができて、動的なウェブサイトがより早く簡単に作れます!

## ブログ一覧テンプレート

前の章で、`posts` 変数でテンプレートに記事のリストを渡しました。今からHTMLで表示をしてみましょう。

Djangoテンプレートで変数を表示するためには、次のように変数の名前を二重中括弧で括ります。

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
{{ posts }}
```

これを `blog/templates/blog/post_list.html` に書いてみて下さい。 （２つめと３つめの `<div></div>` タグをまるごと `{{posts}}` に置き換えて下さい。） ファイルを保存してページをリロードしますと：

![図 13.1](images/step1.png)

見たとおり、このようになります。

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
<QuerySet [<Post: My second post>, <Post: My first post>]>
```

Djangoはオブジェクトのリストと認識します。 **Introduction to Python** を思い出して下さい。 ループを使ってリストを表示しましたよね。 Djangoテンプレートではこう書きます：

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
{% for post in posts %}
    {{ post }}
{% endfor %}
```

これをブログのテンプレートで使ってみましょう。

![図 13.2](images/step2.png)

動きましたね。 しかし、本当は、**Introduction to HTML** で作った静的な記事のように表示してほしいところです。 そこで、HTMLとテンプレートタグを混ぜてみましょう。 `body` タグの中を次のように書いてください：

{% filename %}blog/templates/blog/post_list.html{% endfilename %}

```html
<div>
    <h1><a href="/">Django Girls Blog</a></h1>
</div>

{% for post in posts %}
    <div>
        <p>published: {{ post.published_date }}</p>
        <h1><a href="">{{ post.title }}</a></h1>
        <p>{{ post.text|linebreaksbr }}</p>
    </div>
{% endfor %}
```

`{% for %}` と `{% endfor %}` の間にリストの中のオブジェクトごとに表示したい内容を書くとオブジェクトの数だけ繰り返し書かれます。ページをリロードしてみましょう。

![図 13.3](images/step3.png)

`post` 変数がさっきと違って、`{{ post.title }}` や `{{ post.text }}` になっていることに気づきましたか？ `Post` モデルで定義したそれぞれのフィールドにアクセスしています。 `|linebreaksbr` はpostのテキスト中の改行を段落に変換するフィルタに通すという意味です。

## もう一つ...

今の時点でのウェブサイトを公開して見てみませんか？もう一度PythonAnywhereでデプロイしてみましょう。デプロイのステップをおさらいします。

* まず、GitHubでコードをpushします。

{% filename %}command-line{% endfilename %}

    $ git status
    [...]
    $ git add --all .
    $ git status
    [...]
    $ git commit -m "Modified templates to display posts from database."
    [...]
    $ git push
    

* そしたら、[PythonAnywhere](https://www.pythonanywhere.com/consoles/)に戻って、**Bashコンソール**（か、新しいコンソール）に入って、次のようにコマンドを打ちましょう：

{% filename %}PythonAnywhere command-line{% endfilename %}

    $ cd my-first-blog
    $ git pull
    [...]
    

* 最後に[ブラウザのタブ](https://www.pythonanywhere.com/web_app_setup/)を開いてアプリを**リロード**します。更新が反映されています！ PythonAnywhereサイトで表示されるブログの記事が、あなたのパソコンの中のローカルサーバーのものと違っていても大丈夫です。 ローカルコンピュータにあるデータベースと、PythonAnywhere上のデータベースは同期していません。

おめでとうございます！よくできました! これができたら、Django adminとして新しい投稿を追加しましょう（published_dateを忘れないで！）。PythonAnywhereサイトのDjango管理者であることを確認してください（https://yourname.pythonanywhere.com/admin）。それから、投稿したものがそこに見えるか、リロードしましょう。

動くのが楽しくなってきたでしょう？少しパソコンから離れて、休憩しましょう：）

![図 13.4](images/donut.png)