# 本文書の目的
Stuart Schechter氏が執筆した["Common Pitfalls in Writing about Security and Privacy Human Subjects Experiments, and How to Avoid Them"]( https://www.microsoft.com/en-us/research/publication/common-pitfalls-in-writing-about-security-and-privacy-human-subjects-experiments-and-how-to-avoid-them/) の和訳

## 許諾
ご本人より和訳の許可をいただいています。（2019年3月27日）

___

# 人間を対象にしたセキュリティとプライバシー実験について執筆するときにありがちな落とし穴と、その回避方法
<!-- 
Common Pitfalls in Writing about Security and Privacy Human Subjects Experiments, and How to Avoid Them
-->

Stuart Schechter

Microsoft Research (^1 訳者注：所属は執筆時のものであり、現在の所属ではありません)

## 概要
<!-- Reviewers of papers that describe human subjects experiments of security and privacy often observe that authors are prone to a set of common mistakes that, if they were aware of, could be easily avoided. In this document I provide advice to help researchers avoid these mistakes in designing, performing, and documenting their experiments.  -->
人間を対象にしたセキュリティやプライバシーに関する実験論文の査読者は、著者がよく犯しがちな間違いの傾向に気づくことがある。これらは気をつけていれば簡単に避けることが出来る。
この文書は、研究者が実験を設計、実施、論文化する際の過ちを回避するアドバイスとして記したものである。

## 本文の要約
<!-- Executive Summary -->

<!-- State the hypothesis or hypotheses you are testing precisely. -->
1. あなたがテスト（検定）しようとしている仮説を正確に示すこと。
<!-- If testing a security hypothesis, have a clear and defensible threat model. -->
2. セキュリティの仮説を検定する場合、明確かつ正当化が可能な脅威モデルを持つこと。
<!-- Avoid misleading yourself or your reader in any way, especially in selling your contribution or in translating results into conclusions. -->
3. 自身や読者の判断を誤らせることを避けること。特に論文の貢献の売り込みや、結果から結論を得るときの解釈の時に。
<!--  Carefully explain how participants’ behaviors were observed, scored, and then fed into statistical tests. -->
4. 実験参加者の行動がいかに観察され、スコア化され、そして統計的検定に適用されたかについて注意深く説明すること。
<!-- Explain any ethical considerations of your experiment and disclose whether your study was approved by the ethics review board at your institution(s). -->
5. 実験への倫理的な考察を説明すること。そしてその研究は所属組織の倫理審査委員会の承認を得ているかどうか開示すること。
<!-- Disclose all limitations in your study design and results that you are aware of. -->
6. 研究の設計や結果について認識している限定条件はすべて開示すること。
<!-- Label all axes in graphs and add captions to ensure figures are self explanatory. -->
7. 図表が分かりやすいように、グラフ内のすべての軸にラベルを付け説明文（キャプション）を加えること。
<!-- Do not assume that correlation implies causation -->
8. 相関関係が因果関係を暗示すると思いこまないこと。
<!-- Do not conclude that a hypothesis is false because a statistical test failed to disprove the null hypothesis. -->
9. 検定の結果、帰無仮説の棄却に失敗からといってその仮説が間違っていると結論付けないこと。
<!-- Use a statistical test only when the requirements under which it is valid, such as data fitting a normal distribution or trials being independent, are met. (When in doubt, use a non-parametric test.) -->
10. データが正規分布になることや試行が独立であることなど、要件が合致したときのみ統計的検定を使うこと (もし疑わしい場合はノンパラメトリック検定を使うこと)。
<!-- Don’t be afraid to ask for help. Ask colleagues who were not involved in the research to read an early draft of your paper. -->
11. 助けを求めることを恐れないこと。この研究に参加していない同僚に論文の草稿を読ませること。

## 1. はじめに
<!-- Program committees must often reject papers with fascinating ideas or clever experimental methodologies - which we would love to see presented - because the validity of the experimental results is in question: program committee members cannot ascertain key experimental details from the paper, how data were collected, or whether a statistical test is indeed sufficient to support a hypothesis.  -->
<!-- Many of the mistakes that force program committees to reject papers are common and easily avoided. -->
プログラム委員会は、魅力的なアイデアや巧みな実験方法を持つ論文を実験結果の妥当性が疑問視されているために不採録にしなければならないことが多い（我々はそれが発表されるのを見たいのだが）。これは、データの収集方法、統計的検定が仮説を支持するのに十分であるかどうか、という重要な実験の詳細情報をプログラム委員が論文から確かめることができないからである。
論文の不採録判定をプログラム委員会に余儀なくさせる間違いの多くは、ありがちな事柄であって簡単に避けることが出来る。

<!-- I have written this document to guide researchers in how to avoid the most common pitfalls when submitting to the Symposium on Usable Privacy and Security (SOUPS) and other venues that accept human subjects studies about security and privacy. -->
<!-- I provide a mixture of generally accepted practices for writing computer science papers, practices specific to human subjects studies in security, and less universally accepted advice based on my opinion and past experiences as an author and reviewer. -->
<!-- This work is not intended to be a complete guide to writing a paper. -->
<!-- Rather, it is intended to help those with a general knowledge of how to write an academic paper to adapt their skills to writing up security and privacy human subjects studies and to help all authors avoid common pitfalls.  -->
本稿は、the Symposium on Usable Privacy and Security (SOUPS) や、人間を対象としたセキュリティとプライバシーに関する研究を受け入れるその他の場に投稿する際の、最も一般的な落とし穴を避ける方法について研究者をガイドするために書いた文書である。
私は、コンピュータサイエンスの論文を書くための一般的に受け入れられているプラクティスや、セキュリティに関する人間を対象とした研究に特有のプラクティス、そして（一般的には受け入れられていないが）著者や査読者としての私の意見と過去の経験に基づいたアドバイスを組み合わせて提供する。
本稿は、論文を執筆するための完全なガイドであることを意図していない。
むしろ、学術論文の執筆に一般的な知識を持つ著者がそのスキルをセキュリティやプライバシーに関する人間を対象とした研究の論文執筆に適合させることを助け、すべての著者がありがちな落し穴に落ちないように助けることを意図している。

## 2. あなたの貢献
 <!-- It is important to define your contribution by explaining the general problem you are trying to solve and the specific instance of the problem that is the basis for your work, the hypotheses you wanted to test, unique features of your approach, and your results.  -->
あなたが解決しようとしている一般的な問題と、研究の基礎となっているその問題の具体的な事例、検証したい仮説、アプローチの独自の特徴、そして結果を説明して貢献度を定義することが重要である。

<!-- As you lay out your paper, and especially your contribution, you must be meticulously careful to avoid misleading yourself or your reader in any way. 
Prior work should not be unduly disparaged, your innovations should not be exaggerated, and no limitation of your work should be swept under the rug. 
Graduate students are taught that they need to sell their work and its contribution to the field - and this is an important skill - but good marketing should be about isolating the value of your contribution and presenting it clearly.  -->
あなたが論文をレイアウトするとき、特に貢献の部分をレイアウトするときには、どのようにしてもあなた自身や読者が判断を誤らせないよう細心の注意を払わなければならない。
既存研究を過度にけなしたり、自身のイノベーションを誇張したり、研究内容の限定条件を隠したりすべきではない。
大学院生は、自分たちの研究と分野へのその貢献を売り込む必要があると教えられている。それは重要なスキルではある。しかし、よいマーケティングとは貢献の価値を分離してそれを明確に提示することにあるべきである。

<!-- Exaggerations, undocumented limitations, or other issues that lead reviewers to suspect they are being mislead will cause them to start reading your paper more suspiciously. 
This takes their focus away from appreciating the contribution of your work.  -->
誇張や記載されていない制限、判断を誤らせられていると査読者に疑わせるような事項があると、査読者は論文を疑い深く読み始めてしまうことになる。
こういったことは、研究の貢献を評価することから査読者の焦点を外してしまう。

<!-- Alas, even if you are honest in how you convey your research, it is exceedingly hard to determine if you have conveyed the information necessary for someone other than yourself to understand it. 
The best way to determine if your research will be comprehensible is to ask colleagues who were not involved in the research to read an early draft of your paper. 
If you are not a native-level speaker of the language in which the work is written, find a native-level speaker to point out and help remove any problems with language, spelling, or idioms.  -->
悲しいかな、もし自身の研究を伝えることに誠実であったとしても、自分以外の人たちに研究の理解に必要な情報が伝わったかどうかを判断することは非常に難しい。
自身の研究が理解できるかを判断する最良の方法は、その研究に従事していない同僚に論文の草稿を読んでもらうように依頼することだ。
もしあなたが論文執筆の言語をネイティブレベルに話せない場合は、言語・スペル・熟語におけるすべての問題点を指摘し取り除く助けをしてくれるネイティブレベルに話すことができる人を見つけること。

## 3. 実験のデザイン
<!-- Experiments are designed to test hypotheses. 
It is important that you state the hypothesis or hypotheses you are testing precisely.  -->
実験は仮説を検証するために設計される。
検証される仮説を正確に記述することが重要である。

<!-- Your experimental design should be documented in sufficient detail to allow another researcher to replicate your experiment without consulting you for missing details. 
While many papers fail to reach this standard and still are accepted into top publications, you will be well served by working to ensure that your experiment is documented well enough to allow it to be replicated. -->
実験の設計は、他の研究者があなたに詳細を聞くことなく実験を再現できるように十分に詳細記述がされるべきである。
多くの論文がこの基準に達成していないが、いまだトップレベルの国際会議や論文誌に採録されている。
しかし、実験が再現できる十分な記述を確実に行うようにすれば、それはいずれ自分自身を助けるものになるだろう。

### 3.1 何を含めるか
<!-- One way to collect the details you'll need to present about your experiment is to imagine the chronological progression of your experiment from the perspective of your participants (noting the variations between treatment groups), your perspective as a researcher, and the perspective of anyone else involved in the conduct of the experiment (including recruiters).  -->
<!-- Often, the description of the experiment in your paper will also follow a chronological time line.  -->
<!-- Questions that you'll want to answer in your description of the experiment should include:  -->
実験の記載に必要な詳細記述を集めるための1つの方法は、複数の視点で実験の時系列を想像することである。実験参加者の視点（そのときに実験グループの差異に言及すること）、研究者としての自身の視点、そして実験実施に関係した他者（実験参加者のリクルーティングを行った人を含む）の視点がある。
多くの場合、論文での実験の記述は時系列に沿っている。
実験の記述においては、以下の質問への回答が含まれるべきである。

<!-- 
- What infrastructure did you use or build to facilitate your experiment? 
- How were participants recruited? 
- What incentive was provided to participate? 
- Where did the participants go to participate? 
- What were participants asked to do before, as part of, and following the experiment? 
- What information did participants learn along the way and how might this have inuenced behaviors later on in the experiment? 
- If the study was a between-subjects study, how did the experience (treatment) vary between the groups?
- Did the order of any tasks change for different participants? 
- If deception was used, explain how the deception was perpetuated at each interaction with participants and at what point the deception was revealed.  -->
- 実験促進のためにどのインフラを利用/構築したか
- 実験参加者はどのようにして勧誘されたか
- 実験参加者にどういった報酬（インセンティブ）が提供されたか
- 実験参加者は実験のためにどこに行ったか
- 実験参加者が、実験前、実験中、実験後になにをするように求められたか
- 実験参加者は実験途中でどういう情報を学習し、その後の行動にそれがどのように影響したか
- 実験参加者間で行う実験の場合、グループ間でどういった経験（処置）の差が付けられたか
- 実験参加者によってタスク群の実施順序が変わったか
- もし欺瞞を用いた場合、参加者とのやりとりごとに欺瞞がどう続けされたか、そしてどの時点でその欺瞞が開示されたかを説明すること

<!-- To enumerate more details, examine the study from your perspective as the researcher. -->
より詳細な記述を列挙するために、研究者としての視点でその実験を調査すること。

<!-- Detail the recruiting process and the resulting demographic makeup of the participant pool. 
If the participant pool does not precisely reflect the population of interest you'll want to discuss the differences.  -->
実験参加者群の勧誘プロセスと、その結果の人口統計の構成を詳細に説明すること。
実験参加者群が関心のある母集団を正確に反映していない場合、その違いを議論する必要がある。

<!-- Describe how participants were observed and how observations translated into data points used for later analysis. 
A surprising number of submissions fail to explain how behaviors are observed, scored, and then fed into statistical tests. 
A statistical test is of little value if the reviewer doesn't know how observations were collected, how these observations were translated into numeric scores, or how these numeric scores were processed before a statistical test was applied.  -->
実験参加者はどのように観察され、その後の分析のためにどのように観察結果がデータに変換されたかを記述すること。
驚くほど多くの投稿が、行動がいかに観察され、スコア化され、そして統計的検定に利用されたかの説明ができていない。
観察結果がどのように収集され、観察結果が数値スコアにどのように変換され、数値スコアが統計的検定の適用前にどのように処理されたか、ということを査読者が知らない場合には、統計的検定はほとんど価値を持たない。


<!-- Along the way, you should highlight the decision points you came across in designing the experiment and explain the reasoning behind the choices you made. 
Own up to mistakes, especially if you have suggestions for how the methodology might have been improved. 
I've never run a study and not wished I'd designed their experiment at least slightly differently when the time came to write up the results.  -->
実験を設計するときに浮かんだ決定点を強調すべきである。そして行った選択の根拠を説明すべきである。
特に方法論がどのように改善されたかの提案がある場合には、間違いを白状すること。
私は、結果を書くときになって彼らの実験を少しでも違うように設計すればよかったと望んだり実験を行ったことはない。

### 3.2 倫理と実験参加者の安全
<!-- Many institutions (including all U.S. universities) require human subjects experiments to be approved by an Institutional Review Board (IRB).
Explain whether you or any of your collaborators work at an institution with an institutional ethics review board (IRB).
Explain the process through which your experiment was approved.
Regardless of whether your experiment was reviewed by an IRB, you will want to describe any potential ethical or safety risks and how you addressed them. -->
米国の大学を含む多くの組織は、人間を対象にした実験に対してIRB（組織内審査委員会）の承認を要求する。
あなたや共同研究者が組織内倫理審査委員会（IRB）を持つ組織で働いているかどうかを説明すること。
実験が承認された過程を説明すること。
実験がIRBにより審査されたかに関わらず、潜在的な倫理上または安全性のリスクとそれらへの対処にういて記述する必要がある。

<!-- If participants were deceived at any time during the study, you'll want to explain the nature of the deception, how deception impacted each step of the process from recruiting all the way to behavior measurements, and when the deception was revealed to participants.
Indicate whether participants were given the option to withdraw their consent to participate in the study after the true purpose of the study had been revealed (which is highly recommended).
If participants were never informed of the deception, you will need to disclose this as well.
(Failing to reveal the use of deception is quite controversial. See, for example, this paper.)  -->
実験中に実験参加者に欺瞞を行った場合、その欺瞞の性質と、勧誘から行動観察までの各段階における欺瞞の影響、そしていつその欺瞞が実験参加者に明らかにされたかを説明する必要がある。
真の実験目的が明らかにされた後、実験参加者の同意を撤回するオプションが与えられたかどうかを示すこと（これは強く推奨する）。
もし実験参加者が欺瞞を知らされなかった場合、その事も開示する必要がある。
（欺瞞の仕様を明らかにしないことは、かなりの論争の的になる。[参考例](https://www.tandfonline.com/doi/full/10.1080/10508422.2012.732505)）

<!-- Indicate what steps you took to detect if participants might be harmed by your experiment (if any). -->
実験により実験参加者が被害を受ける可能性があるならば、それを検出するために行った手順を示すこと。

<!-- If you have are planning to run a deception study and would like to use a pre-packaged infrastructure that is carefully designed to detect participants' perceptions of harm, and allow participants who feel harmed to withdraw their consent to participate, please consider contacting The Ethical Research Project the use their survey (disclosure: I am part of that project.)  -->
もし欺瞞を行う実験を計画していて、実験参加者の被害認知の検出と被害を感じた実験参加者に参加同意の撤回の許可をするために丁寧に設計されたパッケージ済みのインフラを用いたい場合、the Ethical Research Projectにコンタクトを取りそのサーベイを利用することを検討されたい（告知：私（Stuart Schechter）はそのプロジェクトの一員である）。
*（訳者注：元の文献にはThe Ethical Research ProjectへのメールアドレスとサーベイへのURLが記載されていたが、サーベイ先のURLは2019年5月の段階で存在していないため、ここでは記載をしていない）*


### 3.3 補足資料
<!-- No matter how hard you try, you may not be able to fit every detail of your experiment { such as the precise wording of every question posed to participants { in the body of the paper.
To assist readers who may have questions that you could not be expected to anticipate or that fall outside the stated contribution of your work, consider attaching your study materials into an appendix at the end of your paper.
Appendices are not a substitute for carefully detailing your methodology in the paper, as reviewers are neither required nor expected to read them.
You must still ensure that you have explained all of the details essential the the validity of your experimental goals, methodology, and conclusions. -->
どのように工夫しても実験の全詳細（たとえば実験参加者へのすべての質問の正確な表現など）を論文の本文に収めることはできないかもしれない。
あなたが予想できなかった質問や研究の貢献範囲外の質問を持つかもしれない読者のために、論文の最後に付録として研究資料の添付を検討すること。
査読者はその付録を読む必要や期待を受けていないため、付録は論文における手法の詳細記述を丁寧に行う代わりにはならない。
付録を付けようとも、あなたが実験目標や方法論そして結論の妥当性に不可欠な詳細のすべてを説明する必要は依然存在する。

## 4. 特別に考慮する事項：模擬攻撃を含む実験
<!-- Experiments involving behavior in response to privacy and security threats warrant extra consideration in areas that may be less important when writing up other HCI experiments -->
プライバシーとセキュリティの脅威に対応する行動を伴う実験では、他のHCI（訳者注：Human Computer Interaction）実験について執筆するときにはそれほど重要ではないことに対しても考慮が必要になる。

### 4.1 明確な脅威モデルを持つこと
<!-- If testing security behavior in response to an attack, clearly explain the assumptions made about the information, capabilities, and resources available to an attacker.
These assumptions are your threat model.
A common failing in papers is to fail to document or justify the assumptions that make up your threat model.
Document how any attack you may simulate is similar to, and different from, a real attack. -->
攻撃に対応するセキュリティの行動をテストする場合、攻撃者が利用可能な情報と能力そしてリソースについての仮定を明確に説明すること。
これらの仮定は、脅威モデルである。
脅威モデルを構成する仮定の記述と正当化を行わないことは、論文でよくある失敗となっている。
シミュレートした攻撃がどれほど実際の攻撃に類似していてどれだけ異なるかを記述すること。


### 4.2 自身のシステムに有利となる偏り（バイアス）を避けること
<!-- If you are testing a system of your own design, beware of the potential or appearance of bias when designing a threat model and experimental design.
An attacker will have more incentive to break your system than you do.
Reviewers may look at an attack you tested against and believe, rightly or wrongly, that they could have designed more effective attacks.
One way to remove bias is to identify third parties with both the talent and incentive to develop the best possible attack against the system you have built.
We've even considered holding contests to identify the most effective attack against which to test our systems. -->
独自設計のシステムをテストする場合、脅威モデルと実験の設計における偏りの潜在ないし出現に注意すること。
攻撃者はあなたが行うよりもシステムを破るインセンティブが大きい。
査読者はあなたがテストした攻撃を見て、より効果的な攻撃が設計できると信じるだろう（正しいか間違っているにかかわらず）。
偏りを取り除く1つの方法は、提案システムに可能な限り最高の攻撃を構築する能力とインセンティブの両方を持つ第3者を特定することである。
我々は、提案システムへの最も効果的な攻撃を特定するためにコンテストを開催することを検討したことがある。


### 4.3 生態学的妥当性を取り扱うこと
<!-- There are many potential reasons why participants in a research study may not behave as they would in the real-life situation that your experiment is designed to emulate. -->
実生活と同じように機能させるように設計された実験において実験参加者が実生活と同じように行動しないことということには、いくつかの潜在的な理由が存在する。

<!-- Ecological validity is especially challenging when designing experiments of security and privacy behavior because, for most of the interesting scenarios to study, security or privacy will not be the primary goal of the individual.
Furthermore, not completing the primary task may also have risks and consequences.
Simulating the forces motivating a user's drive to complete a primary task and response to potential risks is challenging, and so extra attention to ecological validity is warranted as you design and document your experiment. -->
セキュリティとプライバシーの行動実験を設計する時には生態学的妥当性が特に困難である。
なぜなら、研究において興味深いシナリオのほとんどにおいてセキュリティとプライバシーは個人の主目的ではないためである。
加えて、主要タスクを完了しないことはリスクと重大性をもたらす。
利用者に主要タスクを完了させ潜在的リスクに対応させるような動機をシミュレートすることは困難であり、実験の設計と記述をする際には特別な注意が必要である。

<!-- Questions you'll want to address include whether participants knew the study was about security or that the researchers study security.
If they did, would this have led them to pay more attention to security? Did participants believe that they would be negatively impacted if they exhibited an insecure behavior in the same way that they would in real life? Did participants believe they had something to lose if they failed to complete a task because they could not do so securely or did not know how to do so securely? Have you considered the potential for users' behaviors to become habituated in a manner that could negatively impact security or usability?  -->
議論の対象となる疑問点には、実験参加者はこの実験がセキュリティに関するものであることを知っているか、あるいはこの研究者がセキュリティを研究していることを知っているか、が含まれる。
もし知っていた場合、実験参加者はセキュリティにより注意をするようになっただろうか？
実験参加者は実生活と同様に安全でない行動をすると悪影響を受けると考えただろうか？
実験参加者は、安全にタスクを完了させることに失敗したり、タスクをどう安全に終わらせるかを知らないときに何かを失うと考えただろうか？
あなたは、実験参加者の行動がセキュリティやユーザビリティに悪影響を及ぼす可能性のある方法に慣れてしまうことの可能性を検討しただろうか？



## 5. 限定条件の開示
<!-- Be up front and disclose all the limitations of your study design, participant demographics, statistical tests, and other methodological issues. -->
実験の設計や実験参加者の特性を表す統計、統計的検定、その他方法論的な問題といった点のすべての限定条件を事前に検討し開示すること。

<!-- One of the goals of peer review is to keep papers with misleading or fundamentally awed results from receiving additional credibility through publication, leading others to cite awed conclusions as fact.
Reviewers will be looking for undisclosed methodological limitations, overstated results, or other content that may mislead a reader.
Ensuring that readers can correctly identify the scientific implications of your study is your job first, and reviewers second, and so the better you can show that you've done it the better reviewers will feel about your work.
Reviewers will be less likely to critique your study design if they see that you are aware of the limitations of your work and have fully disclosed them.
By showing that you've already looked at your own experiment with a critical eye, you allow your reviewers to focus more on evaluating the implications of your findings and less on searching for flaws that they suspect may be hiding under the covers. -->
査読の目的の1つは、発表を通して追加的な信ぴょう性を受けたことにより判断を誤らせるあるいは根本的に畏れられる結果を含む論文を、維持することにある。
査読者は、方法の非開示限定条件や過大評価された結果、そして読者の判断を誤らせる他の内容を探している。
読者に研究の学術的意義を正確に認識させることが、第1にあなたが行うことである。それらを査読者に行うことは第2である。読者に対して正確に認識をさせたことが上手に示されれば、査読者はあなたの研究成果によい感情を抱くだろう。
あなたが自身の研究成果の限定条件に気づき、それらをすべて開示していることを査読者がわかれば、査読者は研究の設計に対して批判する可能性はより少なくなる。
自身の実験に対して批判的な視点でとらえていることを示すことによって、査読者は隠れていると疑って欠点探しをすることよりも、明らかになったことの意味の評価により焦点を当てることになる。

<!-- Your discussion of limitations may be placed into its own subsection of your methodology section, results, or discussion sections.
You may even want to promote limitations to an independent section of the paper. -->
限定条件の議論は、方法論を記載する章や結論の章、あるいは議論の章の中の小節として置かれるだろう。

## 6. 結果の提示
<!-- For each test, remind the reader of the hypothesis to be tested, present the data used to test the hypothesis, explain your choice of statistical test, and then present the result of that test. -->
それぞれの検定に対して、検定の対象となる仮説を読者に思い出させ、仮説を検定するために利用されたデータを示し、選択した統計的検定手法を説明し、そしてそれらの後に検定結果の提示をすること。

### 6.1 図表
<!-- Clearly label the rows and columns of tables and the axes of figures.
Make sure the title or caption precisely describes what the contents of the table or figure represent.
A surprising number of papers contains axes that are not labeled and graphs for which one cannot determine what data are being plotted. -->
表の行と列、図の軸に明確にラベル付けをすること。
タイトルまたはキャプションが図表が示す内容を正確に述べているか確認すること。
驚くほど多くの論文が、ラベルのない軸とプロットされたデータがどのデータなのかわからないようなグラフを含んでいる。




### 6.2 統計的な妥当性
<!-- There are two common statistical errors that we on the SOUPS committee see every year.
First, authors often describe a failure to disprove the null hypothesis as an indication that the null hypothesis is true.
In other words, we see authors interpret a statistical test score where p > 0:05 as evidence that the hypothesis being tested is false, when it's entirely possible that a larger sample might have yielded p < 0:05.
Rather, failure to disprove the null hypothesis simply means that there was not enough evidence, given the size of the sample and the random outcomes, to prove the null hypothesis to be false.
Failure to prove something is false does not mean it is true.
The only way one could ever prove that no difference existed between two populations would be to test, and obtain a perfect measurement, of every member of both populations, rendering statistical tests unnecessary.
Otherwise, the best you can do is to measure the statistical certainty that the difference between two populations is within a certain bound. -->
**SOUPS委員が毎年見る共通した統計上の誤りが2つある。**
**1つ目は、帰無仮説が棄却できないことをもって帰無仮説が正しいことを述べることである。**
より大きな標本を取れば統計的検定のスコアであるpにおいてp<0.05を得られる可能性が完全にある場合に、著者たちがｐ>0.05であることを仮説が誤りであることの証拠として解釈することが見られる。
むしろ、帰無仮説が棄却できないことは、その標本サイズとランダムな結果では帰無仮説が誤りであることを証明するための十分な証拠がなかったことを単に意味しているにすぎない。
何かが誤りであることの証明失敗は、その何かが正しいことを意味しない。
2つの母集団間に違いが存在しないことを証明する唯一の方法は、完全な測定手段を手に入れて双方の母集団の全要素にテストを行うことである。そのようにすれば統計的な検定は不要になる。
それができない場合、最善の方法は2つの母集団の差が一定の範囲内にあることの統計的な確実性を測定することである。


<!-- I've seen experts describe the results of two experiments as conflicting when one was able to show a statistical difference between the two groups and the other was not.
In some cases, both studies might find the exact same difference, but one study may have had the larger sample.
In other cases, luck caused one study to just pass a significance threshold (say p = 0:48) whereas another just failed to meet it (p =fi0:52).
In this case, the results would be nearly identical with the exception that an arbitrarily chosen threshold lies in the tiny space between them. -->
2つの実験結果において片方が2群間の統計的差異を示すことができている一方で他方が示すことに失敗しているケースにおいて、専門家がその結果が矛盾していると述べているのを見たことがある。
あるケースでは、片方はより大きな標本サイズを持っていたが、両方の研究がまったく同じ違いを見つけることができた。
他のケースでは、片方が運よく有意性の閾値を通過した（p=0.48）が他方が失敗した（p=0.52）。
しかし任意に選択された閾値が双方の研究間の小さな空間に設定されていることを除けば、ほぼ同一の結果である。

<!-- The second common mistake is to use more than one data point per participant in a statistical test that assumes data points are independent.
The very fact that two data points come from a single participant means they are not independent. -->
**2つ目は、データの独立性が仮定されている統計的検定において1人の実験参加者から複数のデータを取っていることである。**
1人に実験参加者から2つのデータを取得することが意味することは、それらは独立していないということである。


<!-- As the number of statistical tests used to test one or more hypotheses grows, so does the chance that one will reach your significance threshold due to random chance.
You may want to correct for multiple testing.
See, for example, the Wikipedia entry on Multiple Comparisons. -->
1つ以上の仮説を検定するために行われる統計的検定の回数が増えるに従い、偶然ある1つの仮説が有意水準に達する確率が高まる。
複数の検定を修正する方法がある。
例えば、Wikipediaの[Multiple Compasirons](https://en.wikipedia.org/wiki/Multiple_comparisons_problem)の項を参照すると良い。

<!-- An example of this mistake is to ask 10 participants 10 questions, and then feed the 100 responses into a statistical test.
The statistical test will produce a p value as it would if there were actually 1 question asked of 100 participants.
If it isn't already clear to you why this is a problem, imagine that one were to ask 50 questions about statistics of one man and one woman.
The statistical test has 50 samples for men and 50 samples for women.
Let's say the man has no knowledge of statistics, and gets all 50 questions wrong.
The woman gets them all right.
Misled to believe that it had 50 independent trials from both men and women, the statistical test would indicate that women are better at statistics than men with a p value far below 0.01 - a significant result! It is hopefully intuitively obvious that one cannot make such a strong conclusion about two populations by sampling only one member from each. -->
この誤りの例として、10人の実験参加者に10の質問を行い、得た100の回答で1つの統計的検定行うことがある。
統計的検定は、それが1つの質問に100人の実験参加者が答えたものとしてp値を算出する。
これがなぜ問題であるか確信ができない場合、さらに別の例を考えよう。
1人の男性と1人の女性に統計学に関する50の質問をしたとする。
統計的検定で、男性の情報として50の標本を、女性の情報として50の標本を得ることになる。
ここでもしその1人の男性が統計学の知識がなくすべての質問で誤答し、その1人の女性はすべての質問に正答したとする。
それぞれ50の独立した試行が男性と女性に行われたと誤解され、統計的検定の結果、p値が0.01をはるかに下回り、女性は男性よりも統計学に優れていることを示す。
重要な結果である！
それぞれが1人のメンバーしかいない2つの母集団からはそのような強い結論を導くことはできない、ということが直感的に明白であることが望ましい。

<!-- There are a number of ways to run statistical tests when you have multiple data points from the same participant.
One simple one is to take a summary statistic for each participant and run the statistical test on the summary statistic.
A student t-test is, after all, a test for comparing students' scores on exams that have many questions.
It is designed to be used for a summary statistic, their test score, over a large enough number of questions that the score fits a normal distribution. -->
同じ実験参加者から複数のデータを取得した場合の統計的な検定手法は多数ある。
簡単なものの1つに、各実験参加者の要約統計量を取り、要約統計量により統計的検定を行う手法がある。
学生T検定は多くの設問がある試験での生徒の点数を比較するための検定である。
これは、学生の点数が正規分布になる十分な量の設問があるときに要約統計量に学生の点数を採用するように設計された検定である。

<!-- Speaking of t-tests, and other statistical tests that rely on scores to be drawn from a normal distribution, you will want to show that your scores indeed appear to resemble a normal distribution if you are using these tests.
At the very least, explain why you believe the scores should fall into a normal distribution.
Better yet, use a non-parametric test when there is any doubt that the distribution is normal.
If you have any question about the right test to use or how to use it, don't be afraid to ask for help.
If you don't have a knowledgeable colleague handy, a number of helpful online guides can be found by searching on the phrase \choosing the right statistical test". -->
T検定やそのほかの正規分布から得られるスコアに依存した統計的検定手法について言えば、そういった検定を使用する場合にはそのスコアが実際に正規分布に似ていることを示す必要がある。
少なくとも、スコアが正規分布になると考えられる理由を説明すること。
分布が正規であることに疑いがあるならば、ノンパラメトリック検定を使用すると良い。
適切な検定やその利用方法に疑問がある場合は、遠慮せずに助けを求めること。
知識のある同僚が身近にいない場合、”choosing the right statistical test（適切な統計的検定手法を選択する）"というフレーズで検索をすれば、多くの役に立つオンラインガイドが見つかる。


<!-- As the number of statistical tests used to test one or more hypotheses grows, so does the chance that one will reach your significance threshold due to random chance.
Be sure to correct for multiple comparisons.
See, for example, the Wikipedia entry on Multiple Comparisons.
This is easy to do but, again, a surprising number of papers have numerous statistical tests and no correction for multiple comparisons. -->
1つ以上の仮説を検定するために行われる統計的検定の回数が増えるに従い、偶然ある1つの仮説が有意水準に達する確率が高まる。
複数の検定を修正する方法がある。
例えば、Wikipediaの[Multiple Compasirons](https://en.wikipedia.org/wiki/Multiple_comparisons_problem)（多重比較）の項を参照すると良い。
これは簡単に利用ができるが、やはり、驚くほど多くの論文が多数の統計的検定を行いながらも多重比較の補正を行っていない。

<!-- After completing both the experiments and analyses required to test a hypothesis, you'll want to discuss your results.
In doing so, be careful not to jump to conclusions beyond those supported by your hypothesis and tests.
Speculation about possible implications that could be tested with future work should be presented as such. -->
仮説検証に必要な実験と分析の双方を完了した後、その結果を議論する必要がある。
その場合、仮説や検定によって裏付けられた結論以上の結論に飛躍してしまわないように注意すること。
考えうる意義に関して今後の課題として検定されるような推測は、そのように示されるべきである。


## 7. 関連研究の引用
<!-- To find related work perform web searches on key terms, scour the HCISEC bibliography and the proceedings of SOUPS, CHI, the IEEE Symposium on Security and Privacy (Oakland), USENIX Security, ACM CCS, and NDSS.
As you look at related work, note key terms that may be useful for searching for other related work.
You may also want to consult with other researchers who have written work in an area closely related to yours. -->
関連研究を見つけるためには、キーとなる用語によるWeb検索の実行と、HCISEC bibliography（訳者注：元の文献にはURLが記載されていたが、2019年5月の段階で存在していないため、ここでは記載をしていない）とSOUPS、CHI、IEEE Symposium on Security and Privacy (Oakland)、USENIX Security、ACM CCS、NDSSの予稿集を探すこと。
関連研究を見るときには、さらに他の関連研究を探すために有用なキーとなる用語に注意すること。
自身の研究に近い分野の論文を書いた他の研究者に相談することも良い。

### 7.1 関連研究の記載はどこへ置く？
<!-- The HCI community mostly adheres to a convention of presenting related work before experiments to ensure that the reader has all necessary background information before reading about the experimental methodology.
This convention exists, in part, because may experiments build on the methodology of prior experiments and so much of the related work is germane to the experimental design. -->
HCIのコミュニティは、読者が実験の方法論に関する部分を読む前に必要となるすべての背景情報を持っていることを確実にするため、実験に関する記載の前に関連研究の記載を置く慣習に大抵は従っています。
この慣習が存在するのは、部分的には、その研究の実験が先行実験の方法論に基づいて構築され、関連研究の多くが実験の設計と密接に関係しているためである。

<!-- The security community mostly adheres to a convention of presenting related work after experiments and results are presented.
This convention makes sense when much of the related work you may want to cite is not needed to motivate or provide background on your experiment.
When this is the case, the related work may bog down a reader who is interested in getting to the details of your experiment and would prefer to understand the broader context later.
If you follow this convention, you may need to cite some papers twice: first in an introductory section to motivate or provide essential background and later, after your experiment and results have been presented, to put your work in broader context. -->
セキュリティのコミュニティは、実験と結果に関する記載の後に関連研究の記載を置く慣習に大抵は従っています。
この慣習は、関連研究が研究背景や実験の提示や興味を起こさせるため引用すべき関連研究の多くは必要とされない場合に意味を持つ。
そういった場合には、実験の詳細記述を知りたくより広い文脈の理解は後ほど行いたい読者にとっては、関連研究が読者を止めてしまうかもしれない。
もしこの慣習に従う場合、いくつかの論文は2度参照されるべきである。最初は導入部分のセクションで本質的な背景の提示と興味を起こさせ、その後で実験と結果に関する記載の後にこの研究をより広い文脈の中でとらえるために。

<!-- Either convention is accepted at SOUPS and so you should choose the convention that works best for your paper. -->
どちらの慣習もSOUPSには受け入れられるので、論文に最も適した慣習を選択するべきである。

### 7.2 引用のエチケット
<!-- Wherever you cite related work, make sure citation numbers server as an essential supplement to more descriptive text that describes the work you are citing, and not a replacement for it.
In other words, do not say \[42] presents an experimental methodology for testing the obsessiveness of paper reviewers" but instead say \Zaphod Beeblebrox et al.
developed one of the first experimental methods for testing the obsessiveness of paper reviewers [42].
" By so doing, you'll help familiarize your reader with the names of those working in the field, your paper will read more smoothly, and those familiar with the literature won't have to flip pages forward and backward to identify which work you are citing. -->
関連研究を引用する時には、引用した研究の記載への補足物として文献番号が提供されていることを確認してください。
言い換えると、「\[42\]は論文査読者の細部へのこだわりをテストするための実験的な方法論を示している」という記載はせずに、「Zaphod Beeblebroxらは、論文査読者の細部へのこだわりをテストするための初期の実験的な方法の1つを開発した\[42\]」のように記述されるべきである。
こうすることで、読者がその分野を研究している研究者の名前に慣れ、論文がよりスムーズに読まれるようになる。文献に詳しい読者は引用された研究が何かを知るためにページを前後にめくる必要がなくなる。

<!-- Providing citation context will also help you avoid making the mistake of citing multiple works with one long string of citation numbers, such as \[59,71,72,78,84]".
Such bulk citations provide inadequate clues to the reader about what each paper is about, its contribution to the field, and its relation to your work.
If work is related enough to cite, it's usually related enough to warrant some explanation. -->
引用の文脈を提供することは、「\[59,71,72,78,84\]」のように1つにまとめて複数文献を引用するという間違いを避けることができる。
こういった大量の引用は、それぞれの論文がなにに関する論文で分野にどういった貢献がありどうこの論文と関係があるかといったことについて、読者に不適切な手がかりを与えてしまう。
もしその研究が引用するのに十分関連している場合は、通常いくらかの説明が必要なほど関連している。

<!-- Citing tenuously related work to increase the reference count will not earn points with reviewers or excuse the absence of key related work that has been overlooked.
While there is no prescribed number of references, expect warning bells to go off in reviewers' minds if you have fewer than ten citations or if more than a quarter of citations are to your own work. -->
参照件数を増やすために関連性の高い研究を内容が乏しいまま参照しても、査読者の評価が高まるわけではない。また見過ごしにより重要な関連研究が欠けていたことの言い訳にもならない。
参考文献の数は規定されていないものの、文献数が10未満の場合や著者自身の研究が4分の1を超えている場合には、査読者の心に警告の鐘が鳴り響くだろう。


## 8. 謝辞
<!-- Assuming you received help along the way, your paper should have an acknowledgements section, though this should not be submitted during review if your paper is anonymized.

I am grateful to Lorrie Cranor and Andrew Patrick for encouraging me to write this article, as well as their comments, corrections, and suggestions along the way.
I am grateful to Rachna Dhamija who helped me navigate my transition to working in, and writing about, human subjects experiments in security and privacy.
Adam Shostack provided additional valuable feedback. -->
研究遂行にあたり様々な助力を得た場合、論文には謝辞の章が入っているべきだろう。もし論文が匿名化されている場合は、査読の間は謝辞の章は提出されるべきではない。

この文献を書くことを後押ししてくれ、そしてその過程で多くのコメントや訂正、提案をくれたLorrie CranorとAndrew Patrickに感謝する。
人間を対象としたセキュリティとプライバシーの実験の研究へと移行することや執筆することに助力をくれたRachna Dhamijaに感謝する。
Adam Shostackはさらに貴重なフィードバックを提供してくれた。

___

