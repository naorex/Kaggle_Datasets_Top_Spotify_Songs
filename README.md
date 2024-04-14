# (kaggle) Datasets : Top Spotify Songs

Top Spotify Songs Datasets のリポジトリ

- directory tree

```
Kaggle_Datasets_Top_Spotify_Songs
├── README.md
├── data         <---- gitで管理するデータ
├── data_ignore  <---- gitで管理しないデータ(モデルとか、特徴量とか、データセットとか)
├── nb           <---- 作成したノートブック
└── src_att      <---- .ipynb 以外のコード
```

## About Dataset

### Context

Dataset contains a comprehensive list of the most famous songs and most streamed songs as listed on Spotify.

It provides insights into each song's ;

- Attributes
- Popularity
- Presence on various music platforms

The dataset includes information such as track name

- Artist's name
- Release date
- Spotify playlists and charts
- Streaming statistics
- Apple Music presence
- Deezer presence
- Shazam charts
- Various audio features

### Popular_Spotify_Songs.csv colomn infomation

notebook: nb001<br>
953 行、24 カラム<br>
<img src='.\data\images\readme\nb001_info.png' width='500'>

## Log

### 20240414

- nb001

===============================================================================<br>
(reference)

### 20230922

- nb001

  - カレーちゃん著『Kaggle のチュートリアル第 6 版』に基づいて作成。
  - 与えられたデータ内容の確認。

  - 死亡者、生存者の人数<br>
    死亡 0 : 549 (61.6%)<br>
    生存 1 : 342 (38.4%)<br>
    全体 : 891<br>
    <img src='.\data\images\readme\nb001_Survived.png' width='500'>

  - 性別<br>
    男性は、死亡者 0 が 生存者 1 の約 5 倍<br>
    女性は、死亡者 0 が 生存者 1 の約 3 割ほどのみ<br>
    【気付き】 女性や子供から優先的に救命艇へ乗せられたため？<br>
    <img src='.\data\images\readme\nb001_Sex_Survived_table.png'><br>
    <img src='.\data\images\readme\nb001_Sex_Survived.png' width='500'>

  - チケットクラス<br>
    1st クラスの乗客の生存率が、3rd クラスの乗客より高い<br>
    <img src='.\data\images\readme\nb001_Pclass_Survived_table.png'><br>
    <img src='.\data\images\readme\nb001_Pclass_Survived.png' width='500'>

  - 年齢の分布<br>
    乳幼児から子供が数十人乗船しており、大人は 10 代後半～ 30 代後半が多い<br>
    また、乳幼児から子供は生存率が高い<br>
    <img src='.\data\images\readme\nb001_Age_Survived_table.png'><br>
    <img src='.\data\images\readme\nb001_Age.png' width='500'><br>
    <img src='.\data\images\readme\nb001_Age_Survived_0.png' width='500'><br>
    <img src='.\data\images\readme\nb001_Age_Survived_1.png' width='500'><br>

  - 兄弟・配偶者の数<br>
    "0" のカテゴリーが大半を占め、次点で "1" のカテゴリー<br>
    <img src='.\data\images\readme\nb001_SibSp.png' width='500'><br>
    "2" 以上のカテゴリーをグループ化し、死亡・生存を確認<br>
    兄弟または配偶者が 1 人の場合の生存率が高い<br>
    <img src='.\data\images\readme\nb001_SibSp_table.png'><br>
    <img src='.\data\images\readme\nb001_SibSp_group.png' width='500'>

  - 両親・子供の数<br>
    "0" のカテゴリーが大半を占める。"3" 以上のカテゴリーはほぼ無し<br>
    <img src='.\data\images\readme\nb001_Parch.png' width='500'><br>
    "3" 以上のカテゴリーをグループ化し、死亡・生存を確認<br>
    両親または子供が 1 人の場合の生存率が高い<br>
    <img src='.\data\images\readme\nb001_Parch_table.png'><br>
    <img src='.\data\images\readme\nb001_Parch_group.png' width='500'>

  - 1 人で乗船か、2 人以上で乗船か<br>
    1 人で乗船の死亡率が高い<br>
    <img src='.\data\images\readme\nb001_IsAlone_table.png'><br>
    <img src='.\data\images\readme\nb001_IsAlone.png' width='500'>

  - 運賃<br>
    大半の乗客は運賃 100 以下<br>
    運賃が高くなるにつれ、生存率が高い<br>
    <img src='.\data\images\readme\nb001_Fare_table.png'><br>
    <img src='.\data\images\readme\nb001_Fare.png' width='500'>

  - 名前<br>
    敬称の種類は 17 種類<br>
    <img src='.\data\images\readme\nb001_Name_Surname.png'><br>
    年齢の平均値。"Master" の平均値が 1 桁のため、子供の愛称的な敬称と思われる<br>
    <img src='.\data\images\readme\nb001_Name_AverageAge.png'>

