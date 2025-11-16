<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>SmartAgri-Box 全監控儀表板</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body { font-family: Arial, "Microsoft JhengHei", sans-serif; margin: 20px; background: #f5f5f5; }
    h1 { margin-bottom: 0; }
    .subtitle { font-size: 0.9em; color: #555; margin-bottom: 10px; }
    .cards { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 10px; }
    .card { background: #ffffff; border-radius: 10px; padding: 10px 12px; box-shadow: 0 2px 6px rgba(0,0,0,0.1); flex: 1 1 150px; min-width: 150px; }
    .card-title { font-size: 0.9em; color: #777; }
    .card-value { font-size: 1.4em; font-weight: bold; margin-top: 4px; }
    .card-status { font-size: 0.85em; margin-top: 4px; }
    .status-bad { color: #b30000; }
    .status-ok { color: #996600; }
    .status-good { color: #006600; }
    .charts { margin-top: 20px; display: flex; flex-direction: column; gap: 20px; }
    .chart-box { background: #ffffff; border-radius: 10px; padding: 15px; box-shadow: 0 2px 6px rgba(0,0,0,0.1); }
    #updateTime { margin-top: 8px; font-size: 0.85em; color: #666; }
  </style>
</head>
<body>
  <h1>SmartAgri-Box 全監控儀表板</h1>
  <div class="subtitle">資料來源：ThingSpeak Channel 3159969</div>
  <div id="updateTime">最後更新時間：讀取中...</div>

  <div class="cards">
    <div class="card"><div class="card-title">環境溫度</div><div class="card-value" id="val-temp">-- °C</div><div class="card-status" id="status-temp">--</div></div>
    <div class="card"><div class="card-title">相對濕度</div><div class="card-value" id="val-humi">-- %</div><div class="card-status" id="status-humi">--</div></div>
    <div class="card"><div class="card-title">光照 Lux</div><div class="card-value" id="val-lux">-- lux</div><div class="card-status" id="status-lux">--</div></div>
    <div class="card"><div class="card-title">土壤濕度</div><div class="card-value" id="val-soil">-- %</div><div class="card-status" id="status-soil">--</div></div>
    <div class="card"><div class="card-title">土壤溫度</div><div class="card-value" id="val-soilT">-- °C</div><div class="card-status" id="status-soilT">--</div></div>
  </div>

  <div class="charts">
    <div class="chart-box">
      <div class="chart-title">溫度 / 濕度</div>
      <canvas id="chartEnv"></canvas>
    </div>

    <div class="chart-box">
      <div class="chart-title">光照 Lux（含 200/500 門檻）</div>
      <canvas id="chartLux"></canvas>
    </div>

    <div class="chart-box">
      <div class="chart-title">土壤濕度 / 土壤溫度</div>
      <canvas id="chartSoil"></canvas>
    </div>
  </div>

  <script>
    const CHANNEL_ID = 3159969;
    const READ_API_KEY = "H0GEHP6Z8PPMTF2X";  /* ← 已幫你填好 */

    const RESULTS = 100;
    const url = `https://api.thingspeak.com/channels/${CHANNEL_ID}/feeds.json?results=${RESULTS}&api_key=${READ_API_KEY}`;

    const TEMP_LOW=15, TEMP_HIGH=30;
    const HUMI_LOW=40, HUMI_HIGH=70;
    const LUX_LOW=200, LUX_HIGH=500;
    const SOIL_DRY=30, SOIL_WET=70;

    let chartEnv=null, chartLux=null, chartSoil=null;

    function formatTime(iso){const t=new Date(iso);return `${t.getHours().toString().padStart(2,'0')}:${t.getMinutes().toString().padStart(2,'0')}`;}

    function setCard(idV,idS,value,low,high,unit){
      const V=document.getElementById(idV), S=document.getElementById(idS);
      if(isNaN(value)){V.textContent=`-- ${unit}`;S.textContent="--";S.className="card-status";return;}
      V.textContent=value.toFixed(unit==="%"?0:1)+" "+unit;

      S.className="card-status ";
      if(value<low){S.textContent="偏低";S.classList.add("status-bad");}
      else if(value>high){S.textContent="偏高";S.classList.add("status-ok");}
      else{S.textContent="正常";S.classList.add("status-good");}
    }

    function update(){
      fetch(url).then(r=>r.json()).then(data=>{
        const f=data.feeds;if(!f.length)return;

        const labels=[],temps=[],humis=[],luxs=[],soils=[],soilTs=[];
        f.forEach(e=>{
          labels.push(formatTime(e.created_at));
          temps.push(parseFloat(e.field1));
          humis.push(parseFloat(e.field2));
          luxs.push(parseFloat(e.field3));
          soils.push(parseFloat(e.field4));
          soilTs.push(parseFloat(e.field5));
        });

        const last=f[f.length-1];
        document.getElementById("updateTime").textContent="最後更新："+new Date(last.created_at).toLocaleString();

        setCard("val-temp","status-temp",parseFloat(last.field1),TEMP_LOW,TEMP_HIGH,"°C");
        setCard("val-humi","status-humi",parseFloat(last.field2),HUMI_LOW,HUMI_HIGH,"%");
        setCard("val-lux","status-lux",parseFloat(last.field3),LUX_LOW,LUX_HIGH,"lux");
        setCard("val-soil","status-soil",parseFloat(last.field4),SOIL_DRY,SOIL_WET,"%");
        setCard("val-soilT","status-soilT",parseFloat(last.field5),10,40,"°C");

        if(chartEnv)chartEnv.destroy();
        if(chartLux)chartLux.destroy();
        if(chartSoil)chartSoil.destroy();

        chartEnv=new Chart(document.getElementById("chartEnv"),{
          type:"line",
          data:{labels,datasets:[
            {label:"溫度 °C",data:temps,yAxisID:"y1"},
            {label:"濕度 %",data:humis,yAxisID:"y2"}
          ]},
          options:{responsive:true,scales:{
            y1:{type:"linear",position:"left"},
            y2:{type:"linear",position:"right",grid:{drawOnChartArea:false}}
          }}
        });

        chartLux=new Chart(document.getElementById("chartLux"),{
          type:"line",
          data:{labels,datasets:[
            {label:"Lux",data:luxs},
            {label:"門檻 200",data:luxs.map(()=>LUX_LOW),borderDash:[5,3]},
            {label:"門檻 500",data:luxs.map(()=>LUX_HIGH),borderDash:[5,3]}
          ]},
          options:{responsive:true}
        });

        chartSoil=new Chart(document.getElementById("chartSoil"),{
          type:"line",
          data:{labels,datasets:[
            {label:"土壤濕度 %",data:soils,yAxisID:"y1"},
            {label:"土壤溫度 °C",data:soilTs,yAxisID:"y2"}
          ]},
          options:{responsive:true,scales:{
            y1:{type:"linear",position:"left"},
            y2:{type:"linear",position:"right",grid:{drawOnChartArea:false}}
          }}
        });
      });
    }

    update();
    setInterval(update,30000);
  </script>
</body>
</html>
