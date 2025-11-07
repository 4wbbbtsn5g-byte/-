# -<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>통영 견내량 에코 모니터링</title>
  <style>
    :root{
      --primary:#116466; /* 짙은 청록 */
      --accent:#2c7a7b;  /* 메인 강조색 */
      --soft:#f3fbfa;
      --card:#ffffff;
      --muted:#6b6b6b;
      --rounded:14px;
      --maxw:980px;
    }
    *{box-sizing:border-box}
    html,body{height:100%;}
    body{
      margin:0;
      font-family: "Noto Sans KR", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background:linear-gradient(180deg,var(--soft),#eef7f6);
      color:#0f1720;
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
    }

    /* Header / Hero */
    header.hero{
      background:linear-gradient(90deg, rgba(17,100,102,0.95), rgba(44,122,123,0.95));
      color:white;
      padding:48px 20px;
      text-align:center;
      clip-path: ellipse(100% 80% at 50% 0%);
    }
    header .inner{max-width:var(--maxw); margin:0 auto;}
    header h1{margin:0; font-size:2.0rem; letter-spacing:-0.02em;}
    header p{margin-top:12px; opacity:0.95; line-height:1.6;}

    main{max-width:var(--maxw); margin:28px auto; padding:0 18px 80px;}

    section.card{
      background:var(--card);
      border-radius:var(--rounded);
      box-shadow: 0 6px 18px rgba(9,18,20,0.06);
      padding:20px;
      margin-bottom:22px;
    }
    h2.section-title{
      display:flex; align-items:center; gap:12px;
      font-size:1.15rem; color:var(--accent);
      margin:6px 0 12px;
    }
    .row{display:flex; gap:14px; flex-wrap:wrap;}
    .col{flex:1 1 300px; min-width:260px;}

    .stat{
      background:linear-gradient(180deg,#fff,#fbfffd);
      border-radius:12px; padding:14px;
      box-shadow: 0 2px 10px rgba(12,20,20,0.04);
    }
    .stat small{display:block; color:var(--muted); margin-bottom:6px;}
    .stat .val{font-weight:700; font-size:1.4rem; color:var(--primary);}
    .muted{color:var(--muted); font-size:0.95rem;}

    /* Form */
    label{display:block; font-weight:600; margin-bottom:6px; font-size:0.95rem;}
    input[type="text"], textarea{
      width:100%; padding:10px 12px; border-radius:10px; border:1px solid #e0e7e6;
      font-size:0.95rem; background:#fbfffe;
    }
    textarea{min-height:90px; resize:vertical;}
    .btn{display:inline-block; background:var(--primary); color:white; padding:10px 14px; border-radius:10px; border:none; cursor:pointer; font-weight:700;}
    .btn.secondary{background:#2c7a7b}

    footer{max-width:var(--maxw); margin:36px auto 80px; padding:0 18px; color:var(--muted); font-size:0.9rem; text-align:center;}

    /* Responsive tweaks */
    @media (max-width:640px){
      header h1{font-size:1.5rem}
    }
  </style>
</head>
<body>

  <header class="hero">
    <div class="inner">
      <h1>통영 견내량 에코 모니터링</h1>
      <p>견내량 해역 전용 환경 모니터링 플랫폼 — 실시간(예시) 데이터와 시민 제보로 지역 해양·생태 위험을 조기에 감지합니다.</p>
    </div>
  </header>

  <main>
    <!-- 1. 실시간 환경 모니터링 (견내량 전용) -->
    <section class="card" id="monitoring">
      <h2 class="section-title">1. 견내량 실시간 모니터링</h2>

      <div class="row">
        <div class="col stat">
          <small>바닷물 온도 (견내량)</small>
          <div class="val" id="seaTemp">18.7°C</div>
          <div class="muted">(예시값 — 실제 연동 가능)</div>
        </div>

        <div class="col stat">
          <small>탁도 (NTU)</small>
          <div class="val" id="turbidity">2.5 NTU</div>
          <div class="muted">탁도는 수질의 투명도를 나타냄</div>
        </div>

        <div class="col stat">
          <small>적조(붉은파도) 가능성</small>
          <div class="val" id="redtide">12%</div>
          <div class="muted">수온·영양염·탁도 기반 예측(예시)</div>
        </div>
      </div>

      <div style="height:14px"></div>

      <div class="row">
        <div class="col stat">
          <small>PM2.5 (통영)</small>
          <div class="val" id="pm25">16 μg/m³</div>
          <div class="muted">환경부 에어코리아 기준</div>
        </div>

        <div class="col stat">
          <small>대기 CO₂ (근접 측정값)</small>
          <div class="val" id="co2">421 ppm</div>
          <div class="muted">참고용 값</div>
        </div>

        <div class="col stat">
          <small>견내량 주변 기온·습도</small>
          <div class="val" id="air">17.2°C · 64%</div>
          <div class="muted">기상청 관측소 예시값</div>
        </div>
      </div>

      <p style="margin-top:12px; color:var(--muted); font-size:0.92rem;">
        ※ 위 수치는 예시입니다. 실제 실시간 값을 보여주려면 아래 주석의 API(국가해양조사원/국립수산과학원/에어코리아/기상청 등)와 연동하세요.
      </p>
    </section>

    <!-- 2. 시민 제보 -->
    <section class="card" id="citizen">
      <h2 class="section-title">2. 시민 참여형 모니터링</h2>

      <div class="row">
        <div class="col">
          <label for="reportDesc">쓰레기/오염 제보 (견내량)</label>
          <textarea id="reportDesc" placeholder="발견한 장소·시간·특이사항을 적어주세요."></textarea>
          <div style="margin-top:10px;">
            <button class="btn" onclick="submitReport()">제보 제출</button>
            <button class="btn secondary" onclick="useMyLocation()">내 위치 사용</button>
          </div>
          <p id="reportMsg" class="muted" style="margin-top:8px;"></p>
        </div>

        <div class="col">
          <label for="photo">오염 사진 업로드 (AI 판별—모의)</label>
          <input type="file" id="photo" accept="image/*">
          <div style="margin-top:10px;">
            <button class="btn" onclick="analyzePhoto()">AI 판별 실행</button>
          </div>
          <p id="aiResult" class="muted" style="margin-top:8px;"></p>

          <hr style="margin:14px 0;border:none;border-top:1px solid #eef6f5;">

          <label for="obs">관찰(벌/식물/조개류) 등록</label>
          <textarea id="obs" placeholder="무엇을 몇 마리/개 관찰했는지 간단히 적어주세요."></textarea>
          <div style="margin-top:10px;">
            <button class="btn" onclick="submitObs()">관찰 제출 (건강도 체크)</button>
          </div>
          <p id="obsResult" class="muted" style="margin-top:8px;"></p>
        </div>
      </div>
    </section>

    <!-- 3. 문제 해결 가이드 -->
    <section class="card" id="guide">
      <h2 class="section-title">3. 문제 해결 가이드 (견내량 기준)</h2>

      <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:12px;">
        <div style="padding:12px;border-radius:12px;background:#fbfffe;">
          <h4>적조 의심 시</h4>
          <ul style="margin:6px 0 0 18px">
            <li>양식장 운영자에게 즉시 통보</li>
            <li>오염원(폐유·하수) 유입 여부 확인</li>
            <li>지역 해양기관(국립수산과학원)에 신고</li>
          </ul>
        </div>

        <div style="padding:12px;border-radius:12px;background:#fbfffe;">
          <h4>해변 쓰레기·기름</h4>
          <ul style="margin:6px 0 0 18px">
            <li>직접 수거 시 장갑·도구 사용</li>
            <li>기름 발견 시 손대지 말고 즉시 지자체 신고</li>
            <li>분류수거 가능하면 분리 배출</li>
          </ul>
        </div>

        <div style="padding:12px;border-radius:12px;background:#fbfffe;">
          <h4>플라스틱 저감 팁</h4>
          <ul style="margin:6px 0 0 18px">
            <li>재사용 가능한 물병·식기 사용</li>
            <li>포장 적은 제품 선택</li>
            <li>바다 정화 봉사 참여</li>
          </ul>
        </div>
      </div>

      <div style="margin-top:14px; font-size:0.94rem; color:var(--muted);">
        <strong>참고 연락처(예시)</strong><br>
        - 통영시 해양환경과 / 경상남도 환경과 / 국립수산과학원 적조예측 센터
      </div>
    </section>

    <!-- 4. 출처 및 실제 연동 가이드 -->
    <section class="card" id="sources">
      <h2 class="section-title">4. 출처 & 실제 연동 안내</h2>
      <p class="muted">
        데이터 출처(연동 권장) — 아래 기관의 공개 API/오픈데이터를 사용해 견내량 전용 실시간 값을 받아올 수 있습니다.
      </p>
      <ul style="color:var(--muted)">
        <li>국가해양조사원(KHOA) - 해양 관측(수온, 탁도 등)</li>
        <li>국립수산과학원(NIFS) - 적조 관련 연구·예측 데이터</li>
        <li>환경부(에어코리아) - 대기(PM2.5) 데이터</li>
        <li>기상청(KMA) - 기온·습도 관측값</li>
      </ul>

      <p style="margin-top:10px; color:var(--muted)">
        ※ 현재 페이지는 '데모/교육용'이며 위 기관의 실제 API로 교체하려면 JavaScript fetch()로 각 기관의 엔드포인트를 호출하고,
        응답 JSON에서 적절한 필드를 화면에 넣으면 됩니다. (CORS, API키 정책 확인 필요)
      </p>
    </section>

  </main>

  <footer>
    © 2025 통영 견내량 에코 모니터링 — 예시 데모. 실제 연동·배포 전 관련 기관 API와 권한을 확인하세요.
  </footer>

  <script>
    // -----------------------------
    // 간단한 클라이언트 기능 (모의/데모)
    // -----------------------------

    // 저장 구조: localStorage 에 제보/관찰 저장 (간단 데모)
    function submitReport() {
      const desc = document.getElementById('reportDesc').value.trim();
      const msg = document.getElementById('reportMsg');
      if (!desc) { msg.textContent = '제보 내용을 입력해주세요.'; return; }

      // 위치(있으면) 가져오기
      const savedLat = document.getElementById('reportDesc').dataset.lat || null;
      const savedLng = document.getElementById('reportDesc').dataset.lng || null;

      const report = {
        id: Date.now(),
        desc,
        lat: savedLat,
        lng: savedLng,
        time: new Date().toISOString()
      };

      const reports = JSON.parse(localStorage.getItem('gn_reports') || '[]');
      reports.unshift(report);
      localStorage.setItem('gn_reports', JSON.stringify(reports));

      msg.textContent = '제보가 접수되었습니다. (로컬 저장 데모)';
      document.getElementById('reportDesc').value = '';
      delete document.getElementById('reportDesc').dataset.lat;
      delete document.getElementById('reportDesc').dataset.lng;
    }

    function useMyLocation() {
      const msg = document.getElementById('reportMsg');
      if (!navigator.geolocation) {
        msg.textContent = '위치 기능을 사용할 수 없습니다.';
        return;
      }
      msg.textContent = '현재 위치를 가져오는 중...';
      navigator.geolocation.getCurrentPosition(pos => {
        const lat = pos.coords.latitude.toFixed(6);
        const lng = pos.coords.longitude.toFixed(6);
        document.getElementById('reportDesc').dataset.lat = lat;
        document.getElementById('reportDesc').dataset.lng = lng;
        msg.textContent = `위치가 설정되었습니다: 위도 ${lat}, 경도 ${lng}`;
      }, err => {
        msg.textContent = '위치 정보를 가져올 수 없습니다. (권한 확인)';
      }, { enableHighAccuracy:true, timeout:10000 });
    }

    // 모의 AI 분석 (실제 AI 모델과 교체 가능)
    function analyzePhoto() {
      const fileInput = document.getElementById('photo');
      const out = document.getElementById('aiResult');
      if (!fileInput.files || fileInput.files.length === 0) {
        out.textContent = '사진을 선택해 주세요.';
        return;
      }
      // 데모용: 파일 이름 기준으로 간단 분류(실제 모델에서는 서버에 올려 분석)
      const name = fileInput.files[0].name.toLowerCase();
      let guess = '기타';
      if (name.includes('bottle') || name.includes('plastic') || name.includes('pet')) guess = '플라스틱 병/용기';
      else if (name.includes('bag') || name.includes('비닐')) guess = '비닐류';
      else if (name.includes('net') || name.includes('그물')) guess = '어망류';
      else guess = '혼합 쓰레기(플라스틱/유기물)';

      // 모의 신뢰도
      const confidence = Math.floor(75 + Math.random()*20);

      out.textContent = `AI 예측: ${guess} (신뢰도 ${confidence}%) — 실제 배포 시 서버 AI 모델(예: TensorFlow.js, Vision API 등)로 대체하세요.`;
    }

    // 관찰 제출 + 간단 건강도 판단
    function submitObs() {
      const txt = document.getElementById('obs').value.trim();
      const out = document.getElementById('obsResult');
      if (!txt) { out.textContent = '관찰 내용을 입력하세요.'; return; }

      // 데모 규칙: "다양성" 단어 포함 시 양호 표시
      let health = '보통';
      if (/(많이|다양|여러|풍부)/.test(txt)) health = '양호';
      else if (/(줄어|없|감소)/.test(txt)) health = '주의필요';

      const obs = { time:new Date().toISOString(), text:txt, health };
      const arr = JSON.parse(localStorage.getItem('gn_obs') || '[]');
      arr.unshift(obs);
      localStorage.setItem('gn_obs', JSON.stringify(arr));

      out.textContent = `제출 완료 — 간단 생태 건강도: ${health} (데모)`;
      document.getElementById('obs').value = '';
    }

    // (옵션) 데모 데이터 갱신 시뮬레이터 — 실제 연동 시 주석 처리하고 fetch로 교체하세요.
    (function demoDataTicker(){
      const seed = [
        {t:18.7, tu:2.5, r:12, pm:16, co2:421, air:'17.2°C · 64%'},
        {t:19.1, tu:2.8, r:15, pm:22, co2:422, air:'17.8°C · 66%'},
        {t:18.4, tu:2.3, r:10, pm:12, co2:420, air:'16.9°C · 61%'}
      ];
      let i=0;
      function tick(){
        const s = seed[i % seed.length];
        document.getElementById('seaTemp').textContent = s.t + '°C';
        document.getElementById('turbidity').textContent = s.tu + ' NTU';
        document.getElementById('redtide').textContent = s.r + '%';
        document.getElementById('pm25').textContent = s.pm + ' μg/m³';
        document.getElementById('co2').textContent = s.co2 + ' ppm';
        document.getElementById('air').textContent = s.air;
        i++;
      }
      tick();
      setInterval(tick, 8000); // 8초마다 (데모)
    })();

    // 유효성 검사: 간단 콘솔 메시지
    console.log('통영 견내량 에코 모니터링 데모 페이지 로드됨. 실제 API 연동 전 데모 데이터가 표시됩니다.');
  </script>
</body>
</html>
