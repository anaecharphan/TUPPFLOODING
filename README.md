<html lang="th">
<head>
  <meta charset="UTF-8" />
  <title>Disaster City Simulator – Upgraded Edition</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    * {
      box-sizing: border-box;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI",
        sans-serif;
    }

    body {
      margin: 0;
      background: radial-gradient(circle at top, #e0f2fe, #f9fafb);
      color: #0f172a;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 1rem;
    }

    .app {
      max-width: 1100px;
      width: 100%;
      background: #ffffffee;
      backdrop-filter: blur(10px);
      border-radius: 22px;
      box-shadow: 0 22px 65px rgba(15, 23, 42, 0.25);
      padding: 1.9rem 1.5rem 2.4rem;
    }

    @media (min-width: 768px) {
      .app {
        padding: 2.3rem 2.6rem 2.6rem;
      }
    }

    .header {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 0.75rem;
      margin-bottom: 1.2rem;
    }

    .title {
      font-size: 1.6rem;
      font-weight: 800;
      display: flex;
      gap: 0.5rem;
      align-items: center;
    }

    .title span {
      font-size: 1.9rem;
    }

    .subtitle {
      font-size: 0.9rem;
      color: #64748b;
    }

    .tag-row {
      display: flex;
      flex-wrap: wrap;
      gap: 0.35rem;
      font-size: 0.8rem;
      align-items: center;
    }

    .pill {
      padding: 0.13rem 0.6rem;
      border-radius: 999px;
      background: #e2e8f0;
    }

    .pill.flood {
      background: #dbeafe;
      color: #1d4ed8;
    }

    .pill.fire {
      background: #fee2e2;
      color: #b91c1c;
    }

    .pill.wind {
      background: #e0f2fe;
      color: #0369a1;
    }

    .pill.tornado {
      background: #f3e8ff;
      color: #7e22ce;
    }

    .pill.best {
      background: #dcfce7;
      color: #15803d;
    }

    .layout {
      display: grid;
      grid-template-columns: 2.2fr 1.8fr;
      gap: 1.5rem;
    }

    @media (max-width: 900px) {
      .layout {
        grid-template-columns: 1fr;
      }
    }

    .card {
      background: #ffffff;
      border-radius: 16px;
      padding: 1.1rem 1rem;
      box-shadow: 0 12px 35px rgba(15, 23, 42, 0.08);
      margin-bottom: 0.8rem;
    }

    .card h2 {
      margin: 0 0 0.5rem;
      font-size: 1.12rem;
      display: flex;
      align-items: center;
      gap: 0.4rem;
    }

    .card p {
      margin: 0.2rem 0 0.6rem;
      font-size: 0.9rem;
      color: #6b7280;
    }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 0.7rem;
      margin-bottom: 0.7rem;
    }

    @media (max-width: 700px) {
      .stats-grid {
        grid-template-columns: 1fr;
      }
    }

    .stat-box {
      padding: 0.45rem 0.65rem;
      border-radius: 12px;
      background: #f1f5f9;
    }

    .stat-label {
      font-size: 0.78rem;
      color: #64748b;
    }

    .stat-value {
      font-weight: 700;
      font-size: 1rem;
    }

    .bar-wrap {
      margin-top: 0.3rem;
      background: #e5e7eb;
      border-radius: 999px;
      height: 10px;
      overflow: hidden;
    }

    .bar {
      height: 100%;
      width: 100%;
      border-radius: 999px;
      transform-origin: left;
      transition: transform 0.2s ease;
    }

    .bar.health {
      background: linear-gradient(90deg, #22c55e, #f97316, #ef4444);
    }

    .bar.budget {
      background: linear-gradient(90deg, #0ea5e9, #22c55e);
    }

    .bar.trust {
      background: linear-gradient(90deg, #4f46e5, #22c55e);
    }

    .small {
      font-size: 0.8rem;
      color: #6b7280;
    }

    .resources-row {
      display: flex;
      flex-wrap: wrap;
      gap: 0.55rem;
      font-size: 0.82rem;
      margin-top: 0.2rem;
    }

    .res-tag {
      padding: 0.15rem 0.55rem;
      border-radius: 999px;
      background: #e5e7eb;
    }

    .res-tag span {
      font-weight: 700;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 0.35rem;
      padding: 0.55rem 0.95rem;
      border-radius: 12px;
      border: none;
      cursor: pointer;
      font-size: 0.9rem;
      font-weight: 600;
      transition: transform 0.07s ease, box-shadow 0.07s ease,
        background-color 0.1s ease;
    }

    .btn-primary {
      background: linear-gradient(135deg, #1d4ed8, #2563eb);
      color: #ffffff;
      box-shadow: 0 10px 25px rgba(37, 99, 235, 0.3);
    }

    .btn-primary:hover:not(:disabled) {
      transform: translateY(-1px);
      box-shadow: 0 14px 30px rgba(37, 99, 235, 0.4);
    }

    .btn-secondary {
      background: #e2e8f0;
      color: #0f172a;
    }

    .btn-secondary:hover:not(:disabled) {
      background: #cbd5e1;
    }

    .btn:disabled {
      opacity: 0.6;
      cursor: default;
      transform: none;
      box-shadow: none;
    }

    .btn-wide {
      width: 100%;
      margin-top: 0.6rem;
    }

    .disaster-type {
      padding: 0.12rem 0.55rem;
      border-radius: 999px;
      font-size: 0.8rem;
      display: inline-flex;
      align-items: center;
      gap: 0.25rem;
    }

    .type-flood {
      background: #dbeafe;
      color: #1d4ed8;
    }

    .type-fire {
      background: #fee2e2;
      color: #b91c1c;
    }

    .type-wind {
      background: #e0f2fe;
      color: #0369a1;
    }

    .type-tornado {
      background: #f3e8ff;
      color: #7e22ce;
    }

    .danger-level {
      padding: 0.1rem 0.6rem;
      border-radius: 999px;
      font-size: 0.8rem;
      display: inline-block;
      margin-left: 0.3rem;
    }

    .danger-low {
      background: #dcfce7;
      color: #15803d;
    }

    .danger-medium {
      background: #fef9c3;
      color: #ca8a04;
    }

    .danger-high {
      background: #fee2e2;
      color: #b91c1c;
    }

    .disaster-title {
      font-size: 1rem;
      font-weight: 700;
      margin: 0.35rem 0 0.4rem;
    }

    .disaster-desc {
      font-size: 0.9rem;
      color: #374151;
      margin-bottom: 0.4rem;
    }

    .resource-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 0.55rem;
      margin-top: 0.35rem;
    }

    @media (max-width: 500px) {
      .resource-grid {
        grid-template-columns: 1fr;
      }
    }

    .btn-resource {
      background: #f1f5f9;
      color: #0f172a;
      box-shadow: 0 4px 12px rgba(15, 23, 42, 0.06);
      width: 100%;
      justify-content: flex-start;
      align-items: flex-start;
      padding: 0.55rem 0.75rem;
    }

    .btn-resource span.icon {
      font-size: 1.1rem;
    }

    .btn-resource:hover:not(.disabled) {
      background: #e0f2fe;
    }

    .btn-resource .label {
      font-size: 0.9rem;
      font-weight: 600;
    }

    .btn-resource .sub {
      font-size: 0.78rem;
      color: #64748b;
    }

    .btn-resource .meta {
      font-size: 0.75rem;
      color: #0f172a;
      margin-top: 0.1rem;
    }

    .feedback {
      font-size: 0.85rem;
      margin-top: 0.5rem;
      min-height: 1.5em;
    }

    .feedback.positive {
      color: #15803d;
    }

    .feedback.negative {
      color: #b91c1c;
    }

    .feedback.neutral {
      color: #6b7280;
    }

    .gameover {
      font-weight: 700;
    }

    .log {
      list-style: none;
      padding-left: 0;
      margin: 0;
      font-size: 0.82rem;
      max-height: 210px;
      overflow-y: auto;
    }

    .log li {
      padding: 0.25rem 0;
      border-bottom: 1px dashed #e2e8f0;
    }

    .log-badge {
      font-size: 0.7rem;
      padding: 0.05rem 0.45rem;
      border-radius: 999px;
      background: #e5e7eb;
      margin-right: 0.35rem;
    }

    .log-good {
      color: #15803d;
    }

    .log-bad {
      color: #b91c1c;
    }

    .log-system {
      color: #0369a1;
    }

    .best-record {
      font-size: 0.82rem;
      color: #0f766e;
      margin-top: 0.3rem;
    }

    footer {
      text-align: center;
      font-size: 0.75rem;
      color: #94a3b8;
      margin-top: 0.6rem;
    }
  </style>
</head>
<body>
  <div class="app">
    <header class="header">
      <div>
        <div class="title">
          <span>🏙️</span> Disaster City Simulator
        </div>
        <div class="subtitle">
          Upgraded Edition – คุณคือ “ผู้ว่าฯ เมือง” ที่ต้องบริหารทรัพยากรจำกัดให้เมืองรอดจากภัยพิบัติหลายรูปแบบ
        </div>
      </div>
      <div class="tag-row">
        <span class="pill flood">Flood</span>
        <span class="pill fire">Fire</span>
        <span class="pill wind">Strong Wind</span>
        <span class="pill tornado">Tornado</span>
        <span class="pill best" id="bestRecordPill">Best: - incidents</span>
      </div>
    </header>

    <main class="layout">
      <!-- LEFT: Main game -->
      <section>
        <div class="card">
          <h2>🧭 City Dashboard</h2>
          <div class="stats-grid">
            <div class="stat-box">
              <div class="stat-label">City Health</div>
              <div class="stat-value">
                <span id="cityHealthText">100</span> / 100
              </div>
              <div class="bar-wrap">
                <div id="cityHealthBar" class="bar health"></div>
              </div>
              <div class="small">ถ้าเหลือ 0 เมืองเข้าสู่ภาวะวิกฤต (Game Over)</div>
            </div>
            <div class="stat-box">
              <div class="stat-label">City Budget (ล้านบาท)</div>
              <div class="stat-value">
                <span id="cityBudgetText">100</span> M
              </div>
              <div class="bar-wrap">
                <div id="cityBudgetBar" class="bar budget"></div>
              </div>
              <div class="small">ใช้มากเกินไป = งบหมดก่อนเหตุการณ์จบ</div>
            </div>
            <div class="stat-box">
              <div class="stat-label">Public Trust</div>
              <div class="stat-value">
                <span id="publicTrustText">100</span> / 100
              </div>
              <div class="bar-wrap">
                <div id="publicTrustBar" class="bar trust"></div>
              </div>
              <div class="small">ตัดสินใจผิดซ้ำ ๆ = ความเชื่อมั่นลดลง</div>
            </div>
          </div>

          <div class="resources-row">
            <div class="res-tag">💧 Pump: <span id="resPump">3</span></div>
            <div class="res-tag">🚒 Firetruck: <span id="resFiretruck">3</span></div>
            <div class="res-tag">👷‍♂️ Rescue: <span id="resRescue">4</span></div>
            <div class="res-tag">🏟️ Shelter: <span id="resShelter">4</span></div>
          </div>

          <div class="resources-row" style="margin-top:0.35rem;">
            <div class="res-tag">Incidents handled: <span id="incidentsHandledText">0</span></div>
            <div class="res-tag">Max incidents this game: <span id="maxIncidentsText">12</span></div>
          </div>

          <button id="newGameBtn" class="btn btn-primary btn-wide">
            🔁 Start New Simulation
          </button>
        </div>

        <div class="card">
          <h2>🚨 Active Incident</h2>
          <p>อ่านสถานการณ์ แล้วเลือก “ทรัพยากรหลัก” ที่จะสั่งการก่อนเป็นลำดับแรก</p>

          <div>
            <span id="disasterTypeBadge" class="disaster-type type-flood">
              Flood · น้ำท่วม
            </span>
            <span id="dangerLevelBadge" class="danger-level danger-medium">
              ระดับปานกลาง (เสี่ยงอันตราย)
            </span>
          </div>

          <div id="disasterTitle" class="disaster-title">-</div>
          <div id="disasterDesc" class="disaster-desc">
            กด “Start New Simulation” เพื่อเริ่มสถานการณ์แรก
          </div>

          <div class="resource-grid">
            <button class="btn btn-resource disabled" data-resource="pump" id="btnPump">
              <span class="icon">💧</span>
              <div>
                <div class="label">Water Pump Team</div>
                <div class="sub">เครื่องสูบน้ำ · จัดการน้ำท่วม</div>
                <div class="meta">Cost: 8M · Stock: <span id="stockPump">3</span></div>
              </div>
            </button>

            <button class="btn btn-resource disabled" data-resource="firetruck" id="btnFiretruck">
              <span class="icon">🚒</span>
              <div>
                <div class="label">Fire Truck</div>
                <div class="sub">ดับเพลิง · เข้าถึงจุดไฟไหม้</div>
                <div class="meta">Cost: 10M · Stock: <span id="stockFiretruck">3</span></div>
              </div>
            </button>

            <button class="btn btn-resource disabled" data-resource="rescue" id="btnRescue">
              <span class="icon">👷‍♂️</span>
              <div>
                <div class="label">Rescue Team</div>
                <div class="sub">ทีมกู้ภัย · อพยพ–ช่วยคน</div>
                <div class="meta">Cost: 6M · Stock: <span id="stockRescue">4</span></div>
              </div>
            </button>

            <button class="btn btn-resource disabled" data-resource="shelter" id="btnShelter">
              <span class="icon">🏟️</span>
              <div>
                <div class="label">Evacuation Shelter</div>
                <div class="sub">ศูนย์อพยพ · รองรับผู้ประสบภัย</div>
                <div class="meta">Cost: 5M · Stock: <span id="stockShelter">4</span></div>
              </div>
            </button>
          </div>

          <div id="feedback" class="feedback neutral"></div>

          <div style="display:flex; gap:0.5rem; margin-top:0.3rem;">
            <button id="nextIncidentBtn" class="btn btn-secondary" disabled>
              ▶ Next Incident
            </button>
            <button id="hintBtn" class="btn btn-secondary" disabled>
              💡 Hint
            </button>
          </div>
        </div>
      </section>

      <!-- RIGHT: Logs & Info -->
      <aside>
        <div class="card">
          <h2>📜 Incident Log</h2>
          <ul id="logList" class="log">
            <li><span class="log-badge log-system">SYS</span>Welcome to Disaster City Simulator – กด “Start New Simulation” เพื่อเริ่มเกม</li>
          </ul>
        </div>

        <div class="card">
          <h2>🎯 Game Objective</h2>
          <p>
            บริหารเมืองให้รอดจาก <strong>เหตุการณ์ต่อเนื่องหลายครั้ง</strong>
            โดยรักษา <strong>Health, Budget และ Public Trust</strong> ให้ไม่เป็นศูนย์ก่อนครบจำนวนเหตุการณ์
          </p>
          <ul class="small" style="padding-left:1.1rem;">
            <li>ตัดสินใจเลือกทรัพยากรหลัก 1 อย่างต่อเหตุการณ์</li>
            <li>เลือกถูกกับประเภทภัยพิบัติ → ความเสียหายลดลง · ความเชื่อมั่นเพิ่ม · อาจได้งบสนับสนุน</li>
            <li>เลือกไม่เหมาะสม → ความเสียหายเพิ่ม · งบถูกใช้เปลือง · ความเชื่อมั่นลดลง</li>
            <li>Stock ของทรัพยากรจะลดลงเมื่อใช้ (ใช้เยอะ = ของหมดก่อนจบเกม)</li>
            <li>ถ้า Health หรือ Budget หรือ Trust ≤ 0 ก่อนครบเหตุการณ์ → Game Over</li>
          </ul>
          <p class="best-record" id="bestRecordText">
            Best Record (เครื่องนี้): -
          </p>
        </div>
      </aside>
    </main>

    <footer>
      © 2025 Disaster City Simulator – Upgraded Edition (Prototype for Learning Purpose)
    </footer>
  </div>

  <script>
    // -------------------------
    // ธนาคารเหตุการณ์ภัยพิบัติ
    // -------------------------
    const DISASTERS = [
      {
        id: 1,
        type: 'flood',
        title: 'น้ำท่วมฉับพลันเขตชุมชนริมน้ำ',
        description:
          'ฝนตกหนักต่อเนื่อง น้ำจากคลองเอ่อล้นเข้าท่วมบ้านเรือนริมน้ำ ระดับน้ำสูงขึ้นเรื่อย ๆ รถเล็กเริ่มผ่านไม่ได้ มีบ้านหลายหลังเริ่มถูกตัดไฟฟ้า',
        dangerLevel: 'high',
        bestResource: 'pump',
        secondaryResource: 'rescue'
      },
      {
        id: 2,
        type: 'flood',
        title: 'น้ำท่วมขังหน้าโรงเรียนและถนนสายหลัก',
        description:
          'ฝนตกทั้งคืน ทำให้เกิดน้ำท่วมขังบริเวณหน้าโรงเรียนและถนนสายหลัก น้ำลึกระดับเข่า รถยังพอผ่านได้ แต่เสี่ยงเกิดอุบัติเหตุและการจราจรติดขัด',
        dangerLevel: 'medium',
        bestResource: 'pump',
        secondaryResource: 'rescue'
      },
      {
        id: 3,
        type: 'fire',
        title: 'ไฟไหม้หอพักในเขตตัวเมือง',
        description:
          'เกิดไฟไหม้ที่ชั้น 3 ของหอพักในเมือง มีควันหนาแน่น ผู้คนตื่นตระหนก บางส่วนยังติดอยู่ในห้องด้านบน',
        dangerLevel: 'high',
        bestResource: 'firetruck',
        secondaryResource: 'rescue'
      },
      {
        id: 4,
        type: 'fire',
        title: 'ไฟไหม้เล็กในตลาดสดช่วงกลางวัน',
        description:
          'มีไฟลุกจากร้านอาหารในตลาดสด แต่ยังจำกัดวงอยู่ในครัว มีคนจำนวนมากอยู่บริเวณใกล้เคียง',
        dangerLevel: 'medium',
        bestResource: 'firetruck',
        secondaryResource: 'rescue'
      },
      {
        id: 5,
        type: 'wind',
        title: 'ลมกรรโชกแรงพัดผ่านเขตที่พักอาศัย',
        description:
          'กลุ่มเมฆดำเคลื่อนตัวเข้ามาพร้อมลมกรรโชกแรง หลังคาบ้านบางส่วนเริ่มสั่นไหว มีต้นไม้ใหญ่ในพื้นที่ใกล้กับสายไฟ',
        dangerLevel: 'medium',
        bestResource: 'rescue',
        secondaryResource: 'shelter'
      },
      {
        id: 6,
        type: 'wind',
        title: 'ลมแรงใกล้สนามกีฬาและโรงเรียน',
        description:
          'ระหว่างกิจกรรมกลางแจ้ง ลมแรงพัดเข้ามาอย่างกะทันหัน อุปกรณ์กีฬาบางส่วนปลิว เด็ก ๆ ยังอยู่ในสนามจำนวนมาก',
        dangerLevel: 'medium',
        bestResource: 'rescue',
        secondaryResource: 'shelter'
      },
      {
        id: 7,
        type: 'tornado',
        title: 'ทอร์นาโดก่อตัวนอกเขตชุมชนและเคลื่อนเข้าใกล้เมือง',
        description:
          'มีรายงานว่าทอร์นาโดขนาดกลางกำลังก่อตัวนอกเขตเมืองและมีแนวโน้มจะพัดผ่านเขตชานเมืองที่มีบ้านเรือนหนาแน่น',
        dangerLevel: 'high',
        bestResource: 'shelter',
        secondaryResource: 'rescue'
      },
      {
        id: 8,
        type: 'tornado',
        title: 'พายุหมุนแรงผ่านเขตโล่งใกล้เขตนิคมอุตสาหกรรม',
        description:
          'พายุหมุนความรุนแรงสูงกำลังเคลื่อนตัวผ่านพื้นที่โล่งและมีโอกาสพัดเข้าสู่เขตโรงงาน หากไม่มีการอพยพล่วงหน้าจะเสี่ยงสูง',
        dangerLevel: 'high',
        bestResource: 'shelter',
        secondaryResource: 'rescue'
      }
    ];

    // -------------------------
    // การตั้งค่าเกมพื้นฐาน
    // -------------------------
    const INITIAL_STATE = {
      health: 100,
      budget: 100, // ล้าน
      trust: 100,
      resources: {
        pump: 3,
        firetruck: 3,
        rescue: 4,
        shelter: 4
      },
      maxIncidents: 12
    };

    const RESOURCE_COST = {
      pump: 8,
      firetruck: 10,
      rescue: 6,
      shelter: 5
    };

    // key ใน localStorage
    const BEST_RECORD_KEY = 'disasterCity_bestRecord_v1';

    // -------------------------
    // สถานะเกม runtime
    // -------------------------
    let cityHealth;
    let cityBudget;
    let publicTrust;
    let resources;
    let incidentsHandled;
    let currentDisaster = null;
    let roundActive = false;
    let gameOver = false;
    let maxIncidents;
    let usedDisasterIds = [];

    // -------------------------
    // DOM elements
    // -------------------------
    const cityHealthText = document.getElementById('cityHealthText');
    const cityHealthBar = document.getElementById('cityHealthBar');
    const cityBudgetText = document.getElementById('cityBudgetText');
    const cityBudgetBar = document.getElementById('cityBudgetBar');
    const publicTrustText = document.getElementById('publicTrustText');
    const publicTrustBar = document.getElementById('publicTrustBar');

    const resPump = document.getElementById('resPump');
    const resFiretruck = document.getElementById('resFiretruck');
    const resRescue = document.getElementById('resRescue');
    const resShelter = document.getElementById('resShelter');

    const stockPump = document.getElementById('stockPump');
    const stockFiretruck = document.getElementById('stockFiretruck');
    const stockRescue = document.getElementById('stockRescue');
    const stockShelter = document.getElementById('stockShelter');

    const incidentsHandledText = document.getElementById('incidentsHandledText');
    const maxIncidentsText = document.getElementById('maxIncidentsText');

    const disasterTypeBadge = document.getElementById('disasterTypeBadge');
    const dangerLevelBadge = document.getElementById('dangerLevelBadge');
    const disasterTitle = document.getElementById('disasterTitle');
    const disasterDesc = document.getElementById('disasterDesc');

    const btnPump = document.getElementById('btnPump');
    const btnFiretruck = document.getElementById('btnFiretruck');
    const btnRescue = document.getElementById('btnRescue');
    const btnShelter = document.getElementById('btnShelter');

    const feedback = document.getElementById('feedback');
    const nextIncidentBtn = document.getElementById('nextIncidentBtn');
    const hintBtn = document.getElementById('hintBtn');
    const newGameBtn = document.getElementById('newGameBtn');
    const logList = document.getElementById('logList');

    const bestRecordPill = document.getElementById('bestRecordPill');
    const bestRecordText = document.getElementById('bestRecordText');

    const resourceButtons = [btnPump, btnFiretruck, btnRescue, btnShelter];

    // -------------------------
    // Helper functions
    // -------------------------
    function shuffleArray(arr) {
      const copy = [...arr];
      for (let i = copy.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [copy[i], copy[j]] = [copy[j], copy[i]];
      }
      return copy;
    }

    function updateBar(el, current, max) {
      const scale = Math.max(0, Math.min(1, current / max));
      el.style.transform = 'scaleX(' + scale + ')';
    }

    function updateDashboard() {
      cityHealthText.textContent = cityHealth;
      updateBar(cityHealthBar, cityHealth, 100);

      cityBudgetText.textContent = cityBudget;
      updateBar(cityBudgetBar, cityBudget, INITIAL_STATE.budget);

      publicTrustText.textContent = publicTrust;
      updateBar(publicTrustBar, publicTrust, 100);

      resPump.textContent = resources.pump;
      resFiretruck.textContent = resources.firetruck;
      resRescue.textContent = resources.rescue;
      resShelter.textContent = resources.shelter;

      stockPump.textContent = resources.pump;
      stockFiretruck.textContent = resources.firetruck;
      stockRescue.textContent = resources.rescue;
      stockShelter.textContent = resources.shelter;

      incidentsHandledText.textContent = incidentsHandled;
      maxIncidentsText.textContent = maxIncidents;

      // enable / disable ทรัพยากรตาม stock, งบ และสถานะรอบ
      resourceButtons.forEach((btn) => {
        const key = btn.getAttribute('data-resource');
        if (!roundActive || gameOver) {
          btn.classList.add('disabled');
        } else if (resources[key] <= 0 || cityBudget < RESOURCE_COST[key]) {
          btn.classList.add('disabled');
        } else {
          btn.classList.remove('disabled');
        }
      });
    }

    function addLogEntry(message, type = 'neutral') {
      const li = document.createElement('li');
      const badge = document.createElement('span');
      badge.classList.add('log-badge');
      if (type === 'good') {
        badge.textContent = 'GOOD';
        badge.classList.add('log-good');
      } else if (type === 'bad') {
        badge.textContent = 'RISK';
        badge.classList.add('log-bad');
      } else if (type === 'system') {
        badge.textContent = 'SYS';
        badge.classList.add('log-system');
      } else {
        badge.textContent = 'LOG';
      }
      li.appendChild(badge);
      li.appendChild(document.createTextNode(' ' + message));
      logList.insertBefore(li, logList.firstChild);
    }

    function setButtonsEnabled(enabled) {
      roundActive = enabled;
      updateDashboard();
    }

    function loadBestRecord() {
      const raw = localStorage.getItem(BEST_RECORD_KEY);
      if (!raw) return null;
      try {
        return JSON.parse(raw);
      } catch {
        return null;
      }
    }

    function saveBestRecord(record) {
      const current = loadBestRecord();
      if (!current || record.incidents > current.incidents ||
          (record.incidents === current.incidents && record.health > current.health)) {
        localStorage.setItem(BEST_RECORD_KEY, JSON.stringify(record));
      }
    }

    function refreshBestRecordUI() {
      const best = loadBestRecord();
      if (!best) {
        bestRecordPill.textContent = 'Best: - incidents';
        bestRecordText.textContent = 'Best Record (เครื่องนี้): ยังไม่มีสถิติ ลองเล่นรอดหลาย ๆ เหตุการณ์ดู!';
      } else {
        bestRecordPill.textContent = `Best: ${best.incidents} incidents`;
        bestRecordText.textContent =
          `Best Record (เครื่องนี้): รอด ${best.incidents} เหตุการณ์ · Health เหลือ ${best.health} · Trust ${best.trust}`;
      }
    }

    function updateDisasterUI(disaster) {
      disasterTypeBadge.className = 'disaster-type';
      if (disaster.type === 'flood') {
        disasterTypeBadge.classList.add('type-flood');
        disasterTypeBadge.textContent = 'Flood · น้ำท่วม';
      } else if (disaster.type === 'fire') {
        disasterTypeBadge.classList.add('type-fire');
        disasterTypeBadge.textContent = 'Fire · ไฟไหม้';
      } else if (disaster.type === 'wind') {
        disasterTypeBadge.classList.add('type-wind');
        disasterTypeBadge.textContent = 'Strong Wind · ลมกรรโชกแรง';
      } else if (disaster.type === 'tornado') {
        disasterTypeBadge.classList.add('type-tornado');
        disasterTypeBadge.textContent = 'Tornado · ทอร์นาโด';
      }

      dangerLevelBadge.className = 'danger-level';
      if (disaster.dangerLevel === 'low') {
        dangerLevelBadge.classList.add('danger-low');
        dangerLevelBadge.textContent = 'ระดับต่ำ (ควรเฝ้าระวัง)';
      } else if (disaster.dangerLevel === 'medium') {
        dangerLevelBadge.classList.add('danger-medium');
        dangerLevelBadge.textContent = 'ระดับปานกลาง (เสี่ยงอันตราย)';
      } else {
        dangerLevelBadge.classList.add('danger-high');
        dangerLevelBadge.textContent = 'ระดับสูง (อันตรายมาก)';
      }

      disasterTitle.textContent = disaster.title;
      disasterDesc.textContent = disaster.description;
    }

    function setGameOver(reason) {
      gameOver = true;
      roundActive = false;
      updateDashboard();
      nextIncidentBtn.disabled = true;
      hintBtn.disabled = true;
      feedback.className = 'feedback negative gameover';
      feedback.textContent =
        `Game Over – ${reason} · กด "Start New Simulation" เพื่อเริ่มใหม่`;

      addLogEntry('Simulation ended: ' + reason, 'bad');

      // บันทึกสถิติ
      saveBestRecord({
        incidents: incidentsHandled,
        health: cityHealth,
        trust: publicTrust
      });
      refreshBestRecordUI();
    }

    // -------------------------
    // Game flow
    // -------------------------
    function startNewGame() {
      cityHealth = INITIAL_STATE.health;
      cityBudget = INITIAL_STATE.budget;
      publicTrust = INITIAL_STATE.trust;
      resources = {
        pump: INITIAL_STATE.resources.pump,
        firetruck: INITIAL_STATE.resources.firetruck,
        rescue: INITIAL_STATE.resources.rescue,
        shelter: INITIAL_STATE.resources.shelter
      };
      incidentsHandled = 0;
      maxIncidents = INITIAL_STATE.maxIncidents;
      usedDisasterIds = [];
      currentDisaster = null;
      gameOver = false;
      feedback.textContent = '';
      feedback.className = 'feedback neutral';
      nextIncidentBtn.disabled = true;
      hintBtn.disabled = true;

      addLogEntry(
        'เริ่ม Simulation ใหม่ · เมืองได้รับงบประมาณ ' +
          cityBudget +
          'M และเตรียมทรัพยากรพร้อม',
        'system'
      );

      updateDashboard();
      generateNextDisaster();
    }

    function generateNextDisaster() {
      if (gameOver) return;

      if (incidentsHandled >= maxIncidents) {
        // ชนะ
        feedback.className = 'feedback positive gameover';
        feedback.textContent =
          'ยินดีด้วย! คุณบริหารเมืองผ่านครบทุกเหตุการณ์ เมืองยังคงยืนอยู่ได้ 🎉';
        addLogEntry(
          'Simulation complete: เมืองรอดครบทุกเหตุการณ์ Health ' +
            cityHealth +
            ', Trust ' +
            publicTrust,
          'good'
        );
        gameOver = true;
        roundActive = false;
        nextIncidentBtn.disabled = true;
        hintBtn.disabled = true;
        saveBestRecord({
          incidents: incidentsHandled,
          health: cityHealth,
          trust: publicTrust
        });
        refreshBestRecordUI();
        return;
      }

      feedback.textContent = '';
      feedback.className = 'feedback neutral';

      // เลือกเหตุการณ์ใหม่
      const available = DISASTERS.filter(
        (d) => !usedDisasterIds.includes(d.id)
      );
      let chosen;
      if (available.length === 0) {
        chosen = DISASTERS[Math.floor(Math.random() * DISASTERS.length)];
      } else {
        chosen = available[Math.floor(Math.random() * available.length)];
      }
      usedDisasterIds.push(chosen.id);
      currentDisaster = chosen;

      updateDisasterUI(currentDisaster);

      roundActive = true;
      nextIncidentBtn.disabled = true;
      hintBtn.disabled = false;
      updateDashboard();

      addLogEntry(
        'Incident #' +
          (incidentsHandled + 1) +
          ': ' +
          chosen.title +
          ' [' +
          chosen.type +
          ']',
        'system'
      );
    }

    function handleResourceChoice(resourceKey) {
      if (!roundActive || gameOver || !currentDisaster) return;
      if (resources[resourceKey] <= 0) return;
      const cost = RESOURCE_COST[resourceKey];
      if (cityBudget < cost) {
        feedback.className = 'feedback negative';
        feedback.textContent = 'งบประมาณไม่พอสำหรับการใช้ทรัพยากรนี้';
        return;
      }

      // ใช้ทรัพยากร
      resources[resourceKey] -= 1;
      cityBudget -= cost;

      const { bestResource, secondaryResource, dangerLevel, type } =
        currentDisaster;

      // คำนวณผลกระทบ
      let deltaHealth = 0;
      let deltaTrust = 0;
      let deltaBudget = 0; // อาจได้เงินสนับสนุนเพิ่มถ้าตัดสินใจดี
      let message = '';
      let logType = 'bad';

      if (resourceKey === bestResource) {
        deltaHealth = +8;
        deltaTrust = +6;
        deltaBudget = +3; // เงินสนับสนุนจากส่วนกลาง
        message =
          'เยี่ยมมาก! การสั่งการสอดคล้องกับประเภทภัย ทำให้ควบคุมสถานการณ์ได้อย่างมีประสิทธิภาพ ประชาชนเชื่อมั่น และได้รับงบสนับสนุนเพิ่ม';
        logType = 'good';
      } else if (resourceKey === secondaryResource) {
        deltaHealth = -5;
        deltaTrust = -3;
        message =
          'พอใช้ได้ แต่ยังไม่เหมาะที่สุด ทรัพยากรที่สั่งไปช่วยได้บางส่วน แต่ยังมีความเสียหายต่อเมืองและความเชื่อมั่นลดลงเล็กน้อย';
      } else {
        deltaHealth = -18;
        deltaTrust = -10;
        message =
          'การสั่งการไม่สอดคล้องกับประเภทภัย เมืองได้รับความเสียหายเพิ่ม และประชาชนเริ่มไม่เชื่อมั่นในระบบจัดการภัยพิบัติ';
      }

      // ปรับตามความรุนแรงของภัย
      let dangerMultiplier = 1;
      if (dangerLevel === 'high') {
        dangerMultiplier = 1.5;
      } else if (dangerLevel === 'low') {
        dangerMultiplier = 0.7;
      }
      deltaHealth = Math.round(deltaHealth * dangerMultiplier);
      deltaTrust = Math.round(deltaTrust * dangerMultiplier);
      deltaBudget = Math.round(deltaBudget * dangerMultiplier);

      cityHealth += deltaHealth;
      publicTrust += deltaTrust;
      cityBudget += deltaBudget;

      if (cityHealth > 100) cityHealth = 100;
      if (publicTrust > 100) publicTrust = 100;
      if (cityBudget > INITIAL_STATE.budget) cityBudget = INITIAL_STATE.budget;

      if (cityHealth < 0) cityHealth = 0;
      if (publicTrust < 0) publicTrust = 0;
      if (cityBudget < 0) cityBudget = 0;

      incidentsHandled++;

      updateDashboard();
      roundActive = false;
      nextIncidentBtn.disabled = false;
      hintBtn.disabled = true;

      // Feedback text
      const detail =
        ` (Health ${deltaHealth >= 0 ? '+' : ''}${deltaHealth}, ` +
        `Trust ${deltaTrust >= 0 ? '+' : ''}${deltaTrust}` +
        (deltaBudget !== 0
          ? `, Budget ${deltaBudget >= 0 ? '+' : ''}${deltaBudget}M`
          : '') +
        ')';

      if (deltaHealth >= 0 && deltaTrust >= 0) {
        feedback.className = 'feedback positive';
      } else if (deltaHealth < 0 || deltaTrust < 0) {
        feedback.className = 'feedback negative';
      } else {
        feedback.className = 'feedback neutral';
      }
      feedback.textContent = message + ' ' + detail;

      addLogEntry(
        `ใช้ทรัพยากร: ${resourceKey} [ค่าใช้จ่าย ${cost}M] → Health ${deltaHealth >= 0 ? '+' : ''}${deltaHealth}, Trust ${deltaTrust >= 0 ? '+' : ''}${deltaTrust}, Budget ${deltaBudget >= 0 ? '+' : ''}${deltaBudget}M`,
        logType
      );

      // check game over
      if (cityHealth <= 0) {
        setGameOver('ความเสียหายต่อเมืองรุนแรงเกินไป (Health = 0)');
      } else if (cityBudget <= 0) {
        setGameOver('งบประมาณหมดลงก่อนควบคุมเหตุการณ์ได้ (Budget = 0)');
      } else if (publicTrust <= 0) {
        setGameOver('ความเชื่อมั่นของประชาชนหมดลง (Public Trust = 0)');
      }
    }

    function showHint() {
      if (!currentDisaster || gameOver) return;
      const { type, bestResource } = currentDisaster;
      let hint = '';

      if (type === 'flood') {
        hint =
          'ภัยนี้เกี่ยวกับ "น้ำ" โดยตรง · ลองคิดถึงทรัพยากรที่ใช้ควบคุมระดับน้ำและระบายออกจากพื้นที่ก่อนอย่างเร่งด่วน';
      } else if (type === 'fire') {
        hint =
          'ไฟไหม้ต้องควบคุม "เปลวไฟ" ให้ได้ก่อน แล้วค่อยอพยพคน ลองคิดถึงทรัพยากรที่มีอุปกรณ์และน้ำแรงดันสูง';
      } else if (type === 'wind') {
        hint =
          'ลมกรรโชกแรงทำให้สิ่งของปลิวและคนบาดเจ็บ · ทรัพยากรที่เน้น "เคลื่อนย้ายและช่วยเหลือคน" อาจเป็นจุดเริ่มต้นที่ดี';
      } else if (type === 'tornado') {
        hint =
          'ทอร์นาโดมีกำลังลมสูง · สิ่งสำคัญคือการอพยพคนไปอยู่ในที่ปลอดภัยก่อน คิดถึงทรัพยากรที่เกี่ยวกับ "ศูนย์อพยพ" หรือ "จุดหลบภัย"';
      }

      feedback.className = 'feedback neutral';
      feedback.textContent = 'Hint: ' + hint;
    }

    // -------------------------
    // Event listeners
    // -------------------------
    newGameBtn.addEventListener('click', startNewGame);
    nextIncidentBtn.addEventListener('click', generateNextDisaster);
    hintBtn.addEventListener('click', showHint);

    btnPump.addEventListener('click', () => handleResourceChoice('pump'));
    btnFiretruck.addEventListener('click', () =>
      handleResourceChoice('firetruck')
    );
    btnRescue.addEventListener('click', () => handleResourceChoice('rescue'));
    btnShelter.addEventListener('click', () =>
      handleResourceChoice('shelter')
    );

    // โหลดค่า best record ตอนเปิดหน้า
    refreshBestRecordUI();
  </script>
</body>
</html>
