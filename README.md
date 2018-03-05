# nmt-chainer 

WAT2017におけるTMU（首都大小町研）のシステムです。
モデルの詳細は
[Tokyo Metropolitan University Neural Machine Translation System for WAT2017](http://aclweb.org/anthology/W17-5716.pdf)
を参照。
デモは
[こちら](http://cl.sd.tmu.ac.jp/~matsumura/translator)
。

## 1. 環境設定
はじめに、以下の環境設定が必要（バージョンは推奨）です。このうち、chainerは記載されたバージョンであることが必須です。
- Python 3.5.1
- chainer (ver 1.24.0)
- h5py (ver 2.7.0)
- gensim (ver 2.2.0)

## 2. 実験設定
実験の設定はconfigファイルにて行います。/sample/sample.configが設定例です。

## 3. 実行方法
プログラムの実行方法は以下のとおりです。
```
python src/nmt.py [MODE] [CONFIG_PATH] [BEST_EPOCH (only testing)]
```
- MODE : "train"、"dev"、"test"のいずれかを指定してください。ただし、"train"済みのモデルが存在しない場合は"dev"、"test"モードは正しく実行されません。
- CONFIG_PATH : 実験設定を記述したconfigファイルのパスを指定してください。
- BEST_EPOCH : "test"モードのときのみ、使用するモデルのエポック数を整数で指定してください。
