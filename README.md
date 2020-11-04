# arduino-cli-docker

## Description

CLIによるM5Stackの開発にあたり、スケッチのコンパイルとアップロードを行う環境

## Installation

```
$ docker-compose build
```

```
$ ./install_libs.sh
```

## Usage

### スケッチのビルド

```
$ docker-compose run arduino-cli compile -v -b esp32:esp32:m5stack-core-esp32 {プロジェクトのディレクトリ}
```

### スケッチのアップロード

```
$ docker-compose run arduino-cli upload -p /dev/ttyUSB0 -b esp32:esp32:m5stack-core-esp32 {プロジェクトのディレクトリ}
```

### スケッチの新規作成

```
$ docker-compose run arduino-cli sketch new {プロジェクト名}
```

- permissionがrootになるので素直にホストでmkdirとtouchした方が良さそう

### ライブラリのインストール

#### arduino-cli経由

```
$ docker-compose run arduino-cli lib install {ライブラリ名}
```

#### 手動(HX711の例)

```
$ git clone https://github.com/bogde/HX711.git
$ mkdir assets/Arduino/libraries/HX711/
$ mv HX711/src/* assets/Arduino/libraries/HX711
$ rm -rf HX711/
```

## Note

### assets/について

- `assets/`ディレクトリにarduino-cliの環境設定やライブラリが保存される
- このディレクトリはpermissionがrootになるので注意
- C++のLanguage Serverのinclude pathにここの中から適切なpathを渡して解析させる予定
