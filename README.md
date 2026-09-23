# PRISM PATH ─ プリズム・パス

**A single-file thinking puzzle about bending light.** ／ 1ファイルで遊べる、光を曲げる思考系パズル。

An **emitter** fires one beam of light. Tap a mirror to flip `/` ⇄ `\`, bend the beam by 90°,
and make **every lamp glow at the same time**.

| | |
|---|---|
| Genre | Logic / laser puzzle（思考系パズル） |
| File | `prism-path.html` — single file, zero dependencies, works offline |
| Modes | 40 procedurally generated levels ＋ endless Challenge (4 difficulties) |
| Screen | Portrait-first (smartphone), fully playable on PC |
| Save | Browser `localStorage` ＋ export / import transfer code |
| Sound | Web Audio synthesis, ON/OFF switch, haptics switch |
| Languages | 日本語 · English · 简体中文 · 한국어 · Español |
| License | MIT |

🌐 [English](#english) · [日本語](#日本語) · [简体中文](#简体中文) · [한국어](#한국어) · [Español](#español)
&nbsp;·&nbsp; A styled multilingual version of this document is included as **`README.html`**.

---

## English

### Overview
PRISM PATH runs entirely in a web browser — on a phone in portrait mode or on a desktop.
There is no build step, no framework, no CDN and no network access: keep the HTML file anywhere and double-click it.

### How to play
| Piece | Name | Behaviour |
|---|---|---|
| ▣ | Emitter | Fires the beam in one direction. Fixed. |
| ／＼ | Mirror | **Tap** to flip `/` ⇄ `\`. Bends light by 90°. |
| ⧅ (violet) | Splitter | Splits light into *straight* + *sideways*. Cannot rotate. |
| ● | Lamp | Lights up when the beam hits it. Absorbs the beam. |
| ▨ | Wall | Blocks light. |

1. Light comes out of the emitter and travels in a straight line.
2. Tap mirrors to route the beam around walls.
3. All lamps must be lit **at the same time** — that clears the puzzle.
4. Rating: 3★ if moves ≤ par, 2★ if ≤ par + 5, otherwise 1★. Using a hint caps you at 2★ (2 hints → 1★). Undo costs nothing but does not lower par.

### Modes & difficulty
| Levels | Grid | Lamps | New element |
|---|---|---|---|
| Lv.1 – 3 | 4 × 5 | 1 | mirrors only |
| Lv.4 – 8 | 4 × 6 | 1 | walls appear |
| Lv.9 – 15 | 5 × 6 | 2 | **splitter** introduced |
| Lv.16 – 23 | 5 × 7 | 2 | longer routes |
| Lv.24 – 32 | 6 × 8 | 3 | more branches |
| Lv.33 – 40 | 7 × 9 | 3 | up to 10 mirrors |

**Challenge** mode generates a fresh random puzzle every round (Easy / Normal / Hard / Expert) and stores your best moves & time per difficulty. Levels unlock one by one as you clear them.

### Save data
Everything is stored locally in `localStorage` under the key **`prismpath.v1`**: unlocked levels, stars, best moves/time, Challenge records, language, sound & vibration switches. Nothing is uploaded anywhere.
* **Transfer:** Settings → *Export* gives a Base64 code; paste it into another device and use *Import*.
* **Reset:** Settings → *Delete* wipes all progress (confirmation required).
* Private / incognito windows may discard the save when closed.

### Getting started
1. Save the game as `prism-path.html`.
2. Double-click it (Chrome, Edge, Safari, Firefox — phone or PC).
3. Optional — serve it locally instead:
   ```bash
   python3 -m http.server 8080      # then open http://localhost:8080/prism-path.html
   npx serve .                      # Node alternative
   ```
4. Hosting on GitHub Pages / Netlify / any static bucket works as-is (single file, no API).

### Under the hood
* **Beam simulation** — a BFS over `(cell, direction)` states with a visited set, so mirror loops and splitter merges terminate cleanly. Each segment keeps its distance from the emitter and is rendered with a staggered CSS delay → the light visibly "flows".
* **Puzzle generation** — solution-first: a random beam tree is carved from the emitter (turns become mirrors, branches become splitters, leaves become lamps), then verified with the same simulator that runs during play. Decorative walls are placed only off-path. Finally every mirror is shuffled and rejected unless the position is *unsolved* and at least a few mirrors are wrong — so **every level shipped to you is guaranteed solvable**, and `par` equals the number of wrongly oriented mirrors.
* **Sound** — pure Web Audio oscillators (tap blip, per-lamp ping, 4-note fanfare). No audio files.
* **i18n** — one flat dictionary per language, applied by attribute; browser language is detected on first launch and can be overridden anytime.
* **Keyboard** — `U` undo · `H` hint · `R` reset (mouse/touch only otherwise).

### Requirements
| Platform | Browser | Notes |
|---|---|---|
| iPhone / iPad | Safari 14+ | portrait recommended; add to Home Screen for a full-screen feel |
| Android | Chrome 90+ / Edge / Samsung Internet | haptics need supported devices |
| Desktop | Chrome, Edge, Firefox, Safari (latest) | keyboard shortcuts available |

Requires JavaScript. No cookies, no tracking, no network calls after load.

### Troubleshooting
* **No sound** → tap the screen once (autoplay policy), then check the speaker icon and the OS mute switch.
* **Progress gone** → you were in a private window, or another browser/profile was used. Use an export code as backup.
* **Board looks small** → rotate to portrait; the board auto-fits both axes on resize.
* **Transfer code fails** → copy the whole code without line-breaks/quotes.

### Customise
| Constant | Meaning |
|---|---|
| `TOTAL` | number of levels (default 40) |
| `TIERS` / `ZEN` | grid size, lamp count, mirror budget, wall count per difficulty |
| `STORE` | localStorage key (`prismpath.v1`) — bump it when you change the save schema |
| `I18N` | one object per language; add a new key to all dictionaries + `LANGS` to add a language |
| `:root` CSS vars | colour theme (cyan beam / amber lamp / violet splitter) |

**License:** MIT. Icons, sound and generator are hand-written for this project — no third-party assets.

---

## 日本語

### 概要
PRISM PATH はブラウザだけで動く思考系パズルです。スマートフォンでは縦画面、PCではそのままダブルクリックで起動します。ビルドもライブラリも通信も不要な、単一HTMLファイル完結のゲームです。

### あそびかた
| 記号 | 名称 | はたらき |
|---|---|---|
| ▣ | エミッタ | 光を1方向に発射します（固定） |
| ／＼ | ミラー | **タップ**で `/` ⇄ `\` を反転。光を90°曲げます |
| ⧅（紫） | スプリッター | 光を「まっすぐ」と「直角」の2方向に分ける。回転しない |
| ● | ランプ | 光が当たると点灯し、光を吸収する |
| ▨ | 壁 | 光を通さない |

1. エミッタから出た光はまっすぐ進みます。
2. ミラーをタップして回り込み、光をランプへ導きます。
3. すべてのランプに**同時に**光が当たればクリアです。
4. 評価：手数≦目標で★3、≦目標+5で★2、それ以外で★1。ヒントを使うと星が減ります（1回で★2上限、2回で★1）。もどす操作は手数を戻せますが、目標値は下がりません。

### モードと難易度
| レベル | 盤面 | ランプ数 | 追加要素 |
|---|---|---|---|
| Lv.1 – 3 | 4 × 5 | 1 | ミラーのみ |
| Lv.4 – 8 | 4 × 6 | 1 | 壁が登場 |
| Lv.9 – 15 | 5 × 6 | 2 | **スプリッター**登場 |
| Lv.16 – 23 | 5 × 7 | 2 | 長距離ルート |
| Lv.24 – 32 | 6 × 8 | 3 | 分岐が増加 |
| Lv.33 – 40 | 7 × 9 | 3 | ミラー最大10個 |

**チャレンジ**モードは毎回ランダムに出題されるやり放題（かんたん／ふつう／むずかしい／エクスパート）。難易度別のベスト手数・タイムが記録されます。レベルはクリアごとに順次解放されます。

### セーブデータ
すべて端末内の `localStorage`（キー名 **`prismpath.v1`**）に保存されます：解放レベル・星・ベスト手数／タイム・チャレンジ記録・言語・サウンド／バイブ設定。外部への送信は一切ありません。
* **引き継ぎ**：設定 →「書出コード」でBase64文字列を取得 → 他の端末で「読込」。
* **リセット**：設定 →「削除」で全消去（確認あり）。
* シークレットモードではブラウザを閉じると消える場合があります。

### 起動方法
1. ゲーム本体を `prism-path.html` として保存します。
2. ダブルクリック（または共有→ブラウザで開く）するだけ。インストール不要です。
   ```bash
   python3 -m http.server 8080      # ローカル配信する場合 → http://localhost:8080/prism-path.html
   npx serve .                      # Node があればこちらでも
   ```
3. GitHub Pages / Netlify など静的ホスティングにそのまま置けます（API不要）。

### 技術メモ
* **光のシミュレーション** — `(マス, 向き)` を状態とする幅優先探索。訪問済み管理によりミラーのループやスプリッター合流でも停止します。各区間に発光源からの距離を保持し、CSSの遅延指定で「流れるように」描画します。
* **自動生成** — 解き優先方式。エミッタから光のツリーをランダムに掘り（曲がりをミラー、分岐をスプリッター、終端をランプ）、プレイ時と同じシミュレーターで全ランプ点灯を検証します。装飾の壁は光路外のみに配置。最後にミラーをシャッフルし、「未完成」かつ「誤りが一定数以上」の盤面だけを採用するため、**解けない問題が出ることはありません**。目標手数は「向きが間違っているミラーの数」です。
* **サウンド** — Web Audio のオシレータ合成のみ（タップ音・点灯音・クリアファンファーレ）。音声ファイルなし。
* **多言語** — 言語ごとにフラットな辞書を1つ持ち、属性を見て差し替えます。初回は端末言語を自動検出、以後いつでも変更できます。
* **キーボード** — `U` もどす · `H` ヒント · `R` やりなおし。

### 動作環境
| 環境 | ブラウザ | 備考 |
|---|---|---|
| iPhone / iPad | Safari 14+ | 縦画面推奨。「ホーム画面に追加」で全画面表示 |
| Android | Chrome 90+ / Edge / Samsung Internet | バイブは対応端末のみ |
| PC | Chrome / Edge / Firefox / Safari 最新 | キーボード操作可 |

JavaScript を有効にしてください。Cookie・追跡・通信はありません。

### つまずきやすい点
* **音が鳴らない** → 初回タップ後に鳴ります（自動再生規制）。スピーカーアイコンと端末のマナーも確認してください。
* **進行が消えた** → シークレットモード、または別のブラウザ／プロファイルの可能性があります。書出コードを保管しておくと安心です。
* **盤面が小さい** → 縦画面にすると盤面は横幅・高さの両方に合わせて自動調整されます。
* **引継ぎコードが読み込めない** → 引用符や改行を除き、最後までコピーしてください。

### カスタマイズ
| 定数 | 内容 |
|---|---|
| `TOTAL` | ステージ数（既定40） |
| `TIERS` / `ZEN` | 難易度別の盤面サイズ・ランプ数・ミラー予算・壁数 |
| `STORE` | localStorage キー。保存形式を変えたら版本号も上げる |
| `I18N` | 言語別辞書。`LANGS` と全辞書に追加すれば言語を増やせます |
| `:root` のCSS変数 | 配色テーマ（シアン＝光／アンバー＝ランプ／パープル＝分岐） |

**ライセンス：** MIT。アイコン・効果音・生成ロジックはすべて本プロジェクトの手書きで、第三者アセットは含みません。

---

## 简体中文

### 概览
PRISM PATH 是只在浏览器里运行的逻辑谜题：手机竖屏或电脑双击即可开始。没有构建步骤、没有依赖、不需要联网——把 HTML 文件放在任意位置打开即可。

### 玩法
| 图形 | 名称 | 作用 |
|---|---|---|
| ▣ | 发射器 | 朝固定方向射出光线 |
| ／＼ | 镜子 | **点击**在 `/` 与 `\` 之间切换，把光转折 90° |
| ⧅（紫） | 分束器 | 把光分成「直行」和「直角」两路，不可旋转 |
| ● | 灯泡 | 被光照射时点亮并吸收光线 |
| ▨ | 墙 | 阻挡光线 |

1. 光线从发射器沿直线射出。
2. 点击镜子绕开墙壁，把光引到灯泡。
3. 所有灯泡**同时**点亮即过关。
4. 评价：步数 ≦ 目标为 ★3，≦ 目标+5 为 ★2，其余 ★1。使用提示会降低星级（1 次上限 ★2，2 次上限 ★1）。撤销可退回步数，但目标值不变。

### 模式与难度
| 关卡 | 棋盘 | 灯泡数 | 新增要素 |
|---|---|---|---|
| Lv.1 – 3 | 4 × 5 | 1 | 仅有镜子 |
| Lv.4 – 8 | 4 × 6 | 1 | 出现墙 |
| Lv.9 – 15 | 5 × 6 | 2 | **分束器**登场 |
| Lv.16 – 23 | 5 × 7 | 2 | 更长的路线 |
| Lv.24 – 32 | 6 × 8 | 3 | 分支更多 |
| Lv.33 – 40 | 7 × 9 | 3 | 镜子最多 10 个 |

**挑战模式**每次随机出题，可无限游玩（简单／普通／困难／专家），并按难度保存最佳步数与时间。关卡随通关逐级解锁。

### 存档
所有数据保存在本机 `localStorage`，键名 **`prismpath.v1`**：已解锁关卡、星星、最佳步数／时间、挑战记录、语言、音效与震动设置。不会上传任何信息。
* **转移：** 设置 →「导出」得到 Base64 代码 → 在另一台设备「导入」。
* **重置：** 设置 →「删除」清空全部进度（有确认）。
* 无痕模式下关闭浏览器可能丢失存档。

### 启动方式
1. 把游戏保存为 `prism-path.html`。
2. 双击打开（或分享→用浏览器打开），无需安装。
   ```bash
   python3 -m http.server 8080      # 本地调试 → http://localhost:8080/prism-path.html
   npx serve .                      # 有 Node 时也可以
   ```
3. 可直接放到 GitHub Pages / Netlify 等静态托管（无需后端）。

### 技术说明
* **光线模拟** — 以 `(格子, 方向)` 为状态的广度优先搜索，配合已访问集合，镜子回路与分束合流都能正常终止。每段光束带有距光源的距离，用 CSS 延迟实现"流动"效果。
* **关卡生成** — 解题优先：先从发射器随机"挖"出一棵光树（转弯→镜子、分支→分束器、末端→灯泡），再用与游戏中完全相同的模拟器验证全部灯泡被点亮；装饰墙只放在光路之外。最后打乱镜子朝向，并只保留"未完成且错误数足够"的棋盘，因此**不会出现无解关卡**。目标步数＝朝向错误的镜子数量。
* **音效** — 仅用 Web Audio 振荡器合成（点击音、点亮音、通关号声），不含音频文件。
* **多语言** — 每种语言一份扁平词典，按属性替换；首次启动自动识别系统语言，之后可随时更改。
* **键盘** — `U` 撤销 · `H` 提示 · `R` 重来。

### 运行环境
| 平台 | 浏览器 | 说明 |
|---|---|---|
| iPhone / iPad | Safari 14+ | 建议竖屏，"添加到主屏幕"可全屏 |
| Android | Chrome 90+ / Edge / Samsung Internet | 震动仅部分设备支持 |
| 电脑 | Chrome / Edge / Firefox / Safari 最新版 | 支持键盘快捷键 |

需要启用 JavaScript。无 Cookie、无跟踪、加载后不发起网络请求。

### 常见问题
* **没有声音** → 先点一下屏幕（自动播放限制），再检查应用内喇叭图标与系统静音。
* **进度丢失** → 可能处于无痕模式或使用了另一个浏览器／配置，建议保存导出代码。
* **棋盘太小** → 请竖屏；棋盘会在宽、高两个方向自适应。
* **导入失败** → 去掉引行号与换行，完整复制整段代码。

### 自定义
| 常量 | 含义 |
|---|---|
| `TOTAL` | 关卡数（默认 40） |
| `TIERS` / `ZEN` | 各难度的棋盘尺寸、灯泡数、镜子预算、墙数 |
| `STORE` | localStorage 键名；改动存档结构时请更新版本号 |
| `I18N` | 各语言词典；同时在 `LANGS` 与全部词典中新增即可扩展语言 |
| `:root` CSS 变量 | 配色主题（青＝光束／琥珀＝灯泡／紫＝分束器） |

**许可：** MIT。图标、音效与生成算法均为本项目手写，不含第三方素材。

---

## 한국어

### 개요
PRISM PATH는 브라우저만으로 동작하는 퍼즐입니다. 스마트폰에서는 세로, PC에서는 더블클릭으로 바로 시작합니다. 빌드·라이브러리·통신이 필요 없는 단일 HTML 파일입니다.

### 게임 방법
| 그림 | 이름 | 설명 |
|---|---|---|
| ▣ | 방출기 | 한 방향으로 빛을 발사 (고정) |
| ／＼ | 거울 | **탭**하면 `/` ⇄ `\` 반전, 빛을 90° 꺾음 |
| ⧅ (보라) | 분할기 | 빛을 '직진'과 '직각' 두 방향으로 나눔. 회전하지 않음 |
| ● | 램프 | 빛이 닿으면 켜지고 빛을 흡수 |
| ▨ | 벽 | 빛을 막음 |

1. 방출기의 빛은 직진합니다.
2. 거울을 탭해 벽을 피해 램프로 안내합니다.
3. 모든 램프에 **동시에** 빛이 닿으면 클리어입니다.
4. 평가: 이동 수 ≦ 목표면 ★3, ≦ 목표+5면 ★2, 아니면 ★1. 힌트를 쓰면 별이 줄어듭니다(1회 ★2 제한, 2회 ★1). 되돌리기는 이동 수를 되돌릴 수 있지만 목표는 낮아지지 않습니다.

### 모드와 난이도
| 레벨 | 판 | 램프 수 | 추가 요소 |
|---|---|---|---|
| Lv.1 – 3 | 4 × 5 | 1 | 거울만 |
| Lv.4 – 8 | 4 × 6 | 1 | 벽 등장 |
| Lv.9 – 15 | 5 × 6 | 2 | **분할기** 등장 |
| Lv.16 – 23 | 5 × 7 | 2 | 긴 경로 |
| Lv.24 – 32 | 6 × 8 | 3 | 분기 증가 |
| Lv.33 – 40 | 7 × 9 | 3 | 거울 최대 10개 |

**챌린지** 모드는 매번 랜덤으로 출제되는 무한 모드(쉬움/보통/어려움/전문가)이며 난이도별 최고 이동 수·시간이 저장됩니다. 레벨은 클리어 순서대로 열립니다.

### 세이브 데이터
모두 기기 내부 `localStorage`(키 **`prismpath.v1`**)에 저장됩니다: 해금 레벨, 별, 최고 이동 수/시간, 챌린지 기록, 언어, 사운드·진동 설정. 외부 전송은 없습니다.
* **옮겨쓰기:** 설정 →「내보내기」로 Base64 코드 발급 → 다른 기기에서「불러오기」.
* **초기화:** 설정 →「삭제」로 전체 삭제(확인 있음).
* 시크릿 모드에서는 창을 닫으면 사라질 수 있습니다.

### 실행 방법
1. 게임을 `prism-path.html`로 저장합니다.
2. 더블클릭(또는 공유 → 브라우저로 열기)하면 끝. 설치 불필요.
   ```bash
   python3 -m http.server 8080      # 로컬 배포 → http://localhost:8080/prism-path.html
   npx serve .                      # Node 가 있으면 이것도 가능
   ```
3. GitHub Pages / Netlify 등 정적 호스팅에 그대로 올릴 수 있습니다(백엔드 불필요).

### 기술 메모
* **빛 시뮬레이션** — `(칸, 방향)` 상태를 쓰는 너비 우선 탐색. 방문 집합으로 거울 루프·분할기 합류도 안전하게 종료합니다. 구간의 광원 거리를 유지해 CSS 지연으로 '흐르는' 연출을 합니다.
* **퍼즐 생성** — 해답 우선 방식. 방출기에서 빛 트리를 무작위로 뚫고(꺾임→거울, 분기→분할기, 끝→램프) 게임 중 쓰는 것과 같은 시뮬레이터로 모든 램프 점등을 검증합니다. 장식 벽은 광로 밖에만 배치합니다. 마지막에 거울을 섞어 '미완성 + 오답 개수 충분'인 판만 채택하므로 **풀 수 없는 문제가 나올 수 없습니다.** 목표 이동 수 = 방향이 틀린 거울의 개수.
* **사운드** — Web Audio 발진기 합성만 사용(탭음·점등음·클리어 팡파르). 오디오 파일 없음.
* **다국어** — 언어별 플랫 사전 하나, 속성 기반으로 치환. 첫 실행 시 기기 언어 자동 감지, 언제든 변경 가능.
* **키보드** — `U` 되돌리기 · `H` 힌트 · `R` 처음부터.

### 동작 환경
| 플랫폼 | 브라우저 | 비고 |
|---|---|---|
| iPhone / iPad | Safari 14+ | 세로 화면 권장, '홈 화면에 추가'로 풀스크린 |
| Android | Chrome 90+ / Edge / Samsung Internet | 진동은 지원 기기만 |
| PC | Chrome / Edge / Firefox / Safari 최신 | 키보드 단축키 지원 |

JavaScript 활성화가 필요합니다. 쿠키·추적·통신 없음.

### 자주 있는 문제
* **소리가 안 남** → 화면을 한 번 탭한 뒤 재생됩니다(자동재생 정책). 스피커 아이콘과 기기 음소거도 확인하세요.
* **기록이 사라짐** → 시크릿 모드이거나 다른 브라우저/프로파일일 수 있습니다. 내보내기 코드를 보관하세요.
* **판이 작음** → 세로 모드로 전환하세요. 판은 가로·세로 모두에 맞춰 자동 조정됩니다.
* **코드를 못 읽음** → 큰따옴표·줄바꿈 없이 전체를 복사하세요.

### 커스터마이즈
| 상수 | 의미 |
|---|---|
| `TOTAL` | 레벨 수 (기본 40) |
| `TIERS` / `ZEN` | 난이도별 판 크기, 램프 수, 거울 예산, 벽 수 |
| `STORE` | localStorage 키. 저장 구조를 바꾸면 버전도 올리기 |
| `I18N` | 언어별 사전. `LANGS`와 모든 사전에 추가하면 언어가 늘어남 |
| `:root` CSS 변수 | 색상 테마(시안=빛 / 앰버=램프 / 퍼플=분할기) |

**라이선스:** MIT. 아이콘·효과음·생성 로직은 모두 직접 작성했으며 서드파티 에셋은 없습니다.

---

## Español

### Resumen
PRISM PATH funciona solo en el navegador: en el móvil en vertical o en el PC con doble clic. Sin compilación, sin librerías y sin conexión: un único archivo HTML.

### Cómo jugar
| Símbolo | Nombre | Función |
|---|---|---|
| ▣ | Emisor | Dispara el rayo en una dirección (fijo) |
| ／＼ | Espejo | **Toca** para cambiar `/` ⇄ `\`. Gira la luz 90° |
| ⧅ (violeta) | Divisor | Parte la luz en *recto* + *lateral*. No gira |
| ● | Lámpara | Se enciende al recibir luz y la absorbe |
| ▨ | Muro | Bloquea la luz |

1. La luz del emisor viaja en línea recta.
2. Toca los espejos para esquivar muros y llegar a las lámparas.
3. Todas las lámparas deben encenderse **a la vez**.
4. Puntuación: 3★ si movimientos ≤ objetivo, 2★ si ≤ objetivo + 5, si no 1★. Las pistas limitan las estrellas (1 pista → máx. 2★, 2 pistas → 1★). Deshacer devuelve movimientos pero no baja el objetivo.

### Modos y dificultad
| Nivel | Cuadrícula | Lámparas | Novedad |
|---|---|---|---|
| Nv.1 – 3 | 4 × 5 | 1 | solo espejos |
| Nv.4 – 8 | 4 × 6 | 1 | aparecen muros |
| Nv.9 – 15 | 5 × 6 | 2 | entra el **divisor** |
| Nv.16 – 23 | 5 × 7 | 2 | rutas más largas |
| Nv.24 – 32 | 6 × 8 | 3 | más ramificaciones |
| Nv.33 – 40 | 7 × 9 | 3 | hasta 10 espejos |

El modo **Desafío** genera un puzzle aleatorio en cada ronda (Fácil / Normal / Difícil / Experto) y guarda tu mejor marca por dificultad. Los niveles se desbloquean de uno en uno.

### Datos guardados
Todo se guarda en el propio dispositivo, en `localStorage`, con la clave **`prismpath.v1`**: niveles desbloqueados, estrellas, mejores movimientos/tiempo, registros del Desafío, idioma y ajustes de sonido/vibración. No se envía nada a ningún servidor.
* **Transferir:** Ajustes → *Exportar* da un código Base64; pégalo en otro dispositivo y usa *Importar*.
* **Reiniciar:** Ajustes → *Borrar* elimina todo (con confirmación).
* En modo incógnito el avance puede perderse al cerrar la ventana.

### Empezar
1. Guarda el juego como `prism-path.html`.
2. Ábrelo con doble clic (o Compartir → Abrir en navegador). Sin instalación.
   ```bash
   python3 -m http.server 8080      # servir en local → http://localhost:8080/prism-path.html
   npx serve .                      # alternativa con Node
   ```
3. Vale cualquier hosting estático (GitHub Pages, Netlify…): no necesita API.

### Bajo el capó
* **Simulación de luz** — BFS sobre estados `(celda, dirección)` con conjunto de visitados: bucles de espejos y uniones del divisor terminan siempre. Cada tramo guarda su distancia al emisor y se pinta con retardo CSS escalonado: la luz «fluye».
* **Generación** — primero la solución: se talla un árbol de luz desde el emisor (giros → espejos, ramas → divisores, hojas → lámparas) y se verifica con el mismo simulador del juego. Los muros decorativos solo van fuera del recorrido. Al final se barajan los espejos y se descarta si la posición ya está resuelta o tiene pocos errores: **ningún puzzle es imposible**, y el objetivo equivale al número de espejos mal orientados.
* **Sonido** — osciladores Web Audio puros (toque, encendido, fanfarria). Sin ficheros de audio.
* **Idiomas** — un diccionario plano por idioma, aplicado por atributo; detecta el idioma del sistema y se puede cambiar cuando quieras.
* **Teclado** — `U` deshacer · `H` pista · `R` reiniciar.

### Requisitos
| Plataforma | Navegador | Notas |
|---|---|---|
| iPhone / iPad | Safari 14+ | mejor en vertical; «Añadir a pantalla de inicio» para verlo completo |
| Android | Chrome 90+ / Edge / Samsung Internet | vibración solo en dispositivos compatibles |
| PC | Chrome, Edge, Firefox, Safari actuales | atajos de teclado disponibles |

Requiere JavaScript. Sin cookies, sin rastreo, sin peticiones de red tras cargar.

### Problemas frecuentes
* **No suena** → toca la pantalla una vez (política de reproducción automática) y revisa el icono del altavoz y el silencioso del sistema.
* **Falta progreso** → puede que usaras modo incógnito u otro navegador/perfil. Guarda un código de exportación.
* **Tablero pequeño** → pon el teléfono en vertical; el tablero se ajusta a ancho y alto.
* **El código no se importa** → cópialo entero, sin comillas ni saltos de línea.

### Personalizar
| Constante | Significado |
|---|---|
| `TOTAL` | número de niveles (40 por defecto) |
| `TIERS` / `ZEN` | tamaño del tablero, lámparas, presupuesto de espejos y muros |
| `STORE` | clave de localStorage; súbelo si cambias el formato de guardado |
| `I18N` | diccionario por idioma; añade claves a todos + `LANGS` para un idioma nuevo |
| variables CSS `:root` | tema de color (cian=luz, ámbar=lámpara, violeta=divisor) |

**Licencia:** MIT. Iconos, sonido y generador escritos a mano para este proyecto; sin recursos de terceros.

---

<sub>Made with plain HTML · CSS · JavaScript — no frameworks, no tracking. · 単一ファイル / 依存ゼロ / オフライン動作</sub>
