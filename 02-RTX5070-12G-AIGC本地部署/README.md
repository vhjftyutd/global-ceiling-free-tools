# RTX 5070 12G AIGC 本地部署指南

> 目标：在 12GB 显存甜点卡上跑通高质量本地图像 / 视频 / LLM 工作流，优先免费开源方案。

## 核心结论

12GB 显存属于**甜点级本地 AIGC**，不是满血天花板：

- 图像：1024×1024 的 SDXL / SD3.5 Medium / FLUX.1 量化版可流畅运行
- LLM：7B–14B Q4/Q5 可跑，上下文建议控制在 4K–8K
- 视频：优先 480p–720p 短片段（LTX-Video、Wan 1.3B、AnimateDiff 等）

**推荐主组合**：ComfyUI + FLUX.1 schnell（GGUF/FP8）+ SDXL + SD3.5 Medium + LM Studio / Ollama

## 第一梯队工具清单

| 类别 | 工具 | 说明 |
|------|------|------|
| 工作流天花板 | ComfyUI | 节点式，生态最强，支持 FP8/NVFP4 降显存 |
| 图像质量 | FLUX.1 schnell / dev GGUF | schnell 商用友好（Apache 2.0），dev 质量更高需量化 |
| 生态与稳定 | SDXL + SD3.5 Medium | SDXL 生态最丰富，SD3.5 Medium 对 8–12G 友好 |
| 低门槛 | Fooocus / Forge / InvokeAI | 不想学节点时的选择 |
| 本地 LLM | LM Studio / Ollama / AnythingLLM | 图形化或 API，适合隐私知识库 |
| 云端兜底 | NVIDIA NIM | 免费原型调用 FLUX / SD3.5 / SDXL 等 |
| 视频尝鲜 | LTX-Video、Wan 1.3B、AnimateDiff | 短片段、低分辨率优先 |
| 音频 | ACE-Step、MusicGen、Whisper、GPT-SoVITS | 本地免费可跑 |

## 三套可抄组合

### 方案 A：零折腾云端
NVIDIA NIM + Hugging Face Spaces + 免费多模态入口。不吃显存，适合验证提示词。

### 方案 B：本地图像主力（最推荐）
ComfyUI + FLUX.1 schnell GGUF/FP8 + SDXL + SD3.5 Medium。  
设置建议：1024×1024、batch=1、FP8 或 GGUF Q4–Q8、分步放大。

### 方案 C：本地文本 + 知识库
LM Studio 或 Ollama 跑 7B/14B Q4 + AnythingLLM 做 RAG。系统内存建议 32GB+。

## 12G 显存边界参考

| 任务 | 推荐模型 | 量化 | 建议参数 |
|------|----------|------|----------|
| 图像 | FLUX schnell / SDXL / SD3.5 Medium | GGUF Q4–Q8 / FP8 | 1024，batch=1 |
| 高质量图像 | FLUX.1 dev | GGUF Q4/Q8 | 分步放大 |
| LLM | 7B–14B | Q4/Q5 | 4K–8K 上下文 |
| 视频 | LTX / Wan 1.3B | FP8/量化 | 480p–720p，短片段 |

## 许可证提醒

- FLUX.1 schnell：Apache 2.0，商用相对友好
- FLUX.1 dev：偏非商用，商用需确认
- SDXL / SD3.5：各自社区许可证，商用前查官方

## 获取方式

- GitHub 搜索 ComfyUI、Fooocus、InvokeAI、Ollama、LM Studio
- ComfyUI Manager 安装插件与模型节点
- NVIDIA 开发者计划注册后使用 NIM
- Hugging Face / Civitai 下载模型时务必看许可证与 NSFW 标记

更多详细参数、安装步骤与工作流模板将在本目录持续补充。
