sleepi2-monitor
====================

slee-Pi 2 でシステムの監視を行うためのツール類を提供します。

## 提供ファイル  
次のファイルがパッケージに含まれています。

* /usr/sbin/sleepi2mon  
  slee-Pi 2 のパワーマネジメントモジュールを監視するためのツールです。  
  設定可能な項目を次に示します。

  -D : デーモンとして動作します。  

* /usr/share/doc/sleepi2-monitor/copyright  
  著作権とライセンスを記載したファイルです。  

* /usr/share/doc/sleepi2-monitor/changelog.Debian.gz  
  パッケージの変更履歴を記録したファイルです。  

* /etc/sleepi2-monitor.conf  
  slee-Pi 2 の監視動作の設定を行うためのファイルです。  
  設定可能な項目は各セクションに分かれています。  

  + [common]  
    共通設定のセクションです。  
    - interval  
      監視動作のインターバルです。  
      単位は [秒] です。  
      無効にするには 0 を指定します。  
      デフォルトは 1 です。  

  + [switch]  
    SW1 の監視動作を設定するセクションです。  
    - command  
      SW1 のカウントが threshold を上回った場合に実行されるコマンドです。  
      デフォルトは "shutdown -h now" です。  

    - oneshot  
      command の実行方法を設定します。  
      true または false を指定します。  
      デフォルトは true です。  
      実行条件が満たされた場合に command は一度だけ実行されます。  
      実行条件が満たされている場合に command を繰り返し実行するには false を指定します。  

    - threshold  
      SW1 のカウントが指定値を上回った場合に command が実行されます。  
      単位は [秒] です。  
      無効にするには 0 を指定します。  
      デフォルトは 3 です。  
      最大値は 255 です。  

  + [extin]  
    外部信号入力コネクタ（CN3） の監視動作を設定するセクションです。  
    - command  
      外部信号入力のカウントが threshold を上回った場合に実行されるコマンドです。  
      デフォルトは "shutdown -h now" です。  

    - oneshot  
      command の実行方法を設定します。  
      true または false を指定します。  
      デフォルトは true です。  
      実行条件が満たされた場合に command は一度だけ実行されます。  
      実行条件が満たされている場合に command を繰り返し実行するには false を指定します。  

    - threshold  
      外部信号入力のカウントが指定値を上回った場合に command が実行されます。  
      単位は [秒] です。  
      無効にするには 0 を指定します。  
      デフォルトは 0 です。  
      最大値は 255 です。  

  + [voltage]  
    電源電圧の監視動作を設定するセクションです。  
    ハードウェアの構造上、CN1, CN2 の高いほうの電圧が検出されます。  
    - command  
      電源電圧が threshold を下回った場合に実行されるコマンドです。  
      デフォルトは "shutdown -h now" です。  

    - oneshot  
      command の実行方法を設定します。  
      true または false を指定します。  
      デフォルトは true です。  
      実行条件が満たされた場合に command は一度だけ実行されます。  
      実行条件が満たされている場合に command を繰り返し実行するには false を指定します。  

    - threshold  
      電源電圧が指定値を下回った場合に command が実行されます。  
      単位は [mV] です。  
      無効にするには 0 を指定します。  
      デフォルトは 0 です。  
      最大値は 65535 です。  

* /lib/systemd/system/sleepi2-monitor.service  
  slee-Pi 2 の監視サービスを実行するためのファイルです。  
  sleepi2mon をデーモンとして動作させます。  
