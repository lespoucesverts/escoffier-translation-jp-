# エスコフィエ『料理の手引き』全注解　作業用リポジトリ #

## Boards 活用のご提案

Githubにも似たものはありましたが、Bitbucket の場合は別サービスをプラグインにしているようで、別途アカウントの作成があります。進捗状況の把握に非常に便利ですので、ぜひともご活用いただくことを提案します。

アカウントの作成は以下のリンクからお願いします。

[Boards](https://trello.com/invite/b/ktOU4u29/16407b25f072f2a2898075eab48b494c/escoffier-working)

# EPUB 対応のために、一部の書式を変更しました。これまでに下訳していただいた分は僕が対応しますが、これから先の分については、以下の変更点をご配慮いただければ幸いです。

## 【重要】 EPUB 対応をスムーズにおこなうには、半角文字（数字、アルファベット、記号）の前後に半角スペースを入れるときれいに出力されます。もちろんCSSで調整できるんですが、前にも半角スペースを入れてあるとプレビューでも見易いので、原則、この方針でいきませんか? ただし、直後に句読点などの「役物」が来る場合にスペースを開けると禁則処理が崩れますので、その場合のみ半角スペースは入れないでください。


## 【重要】作業はページ順には進行していません。現時点での作業予定は、下記ロードマップをご参照ください。

* 2018年6月……野菜、パスタ、
* 7月……魚料理
* 8月……魚料理
* 9月……牛
* 10月……仔牛
* 11月……羊、豚
* 12月……ポタージュ
* 2019年1月……鶏、ジビエ
* 2月……オードブル
* 3月……卵料理、Entrées mixtes、ロースト、冷製
* 4月……アントルメ
* 5月……アントルメ
* 6月……アイス、ジャム、軽食、ドリンク



## 【重要】 Markdown ``.md`` ファイルでは、改行はただの半角スペースになってしまいますので、段落を変える場合は、空行をひとつ入れてください。

なお、段落を変えずに改行する必要がある場合はないと思います（レシピなど段落の1字下げしていませんし）が、それが必要な場合は行の最後に半角スペースを2つ入れます。


## フランス語見出しをTeXの書式からHTMLの書式に変更しました。  
  
    <div class="frchap">フランス語の章題</div>  
    <div class="frsec">フランス語の節タイトル=日本語が（##）になる部分に対応</div>  
    <div class="frsecb">フランス語の小節タイトル=日本語が(###)になる部分に対応</div>  
    <div class="frsub">レシピ名</div>
    
  

ダブルクォートや終わりの``</div>``は忘れやすいので気をつけてください。パソコン上にリポジトリをクローンしてエディタを使う場合は、スニペットと呼ばれるショートカット設定プログラムがあります(僕はEmacs で yasnippet というのを使っています)。あるいは、日本語変換に上の書式を適当なキーワードで登録してください。記号、アルファベットはすべて半角を用いてください。



## 1段組と2段組の自動組版をするために、  
  
  
    <div class="main">  
    一段組みの部分（タイトル含む）  
    </div>  
    
    
    <div class="resette">
    二段組みの部分つまりレシピのところ
    </div>
     
  
  
となります。これも最後の``</div>``を忘れやすいので注意してください。僕は
  
  
  
    <div class="main"><!--beginMain-->  
    一段組みの部分（タイトル含む）  
    </div><!--endMain-->  
    
    
    <div class="resette"><!--beginRecette-->
    二段組みの部分つまりレシピのところ
    </div><!--endRecette-->
    
  
  
のように、HTMLのコメント付きで書いています。あとでわかりやすいですから。



## 各原稿ファイル .md の上部に必要な yaml metadata block を入れることにしました(EPUB,PDF両方であったほうがいいので)



具体的には

    ---
    title: エスコフィエ『料理の手引き』全注解
    author:
    - 五 島　学
    - 河井 健司
    - 春野 裕征
    - 山本 学
    pandoc-latex-environment:
        main: [main]
        recette: [recette]
        frsubenv: [frsubenv]
        frsecenv: [frsecenv]
        frsecbenv: [frsecbenv]
        frchapenv: [frchapenv]
    ...


  
となります。これはEPUBバージョンを作る際には揃っている必要あがあるので、このまま行けるようよろしくお願いします。この部分に名前だあるということは、最低でも扉と奥付において「共著者」としてクレジットされることを意味します。それはすなわち**文責**があるということでもあります。作業がそれに伴わない場合はここのリストからはお名前を消して、「訳者あとがき」で謝辞を書かせていただくのが限界となります。

このデータブロックはファイルの先頭に置き（実際にはどこれも大丈夫なんですが間違いを避けるため文頭にします。）冒頭と最後の行頭に3つハイフンおよびピリオド3つ(すべて半角)が入ります。行頭は必ずハイフン3つです。新規にファイルを作る場合には他のファイルからコピペしてください。後半は変換プログラム pandoc で使う**フィルター**と呼ばれるものの設定です。上で書いた HTML の書式に変更した理由が、ここで設定されているフィルタを使って、EPUBでもdocxでもフランス語が欠落しないようにさせることです。

## 下線を廃止して強調はゴチにしました。``\ul{foobar}``は使わないでください。

通常の Markdown の強調を用います。

    **ゴチ(太字)**  
    
です。欧文（書名などで使われます)では 

    *italicイタリク*  
    
も使えます。日本語の斜体は組版的に美しくないので使いません。    


    
## ルビの書式も変えました。
  
    [よみかな](-漢字)
      
です。インデックスのマークアップと同じ順なのでかえってやりやすいかも知れません。EPUB ではいまのところ実現できていませんが、ソースとして出力されているものは正しい記述になっているので、いずれ対応できると思います。もちろん現状でもPDFにする際はこの書式が有効になっています。

現状では従来の``\ruby{漢字}{よみかた}``も一応は有効になっていますが、EPUBにするとごっそり漢字ごと欠落するので使用を控えてください。

## GithubのWikiを docs ディレクトリに移送しました。
* 操作方法、編集協力の方法についての詳しいドキュメントはこのリポジトリのdocsディレクトリにあります。現状は Github の説明のままです。必要に応じてご説明します。

以下、不要とは思いますが旧README.mdの内容です。注および半角数字、単位については変更ありません。が、分数は前後に半角スペースを入れておいてください(直後が句読点=役物の場合を除く -> 単位などと同様に分数も直後に句読点などが来るときはスペースを空けないでください)。

-----
# Obsolete

## 「チラ見」ファイルの閲覧、ダウンロード ##

* 「チラ見」用のPDFは<>code の最上位ディレクトリにあります。ファイル名は SPECIMEN.pdf です。拡張子にご注意ください。

* 本文は1段組み、レシピは二段組です。PDFの設定上は現在、A4版、文字サイズは14級（近似値的）。パソコンや高解像度のタブレットだと読みやすいでしょう。スマートフォンの場合は、画面の小さな機種では非常に読みづらいかも知れません。


## 編集協力の方法 ##

編集協力者は常時募集中です。Githubのシステム上、アカウントをお持ちであればどなたでも編集にご協力いただけます。詳しくは、このリポジトリの Wiki をご参照ください。

### 1. WEBブラウザで編集する ###

これがいちばん簡単な方法です。Githubでググるとリポジトリをフォークして云々……と出てきますが、**そんなこと気にせずに、このリポジトリのディレクトリにある\*.mdファイルを開いて編集しちゃってみてください**。Wikiページの「01_基礎編」をお読みください。たいていはこのドキュメントが理解できれば大丈夫です。

### 2. 自分のパソコンで編集する ###

とはいえ、お手元のパソコンで好きなエディタを使って作業ができるようにしたいかも知れませんので、その方法を書いておきました。Wikiページの「02_中級編」をお読みください。

### 3. Collaborator になるには……

とにかくプルリクエストを重ねて積極的に参加してください。オーナー側がいちいちプルリクエストの内容を確認する必要がないと判断した場合に、Collaboratorに指名させていただきます。Wikiページの「03_中級編2」をお読みください。


### 4. 誤字、脱字の修正で作業していただきたいファイル ###

Markdownファイル（.md）が作業ファイル=原稿です。TeXの独自命令が増えてしまったので、markdown と TeX の**ちゃんぽん**のような書式になっています。バックスラッシュ\で始まる文字列がTeXの命令ですが、なんとなく意味はおわかりいただけるように書いているつもりです。

[Pandoc Extended Markdown](https://pandoc.org/MANUAL.html#pandocs-markdown)いう書式を用いており（[日本語版はこのリンクの上から1/3くらいのところ](http://sky-y.github.io/site-pandoc-jp/users-guide/)、ただし内容が古いので出来るだけ英語版を参照してください）、このサービスで標準とされている Github Flavored Markdown に準拠していない部分があるため、ブラウザ上でのプレビューは正しく表示されないことがほとんどです。

原稿そのものを適切にプレビューするには、Pandoc Extended Markdown に対応したエディタが必要です。（Atomというエディタの追加パッケージで対応する、markdown preview plus というものがあり、とても便利です）。

**番号（=章番号）で始まるディレクトリ内のMarkdownファイルに対してのみ編集してコミットするようにしてください**。（以下にファイル名を列挙しておきます）

命名規則は

章番号-節番号-pp原書のページ範囲.md

* 00-avant-propos/00-avant-propos.md
* 01-sauces/01-01-pp1-12.md
* 01-sauces/01-02-pp13-17.md
* 01-sauces/01-03-pp18-27.md
* 01-sauces/01-04-pp28-41.md
* 01-sauces/01-05-pp42-46.md
* 01-sauces/01-06-pp47-52.md
* 01-sauces/01-07-pp53-57.md
* 01-sauces/01-08-pp58-62.md
* 01-sauces/01-09-pp63-67.md
* 02-garnitures/02-01-pp68-77.md
* 02-garnitures/02-02-pp78-82.md
* 02-garnitures/02-03-pp83-88.md
* 02-garnitures/02-04-pp89-103.md

**慣れないうちは、これらのファイルに対してだけ変更をコミットしてください。**

もちろん、これらのファイルを参考にして、まだ訳と注釈をつけていない部分のファイルを作成してコミットしてくださることは大歓迎です。

PDFは適時マージされます。単に組版イメージ確認のためのものであり、コミットいただいた内容がリアルタイムで反映されるとはかぎりません。

それ以外のファイル（TeX関連が主です）は、Lualatex を分る方以外は触らないようにご注意ください。目まいがするか、頭が痛くなっても責任は負えません。基本的に自動生成させて、手を加えてから PDF を LuxLaTeX により自動組版させています。

原稿ファイル（.md）には時折\{\#fonds-blanc-volaille\} のようなものが見出しにありますが、これはPDFやHTML、EPUBで内部リンクを張るための「ラベル」です。原書の項目名を、すべて小文字」にしてアクサンなし、ハイフンでつないでいます。


## 重要! ローカルルール #####

* 数字は一桁のものも半角数字を用いてください（全角は用いないでください）。アルファベット、ローマ数字も半角を用いてください。原則的には前後にスペースを入れる必要はありません（とりわけ禁則文字、役物の一部が自動処理されずに問題が発生することが確認されました）。
* ただし、単位を表す mL, dL, L, g, kg, mm, cm なども半角文字を使いますが、これら単位の直前、つまり半角数字の直後には半角スペースを挟んでください。（例） ワイン1 dL、

これらはTeXで処理する際に、自動的に適当に文字間を調整して表示されます。


### 注釈の編集、追加方法 ####

すでにある注釈に変更を加える場合は、直接書き込んでください。その直後に\[\](○○変更)のようにコメントがあるとわかりやすいでしょう。

あらたに注釈を追加する場合、すでにある番号とダブってしまうとエラーの原因になりますので、

    本文[^15]本文本文[^15bis]本文本文本文
    本文本文本文。

    [^15]: すでにある注釈だけどここは変更[](20180129○○変更)注釈文の続き

    [^15bis]: あらたに追加した注釈

のように、直前の注釈番号にbisをつけてください。すでに直前のものにbisがついている場合は、bis2、bis3のようにして、かならず番号がダブらないようご注意ください。また、注釈は対象の段落の直後がわかりやすくて便利です。

### TeX命令文が含まれています ###

基本的に、TeXという組版プログラム群を使う前提の md ファイルです。そのため、markdown の書式ではないTeX命令の行がしばしばあり、プレビュー状態でも表示されてしまいます。

    \index{garniture@garniture!madeleine@--- Madeleine}
    \index{madeleine@Madeleine!garniture@garuniture ---}
    \index{かるにちゆーる@ガルニチュール!まとれーぬ@---・マドレーヌ}
    \index{まとれーぬ@マドレーヌ!かるにちゆーる@ガルニチュール・---}


あるいは

    \newpage

あるいは

    文章\ruby{漢字}{ふりがな}

など。



### 分数の表示はMarkdownで一般によく使われているTeX表記です #####

#### 表記

    $\frac{分子}{分母}$

つまり

    1/2 = $\frac{1}{2}$

という感じになります。分子と分母がわかれば数字のチェックも可能だと思います。

**TeXに不慣れな方はバックスラッシュ\で始まるこれらの表現には触れないようにしてください**。お願いします。

### 編集コメント ###

短かいコメントは**文中に**、少し長いなら、該当段落の下にカラ行を多めに入れてあるので、そこに、

    [](コメント)

として書いてください。\[と\]の間はスペースなし。**半角記号**です。カッコも必ず**半角**にしてください。多少長くなっても大丈夫ですが、余分な改行は入れないほうがコメント行としてきちんと機能する可能性が高いので、改行しないようお願いします。

編集モードでこの行の下を見るとコメントの実例が見られます。

[](これはコメントの例です)

このようにして書いたコメントは「プレビュー」モードで表示されなくなりますが、編集モードとdiff表示において表示されます。

長いコメントは、コミットする際（後述）にコメント欄がありますので、そこでも大丈夫です。


### コミット ###

とても**大事なこと**なのでここでも書いておきます。

ブラウザ上で編集した場合、作業後に

1. 上のほうにある Preview Changes を押して変更内容を確認します。環境によってはちょっと待たされることがあります。
2. OKであれば、スクロールして下の方にある Create a new branch for this commit and start a pull request. の左のラジオボタンが選択されていることを確認し、上のコメント覧に変更内容等を書いてください。
3. 大きなボタン Commit Changes を押します。
4. 画面が変わり、Create a Pull Request なんたらという表示が出るので、再確認ボタンを押すと「プルリクエスト」が作成されたことになります。この時点ではこのリポジトリのファイルに変更は加えられていません。要するに「変更の提案」ということです。このときにコメント欄があります。これが主な議論の場となりますので活用してください。
5. プルリクエストがあると、僕が変更内容を確認し、妥当と判断すればマージ（ファイルに取り込むこと）します。

**プルリクエストがマージされた後に、pandocでいったんTeXファイルに変換、必要な処置をしてからPDF化するので、マージ直後にPDFに修正が反映されるわけではありません**。

### Markdownプレビューモードでの注番号について ###

**Githubでのプレビューモードでは、注が正しく表示されません**。原稿ファイルを「編集モード」で見るか、ファイルをダウンロードしてMarkdown対応エディタのプレビューを使うか、pandocで適宜変換してください。


### ブラウザ上で編集する際の注意 ###

ブラウザ上で編集する場合、「コミット」が完了するまで変更した内容が保存されません。僕はよくやってしまうのですが、誤ってページのリロード、バックなどしてしまうと、それまでの編集内容が全て失なわれてしまいます。

そのため、多少煩雑になっても、1ファイルまとめて全部徹底的に、ではなく、数回に分けて編集、コミットするほうが安全です。

あるいは、エディタにコピペして作業し、それを戻していただいても結構ですが、その場合は、**余計な空白行などが入らない**ようご注意ください。Diffによる変更点の比較がうまくいかなくなりますので。

もっとも、エディタで作業できるのであれば、Githubアプリをお使いいただくほうが便利だと思います。

### 見出しの階層 ###

    # 章(ソース、ガルニチュール etc）= chapter
    ## 節（基本ソース、茶色い派生ソース etc.）= section
    \frsec{section en fr} 節のフランス語表記。注をここにはつけない。上の\#\# の節につける。
    ### 小節 = subsection
    \frsecb{subsection-b en fr} 小節のフランス語表記(節よりやや小さい文字サイズを使用)。注も上の日本語部分につけること。
    #### レシピ名
    \frsub{recette en fr} レシピ名のフランス語表記。これも注は不可。
    ##### 予備
    ###### 原注ほか

※ フランス語見出し、たとえば ``\frsub{Nom de recette}`` にどうしても注をつける場合はLaTeXの注の方式なら大丈夫です。``\frasub{Nom\protect\footnote{Voici une note} de recette}`` のようになります。原稿の可読性が大きく下がるので、出来るだけ日本語部分にMarkdown書式で注をつけるようにしましょう。

  
## スポンサーのお願い

原書の本文900ページを翻訳し、同等かそれ以上の注釈を付けていく作業は、ボランティアだけでは不可能です。他の多くのプロジェクト同様にスポンサードを切にお願いする次第です。原稿完成後の先行きが不透明な現在、クラウドファンディングによくある「見返り」をお約束することは出来ませんが、1口以上で原稿に「後援者の皆様」としてお名前を表示させていただくことと、その後のPDFあるいは印刷物になる際にもその表示をさせていただくことだけはお約束いたします。下記リンクからお願いいたします。

[https://lespoucesverts.org/archives/7042](https://lespoucesverts.org/archives/7042)
  
  
  
©Manabu GOTO 2018 All Rigths Reserved
