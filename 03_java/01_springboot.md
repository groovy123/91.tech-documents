# springbootについて

### ApplicationRunnerとCommandLineRunnerについて
|内容|ApplicationRunner|CommandLineRunner|
|--|--|--|
|メソッド| run(ApplicationArguments args) | run(String... args) |
|オプション引数|Springが提供|独自でパースする必要がある|
|非オプション引数|getNonOptionArgs()で取得|配列としてアクセス|
|実行順序|@Orderで制御|@Orderで制御|


### application.ymlファイルにprofileごとの設定を記述する
#### 1. ファイル分割による管理
```
src/main/resources/
  ├── application.yml
  ├── application-dev.yml
  └── application-prod.yml
```
application.yml（共通設定）
```yaml
spring:
  profiles:
    active: dev # デフォルトでdevプロファイルを有効化
server:
  port: 8080
```
application-dev.yml（開発用設定）
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/devdb
myapp:
  memo: This is dev.

```
application-prod.yml（本番用設定）
```yaml
spring:
  datasource:
    url: jdbc:mysql://prodhost:3306/proddb
myapp:
  memo: This is production.

```

#### 2. プロファイルの有効化
- デフォルトプロファイルはapplication.ymlでspring.profiles.activeを指定できます。
- 起動時にコマンドライン引数で上書きも可能です。
```bash
java -jar myapp.jar --spring.profiles.active=prod
```

#### 3. 設定ファイルのインポート・グループ化（Spring Boot 2.4以降）
- spring.config.importで他のYAMLファイルをインポートできます。
- spring.profiles.groupを使うと、複数の設定ファイルをグループ化して読み込ませることもできます
```yaml
spring:
  profiles:
    group:
      local:
        - common
        - local
      staging:
        - common
        - staging

```

#### 複数プロファイル指定時の注意
- 複数プロファイルを指定した場合、指定した順に設定が上書きされ、「後勝ち」となります
- 例えば--spring.profiles.active=a,bの場合、application-a.ymlの後にapplication-b.ymlが読み込まれ、bの設定が優先されます。


### 一つのyamlファイルに複数の設定を記述する
#### 1. 共通設定とプロファイル固有設定の分離
```yaml
server:
  port: 8080
spring:
  datasource:
    username: user
    password: pass

---
spring:
  profiles: dev
  datasource:
    url: jdbc:h2:mem:devdb
    driver-class-name: org.h2.Driver

---
spring:
  profiles: prod
  datasource:
    url: jdbc:mysql://prodserver:3306/myapp
    driver-class-name: com.mysql.cj.jdbc.Driver

```