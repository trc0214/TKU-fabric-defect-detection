# TKU Fabric Defect Detection

本專案提供影像/影片瑕疵偵測的完整流程（資料讀取、訓練、推論、後處理、指標與視覺化、影片輸出）。

## 資料夾與檔案放置說明
- `texture_train_images/`
	- 放置訓練與測試的範例影像與對應標準答案（地真值）。
	- 必要檔名（灰階影像）：
		- `image1.png`, `image2.png`
		- `image1_groundtruth.png`, `image2_groundtruth.png`（地真值，黑=缺陷 0、白=背景 255）
	- 若資料夾格式打錯（如 `texture train images/`），Notebook 會自動嘗試容錯。

- `texture_test_images/`
	- 放置您要實際測試的新增影像（支援副檔名：png/jpg/jpeg/bmp/tif/tiff）。
	- 於 Notebook 的「推論與結果輸出」單元格中，會自動讀取此資料夾所有影像並輸出結果到 `texture_result_images/`。

- `texture_test_videos/`
    - 放置您要實際測試的新增影片 (支援副檔名：avi/mp4)。

- `tinyunet_weights.pth`
	- 模型權重檔（訓練後儲存、推論時載入以避免重訓）。
	- 已在 `.gitignore` 忽略，若需版本控管可改用 Git LFS。

## 使用步驟（簡述）
1. 將範例影像與地真值放入 `texture_train_images/`（或容錯資料夾）。
2. 開啟並依序執行 Notebook：
	 - 擴增與訓練（可選）
	 - 讀取影像與標準答案
	 - 儲存/載入模型權重（避免每次重訓）
	 - 影像偵測與結果儲存 + 指標 + 對比圖
	 - 影片偵測並輸出影片
3. 將欲測試的新影像放到 `texture_test_images/`，執行推論單元格以產生  `texture_result_images/` 的輸出。

## 重要約定
- 地真值遮罩約定：黑色（0）= 缺陷、白色（255）= 背景。
- 輸出遮罩遵循同樣約定，便於對比檢視與指標計算。