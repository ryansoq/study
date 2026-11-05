# study

GPU 架構與 AI 模型的互動學習筆記。每一頁都是單一 HTML 檔，用動畫和逐步模擬把底層運作畫出來，直接用瀏覽器打開就能看。

🌐 **線上瀏覽：<https://ryansoq.github.io/study/>**

## 頁面

| 頁面 | 內容 | 連結 |
|---|---|---|
| **從 Work-item 到 SM** | OpenCL 的 NDRange / work-group / sub-group / work-item 如何對應到 NVIDIA、AMD、PowerVR、Mali 的硬體。5 步動畫：切 work-group → 派送 → 切 warp → SIMT 執行與 latency hiding → divergence；附名詞對照表與 occupancy 計算器 | [開啟](https://ryansoq.github.io/study/) |
| **SIMT 分支機制** | 同一段巢狀 `if / else`，逐步比較各家編譯器插入的指令與硬體狀態：NVIDIA SIMT stack 與 `BSSY` / `BSYNC`、AMD `EXEC` mask、PowerVR `CNDST` / `CNDEF` / `CNDEND` mask count、Mali `.reconverge`；另含迴圈與 waterfall 迴圈 | [開啟](https://ryansoq.github.io/study/SIMT_COND.html) |
| **Transformer 解剖** | 用一句五個字的例子，把 Transformer 每一步的數字算給你看：token 與向量、attention、multi-head、MLP / 殘差 / LayerNorm、生成，以及參數、算力和 KV cache 的估算 | [開啟](https://ryansoq.github.io/study/Transformer%20.html) |

### 舊版

| 檔案 | 說明 |
|---|---|
| [`index_v0.html`](https://ryansoq.github.io/study/index_v0.html) | 「從 Work-item 到 SM」第一版，只有 NVIDIA 與 AMD |
| [`OpenCL_NVIDIA_AMD Execution Model.html`](https://ryansoq.github.io/study/OpenCL_NVIDIA_AMD%20Execution%20Model.html) | 同上 |

## 涵蓋的硬體

| | NVIDIA | AMD | PowerVR | Arm Mali |
|---|---|---|---|---|
| 核心 | SM | CU / WGP | USC | Shader core |
| sub-group | warp = 32 | wavefront = 64（RDNA 為 32） | task ≤ 32（Type 2–4 ≤ 128） | warp = 16（Valhall） |
| divergence | SIMT stack → convergence barrier | `EXEC` mask | 每個 instance 的 mask count | 硬體管理，`.reconverge` |

## 本機瀏覽

```bash
git clone https://github.com/ryansoq/study.git
cd study
python3 -m http.server 8000   # 打開 http://localhost:8000
```

也可以直接雙擊 HTML 檔用瀏覽器打開。頁面只會從 Google Fonts 載入字型，沒有其他外部相依。

## 資料來源

各頁底部都列有引用來源，主要包括：

- Imagination：PowerVR Compute Development Recommendations、PowerVR Instruction Set Reference
- Arm：Mali / Immortalis GPU 規格表
- LLVM AMDGPU 後端原始碼（`SILowerControlFlow.cpp`）
- arXiv 2407.02944、2607.23402（NVIDIA 控制流程與 warp divergence）
- AnandTech、Chips and Cheese、Collabora、Mesa 的架構分析

> 部分組合語言與硬體行為是依公開文件推演的示意，不是真實編譯器輸出。各頁都有標註哪些地方是示意。
