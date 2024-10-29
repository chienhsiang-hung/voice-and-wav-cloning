# voice-and-wav-cloning
## Quick Start
Local use:
> `git clone https://github.com/chienhsiang-hung/voice-and-wav-cloning.git`

Colab use:
> Click the ![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg) in each section below [Pipeline](#Pipeline).

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
#### 1. Lip Sync Video
( 如果有乾淨影片檔，建議選這一個方法 ) 實現高精度的唇形同步技術
a. 開啟 [Wav2Lip_simplified_v5.ipynb](Wav2Lip_simplified_v5.ipynb) [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chienhsiang-hung/voice-and-wav-cloning/blob/main/Wav2Lip_simplified_v5.ipynb)
b. 上傳欲 lip sync 的參考影片
c. 上傳欲 lip sync 的音檔
d. Inference
e. 下載 Output 影片

Ref: [Rudrabha/Wav2Lip](https://github.com/Rudrabha/Wav2Lip)
#### 2. Faceless video generator
( 如果只有相片的話，選這一個方法 ) 通過音頻驅動單張圖像生成逼真的3D說話人臉動畫

a. 安裝依賴項：首先安裝必要的庫和工具。這個過程大約需要五分鐘。
b. 上傳源圖像：你可以使用本地庫中的現有圖像或上傳自己的圖像。這張圖像將作為動畫面部的基礎。
c. 生成腳本 (optional)：使用OpenAI根據你選擇的主題生成腳本。或者，你也可以手動輸入腳本。
d. 使用TTS生成音頻 (optional)：使用文本轉語音（TTS）模型如gTTS生成音頻。請注意，gTTS通常生成女性聲音，如果你需要不同的聲音，可能需要探索其他TTS模型。( 請直接使用我們 [Pipeline](#Pipeline) 中 [Text to speech](#Text-to-speech) 的音檔 )
e. 生成視頻：當圖像和音頻準備好後，在筆記本中運行視頻生成步驟以生成無面視頻。這個過程大約需要5到10分鐘。
f. 下載視頻：運行筆記本中的最後一個單元格以創建可播放的視頻，並可以下載供個人使用。

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
