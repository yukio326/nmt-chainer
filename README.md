# nmt-chainer 

## English

This is an implementation of TMU-NMT using in WAT2017. The system description is [Tokyo Metropolitan University Neural Machine Translation System for WAT2017](http://aclweb.org/anthology/W17-5716.pdf).
The demonstration is [here](http://cl.sd.tmu.ac.jp/~matsumura/translator).

### 1. Environmental Settings
You have to install these modules. The written virsion is recommended.
- Python 3.5.1
- chainer (ver 4.0.0)
- numpy (ver 1.14.2)
- cupy (ver 4.0.0)
- h5py (ver 2.7.1)
- gensim (ver 2.2.0)

### 2. Experimental Settings
You have to write experimental settings in the configration file. You can see the sample configration file [sample.config](https://github.com/yukio326/nmt-chainer/blob/master/sample/sample.config).


- **model** : Model name.
- **source_train** : The path to source train file.
- **target_train** : The path to target train file.
- **source_dev** : The path to source development file.
- **source_test** : The path to source test file.
- **use_gpu** : True / False
- **gpu_device** : The GPU number.
- **use_word2vec** : "Make" / "Load" / "None" 
- **source_word2vec_file** : The path to source word2vec file.
- **target_word2vec_file** : The path to target word2vec file.
- **epoch** : The epoch number on training.
- **optimizer** : "SGD" / "Adam" / "AdaDelta" / "AdaGrad"
- **learning_rate** : The initial learning rate.
- **use_dropout** : True / False
- **dropout_rate** : The dropout rate.
- **source_vocabulary_size** : The source vocabulary size.
- **target_vocabulary_size** : The target vocabulary size.
- **embed_size** : The embedding size.
- **hidden_size** : The hidden size.
- **batch_size** : The minibatch size.
- **pooling** : The minibatch pooling size.
- **generation_limit** : The generation limit number on testing.
- **use_beamsearch** : True / False
- **beam_size** : The beam size on testing.

### 3. Execution

```
python src/nmt.py [MODE] [CONFIG_PATH] [BEST_EPOCH (only testing)]
```

- **MODE** : "train" / "dev" / "test"
- **CONFIG_PATH** : The path to configration file.
- **BEST_EPOCH** : The epoch number of model using on testing.


## 日本語

WAT2017におけるTMU（首都大小町研）のシステムです。
モデルの詳細は
[Tokyo Metropolitan University Neural Machine Translation System for WAT2017](http://aclweb.org/anthology/W17-5716.pdf)
を参照。
デモは
[こちら](http://cl.sd.tmu.ac.jp/~matsumura/translator)
。

### 1. 環境設定
はじめに、以下の環境設定が必要（バージョンは推奨）です。このうち、chainerは記載されたバージョンであることが必須です。
- Python 3.5.1
- chainer (ver 4.0.0)
- numpy (ver 1.14.2)
- cupy (ver 4.0.0)
- h5py (ver 2.7.1)
- gensim (ver 2.2.0)

### 2. 実験設定
実験の設定はconfigファイルにて行います。[sample.config](https://github.com/yukio326/nmt-chainer/blob/master/sample/sample.config)が設定例です。

- **model** : 保存するモデルの名前を指定してください。
- **source_train** : 学習用ソースファイルのパスを指定してください。
- **target_train** : 学習用ターゲットファイルのパスを指定してください。
- **source_dev** : 開発用ソースファイルのパスを指定してください。
- **source_test** : 評価用ソースファイルのパスを指定してください。
- **use_gpu** : GPUを使用する場合はTrue、CPUを使用する場合はFalseを指定してください。
- **gpu_device** : 使用するGPUの番号を整数で指定してください。
- **use_word2vec** : gensimのword2vecを用いてEncoderおよびDecoderのword embeddingを初期化することができます。新しくデータを作成して用いる場合は"Make"、すでに作成済みのデータを用いる場合は"Load"、word2vecを用いずにランダムな初期化を行う場合は"None"を指定してください。 
- **source_word2vec_file** : 作成済みのword2vecを用いる場合のソース言語ファイルのパスを指定してください。
- **target_word2vec_file** : 作成済みのword2vecを用いる場合のターゲット言語ファイルのパスを指定してください。
- **epoch** : 学習時のエポック数を整数で指定してください。
- **optimizer** : 学習時の最適化手法を"SGD"、"Adam"、"AdaDelta"、"AdaGrad"の中から指定してください。
- **learning_rate** : 学習時の最適化手法における初期学習率を小数で指定してください。ただし、最適化手法が"SGD"および"AdaGrad"の時のみ有効です。
- **use_dropout** : 学習時にdropoutを適用する場合はTrue、適用しない場合はFalseを指定してください。
- **dropout_rate** : 学習時のdropoutを適用する場合の適用率を小数で指定してください。
- **source_vocabulary_size** : ソース言語側の語彙サイズを整数で指定してください。
- **target_vocabulary_size** : ターゲット言語側の語彙サイズを整数で指定してください。
- **embed_size** : EncoderおよびDecoderのword embeddingの次元数を整数で指定してください。
- **hidden_size** : EncoderおよびDecoderの隠れ層の次元数を整数で指定してください。
- **batch_size** : 学習時のミニバッチサイズを整数で指定してください。
- **pooling** : 学習時にはコーパス全体の文をランダムに入れ替えた後、batch\_size×pooling文のブロック内で文がソートされ、ミニバッチを作成します。この数は整数で指定してください。
- **generation_limit** : 開発時および評価時の生成単語制限数を整数で指定してください。この機能は無限に単語を生成し続けることを防ぐためのものです。指定した制限数の単語をすでに生成している場合、仮に翻訳の途中であっても文が終了してしまうことに注意してください。
- **use_beamsearch** : 評価時にbeam searchを行う場合はTrue、行わない場合はFalseを指定してください。
- **beam_size** : 評価時にbeam searchを行う場合のbeam sizeを整数で指定してください。

### 3. 実行方法
プログラムを実行するには、モデルを保存したい（保存してある）ディレクトリで以下のコマンドを実行してください。
```
python src/nmt.py [MODE] [CONFIG_PATH] [BEST_EPOCH (only testing)]
```
- **MODE** : "train"、"dev"、"test"のいずれかを指定してください。ただし、"train"済みのモデルが存在しない場合は"dev"、"test"モードは正しく実行されません。
- **CONFIG_PATH** : 実験設定を記述したconfigファイルのパスを指定してください。
- **BEST_EPOCH** : "test"モードのときのみ、使用するモデルのエポック数を整数で指定してください。
