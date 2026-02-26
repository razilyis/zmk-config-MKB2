# zmk-config-MKB2 TouchPass プロジェクト概要

このドキュメントは、`zmk-config-MKB2` の `TouchPass` ブランチにおける構成と作業目標をまとめたものです。

## 1. プロジェクト構成

- **リポジトリ**: `zmk-config-MKB2`
- **ブランチ**: `TouchPass`
- **使用モジュール**: `zmk-module-TouchPass`
  - ローカルパス: `/Users/ryosaitoh/Desktop/git/zmk-module-TouchPass`

## 2. ハードウェア構成

### 左手側 (Central): MKB-L_FPM
指紋認証モジュール（Fingerprint Module）を搭載したユニットです。

- **モジュール名**: MKB-L_FPM
- **機能**:
  - 指紋認証によるセキュアなログイン/パスワード入力（TouchPass）
  - CDC-ACM UART (USB) によるシリアル通信
- **配線構成 (UART0)**:
  - **TX**: D4 (P0.04) → R502-A RX
  - **RX**: D5 (P0.05) ← R502-A TX
- **オーバーレイ**: [MKB_L_FPM.overlay](file:///Users/ryosaitoh/Desktop/git/zmk-config-MKB2/boards/shields/MKB/MKB_L_FPM.overlay)

### 右手側 (Peripheral): MKB-R_TB
トラックボールモジュールを搭載したユニットです。

- **モジュール名**: MKB-R_TB
- **機能**:
  - トラックボールによるポインティング操作 (PMW3610)
- **配線構成 (SPI)**:
  - **SCK**: P1.13
  - **MOSI/MISO**: P0.04 (3-wire SPI)
  - **IRQ**: D5 (P0.05)
  - **CS**: D7 (P0.28)
- **オーバーレイ**: [MKB_R_TB.overlay](file:///Users/ryosaitoh/Desktop/git/zmk-config-MKB2/boards/shields/MKB/MKB_R_TB.overlay)

## 3. 今後の作業内容

1. **TouchPass モジュールの統合確認**:
   - `west.yml` における `zmk-module-TouchPass` の参照設定が正しいか確認。
   - すでにローカルパスで設定済み：`/Users/ryosaitoh/Desktop/git/zmk-module-TouchPass`

2. **ファームウェアのビルド**:
   - 左手側: `MKB_L_Base` + `MKB_L_FPM`
   - 右手側: `MKB_R_Base` + `MKB_R_TB`
   - 設定リセット用ファームウェアのビルド

3. **TouchPass 機能の動作確認**:
   - 指紋認証モジュールの動作およびシリアル通信の確認。

---

> [!NOTE]
> 左手側の UART ピン (P0.04, P0.05) は、I2C0 と競合するため、オーバーレイで `i2c0` を無効化しています。
