# 本文書の目的
Stuart Schechter氏が執筆した["Common Pitfalls in Writing about Security and Privacy Human Subjects Experiments, and How to Avoid Them"]( https://www.microsoft.com/en-us/research/publication/common-pitfalls-in-writing-about-security-and-privacy-human-subjects-experiments-and-how-to-avoid-them/) の和訳

## 許諾
ご本人より和訳の許可をいただいています。（2019年3月27日）

___

# セキュリティとプライバシーにおける人を対象にした実験について執筆するときにありがちな落とし穴と、その回避方法
<!-- 
Common Pitfalls in Writing about Security and Privacy Human Subjects Experiments, and How to Avoid Them
-->

Stuart Schechter

Microsoft Research (^1 訳者注：所属は執筆時のものであり、現在の所属ではありません)

## 概要
<!-- Reviewers of papers that describe human subjects experiments of security and privacy often observe that authors are prone to a set of common mistakes that, if they were aware of, could be easily avoided. In this document I provide advice to help researchers avoid these mistakes in designing, performing, and documenting their experiments.  -->
人を対象にしたセキュリティやプライバシーに関して実験論文の査読者は、著者がよく犯しがちな間違いの傾向に気づくことがある。これらは気をつけていれば簡単に避けることが出来る。
この文書は、研究者が実験をデザイン、実行、論文化する際の過ちを回避するアドバイスとして記したものである。

## 本文の要約
<!-- Executive Summary -->

1. あなたがテスト（検定）しようとしている仮説を正確に示すこと。<!-- State the hypothesis or hypotheses you are testing precisely. -->
2. セキュリティの仮説を検定する場合、明確かつ防御可能（弁護可能？）な脅威モデルを持つこと。<!-- If testing a security hypothesis, have a clear and defensible threat model. -->
3. 著者自身や読者をミスリードすることを避けること。特に論文の貢献の売り込みや、結果からまとめを得るときの解釈の時に。<!-- Avoid misleading yourself or your reader in any way, especially in selling your contribution or in translating results into conclusions. -->
4. 実験参加者の行動がいかに観察され、スコア化され、そして統計の検定に適用されたかについて注意深く説明すること。<!--  Carefully explain how participants’ behaviors were observed, scored, and then fed into statistical tests. -->
5. 実験への倫理的な考察を説明すること。そしてその研究は所属組織の倫理審査委員会の承認を得ているかどうか明らかにすること。<!-- Explain any ethical considerations of your experiment and disclose whether your study was approved by the ethics review board at your institution(s). -->
6. 研究の設計や得られた結果についての制限で著者らが認識しているものはすべて開示すること。<!-- Disclose all limitations in your study design and results that you are aware of. -->
7. グラフがそれ自身で説明されうるようにすべての軸にラベルを書き、説明文（キャプション）を加えること。<!-- Label all axes in graphs and add captions to ensure figures are self explanatory. -->
8. 相関関係が因果関係を暗示すると思いこまないこと。<!-- Do not assume that correlation implies causation -->
9. 検定の結果、帰無仮説の棄却に失敗からといってその仮説が間違っていると結論付けないこと。<!-- Do not conclude that a hypothesis is false because a statistical test failed to disprove the null hypothesis. -->
10. 正規分布への当てはめや試行が独立であることなど、要件が合致したときのみ統計テストを使うこと (もし疑わしい場合はノンパラメトリック検定を使うこと。)<!-- Use a statistical test only when the requirements under which it is valid, such as data fitting a normal distribution or trials being independent, are met. (When in doubt, use a non-parametric test.) -->
11. 助けを求めることを恐れないこと。この研究に参加していない仲間・同僚に論文の草稿を読ませること。<!-- Don’t be afraid to ask for help. Ask colleagues who were not involved in the research to read an early draft of your paper. -->

## 1. はじめに
<!-- Program committees must often reject papers with fascinating ideas or clever experimental methodologies - which we would love to see presented - because the validity of the experimental results is in question: program committee members cannot ascertain key experimental details from the paper, how data were collected, or whether a statistical test is indeed sufficient to support a hypothesis.  -->
<!-- Many of the mistakes that force program committees to reject papers are common and easily avoided. -->
プログラム委員会は、魅力的なアイデアや巧みな実験方法を持つ論文を実験結果の妥当性が疑問視されているために却下しなければならないことが多い（我々はそれが発表されるのを見たいのだが）。これは、データの収集方法、統計的検定が仮説を支持するのに十分であるかどうか、という重要な実験の詳細をプログラム委員が論文から確かめることができないからである。
論文の不採録判定をプログラム委員会に余儀なくさせる間違いの多くは、ありがちな事柄であって簡単に避けることが出来る。

<!-- I have written this document to guide researchers in how to avoid the most common pitfalls when submitting to the Symposium on Usable Privacy and Security (SOUPS) and other venues that accept human subjects studies about security and privacy. -->
<!-- I provide a mixture of generally accepted practices for writing computer science papers, practices specific to human subjects studies in security, and less universally accepted advice based on my opinion and past experiences as an author and reviewer. -->
<!-- This work is not intended to be a complete guide to writing a paper. -->
<!-- Rather, it is intended to help those with a general knowledge of how to write an academic paper to adapt their skills to writing up security and privacy human subjects studies and to help all authors avoid common pitfalls.  -->
本稿は、the Symposium on Usable Privacy and Security (SOUPS) や、人間を対象としたセキュリティとプライバシーに関する研究を受け入れるその他の場に投稿する際の、最も一般的な落とし穴を避ける方法について研究者をガイドするために書いた文書である。
私は、コンピュータサイエンスの論文を書くための一般的に受け入れられているプラクティスや、セキュリティに関する人間を対象とした研究に特有のプラクティス、そして（一般的には受け入れられていないが）著者や査読者としての私の意見と過去の経験に基づいたアドバイスを組み合わせて提供する。
本稿は、論文を執筆するための完全なガイドであることをを意図していない。
むしろ、学術論文の執筆に一般的な知識を持つ著者がそのスキルをセキュリティやプライバシに関する人間を対象とした研究の論文執筆に適合させることを助け、すべての著者がありがちな落し穴に落ちないようにすることを助けることを意図している。

## 2. あなたの貢献
 <!-- It is important to define your contribution by explaining the general problem you are trying to solve and the specific instance of the problem that is the basis for your work, the hypotheses you wanted to test, unique features of your approach, and your results.  -->
あなたが解決しようとしている一般的な問題と、研究の基礎となっているその問題の具体的な事例、検証したい仮説、アプローチの独自の特徴、そして結果を説明して貢献度を定義することが重要です。

<!-- As you lay out your paper, and especially your contribution, you must be meticulously careful to avoid misleading yourself or your reader in any way. 
Prior work should not be unduly disparaged, your innovations should not be exaggerated, and no limitation of your work should be swept under the rug. 
Graduate students are taught that they need to sell their work and its contribution to the field - and this is an important skill - but good marketing should be about isolating the value of your contribution and presenting it clearly.  -->
あなたが論文をレイアウトするとき、特に貢献の部分をレイアウトするときには、どのようにしてもあなた自身や読者が誤解しないように細心の注意を払わなければならない。
既存研究を過度にけなしたり、自身のイノベーションを誇張したり、研究内容の制限を隠したりすべきではない。
大学院生は、自分たちの研究と分野へのその貢献を売り込む必要があると教えられている。それは重要なスキルではある。しかし、よいマーケティングとは貢献の価値を分離してそれを明確に提示することにあるべきです。

<!-- Exaggerations, undocumented limitations, or other issues that lead reviewers to suspect they are being mislead will cause them to start reading your paper more suspiciously. 
This takes their focus away from appreciating the contribution of your work.  -->
誇張や記載されていない制限、欺かれていると査読者に疑わせるような事項があると、査読者は論文を疑い深く読み始めてしまうことになる。
こういったことは、研究の貢献を評価することから査読者の焦点を外してしまう。

<!-- Alas, even if you are honest in how you convey your research, it is exceedingly hard to determine if you have conveyed the information necessary for someone other than yourself to understand it. 
The best way to determine if your research will be comprehensible is to ask colleagues who were not involved in the research to read an early draft of your paper. 
If you are not a native-level speaker of the language in which the work is written, find a native-level speaker to point out and help remove any problems with language, spelling, or idioms.  -->
悲しいかな、もし自身の研究を伝えることに誠実であったとしても、自分以外の人たちに研究の理解に必要な情報を伝えたかどうかを判断することは非常に難しい。
自身の研究が理解できるかを判断する最良の方法は、その研究に従事していない同僚に論文の草稿を読んでもらうように依頼することだ。
もしあなたが論文執筆の言語をネイティブレベルに話せない場合は、言語・スペル・熟語におけるすべての問題点を指摘し取り除く助けをしてくれるネイティブレベルに話すことができる人を見つけなさい。

## 3. 実験のデザイン

### 3.1 何を含めるか

### 3.2 倫理と実験参加者の安全

### 3.3 補足資料

## 4. 特別に考慮する事項：模擬攻撃を含む実験

プライバシーとセキュリティの脅威に関する行動を含む実験では、他のHCIの実験について執筆するときにはそれほど重要ではないことに対しても考慮が必要になります。
<!-- Experiments involving behavior in response to privacy and security threats warrant extra consideration in areas that may be less important when writing up other HCI experiments -->

### 4.1 明確な脅威モデルを持つこと

### 4.2 自身のシステムに有利となるバイアスを避けること

### 4.3 生態学的妥当性を取り扱うこと

## 5. 限定条件の開示

## 6. 結果の提示

### 6.1 図表

### 6.2 統計的な妥当性

## 7. 関連研究の引用

### 7.1 関連研究はどこへ向かう？

### 7.2 引用のエチケット

## 8. 謝辞

