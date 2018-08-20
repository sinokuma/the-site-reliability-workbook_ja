# サイトリライアビリティワークブック - SRE実装のための実践方法

## 序文1

Mark Burgess

O'Reillyの最初のSRE本を紹介したので、続編に招待されて光栄です。
この本において執筆チームは最初の本の歴史をそのまま残しているだけでなく、直接的な経験や事例研究、形式張らないガイダンスを提供することで幅広い読者にアプローチしています。
おそらく再分類と優先順序の見直しが行われ、広い範囲に渡るテーマは現代的なビジネス意識を持っている方やIT関係者の皆によく知られています。
技術的な説明は置いておいて、ここにはユーザが直面するサービスがあり、そのサービスには決まりごとや目標があります。
ヒューマンコンピュータシステムは、無防備で新品状態のインフラストラクチャに激突する見知らぬ隕石からではなく、その目的に固有な加速するビジネスの中から発生していると考えられます。
すべてのヒューマンコンピュータ部品の連携が焦点です。実際のところ、この本は次のように要約することはできるでしょう。

* サービス目標、期待値、レベルを設定した約束を果たすことを誓うこと。
* メトリクスと予算の限度によって、これらの約束を継続的に評価すること。
* 約束を守る、もう一度守るために迅速に対応すること、オンコール対応をすること、新たなゲートキーパーを生みださないために自律性を守り抜くこと。

すべての利害関係者にとって確実に約束を守ることは、依存関係や目的、関与する人々の生活の安定性に左右されます(Thinking in Promises参照)。
注目すべきは、ヒューマンコンピュータシステムの人間の側面は、認識される規模の脅威と一緒でないと成長しないということです。
自動化は人間を排除するものではないことが判明しました。
むしろ、私たちは個々のアイデアの発生からグローバルなユーザ基盤のための大規模なデプロイに至るまで、あらゆる規模で人間の必要性を再確認することに私たちに挑戦しています。

これらの教訓を伝えるというのは、それ自体がサービスの課題であり、あらゆるサービスと同様に苦労して得た知識は反復的なプロセスです。
これらの教訓は質問したり、試行したり、失敗したり、リハーサルしたり、そして完成させることによって会得します。
この本には、熟考したり適合したりするための豊富な資料がありますので、見てみてください。

## 序文2

Andrew Clay Shafer

