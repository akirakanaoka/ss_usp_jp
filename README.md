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

