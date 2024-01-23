# マルチステージビルドの例

#Stage1

# Go言語のバージョン1.16.4とAlpine Linuxのバージョン3.13を含むDockerイメージをベースイメージとする
# as builderは、このビルドステージの名前をbuilderとして定義している
FROM golang:1.16.4-alpine3.13 as builder

# ローカルのmain.goを、コンテナイメージのワーキングディレクトリ（WORKDIR 命令で設定された場所または /）にコピーする
# 今回は./以下にコピーする
COPY ./main.go ./

# main.goをソースからビルド（コンパイル）して、msbという実行可能なバイナリファイルを生成する
RUN go build -o /msb ./main.go


#Stage2

#alpineのベースイメージを取得
FROM alpine:3.13

# ビルドステージ builder で作成された /msb ファイルを、このイメージの /usr/local/bin/msb にコピーする
# このように、ビルドステージ builder で作成されたファイルを、別のビルドステージで利用することができる
COPY --from=builder /msb /usr/local/bin/msb

# コンテナ起動時に実行されるコマンドを指定する
# 今回は、/usr/local/bin/msb という実行可能なバイナリファイルを実行する
ENTRYPOINT [ "/usr/local/bin/msb" ]