作者たちが2番目のSRE本を手がけていることがわかったとき、私は連絡を取って少しばかりメッセージを書くことができるかどうか尋ねました。
最初のSRE本の原則は私が日頃からDevOpsであると想像していたものとよく似ていて、Googleの外部では100％適用されない場合でも、実践することで物事の本質を見抜くことができます。
最初のSRE本の[リスクの受容(第3章)](https://landing.google.com/sre/book/chapters/embracing-risk.html)、[サービスレベル目標(第4章)](https://landing.google.com/sre/book/chapters/service-level-objectives.html)および[トイルの撲滅(第5章)](https://landing.google.com/sre/book/chapters/eliminating-toil.html)にかかれてある原則を読んだ後、私は屋上からそのメッセージを叫びたくなりました。
従来型の組織が変革を促進させる手助けをするために何度も同じような言葉を使っていたので、「リスクの受容」には大変共感しました。
創造的でより高次元な作業のためにより多くの時間を人間に与え、人間をもっと人間らしくするために、第6章は常に絶対的なDevOpsの目標となりました。
それだけでなく、私は「サービスレベル目標」に惚れ込みました。言語とプロセスが運用上の考慮事項と新しい機能の提供との間に公平な契約を結んでいることが大好きです。
SRE、SWE（ソフトウェアエンジニア）、ビジネスはすべて、サービスが価値あるものでなければならないことに同意しています。SREソリューションは、行動と優先事項を推進する目標を定量化します。
サービスレベルを目標にし、目標を下回っている場合は機能よりも信頼性を優先するこのソリューションは、運用と開発者の従来の競合を排除します。
これはシンプルでエレガントな再構成で、問題を抱えることなく解決します。
私はこれらの3つの章を、私が過去に会ったほとんどの人に宿題として与えています。
それくらい素晴らしいものです。誰もが知っているべきです。 すべての友達に伝えてあげてください。私は全員に伝えました。

過去10年間の私のキャリアでは、より良いツールとプロセスで人々がソフトウェアを提供できるよう支援することに重点を置いてきました。
時々、私がDevOpsの発明に貢献したと言われることがありますが、私はさまざまな組織やプロジェクトの中から成功したパターンを借りて盗んだだけです。
「DevOps」が色んな人の中でも特に私によって発明されたものだと言われると恥ずかしい気持ちになります。
自分自身を何らかの分野における専門家だとは考えていません。ただし、好奇心は強いです。
私の理想的なDevOpsは、いつも私が友人から引き出したり推測したりできる情報をパターン化したものです。私の友人は偶然インターネットを構築していました。
私は、世界で最もとてつもないインフラストラクチャとアプリケーションの代表となるお手本をデプロイ、運用する人々に内密に接触できる特権を持っていました。
DevOpsは、インターネット上で高可用性のソフトウェアを迅速に提供するために必要な緊急および現実的な最適化の側面を象徴しています。
物理媒体で提供されるソフトウェアからサービスとして提供されるソフトウェアへの転換は、ツールとプロセスの進化を余儀なくさせました。
この進化によって、運用のバリューチェーンに対する貢献は高まりました。
システムが停止している場合、ソフトウェアに価値はありません。
良い知らせとしては、ソフトウェアを変更するために次のパッケージが出荷されるのを待つ必要はないということです。
ただし、ある種の人たちにとっては、これは悪い知らせでもあります。
私は、単に受け入れようとしている読者に対して、新しい方法の最も成功したパターンをはっきりと述べる機会と視点を持っていただけです。

2008年、私たちが今のようにDevOpsという言葉を使用する前だったのですが、ドットコム・バブルの崩壊や大学院を経て、複数のベンチャーキャピタルの浮き沈みの激しい中を開発者として、日々Googleで答えを検索しながら過ごしていました。
私はPuppetにてフルタイムで働いており、自動化にはIT組織を変革する可能性を感じ、魅了されたのです。
Puppetは私に運用領域の問題を解決するよう背中を押しました。
現時点では、GoogleはPuppetサーバの将来性を押し進める規模で、Puppetを使用して企業のLinuxおよびOSXワークステーションを管理していました。
私たちはGoogleと素晴らしい仕事の関係を築いてきましたが、Googleはポリシーの問題として社内業務の秘密を秘密にしていました。
私は元々好奇心が強く、より多くの情報を絶えず求めていたので、このことを知っています。
私はいつもGoogleには素晴らしい内部ツールやプロセスを持っているに違いないと思っていましたが、これらのツールとプロセスの実体が常にはっきりとしませんでした。
結局、私はBorgについて深掘りすることを受け入れたのですが、これは現在の会話があまり進んでいない可能性があることを意味していました。
私がGoogleが色々なことをどのように実行しているかもっと知りたがっていたとしても、当時は許されていませんでした。
2008年の重要性には、最初のO'Reilly Velocityカンファレンス開催と、Patrick Deboisと出会った年であることが含まれています。
"DevOps"はまだ形成されていませんでしたが、出来上がる寸前の状態でした。
その時が訪れ、世界の準備が整いました。 DevOpsは新しい方法、より良い方法のシンボルとなりました。
当時SREが公開されてい他ならば、形成されたコミュニティは「トイルの撲滅」という題字を立て、DevOpsという用語は決して存在することはなかっただろうと考えています。
事実とは反するにも関わらず、個人的には最初のSRE本が私の理解をさらに進めてくれました。既にSRE原則だけで多くの人を支援しました。

DevOps初期段階ではあらゆることが急速に進化しており、DevOpsの可能性に制限をかけたくなかったため、プラクティスの体系化を意識的に避けていました。
さらに、DevOpsを「所有する」ことを私は望んでいませんでした。
2010年にDevOpsについて執筆した時、3つのポイントをまとめました。
第一に、開発者と運用者は一緒に働くことができるし、一緒に働くべきだということです。
第二に、システム管理はますますソフトウェア開発のようになるであろうということです。
最後に、プラクティスをグローバルコミュニティで共有することによって、私たちの集団としての能力を加速し倍増させ流ということです。
同じ時期に、私の友人のDamon EdwardとJohn Willisは、文化(Culture)、自動化(Automation)、メトリクス(Metrics)、共有(Sharing)の頭文字をとってCAMSを作りました。
Jez Humbleは後にリーン(Lean)開発による継続的改善を加えることによって、この略語をCALMSに拡大しました。
これらの言葉が示す事柄は1冊の完全な本に値するものですが、SREがGoogleの継続的改善に関する逸話と共に、文化、自動化、メトリクス、共有についてはっきりと言及しているため、ここでも触れておきます。
最初のSRE本を出版することで、Googleはその原則とプラクティスをグローバルコミュニティに共有しました。
今では、DevOpsを単に「人間のパフォーマンスとソフトウェア運用経験をソフトウェアおよび人間によって最適化すること」であると定義します。
私は誰に対しても口を挟みたくはないのですが、SREを説明するには非常に良い手段であると思っています。

結局のところ、GoogleでDevOpsとSREを経験した際、私はDevOpsを理論と実践において最も先進的な実装の1つとして理解しています。
優れたIT運用は常に優れたエンジニアリングに依存しており、ソフトウェアによる運用上の問題を解決することは常にDevOpsの中心でした。
SREではエンジニアリング側面がより明確になります。
誰かが「SRE対DevOps」と言うのが聞こえると、私はうんざりします。
私からすれば、ソフトウェアによって現代のインフラストラクチャを提供する社会技術システムを表すラベルとして、時間的にも空間的にも切り離すことはできません。
DevOpsは緩やかで一般的な原則の集合であり、SREは高度で明示的な実装であると考えています。
アジャイルとExtreme Programming(XP)との間に同じような類似点があります。
確かに、XPはアジャイルであり、おそらくアジャイルの中でも最高ですが、すべての組織がXPを採用することはできません。
