# voice-and-wav-cloning
![GitHub followers](https://img.shields.io/github/followers/chienhsiang-hung)
![GitHub forks](https://img.shields.io/github/forks/chienhsiang-hung/voice-and-wav-cloning)
![GitHub Repo stars](https://img.shields.io/github/stars/chienhsiang-hung/voice-and-wav-cloning)
## Quick Start
Local use:
> `git clone https://github.com/chienhsiang-hung/voice-and-wav-cloning.git`

Colab use:
> Click the [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/chienhsiang-hung/voice-and-wav-cloning) in each section below [Pipeline](#Pipeline).

## Pipeline
### Text to speech
( 涵 fine-tune training )
1. 先從 Youtube 找尋素材影片跟聲音: [範例](https://m.youtube.com/watch?v=2cUEZfT6w3k)

<a id="my2"></a>

2. 先用 [colab_webui.ipynb](colab_webui.ipynb) ( 可參考 [GPT-SoVITS指南](https://www.yuque.com/baicaigongchang1145haoyuangong/ib3g1e/zqbopihzr6eqoyl8) ) [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chienhsiang-hung/voice-and-wav-cloning/blob/main/colab_webui.ipynb)

    a. 下載預訓練模型

    <a id="my2b"></a>

    b. 上傳音檔 -> 切割、降噪、標注
4. Training: [2.b.](#my2b) 的材料訓練
5. Inference: 提供參考音檔、音檔逐字稿、欲生成音檔的逐字稿

    - 範例使用 `test_e8_s128.pth`, `test-e15.ckpt`
6. 下載 Output 音檔 與 [2.](#my2) 訓練完畢的權重

Ref: [RVC-Boss/GPT-SoVITS](https://github.com/RVC-Boss/GPT-SoVITS)
### Speech to lip generation
以下提供兩種方法，都是純 inferencing
#### a. Lip Sync Video
( 如果有乾淨影片檔，建議選這一個方法 ) 實現高精度的唇形同步技術

1. 開啟 [Wav2Lip_simplified_v5.ipynb](Wav2Lip_simplified_v5.ipynb) [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chienhsiang-hung/voice-and-wav-cloning/blob/main/Wav2Lip_simplified_v5.ipynb)
2. 上傳欲 lip sync 的參考影片
3. 上傳欲 lip sync 的音檔
4. Inference
5. 下載 Output 影片

Ref: [Rudrabha/Wav2Lip](https://github.com/Rudrabha/Wav2Lip)
#### b. Faceless video generator
( 如果只有相片的話，選這一個方法 ) 通過音頻驅動單張圖像生成逼真的3D說話人臉動畫

1. 開啟 [FacelessColab.ipynb](FacelessColab.ipynb) [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chienhsiang-hung/voice-and-wav-cloning/blob/main/FacelessColab.ipynb)
2. 安裝依賴項：首先安裝必要的庫和工具。這個過程大約需要五分鐘。
3. 上傳源圖像：你可以使用本地庫中的現有圖像或上傳自己的圖像。這張圖像將作為動畫面部的基礎。
4. *生成腳本 (optional)：使用OpenAI根據你選擇的主題生成腳本。或者，你也可以手動輸入腳本。*
5. _使用TTS生成音頻 (optional)：使用文本轉語音（TTS）模型如gTTS生成音頻。請注意，gTTS通常生成女性聲音，如果你需要不同的聲音，可能需要探索其他TTS模型。( **請直接使用我們在 [Pipeline](#Pipeline) 中 [Text to speech](#Text-to-speech) 生成的音檔** )_
6. 生成視頻：當圖像和音頻準備好後，在筆記本中運行視頻生成步驟以生成無面視頻。這個過程大約需要5到10分鐘。
7. 下載視頻：運行筆記本中的最後一個單元格以創建可播放的視頻，並可以下載供個人使用。

Ref: [SamurAIGPT/AI-Faceless-Video-Generator](https://github.com/SamurAIGPT/AI-Faceless-Video-Generator) ( Utilized [OpenTalker/SadTalker](https://github.com/OpenTalker/SadTalker) )
## Env
上面步驟皆需要 ( Colab ) GPU 支援
### Colab runtime setting
![image](https://github.com/user-attachments/assets/9bf435ef-4296-4741-851e-1260447b9b7a)

Config: (Minimum requirements)
```json
{
    "Runtime type": "Python 3",
    "Hardware accelerator": "T4 GPU"
}
```
## 說明
### GPT-SoVITS
一個強大的網頁工具，用於語音轉換和文本轉語音（TTS），基於GPT模型。這個項目支持零樣本和少樣本微調，跨語言推理，並集成了多種語音處理和訓練工具。

主要功能包括：

- 零樣本TTS：輸入5秒鐘的聲音樣本，即可進行即時文本轉語音轉換。
- 少樣本TTS：只需1分鐘的訓練數據即可微調模型，提高語音相似度和真實感。
- 跨語言支持：可以在與訓練數據不同的語言中進行推理，目前支持英語、日語、韓語、粵語和中文。
- 這個項目還提供了語音伴奏分離、自動訓練集分割、中國語音識別（ASR）和文本標註等工具，幫助初學者創建訓練數據集和GPT/SoVITS模型。
### Wav2Lip
開源項目，旨在實現高精度的唇形同步技術。該項目基於一篇發表於2020年ACM Multimedia會議的論文《A Lip Sync Expert Is All You Need for Speech to Lip Generation In the Wild》。Wav2Lip 提供了完整的訓練和推理代碼、預訓練模型以及評估指標。

這個項目可以將任何語音與目標視頻中的唇形進行高精度同步，支持任何身份、語音和語言，甚至可以應用於CGI面孔和合成語音。用戶可以通過Google Colab Notebook快速開始使用，並且提供了多種評估基準和指標來測量唇形同步的精度。
### SadTalker
由西安交通大學的研究人員提出的項目，旨在通過音頻驅動單張圖像生成逼真的3D說話人臉動畫。該項目在2023年的CVPR會議上展示，並且已經集成到Discord中，允許用戶免費使用。SadTalker的主要功能包括生成高質量的視頻、支持多種模式（如靜態模式、參考模式和調整大小模式），並且可以從文本提示生成視頻。

該項目使用Apache 2.0許可證，並且已經移除了非商業限制。用戶可以通過克隆GitHub上的倉庫來下載SadTalker，並按照安裝指南進行安裝和使用。

如果你有任何問題，可以參考他們的FAQ或在GitHub上提交問題。
