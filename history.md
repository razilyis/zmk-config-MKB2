# History

## 2026-03-05
- **目的**: MKB2 の `TouchPass` ブランチにて、基本の ZMK を `v0.3-branch` に更新し、PMW3610 ドライバを `dev-v0.3_against-runaway` に変更する。
- **実施内容**:
    - `config/west.yml` の `zmk` プロジェクトを `zmkfirmware` の `v0.3-branch` に変更。
    - `zmk-pmw3610-driver` を `TouchPass` (razilyis) の `dev-v0.3_against-runaway` に変更。
- **影響範囲**: ZMKコアバージョンおよびPMW3610ドライバの動作。
- **動作確認方法**: CIビルドが問題なく通ること、および実機にてトラックボールのレイヤー閾値機能が意図通り動くかの確認。
- **次の候補**: 新しいPMW3610ドライバの挙動テストおよび閾値パラメーターの調整。

## 2026-02-25
- **目的**: Keymap Editor (GUI) での利便性向上のため、Behavior 定義を外部インクルードから直接記述に変更。
- **実施内容**:
    - `config/mkb.keymap`:
        - `#include <layout_shift_kp_override.dtsi>` を削除。
        - `behaviors` ブロックに `touchpass` および `Layout Shift` 関連の全定義を直接展開。
        - 外部モジュールを編集せずに GUI で全ての Behavior が編集可能になった。
    - `boards/shields/MKB/MKB_L_FPM.overlay`:
        - `#include <behaviors/touchpass.dtsi>` を削除（Keymap 側で定義されるため）。
- **影響範囲**:
    - `TouchPass` ブランチのビルド成果物。
    - Keymap Editor での操作。
- `TouchPass` ブランチにて `MKB_R_ENC.conf` および `MKB_R_JOY` 関連ファイルを修正。
  - `MKB_R_ENC.conf`: `CONFIG_EC11=y` を追加。
  - `MKB_R_JOY.conf`: `CONFIG_EC11=y` を追加。
  - `MKB_R_JOY.overlay`: ジョイスティックと競合するマトリックスピン (D2, D3) を除外。
- `main` ブランチを `upstream/main` と同期。
