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

### 20240421

- nb001 データ整形と可視化
  - 以下を実施。[参考リンク(Kaggle)](https://www.kaggle.com/code/kamalikoshy/spotify-data-analysis)
    - データクリーニングと前処理
    - データの整形
    - 9 つの切り口でデータの可視化

### 20240429

- nb002 探索的データ分析(EDA)
  - 以下を実施。[参考リンク(Kaggle)](https://www.kaggle.com/code/lucasguiraldelli/eda-of-spotify-artist-songs-and-related-data)
    - 簡単なデータクリーニング
    - データを可視化しながら、特徴を探る
