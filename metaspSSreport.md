Metasploitable サービススキャン調査レポート

対象ホスト情報
- IPアドレス：192.168.56.104
- スキャン日時：2025年6月18日
- 使用ツール：nmap
- スキャンコマンド：nmap -sS -sV -O -T4 192.168.56.104 -oN scan_report.txt


スキャン結果（抜粋）

| ポート | サービス | バージョン	 | 備考（脆弱性候補）            |
| 21/tcp | FTP      | vsftpd 2.3.4       | CVE-2011-2523（バックドア）   |
| 22/tcp | SSH      | OpenSSH 4.7p1      | 弱い鍵交換方式の可能性あり    |
| 23/tcp | Telnet   | Linux telnetd      | パスワードが平文              |
| 80/tcp | HTTP     | Apache 2.2.8       | Directory Traversal脆弱性候補 |
| 139/tcp| Samba    | smbd 3.0.20        | CVE-2007-2447（ユーザ名RCE）  |


考察

- vsftpdは既知CVEがあるため、最も優先度が高い侵入口である
- Sambaは手動Exploit可能で再現性が高い
- ApacheなどWeb系は今後DVWA導入後の攻撃対象に予定


今後の計画

- vsftpd攻撃を手動で再現（CVE-2011-2523）
- SambaへのRCE実験（CVE-2007-2447）
- Web攻撃用にDVWAを導入して調査
- 防衛視点：iptablesで不審IPを遮断