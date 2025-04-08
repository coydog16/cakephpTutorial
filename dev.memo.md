2025/4/9--------------------------------------
◆Error：http://localhost/HelloCakePHP/hello

Not Found
The requested URL was not found on this server.

Apache/2.4.58 (Win64) OpenSSL/3.1.3 PHP/8.2.12 Server at localhost Port 80

1.確認したこと
  ApatchのAdmin画面には接続できる。
  templates/HelloCakePHP/hello.phpがあることも確認した。
  ControllerとTemplatesファイルにスペルミスはないはず。
  cakePHP4からはtemplatesの拡張子は.ctpではなく.phpとなっている

2.XamppのドキュメントルートをこのプロジェクトのcakePHPに変更して解決

  xamppのhttpd.confでdocument rootをE:\xampp\htdocs\cakePHP\cakephpTutorial\webrootに変更。

◆解決
開発プロジェクトを変える度にドキュメントルート変更しないといけないの？
それは面倒くさいということで、他のアクセス方法を検討。
Dockerでコンテナを作成すると後が楽そうだけど、時間がないので今回はXAMPPのApacheでバーチャルホストを設定。

E:\xampp\apache\conf\extra\httpd-vhosts.confに以下を追記

<VirtualHost *:80>
    DocumentRoot "e:/xampp/htdocs/cakePHP/cakephpTutorial/webroot"
    ServerName cakephp-tutorial.local
    <Directory "e:/xampp/htdocs/cakePHP/cakephpTutorial/webroot">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>

C:\Windows\System32\drivers\etc\hostsに以下を追記

127.0.0.1 cakephp-tutorial.local

これでhttp://cakephp-tutorial.local/でアクセスできるようになる。
※コントローラーはパスカルケースだがURLのルーティングではケバブケースに変換される。
　URLはルーティング設定で変更可。
----------------------------------------------