- 年齢が生存率に与える影響が大きい傾向があるため、

  - Master = 1
  - Miss = 2
  - Mr = 3
  - Mrs = 4<br>

  に変換し、新しい特徴量として使えるようにしておく。

```
data/datasets_nb001
├── nb001_train.csv
└── nb001_test.csv
```

### 20230923

- nb002

  - データの前処理、LightGBM を用いて学習および生存予測
  - One-Hot Encoding で "Sex" と "Embarked" を前処理 (Pandas の get_dummies)
  - LightGBM の導入
    - LightGBM の仕様が変わっているようなので注意 [(参考リンク)](https://qiita.com/c60evaporator/items/2b7a2820d575e212bcf4)
    - score 82.37
    ```bash
    # Early stopping, best iteration is:
    # [29]	training's binary_logloss: 0.301373	valid_1's binary_logloss: 0.400278
    ```

- nb003

  - scikit-learn interface を使用して推定する手法にトライ
  - nb002 と同じ結果が出る事を確認
    - score 82.37
    ```bash
    # Early stopping, best iteration is:
    # [29]	training's binary_logloss: 0.301373	valid_1's binary_logloss: 0.400278
    ```

- nb004
  - ここからオリジナル
  - RandomForestClassifier による推定
  - 話を簡単にするため、object 型の列データを除外
  - train_size=0.8, test_size=0.2 で分割（交差検証 CV : 無し）<br><br>
    - Case-1 : そのまま推定。random_state=1
    - Validation MAE: 0.238, モデルのスコア: 0.945
    - Kaggle Public Score: 0.72727<br><br>
    - Case-2 : 決定木の max_leaf_nodes を範囲設定して最小 MAE を探索。random_state=1
    - 範囲設定 => range(2,102,1) => 最適ツリーサイズ: 5
    - Validation MAE: 0.182, モデルのスコア: 0.818
    - Kaggle Public Score: 0.78468<br><br>
  - 一般的に Case-2 の方が良いスコアが出るものだが、今回のケースはスコアは却って悪化した
  - もしくは逆に、Case-1 は過学習気味？
  - 両ケースの結果を提出。Public Score は Case-2 の方が良かった<br>
    <img src='.\data\images\readme\nb004_public_score.png' width='800'>
  - 次は交差検証を用いて推定を行う

### 20230924

- nb005

  - RandomForestClassifier による推定に、交差検証を導入
  - 話を簡単にするため、object 型の列データを除外
  - 5 fold による交差検証
  - 結果、ツリーの数 n_estimators = 300 が最適と出た<br>
    <img src='.\data\images\readme\nb005_graph_mae_nesti.png'>

  - 各 n_estimators での Average MAE Score<br>
    <img src='.\data\images\readme\nb005_nesti_detail.png'><br>

  - 結果を提出
    - Kaggle Public Score: 0.73684
  - 次の方針はどうするか

### 20231001

- nb006

  - 『探索的データ探索』の本のプロセスを実施。以下メモ。
  - 良いデータを見つけるためのプロセス

    - STEP 1: データの理解
      - まずはコンペの目的、データの概要、意味、値を確認する
    - STEP 2: データのクリーニング
      - データセットには欠損や分析に不適なデータが必ず含まれるため除外
      - 代表的な手法は以下<br>
        <img src='.\data\images\readme\nb006_1.png' width='600'><br>
    - STEP 3: データ分析の切り口の検討
      - どんな切り口で分析するかが非常に重要
      - 代表的な切り口は以下<br>
        <img src='.\data\images\readme\nb006_2.png' width='600'><br>
    - STEP 4: データの分析
      - データの切り口を決めたら、データの分析へ
      - 代表的な分析手法は以下<br>
        <img src='.\data\images\readme\nb006_3.png' width='600'><br>
    - STEP 5: データの選択
      - 分析が終わったら結果をまとめて、目的変数に関連度合いに応じて優先度を付ける

  - データの種類から分析する視点を変える
  - 基本の 2 パターンは以下
    - 質的データ（カテゴリデータ）
      - 数値で測定できないデータ
    - 量的データ
      - 数値測定が可能なデータ
      - 連続データと離散データの 2 種類に分かれる
  - 尺度分類　データの分類・水準

    - 以下の 4 つに分類<br>
      <img src='.\data\images\readme\nb006_4.png' width='800'><br>

  - 欠損値は残すか消すこと、原則として補間処理はしない

    - 探索的データ分析の段階では、欠損値の補間は行わないこと
      - 欠損値が多い場合、または目的変数との関連が弱い場合: データ列を削除する
      - 欠損値が少ない場合、または目的変数との関連が強い場合: 欠損値のまま残す

  - 外れ値は外すこと

    - 外れ値の判断はデータの特性にもよるが、まずは
      - 常識的に考えて異常なデータは除外
      - 範囲による外れ値の判定
        - 例えば上位下位 25%（四分位範囲）は除外する<br>
          <img src='.\data\images\readme\nb006_Age_boxplot.png' width='400'><br>
        - 他には、閾値設定を行う<br>
          <img src='.\data\images\readme\nb006_Fare_histplot.png' width='500'><br>
        - 平均 32,標準偏差 49,最大値 512 と分布に偏りがある<br>
          <img src='.\data\images\readme\nb006_Fare_detail.png'><br>
        - 運賃 50 以上は除外した後<br>
          <img src='.\data\images\readme\nb006_Fare_histplot_after.png' width='500'><br>
        - 平均 15,標準偏差 10 と分布の偏りが是正された<br>
          <img src='.\data\images\readme\nb006_Fare_detail_after.png'>

  - データ分析に適した姿へ変換

    - データの型変換（テキストから数値へ変換）
      - 男性/女性　 ⇒ 　 0/1 に変換
    - データの型変換（数値からテキストへ変換）
      - 数値の範囲から、グループの塊へ変換

  - 規則性を見抜いて意味のあるデータを作成

    - Cabin の先頭文字を見ると、客室ランクを表している事が推察できる<br>
      <img src='.\data\images\readme\nb006_Fare_Cabin_ini.png' width='500'><br>
    - しかし、データのばらつきが多いので利用は難しいか<br>
      <img src='.\data\images\readme\nb006_Fare_Cabin_ini_detail.png'><br>
    - 分析する意味のないデータは、見るだけ時間の無駄なので思い切って削除するのが吉

  - データ分析の切り口 6 種

    - 要約統計量<br>
      <img src='.\data\images\readme\nb006_5.png' width='800'><br>
    - スライシング
    - ドリルダウン
    - 合成
    - 尺度変換
    - 無名数化

  - データ分析の基本 6 パターン
    - 単変数のデータ分析
      - 性別で傾向が異なることが分かる<br>
        <img src='.\data\images\readme\nb006_Sex_Age.png' width='500'><br>
    - 変数間のデータ分析
      - 客室ごと年齢を棒グラフで表現
    - 箱ひげ図
      - データの分布が分かる
    - 折れ線グラフ
      - 時系列データ
    - 相関分析
      - 散布図でデータ関係の詳細が分かる
    - ヒートマップ
      - 散布図と同様に関係が分かる
