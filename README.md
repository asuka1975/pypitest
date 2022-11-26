# pypitest

自作pythonパッケージ公開について勉強するためのローカルテスト環境(pypiserver)．
ライブラリの作成，ライブラリの公開，そのライブラリのインストールをローカルの仮想環境上で行うことができる．

## 利用方法

### 想定環境

- docker
- docker-compose

### 実行

1. クローン

```shell
$ git clone https://github.com/asuka1975/pypitest.git
$ cd pypitest
```

2. コンテナの起動

```shell
$ sudo docker-compose -p pypitest up -d
```

3. ライブラリ作成

ライブラリの作成とローカルpypiサーバへの公開はlibrarianコンテナ上で行う．一連の流れは以下のようになる．

- librarianコンテナ上にバインドマウントされているpackagesディレクトリにライブラリを配置する．
- librarianコンテナにアタッチし，配置したライブラリのパッケージを作成しtwine二よりpypiサーバへ公開する．

```shell
$ cp -r `your package` packages/
$ sudo docker-compose -p pypitest exec librarian /bin/bash
$ cd packages/`your package`
$ python3 setup.py bdist_wheel
$ python3 -m twine upload --repository privatepypi dist/*
```

4. 自作ライブラリのインストール

clientコンテナにアタッチし，自作したライブラリをインストールしたのちテストする．

```shell
$ python3 -m pip install `your package`
```