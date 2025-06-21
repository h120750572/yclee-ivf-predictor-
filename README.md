# yclee-ivf-predictor-
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


預測變數與其對成功率影響
1. AMH 對活產率的預測效度
Hum Reprod Update
. 2014 Jul-Aug;20(4):560-70. doi: 10.1093/humupd/dmu003. 系統回顧指出 AMH 與活產率具中等相關性，可作為預測輔助之一 


另有研究指出 AMH 獨立於年齡，能提供活產預後資訊，但其獨立預測力「有限」。

📌 結論：AMH 是有力的卵巢儲備指標，但預測活產率須搭配其他變項 (如年齡)。

2. BMI 升高對 IVF 預後的影響
Luke et al., Hum Reprod 2011 系列文章使用大規模 SART 資料庫，顯示高 BMI （≥30）與 IVF 活產率下降有顯著負相關，且流產率增加 
Fertil Steril  2018;109:258–65.
Hum Reprod. 2011 Jan;26(1):245-52. doi: 10.1093/humrep/deq306. Epub 2010 Nov 11.
。

2019 年對 21 項研究的系統回顧也指出肥胖者 IVF 活產率顯著低於正常體重者 (RR≈0.85) 。

📌 結論：BMI 異常（過重或肥胖）確實與較差 IVF 預後相關。

3. 冷凍胚胎 vs 新鮮胚胎之成功率比較
多篇 RCT 及 Meta-analysis（如 Chen ZJ et al., NEJM 2016）指出冷凍胚胎移植（FET）相較新鮮胚胎在活產率上有優勢，也因為較低 OHSS 風險而常推薦使用。

雖未列入 tool 中，但我所用年齡分層新鮮 vs 冷凍數據，來源於2024年公告 台灣《111年人工生殖施行結果分析報告》。建議您如欲學術引用，可參考該官方報告或 Chen ZJ 等研究進行補強。
N Engl J Med 2016;375:523-533 DOI: 10.1056/NEJMoa1513873


📌 結論：國內外研究一致支持冷凍胚胎成功率較新鮮高。

4. 多胞胎率、性別分佈與先天缺陷機率
多胞胎率：依據 ART 報告資料（如美國 NEJM 報告）約為 36% 雙胞胎、較低的三胞胎率 
Fertil Steril. 2017 Apr;107(4):868-877. doi: 10.1016/j.fertnstert.2017.02.114.
N Engl J Med 2013;369:2218-2225 DOI: 10.1056/NEJMoa130146
，類似工具中假設的「15%雙胎」為保守取值（僅單胎活產群）。

性別比率：一般自然與 IVF 存活嬰性別為約男 51–53%、女 47–49%；我採用 53.1% 為中間取值。

先天缺陷率：根據 Davies MJ et al., NEJM 2012，IVF 兒童與自然懷孕組相比略高，但整體低於約2%（我採約1%作平均估算，可視需要進一步文獻補強）。
N Engl J Med 2016;375:523-533 DOI: 10.1056/NEJMoa1513873

📌 結論：以上估算為依據文獻與大型報告推估之合理值，仍可依實際族群做調整。
ps:建議每年根據國家公報調整 根據各自機構常規校正 有意見跟自己的主治醫師討論 統計值不是你個人真實環境數值 僅供參考不得為醫療決策唯一指標 應跟醫師討論！
