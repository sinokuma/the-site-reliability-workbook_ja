# SREはどのようにDevOpsと関連しているか

SREクラスがDevOpsインタフェースを実装している

By Niall Richard Murphy, Liz Fong-Jones, and Betsy Beyer, with Todd Underwood, Laura Nolan, and Dave Rensin

原則としての運用は難しいものです。[1]
システムをどのようにうまく運用するかという一般的に解決されていない問題があるだけでなく、うまくいくと判明したベストプラクティスもコンテキスト依存性が高く、幅広く採用するには程遠いものです。
また、どのように運用チームをうまく運営するかという、ほぼ言及されていない問題があります。
これらの話題の詳細な分析は、第二次世界大戦中の連合軍のプロセスと成果の向上に専念した[運用研究](https://www.informs.org/Resource-Center/INFORMS-Student-Union/Career-FAQs)に由来すると一般的に考えられていますが、現実には[何千年もの間、物事をより良く運用する](http://www.operationsmanager.com/what-is-operations-management/provence-france/)方法を考えてきました。

Yet, despite all this effort and thought, reliable production operations remains elusive — particularly in the domains of information technology and software operability.
The enterprise world, for example, often treats operations as a cost center[2], which makes meaningful improvements in outcomes difficult if not impossible.
The tremendous short-sightedness of this approach is not yet widely understood, but dissatisfaction with it has given rise to a revolution in how to organize what we do in IT.
しかし、このような努力や思想にもかかわらず、信頼性のある本番運用は、特に[情報技術](https://www.independent.ie/business/irish/rbsulster-bank-fined-56m-for-2012-it-system-crash-30759473.html)と[ソフトウェア運用](https://threatpost.com/fda-software-failures-responsible-24-all-medical-device-recalls-062012/76720/)の分野では定義が難しいままです。
たとえば、エンタープライズの世界では、運用をコストセンターとして処理することが多く、[2]結果として意義のある改善活動が不可能ではないにしても困難になります。
このアプローチの大きな短所はまだ広く理解されていませんが、それに不満を抱いて我々がITで行っていることをどのように体系化するかの革命が起こりました。

----------
[1]この議論はSREについての書籍に掲載されているように、この議論の一部はIT運用とは対照的にソフトウェアサービス運用特有のものであることに注意してください。

[2]Mary Poppendieckがこのことについて書いた「[コストセンタートラップ](http://www.leanessays.com/2017/11/the-cost-center-trap.html)」という優れた記事があります。
このアプローチが失敗する別の方法は、非常に大きくて起こりそうもない災害が、軽度の運用モデル(2017年5月のブリティッシュ・エアウェイズ停電など）に移行したことによるコスト削減を完全に帳消しにする場合です。
