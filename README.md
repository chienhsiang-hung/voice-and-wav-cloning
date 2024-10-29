# voice-and-wav-cloning
[GPT-SoVITS指南](https://www.yuque.com/baicaigongchang1145haoyuangong/ib3g1e/zqbopihzr6eqoyl8)
- 使用 `test_e8_s128.pth`, `test-e15.ckpt`

## Pipeline
### Text to speech
( 涵 fine-tune training )
1. 先從 Youtube 找尋[素材影片跟聲音](https://m.youtube.com/watch?v=2cUEZfT6w3k)
2. 先用 [colab_webui.ipynb](colab_webui.ipynb) ( 可參考 [GPT-SoVITS指南](https://www.yuque.com/baicaigongchang1145haoyuangong/ib3g1e/zqbopihzr6eqoyl8) )

    a. 下載預訓練模型
    b. 上傳音檔 -> 切割、降噪、標注
3. Training: `2.b` 的材料訓練
4. Inference: 提供參考音檔、音檔逐字稿、欲生成音檔的逐字稿
5. 下載 Output 音檔 與 `2.` 訓練完畢的權重

### Speech to lip generation
( 純 inferencing )
1. 上傳欲 lip sync 的參考影片
2. 上傳欲 lip sync 的音檔
3. Inference
4. 下載 Output 影片
