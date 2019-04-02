# 本文書の目的
Stuart Schechter氏が執筆した["Common Pitfalls in Writing about Security and Privacy Human Subjects Experiments, and How to Avoid Them"]( https://www.microsoft.com/en-us/research/publication/common-pitfalls-in-writing-about-security-and-privacy-human-subjects-experiments-and-how-to-avoid-them/) の和訳

## 許諾
ご本人より和訳の許可をいただいています。（2019年3月27日）

___

# セキュリティとプライバシーにおける被験者実験について執筆するときにありがちな落とし穴と、その回避方法
<!-- 
Common Pitfalls in Writing about Security and Privacy Human Subjects Experiments, and How to Avoid Them
-->

Stuart Schechter

Microsoft Research (^1 訳者注：所属は執筆時のものであり、現在の所属ではありません)

## 本文の要約

1. あなたがテスト（検定）しようとしている仮説を正確に示すこと。<!-- State the hypothesis or hypotheses you are testing precisely. -->
2. セキュリティの仮説を検定する場合、明確かつ防御可能（弁護可能？）な脅威モデルを持つこと。<!-- If testing a security hypothesis, have a clear and defensible threat model. -->
3. 著者自身や読者をミスリードすることを避けること。特に論文の貢献の売り込みや、結果からまとめを得るときの解釈の時に。<!-- Avoid misleading yourself or your reader in any way, especially in selling your contribution or in translating results into conclusions. -->
4. 被験者の行動がいかに観察され、スコア化され、そして統計の検定に適用されたかについて注意深く説明すること。<!--  Carefully explain how participants’ behaviors were observed, scored, and then fed into statistical tests. -->
5. 実験への倫理的な考察を説明すること。そしてその研究は所属組織の倫理審査委員会の承認を得ているかどうか明らかにすること。<!-- Explain any ethical considerations of your experiment and disclose whether your study was approved by the ethics review board at your institution(s). -->
6. ユーザスタディなどの設計や得られた結果についての制限で著者らが認識しているものはすべて開示すること。<!-- Disclose all limitations in your study design and results that you are aware of. -->
7. グラフがそれ自身で説明されうるようにすべての軸にラベルを書き、説明文（キャプション）を加えること。<!-- Label all axes in graphs and add captions to ensure figures are self explanatory. -->
8. 相関関係が因果関係を暗示すると思いこまないこと。<!-- Do not assume that correlation implies causation -->
9. 検定の結果、帰無仮説の棄却に失敗からといってその仮説が間違っていると結論付けないこと。<!-- Do not conclude that a hypothesis is false because a statistical test failed to disprove the null hypothesis. -->
10. 正規分布への当てはめや試行が独立であることなど、要件が合致したときのみ統計テストを使うこと (もし疑わしい場合はノンパラメトリック検定を使うこと。)<!-- Use a statistical test only when the requirements under which it is valid, such as data fitting a normal distribution or trials being independent, are met. (When in doubt, use a non-parametric test.) -->
11. 助けを求めることを恐れないこと。この研究に参加していない仲間・同僚に論文の草稿を読ませること。<!-- Don’t be afraid to ask for help. Ask colleagues who were not involved in the research to read an early draft of your paper. -->

## 1. はじめに

## 2. あなたの貢献

## 3. 実験のデザイン

### 3.1 何を含めるか

### 3.2 倫理と被験者の安全

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

