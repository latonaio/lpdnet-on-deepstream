# lpdnet-on-deepstream
lpdnet-on-deepstream は、DeepStream 上で LPDNet の AIモデル を動作させるマイクロサービスです。  

## 動作環境
- NVIDIA 
    - DeepStream
- LPDNet
- Docker
- TensorRT Runtime

## LPDNetについて
LPDNet は、画像内のナンバープレートをを検出し、カテゴリラベルを返すAIモデルです。  
LPDNet は、特徴抽出にCSPDarkNet-Tinyを使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順
### Dockerコンテナの起動
Makefile に記載された以下のコマンドにより、LPDNet の Dockerコンテナ を起動します。
```
docker-run: ## Docker ストリーミング用コンテナを建てる
	docker-compose -f docker-compose.yaml up -d
```
### ストリーミングの開始
Makefile に記載された以下のコマンドにより、DeepStream 上の LPDNet でストリーミングを開始します。  
```
stream-start: ## ストリーミングを開始する
	xhost +
	docker exec -it deepstream-lpdnet deepstream-app -c /app/src/deepstream_app_source1_trafficcamnet_lpdnet.txt
```
## 相互依存関係にあるマイクロサービス  
本マイクロサービスを実行するために LPDNet の AIモデルを最適化する手順は、[lpdnet-on-tao-toolkit](https://github.com/latonaio/lpdnet-on-tao-toolkit)を参照してください。  


## engineファイルについて
engineファイルである lpdnet.engine は、[lpdnet-on-tao-toolkit](https://github.com/latonaio/lpdnet-on-tao-toolkit)と共通のファイルであり、当該レポジトリで作成した engineファイルを、本リポジトリで使用しています。  
