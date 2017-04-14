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
      command の実行条件を設定します。  
      true または false を指定します。  
      デフォルトは true です。  
      threshold に設定された条件を満たした場合に

    - threshold  
      SW1 のカウントが指定値を上回った場合に command を実行します。  
      単位は [秒] です。  
      無効にするには 0 を指定します。  
      デフォルトは 1 です。  
      最大値は 255 です。  

  + [extin]  
    外部信号入力コネクタ（CN3） の監視動作を設定するセクションです。  

  + [voltage]  
    電源電圧の監視動作を設定するセクションです。  
    ハードウェアの構造上、CN1, CN2 の高いほうの電圧が検出されます。  

  + BUTTON_THRESHOLD  
    SW1 のカウントが指定値を上回った場合に BUTTON_ACTION を実行します。  
    単位は [秒] です。  
    無効にするには 0 を指定します。  
    デフォルトは 1 です。  
    最大値は 255 です。  

  + BUTTON_ACTION  
    SW1 のカウントが BUTTON_THRESHOLD を上回った場合に実行されるコマンドです。  
    デフォルトは "shutdown -h now" です。  

  + VOLTAGE_THRESHOLD  
    電源電圧が指定値を下回った場合に VOLTAGE_ACTION を実行します。  
    単位は [mV] です。  
    無効にするには 0 を指定します。  
    デフォルトは 0 です。  

  + VOLTAGE_ACTION  
    電源電圧が VOLTAGE_THRESHOLD を下回った場合に実行されるコマンドです。  
    デフォルトは "shutdown -h now" です。

  + HEARTBEAT_TIMEOUT  
    システムの応答がない場合に電源を再投入するまでの時間です。  
    単位は [秒] です。  
    無効にするには 0 を指定します。  
    デフォルトは 30 です。  

  + SHUTDOWN_DELAY  
    システムのシャットダウンが完了してから電源を遮断するまでの時間です。  
    単位は [秒] です。  
    無効にするには 0 を指定します。  
    デフォルトは 5 です。  

* /lib/systemd/system/sleepi2-monitor.service  
  slee-Pi 2 の監視サービスを実行するためのファイルです。  
  sleepi2mon をデーモンとして動作させます。  
