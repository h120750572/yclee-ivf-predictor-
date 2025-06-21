# yclee-ivf-predictor-

# 建立純 HTML + JavaScript 靜態版（不含 Flask）
static_html = """
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <title>試管嬰兒成功率預測工具</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #0066cc; }
        label, select, input { margin-top: 10px; display: block; }
        .result { margin-top: 20px; padding: 10px; background: #f0f8ff; border: 1px solid #ccc; }
    </style>
</head>
<body>
    <h1>試管嬰兒成功率預測工具（靜態版）</h1>

    <label for="age">年齡層：</label>
    <select id="age">
        <option value="<35">小於35歲</option>
        <option value="35-39">35-39歲</option>
        <option value="≥40">大於等於40歲</option>
    </select>

    <label for="type">胚胎類型：</label>
    <select id="type">
        <option value="fresh">新鮮胚胎</option>
        <option value="frozen">冷凍胚胎</option>
    </select>

    <label for="amh">AMH (ng/mL)：</label>
    <input type="number" step="0.1" id="amh" />

    <label for="bmi">BMI：</label>
    <input type="number" step="0.1" id="bmi" />

    <button onclick="predict()">預測</button>

    <div id="output" class="result"></div>

    <script>
        const stats = {
            '<35': {
                fresh: {pregnancy: 38.6, live_birth: 29.1},
                frozen: {pregnancy: 56.3, live_birth: 45.5},
                miscarriage: 15
            },
            '35-39': {
                fresh: {pregnancy: 27.0, live_birth: 18.1},
                frozen: {pregnancy: 46.4, live_birth: 34.8},
                miscarriage: 22
            },
            '≥40': {
                fresh: {pregnancy: 13.5, live_birth: 6.0},
                frozen: {pregnancy: 27.7, live_birth: 15.6},
                miscarriage: 30
            }
        };

        function predict() {
            const age = document.getElementById('age').value;
            const type = document.getElementById('type').value;
            const amh = parseFloat(document.getElementById('amh').value);
            const bmi = parseFloat(document.getElementById('bmi').value);

            let result = stats[age][type];
            let live_birth = result.live_birth;

            if (!isNaN(amh) && amh > 3.5) live_birth += 3;
            if (!isNaN(bmi) && (bmi < 18.5 || bmi > 30)) live_birth -= 3;

            const output = `
                <strong>懷孕率：</strong> ${result.pregnancy.toFixed(1)}%<br>
                <strong>活產率：</strong> ${live_birth.toFixed(1)}%<br>
                <strong>自然流產率：</strong> 約 ${stats[age].miscarriage}%<br>
                <strong>預估活產胎數：</strong> 單胎(85%) / 雙胎(15%)<br>
                <strong>性別比率：</strong> 男 53.1% / 女 46.9%<br>
                <strong>先天缺陷機率：</strong> 約 1.0%
            `;
            document.getElementById('output').innerHTML = output;
        }
    </script>
</body>
</html>
"""

# 儲存為 HTML 檔案
html_path = Path("/mnt/data/ivf_predictor_static.html")
html_path.write_text(static_html, encoding="utf-8")

html_path.name
Result
'ivf_predictor_static.html'

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

