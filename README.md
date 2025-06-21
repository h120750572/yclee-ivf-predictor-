# yclee-ivf-predictor-
預測變數與其對成功率影響
1. 年齡（Age）
影響機率：

年齡為最關鍵變項之一，隨年齡增加，懷孕率與活產率下降，流產率上升。

特別在 ≥40 歲女性中，自然流產率接近 30%，活產率低於 20%。

資料來源：

2022年《111年人工生殖施行結果分析報告》（臺灣國健署）：

活產率由 <35歲女性的 45.5%（冷凍胚胎）降至 >40歲女性的 15.6%
。

Practice Committee of ASRM. Fertil Steril. 2020;114(6):1232-1242.

女性年齡是胚胎染色體異常與流產率的主要風險因子。

2. 胚胎類型（Fresh vs. Frozen Embryo Transfer）
影響機率：

在所有年齡層中，冷凍胚胎移植的懷孕率與活產率普遍優於新鮮胚胎。

特別在 <35 歲女性，冷凍胚胎活產率為 45.5%，新鮮胚胎為 29.1%。

資料來源：

2022臺灣人工生殖報告：冷凍胚胎成功率顯著高於新鮮胚胎
。

Chen ZJ et al., NEJM 2016; 374:1310–1320

冷凍胚胎移植在非多囊性卵巢女性中提供更高的活產率與較低的OHSS風險。

3. AMH 值（Anti-Müllerian Hormone）
影響機率：

AMH 代表卵巢儲備力，數值越高代表可取得卵數越多。

AMH >3.5 ng/mL 可輕微提升活產率，低於 1 ng/mL 為卵巢功能衰退指標。

文獻依據：

Broer SL et al., Hum Reprod Update. 2014;20(6):688-701.

AMH 在預測卵數與活產率中有中等相關性，建議與年齡結合使用。

La Marca A, et al. Fertil Steril. 2010;93(3):911-918.

4. BMI（Body Mass Index）
影響機率：

高於30或低於18.5會降低懷孕與活產率，並增加流產、早產與妊娠併發症風險。

正常 BMI（18.5–24.9）者有較佳的胚胎植入與懷孕結果。

文獻依據：

Luke B, et al. N Engl J Med. 2011;364:256-265.

肥胖女性在試管嬰兒中的臨床懷孕率與活產率顯著下降。

Best D, et al. Hum Reprod. 2012;27(2):457-467.

BMI 是 IVF 預後模型的關鍵因子之一。

5. 多胞胎率、性別分布、先天缺陷機率
多胞胎率：

單胚胎植入活產中，84.8%為單胎，15%為雙胎，0.2%為三胎

多胎風險與植入胚胎數正相關。

性別比例：

男嬰：53.1%、女嬰：46.9%（根據2022台灣活產數據）

先天缺陷機率：

整體先天外觀缺陷率為 1.0%，<1500g 早產兒高達 4.8%

資料來源：


臺灣《111年人工生殖施行結果分析報告》

Davies MJ et al., NEJM. 2012;366(19):1803-1813.

IVF 兒童在早產與先天缺陷風險上略高於自然懷孕。

要將您的「試管嬰兒成功率預測工具」部署到 GitHub Pages 上，讓病患或大眾可透過網址直接試用、查閱，以下為完整圖文說明步驟：

✅ 一鍵部署「預測懷孕機」到 GitHub Pages
📁 準備階段：您需要
項目	說明
GitHub 帳號	若沒有帳號，請前往 https://github.com 註冊
ivf_predictor_static.html 檔案	即您已產出的靜態網頁（您自己用python生成）
基礎 Git 操作能力	可用 GitHub 網頁版或 GitHub Desktop 操作

🧱 步驟 1：建立 GitHub Repository
登入 GitHub → 點選右上角「+」→ 選擇「New repository」

命名為例如：ivf-predictor

⚠️ 選擇「Public」+ ✅ 勾選「Add a README file」

點選「Create repository」

🧰 步驟 2：上傳 ivf_predictor_static.html
方法 A：直接上傳
點選「Add file」→「Upload files」

上傳 ivf_predictor_static.html（你可從下方連結下載）
👉 下載 html 檔

點選「Commit changes」

方法 B：用 Git 上傳（終端機）
bash
Copy
Edit
git clone https://github.com/你的帳號/ivf-predictor.git
cd ivf-predictor
cp /path/to/ivf_predictor_static.html index.html
git add .
git commit -m "Add IVF predictor tool"
git push origin main
🌐 步驟 3：啟用 GitHub Pages
點選 repository →「Settings」→ 左側點選「Pages」

在 Source 選項選擇：

分支：main

資料夾：/ (root)

點選「Save」

⏳ 幾分鐘後 GitHub 會顯示您的網站網址，例如：

arduino
Copy
Edit
https://your-username.github.io/ivf-predictor/
📲 分享與使用
✅ 貼給病人、朋友、社群或醫療同仁

✅ 可嵌入診所官網 iframe

✅ 可加上短網址（bit.ly / reurl.cc）
