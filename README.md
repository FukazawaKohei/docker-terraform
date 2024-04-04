# Docker上にterraform環境を構築

dockerとterraformなどプロジェクトのインフラ部分を担う想定です。  
mysqlに関してはおまけとなっております。

## なぜDocker上にterraform環境を構築するのか？
ローカルマシンのOS、CPUアーキテクチャ差異による環境構築の手間を省くメリットがあります。  
また、複数のプロジェクトを横断する際にローカルマシン上にterraform環境を構築していると  
プロジェクト毎にterraformのバージョン差があると切替が面倒だからです。

### ・AWSアカウントについて
terraformで使用されるAWSアカウントはセキュリティの観点からインフラプロジェクトに記載すべきではないため  
ローカルマシンにあるAWSアカウントを使用するように構築しています。  
AWSアカウントの設定がお済みではない方は「aws cli プロファイル 作成」で検索して設定をお願いいたします。

## dockerコンテナ ビルド
```
# docker-compose build
```

## dockerコンテナ 立ち上げ
```
# docker-compose up -d mysql terraform
```

## terraformコンテナへ接続
接続後のディレクトリはsrc配下となっています。
```
# docker-compose exec terraform bash
```

### ・接続後aws、terraformがインストールされているか確認
```
# terraform --version
Terraform v1.7.5
on linux_amd64

# aws iam get-user
{
    "User": {
        "Path": "/",
        "UserName": "hogehoge",
        "UserId": "(省略)",
        "Arn": "arn:aws:iam::(省略):user/hogehoge",
        "CreateDate": "2024-03-03T13:05:45+00:00",
        "PasswordLastUsed": "2024-03-24T09:42:06+00:00"
    }
}
```
