<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Quant Finance Projects Grid</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    background: #f8f9fa;
    padding: 20px;
    color: #1a1a1a;
  }
  .container {
    max-width: 1500px;
    margin: 0 auto;
    background: white;
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    padding: 24px;
  }
  h1 { font-size: 24px; margin-bottom: 6px; }
  .subtitle { color: #666; margin-bottom: 20px; font-size: 13px; }

  .view-toggle {
    display: flex;
    gap: 8px;
    margin-bottom: 16px;
    padding: 4px;
    background: #f0f0f0;
    border-radius: 8px;
    width: fit-content;
  }
  .view-toggle button {
    padding: 8px 16px;
    border: none;
    background: transparent;
    border-radius: 6px;
    cursor: pointer;
    font-size: 13px;
    font-weight: 500;
    color: #555;
    transition: all 0.2s;
  }
  .view-toggle button.active {
    background: white;
    color: #1a1a1a;
    box-shadow: 0 1px 3px rgba(0,0,0,0.1);
  }

  .filter-panel {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    margin-bottom: 16px;
    padding: 16px;
    background: #fafafa;
    border-radius: 8px;
    border: 1px solid #eee;
  }
  .filter-section {
    display: flex;
    flex-direction: column;
  }
  .filter-section-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 8px;
  }
  .filter-section-title {
    font-size: 11px;
    font-weight: 700;
    color: #333;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }
  .filter-toggle-all {
    font-size: 10px;
    color: #2196F3;
    cursor: pointer;
    background: none;
    border: none;
    text-decoration: underline;
  }
  .filter-checkboxes {
    display: flex;
    flex-direction: column;
    gap: 4px;
    max-height: 150px;
    overflow-y: auto;
    padding-right: 4px;
  }
  .checkbox-label {
    display: flex;
    align-items: center;
    gap: 6px;
    font-size: 12px;
    cursor: pointer;
    padding: 3px 4px;
    border-radius: 4px;
    transition: background 0.15s;
  }
  .checkbox-label:hover { background: #eee; }
  .checkbox-label input[type="checkbox"] { cursor: pointer; }
  .color-swatch {
    width: 10px;
    height: 10px;
    border-radius: 2px;
    flex-shrink: 0;
  }

  .stats {
    display: flex;
    gap: 16px;
    margin-bottom: 16px;
    padding: 12px;
    background: #f5f5f5;
    border-radius: 8px;
  }
  .stat { flex: 1; text-align: center; }
  .stat-value { font-size: 22px; font-weight: 700; color: #2196F3; }
  .stat-label { font-size: 11px; color: #666; text-transform: uppercase; letter-spacing: 0.5px; margin-top: 2px; }

  #chart {
    width: 100%;
    border: 1px solid #eee;
    border-radius: 8px;
    background: #fdfdfd;
    overflow: auto;
  }
  #chart svg { display: block; }

  .axis-label { font-size: 12px; font-weight: 600; fill: #333; }
  .axis-tick { font-size: 11px; fill: #555; }
  .grid-line { stroke: #e8e8e8; stroke-width: 1; }
  .grid-band { fill: #f5f5f5; opacity: 0.3; }

  .bubble { cursor: pointer; transition: opacity 0.2s; }
  .bubble:hover { stroke-width: 3px; }
  .bubble.secondary {
    stroke-dasharray: 3 2;
    opacity: 0.5;
  }

  .tooltip {
    position: absolute;
    padding: 10px 14px;
    background: rgba(0,0,0,0.92);
    color: white;
    border-radius: 6px;
    pointer-events: none;
    font-size: 12px;
    line-height: 1.6;
    max-width: 300px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.3);
    z-index: 1000;
    opacity: 0;
    transition: opacity 0.15s;
  }
  .tooltip.visible { opacity: 1; }
  .tooltip-title {
    font-weight: 700;
    margin-bottom: 6px;
    font-size: 13px;
    border-bottom: 1px solid rgba(255,255,255,0.3);
    padding-bottom: 4px;
  }
  .tooltip-row { margin: 3px 0; }
  .tooltip-label { color: #aaa; }
  .multi-badge {
    display: inline-block;
    background: #FF5722;
    color: white;
    font-size: 10px;
    padding: 2px 6px;
    border-radius: 8px;
    margin-left: 4px;
  }

  .legend {
    margin-top: 16px;
    display: flex;
    gap: 24px;
    flex-wrap: wrap;
    padding: 14px;
    background: #f9f9f9;
    border-radius: 8px;
  }
  .legend-section { flex: 1; min-width: 180px; }
  .legend-title {
    font-size: 11px;
    font-weight: 700;
    color: #333;
    margin-bottom: 8px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }
  .legend-item {
    display: flex;
    align-items: center;
    gap: 6px;
    margin: 4px 0;
    font-size: 12px;
  }
  .legend-color { width: 14px; height: 14px; border-radius: 50%; }
  .legend-color.bordered { background: transparent; border: 3px solid; }

  .info-text {
    font-size: 11px;
    color: #888;
    margin-top: 10px;
    font-style: italic;
  }
</style>
</head>
<body>
<div class="container">
  <h1>🎯 Quant Finance Projects Portfolio</h1>
  <p class="subtitle">Full portfolio: CV projects, GitHub pins, syllabus work, learning exercises, and research backlog</p>

  <div class="view-toggle">
    <button id="viewMLDomain" class="active">ML Category × Domain</button>
    <button id="viewMLComplexity">ML Category × Complexity</button>
    <button id="viewDomainComplexity">Domain × Complexity</button>
  </div>

  <div class="filter-panel">
    <div class="filter-section">
      <div class="filter-section-header">
        <span class="filter-section-title">ML Category</span>
        <button class="filter-toggle-all" data-group="mlCategory">Toggle all</button>
      </div>
      <div class="filter-checkboxes" id="filterMLCategory"></div>
    </div>
    <div class="filter-section">
      <div class="filter-section-header">
        <span class="filter-section-title">Domain</span>
        <button class="filter-toggle-all" data-group="domain">Toggle all</button>
      </div>
      <div class="filter-checkboxes" id="filterDomain"></div>
    </div>
    <div class="filter-section">
      <div class="filter-section-header">
        <span class="filter-section-title">Complexity</span>
        <button class="filter-toggle-all" data-group="complexity">Toggle all</button>
      </div>
      <div class="filter-checkboxes" id="filterComplexity"></div>
    </div>
    <div class="filter-section">
      <div class="filter-section-header">
        <span class="filter-section-title">Tier</span>
        <button class="filter-toggle-all" data-group="tier">Toggle all</button>
      </div>
      <div class="filter-checkboxes" id="filterTier"></div>
    </div>
  </div>

  <div class="stats">
    <div class="stat"><div class="stat-value" id="statProjects">0</div><div class="stat-label">Visible Projects</div></div>
    <div class="stat"><div class="stat-value" id="statMulti">0</div><div class="stat-label">Multi-Category</div></div>
    <div class="stat"><div class="stat-value" id="statCategories">0</div><div class="stat-label">ML Categories</div></div>
    <div class="stat"><div class="stat-value" id="statDomains">0</div><div class="stat-label">Domains</div></div>
  </div>

  <div id="chart"></div>
  <p class="info-text">💡 Hover bubbles for details • Multi-category projects appear in each of their categories (solid = primary, dashed = secondary) • Use filters to focus on specific subsets</p>

  <div class="legend">
    <div class="legend-section">
      <div class="legend-title">Tier (Fill Color)</div>
      <div id="legendTier"></div>
    </div>
    <div class="legend-section">
      <div class="legend-title">Complexity (Size)</div>
      <div class="legend-item"><span class="legend-color" style="background:#999;width:12px;height:12px"></span> Foundation</div>
      <div class="legend-item"><span class="legend-color" style="background:#999;width:16px;height:16px"></span> Intermediate</div>
      <div class="legend-item"><span class="legend-color" style="background:#999;width:22px;height:22px"></span> Advanced</div>
      <div class="legend-item"><span class="legend-color" style="background:#999;width:28px;height:28px"></span> Research-Grade</div>
    </div>
    <div class="legend-section">
      <div class="legend-title">Multi-Category Indicator</div>
      <div class="legend-item"><svg width="20" height="20"><circle cx="10" cy="10" r="8" fill="#999" stroke="#333" stroke-width="2"/></svg> Primary (solid border)</div>
      <div class="legend-item"><svg width="20" height="20"><circle cx="10" cy="10" r="8" fill="#999" stroke="#333" stroke-width="2" stroke-dasharray="3 2" opacity="0.5"/></svg> Secondary (dashed)</div>
    </div>
  </div>
</div>

<div class="tooltip" id="tooltip"></div>

<script>
// ============ DATA — Multi-category support ============
// mlCategories is now an ARRAY (first = primary)
const projects = [
  {id:0, name:"Tech Adoption Classifier", mlCategories:["Unsupervised","Supervised"], techniques:["K-Means","NLP","Clustering"], domain:"Alternative Data", complexity:"Advanced", tier:"CV"},
  {id:1, name:"Econometrics Portfolio", mlCategories:["Supervised","Statistical Methods"], techniques:["Linear Regression","LASSO/Ridge","GARCH"], domain:"Factor Models", complexity:"Research-Grade", tier:"CV"},
  {id:2, name:"Backtesting Framework", mlCategories:["Numerical Methods","Engineering"], techniques:["Monte Carlo","Optimization","Simulation"], domain:"Strategy Development", complexity:"Advanced", tier:"CV"},
  {id:3, name:"Stat Arb Suite", mlCategories:["Statistical Methods"], techniques:["Cointegration","Time Series"], domain:"Strategy Development", complexity:"Advanced", tier:"CV"},
  {id:4, name:"VaR & Stress Testing", mlCategories:["Numerical Methods","Statistical Methods"], techniques:["Monte Carlo","Scenario Analysis"], domain:"Risk Management", complexity:"Advanced", tier:"GitHub Pin"},
  {id:5, name:"Patent Network", mlCategories:["Unsupervised"], techniques:["Community Detection","Network Analysis","Clustering"], domain:"Alternative Data", complexity:"Advanced", tier:"GitHub Pin"},
  {id:6, name:"Factor Attribution", mlCategories:["Statistical Methods","Supervised"], techniques:["Linear Regression","Decomposition"], domain:"Portfolio Construction", complexity:"Advanced", tier:"GitHub Pin"},
  {id:7, name:"TAA Regime Detection", mlCategories:["Unsupervised"], techniques:["HMM","Time Series"], domain:"Macro Analysis", complexity:"Advanced", tier:"GitHub Pin"},
  {id:8, name:"GARCH + LSTM", mlCategories:["Deep Learning","Statistical Methods"], techniques:["GARCH","LSTM","Time Series"], domain:"Risk Management", complexity:"Advanced", tier:"GitHub Pin"},
  {id:9, name:"Data Pipeline", mlCategories:["Engineering"], techniques:["ETL","APIs"], domain:"Infrastructure", complexity:"Intermediate", tier:"GitHub Pin"},
  {id:10, name:"Alpha Decay Study", mlCategories:["Statistical Methods"], techniques:["Time Series"], domain:"Market Microstructure", complexity:"Advanced", tier:"GitHub Pin"},
  {id:11, name:"2008 Crisis Test", mlCategories:["Numerical Methods"], techniques:["Scenario Analysis"], domain:"Risk Management", complexity:"Intermediate", tier:"GitHub Pin"},
  {id:12, name:"Golden Cross", mlCategories:["Statistical Methods"], techniques:["Technical Indicators","Time Series"], domain:"Strategy Development", complexity:"Foundation", tier:"Technical Deep Dive"},
  {id:13, name:"Options Greeks", mlCategories:["Numerical Methods"], techniques:["Black-Scholes","Finite Difference"], domain:"Derivatives", complexity:"Intermediate", tier:"Technical Deep Dive"},
  {id:14, name:"Regime Framework", mlCategories:["Unsupervised","Statistical Methods"], techniques:["HMM","Clustering","Time Series"], domain:"Macro Analysis", complexity:"Advanced", tier:"Technical Deep Dive"},
  {id:15, name:"Short Scoring", mlCategories:["Supervised"], techniques:["Scoring Models"], domain:"Strategy Development", complexity:"Intermediate", tier:"Technical Deep Dive"},
  {id:16, name:"Liquidity Risk", mlCategories:["Statistical Methods"], techniques:["Time Series","Risk Metrics"], domain:"Risk Management", complexity:"Intermediate", tier:"Technical Deep Dive"},
  {id:17, name:"Earnings Sentiment", mlCategories:["Supervised"], techniques:["NLP","Sentiment Analysis"], domain:"Alternative Data", complexity:"Intermediate", tier:"Technical Deep Dive"},
  {id:18, name:"Kalman Pairs", mlCategories:["Statistical Methods"], techniques:["Kalman Filter","Cointegration","Time Series"], domain:"Strategy Development", complexity:"Advanced", tier:"Technical Deep Dive"},
  {id:19, name:"Vol Crush", mlCategories:["Statistical Methods","Numerical Methods"], techniques:["Options Pricing","Vol Surface"], domain:"Derivatives", complexity:"Advanced", tier:"Technical Deep Dive"},
  {id:20, name:"Cross-Sectional Mean Rev", mlCategories:["Statistical Methods","Supervised"], techniques:["Cross-Sectional Regression","Time Series"], domain:"Strategy Development", complexity:"Advanced", tier:"Technical Deep Dive"},
  {id:21, name:"Dispersion Vol Arb", mlCategories:["Statistical Methods","Numerical Methods"], techniques:["Options Pricing","Correlation"], domain:"Derivatives", complexity:"Advanced", tier:"Technical Deep Dive"},
  {id:22, name:"Random Forest", mlCategories:["Supervised"], techniques:["Random Forest","Feature Importance"], domain:"Factor Models", complexity:"Advanced", tier:"Technical Deep Dive"},
  {id:23, name:"XGBoost", mlCategories:["Supervised"], techniques:["XGBoost","Gradient Boosting"], domain:"Strategy Development", complexity:"Advanced", tier:"Technical Deep Dive"},
  {id:24, name:"Risk Model Library", mlCategories:["Unsupervised","Statistical Methods"], techniques:["PCA","Factor Analysis"], domain:"Risk Management", complexity:"Advanced", tier:"Tools"},
  {id:25, name:"Risk Metrics Library", mlCategories:["Statistical Methods","Engineering"], techniques:["Risk Metrics"], domain:"Risk Management", complexity:"Intermediate", tier:"Tools"},
  {id:26, name:"Performance Decomp", mlCategories:["Statistical Methods"], techniques:["Attribution","Decomposition"], domain:"Portfolio Construction", complexity:"Advanced", tier:"Tools"},
  {id:27, name:"Fund Comparison", mlCategories:["Statistical Methods"], techniques:["Benchmarking"], domain:"Portfolio Construction", complexity:"Intermediate", tier:"Case Study"},
  {id:28, name:"Pairs Simulator", mlCategories:["Statistical Methods"], techniques:["Cointegration","Time Series"], domain:"Strategy Development", complexity:"Intermediate", tier:"Case Study"},
  {id:29, name:"Crypto Vol Regime", mlCategories:["Unsupervised","Statistical Methods"], techniques:["HMM","GARCH"], domain:"Alternative Data", complexity:"Intermediate", tier:"Case Study"},
  {id:30, name:"Risk Limits", mlCategories:["Statistical Methods","Engineering"], techniques:["Risk Metrics"], domain:"Risk Management", complexity:"Intermediate", tier:"Case Study"},
  {id:31, name:"Surprise Index", mlCategories:["Statistical Methods"], techniques:["Nowcasting","Time Series"], domain:"Macro Analysis", complexity:"Intermediate", tier:"Case Study"},
  {id:32, name:"Value Chain", mlCategories:["Unsupervised"], techniques:["Network Analysis","Clustering"], domain:"Alternative Data", complexity:"Advanced", tier:"L/S Equity"},
  {id:33, name:"Platform Competition", mlCategories:["Statistical Methods","Supervised"], techniques:["Classification"], domain:"Strategy Development", complexity:"Advanced", tier:"L/S Equity"},
  {id:34, name:"Network Effects", mlCategories:["Unsupervised"], techniques:["Network Analysis"], domain:"Alternative Data", complexity:"Advanced", tier:"L/S Equity"},
  {id:35, name:"Fund Peer Tool", mlCategories:["Statistical Methods"], techniques:["Benchmarking"], domain:"Portfolio Construction", complexity:"Intermediate", tier:"Portfolio Analyst"},
  {id:36, name:"P&L Decomp", mlCategories:["Statistical Methods"], techniques:["Attribution","Decomposition"], domain:"Portfolio Construction", complexity:"Advanced", tier:"Portfolio Analyst"},

  // ============ SYLLABUS MANDATED (Personal Learning) ============
  {id:37, name:"Numerical PDE Solver", mlCategories:["Numerical Methods"], techniques:["Finite Difference","PDE"], domain:"Derivatives", complexity:"Intermediate", tier:"Syllabus"},
  {id:38, name:"Options & Vol Module", mlCategories:["Numerical Methods","Statistical Methods"], techniques:["Black-Scholes","Vol Modeling"], domain:"Derivatives", complexity:"Intermediate", tier:"Syllabus"},
  {id:39, name:"Credit Strategies Module", mlCategories:["Statistical Methods"], techniques:["Credit Models","Spreads"], domain:"Strategy Development", complexity:"Intermediate", tier:"Syllabus"},
  {id:40, name:"Macro Strategies Module", mlCategories:["Statistical Methods"], techniques:["Macro Indicators"], domain:"Macro Analysis", complexity:"Intermediate", tier:"Syllabus"},
  {id:41, name:"Portfolio Construction Module", mlCategories:["Numerical Methods"], techniques:["Mean-Variance","Optimization"], domain:"Portfolio Construction", complexity:"Intermediate", tier:"Syllabus"},
  {id:42, name:"Position Sizing Module", mlCategories:["Numerical Methods"], techniques:["Kelly Criterion","Sizing"], domain:"Portfolio Construction", complexity:"Foundation", tier:"Syllabus"},
  {id:43, name:"Tail Risk Module", mlCategories:["Statistical Methods"], techniques:["Tail Risk","Hedging"], domain:"Risk Management", complexity:"Intermediate", tier:"Syllabus"},
  {id:44, name:"Monetary Policy & Yield Curves", mlCategories:["Statistical Methods"], techniques:["Yield Curves","Rate Models"], domain:"Macro Analysis", complexity:"Foundation", tier:"Syllabus"},
  {id:45, name:"Economic Forecasting Module", mlCategories:["Statistical Methods","Supervised"], techniques:["Forecasting","Time Series"], domain:"Macro Analysis", complexity:"Intermediate", tier:"Syllabus"},
  {id:46, name:"Macro Trading Module", mlCategories:["Statistical Methods"], techniques:["Macro Signals"], domain:"Macro Analysis", complexity:"Intermediate", tier:"Syllabus"},
  {id:47, name:"Google Colab Setup", mlCategories:["Engineering"], techniques:["Cloud Compute"], domain:"Infrastructure", complexity:"Foundation", tier:"Syllabus"},
  {id:48, name:"Bloomberg Terminal", mlCategories:["Engineering"], techniques:["Data Terminal"], domain:"Infrastructure", complexity:"Foundation", tier:"Syllabus"},

  // ============ LEARNING EXERCISES ============
  {id:49, name:"Black-Scholes Pricing", mlCategories:["Numerical Methods"], techniques:["Black-Scholes"], domain:"Derivatives", complexity:"Foundation", tier:"Learning Exercise"},
  {id:50, name:"MC Option Pricer", mlCategories:["Numerical Methods"], techniques:["Monte Carlo"], domain:"Derivatives", complexity:"Foundation", tier:"Learning Exercise"},
  {id:51, name:"Mean-Variance Optimization", mlCategories:["Numerical Methods"], techniques:["Optimization"], domain:"Portfolio Construction", complexity:"Foundation", tier:"Learning Exercise"},
  {id:52, name:"Correlation Matrix Viz", mlCategories:["Statistical Methods"], techniques:["Correlation"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:53, name:"Return Distribution Analysis", mlCategories:["Statistical Methods"], techniques:["Distributions"], domain:"Risk Management", complexity:"Foundation", tier:"Learning Exercise"},
  {id:54, name:"Risk Parity Basics", mlCategories:["Statistical Methods"], techniques:["Risk Parity"], domain:"Risk Management", complexity:"Foundation", tier:"Learning Exercise"},
  {id:55, name:"Moving Average Strategies", mlCategories:["Statistical Methods"], techniques:["Technical Indicators"], domain:"Strategy Development", complexity:"Foundation", tier:"Learning Exercise"},
  {id:56, name:"RSI/MACD Testing", mlCategories:["Statistical Methods"], techniques:["Technical Indicators"], domain:"Strategy Development", complexity:"Foundation", tier:"Learning Exercise"},
  {id:57, name:"Covariance Estimation", mlCategories:["Statistical Methods"], techniques:["Covariance"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:58, name:"Bootstrap Resampling", mlCategories:["Statistical Methods"], techniques:["Resampling"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:59, name:"MLE Practice", mlCategories:["Statistical Methods"], techniques:["Maximum Likelihood"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:60, name:"Hypothesis Testing", mlCategories:["Statistical Methods"], techniques:["Hypothesis Testing"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:61, name:"Time Series Decomposition", mlCategories:["Statistical Methods"], techniques:["Time Series"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:62, name:"ACF/PACF Analysis", mlCategories:["Statistical Methods"], techniques:["Autocorrelation"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:63, name:"Linear Regression Basics", mlCategories:["Supervised"], techniques:["Linear Regression"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:64, name:"Logistic Regression Basics", mlCategories:["Supervised"], techniques:["Logistic Regression"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:65, name:"K-Means Basics", mlCategories:["Unsupervised"], techniques:["K-Means"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:66, name:"PCA Basics", mlCategories:["Unsupervised"], techniques:["PCA"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:67, name:"Cross-Validation", mlCategories:["Supervised"], techniques:["Cross-Validation"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},
  {id:68, name:"Grid Search HP Tuning", mlCategories:["Supervised"], techniques:["Hyperparameter Tuning"], domain:"Foundations", complexity:"Foundation", tier:"Learning Exercise"},

  // ============ RESEARCH / EXPERIMENTAL BACKLOG ============
  {id:69, name:"Full Value Chain Analysis", mlCategories:["Unsupervised"], techniques:["Network Analysis","Clustering"], domain:"Alternative Data", complexity:"Advanced", tier:"Research Backlog"},
  {id:70, name:"2nd/3rd Order Company ID", mlCategories:["Unsupervised"], techniques:["Network Analysis"], domain:"Alternative Data", complexity:"Advanced", tier:"Research Backlog"},
  {id:71, name:"TFP & Productivity Metrics", mlCategories:["Statistical Methods"], techniques:["Productivity Analysis"], domain:"Macro Analysis", complexity:"Advanced", tier:"Research Backlog"},
  {id:72, name:"R&D Efficiency Scoring", mlCategories:["Supervised","Statistical Methods"], techniques:["Scoring Models"], domain:"Alternative Data", complexity:"Advanced", tier:"Research Backlog"},
  {id:73, name:"VC Survival/Hazard Model", mlCategories:["Supervised","Statistical Methods"], techniques:["Survival Analysis"], domain:"Alternative Data", complexity:"Advanced", tier:"Research Backlog"},
  {id:74, name:"Regulatory Shocks Causal Inference", mlCategories:["Statistical Methods"], techniques:["Causal Inference","Diff-in-Diff"], domain:"Macro Analysis", complexity:"Research-Grade", tier:"Research Backlog"},
  {id:75, name:"Platform Competition Modeling", mlCategories:["Statistical Methods","Supervised"], techniques:["Game Theory","Classification"], domain:"Strategy Development", complexity:"Advanced", tier:"Research Backlog"},
  {id:76, name:"Network Effects Quantification", mlCategories:["Unsupervised"], techniques:["Network Analysis","Graph Metrics"], domain:"Alternative Data", complexity:"Advanced", tier:"Research Backlog"},
  {id:77, name:"Reddit/Twitter Sentiment", mlCategories:["Supervised"], techniques:["NLP","Sentiment Analysis"], domain:"Alternative Data", complexity:"Intermediate", tier:"Research Backlog"},
  {id:78, name:"Job Postings Sector Health", mlCategories:["Supervised"], techniques:["Web Scraping","Feature Engineering"], domain:"Alternative Data", complexity:"Intermediate", tier:"Research Backlog"},
  {id:79, name:"Satellite Imagery Analysis", mlCategories:["Deep Learning","Supervised"], techniques:["Computer Vision","CNN"], domain:"Alternative Data", complexity:"Advanced", tier:"Research Backlog"},
  {id:80, name:"Web Scraping Pipeline", mlCategories:["Engineering"], techniques:["Web Scraping","ETL"], domain:"Alternative Data", complexity:"Intermediate", tier:"Research Backlog"},

  // ============ NEW ADDITIONS — MAY 2026 ============
  {id:81, name:"ML Return Prediction", mlCategories:["Supervised","Statistical Methods"], techniques:["XGBoost","Purged CV","SHAP","Cross-Sectional"], domain:"Factor Models", complexity:"Research-Grade", tier:"GitHub Pin"},
  {id:82, name:"Purged Walk-Forward CV", mlCategories:["Statistical Methods","Engineering"], techniques:["Purged CV","Embargo","Cross-Validation"], domain:"Infrastructure", complexity:"Advanced", tier:"Technical Deep Dive"}
];

// ============ COLORS & SIZES ============
const mlCategoryOrder = ["Engineering","Numerical Methods","Statistical Methods","Supervised","Unsupervised","Deep Learning"];
const mlCategoryColors = {
  "Supervised":"#FFC107", "Unsupervised":"#2196F3", "Deep Learning":"#E91E63",
  "Statistical Methods":"#4CAF50", "Numerical Methods":"#9C27B0", "Engineering":"#607D8B"
};
const complexityOrder = ["Foundation","Intermediate","Advanced","Research-Grade"];
const complexitySize = {"Foundation":10, "Intermediate":14, "Advanced":18, "Research-Grade":22};
const tierColors = {
  "CV":"#FF5722", "GitHub Pin":"#FF9800", "Technical Deep Dive":"#2196F3",
  "Tools":"#4CAF50", "Case Study":"#9C27B0", "L/S Equity":"#00BCD4", "Portfolio Analyst":"#795548",
  "Syllabus":"#546E7A", "Learning Exercise":"#B0BEC5", "Research Backlog":"#EC407A"
};

// ============ STATE ============
const allMLCategories = [...new Set(projects.flatMap(p => p.mlCategories))];
const allDomains = [...new Set(projects.map(p => p.domain))];
const allComplexity = complexityOrder;
const allTiers = [...new Set(projects.map(p => p.tier))];

let selected = {
  mlCategory: new Set(allMLCategories),
  domain: new Set(allDomains),
  complexity: new Set(allComplexity),
  tier: new Set(allTiers)
};

let currentView = 'MLDomain'; // 'MLDomain', 'MLComplexity', 'DomainComplexity'

// ============ BUILD CHECKBOXES ============
function buildCheckboxes(containerId, items, group, colorMap) {
  const container = document.getElementById(containerId);
  container.innerHTML = '';
  items.forEach(item => {
    const label = document.createElement('label');
    label.className = 'checkbox-label';
    const cb = document.createElement('input');
    cb.type = 'checkbox';
    cb.checked = true;
    cb.dataset.group = group;
    cb.dataset.value = item;
    cb.addEventListener('change', () => {
      if (cb.checked) selected[group].add(item);
      else selected[group].delete(item);
      render();
    });
    const swatch = document.createElement('span');
    swatch.className = 'color-swatch';
    if (colorMap && colorMap[item]) {
      swatch.style.background = colorMap[item];
    } else {
      swatch.style.display = 'none';
    }
    const span = document.createElement('span');
    span.textContent = item;
    label.appendChild(cb);
    if (colorMap && colorMap[item]) label.appendChild(swatch);
    label.appendChild(span);
    container.appendChild(label);
  });
}

buildCheckboxes('filterMLCategory', mlCategoryOrder.filter(c => allMLCategories.includes(c)), 'mlCategory', mlCategoryColors);
buildCheckboxes('filterDomain', allDomains.sort(), 'domain', null);
buildCheckboxes('filterComplexity', complexityOrder, 'complexity', null);
buildCheckboxes('filterTier', allTiers, 'tier', tierColors);

// Toggle-all buttons
document.querySelectorAll('.filter-toggle-all').forEach(btn => {
  btn.addEventListener('click', () => {
    const group = btn.dataset.group;
    const containerId = 'filter' + group.charAt(0).toUpperCase() + group.slice(1);
    const checkboxes = document.querySelectorAll(`#${containerId} input[type="checkbox"]`);
    const anyChecked = Array.from(checkboxes).some(cb => cb.checked);
    checkboxes.forEach(cb => {
      cb.checked = !anyChecked;
      if (cb.checked) selected[group].add(cb.dataset.value);
      else selected[group].delete(cb.dataset.value);
    });
    render();
  });
});

// View toggle
document.getElementById('viewMLDomain').addEventListener('click', () => switchView('MLDomain'));
document.getElementById('viewMLComplexity').addEventListener('click', () => switchView('MLComplexity'));
document.getElementById('viewDomainComplexity').addEventListener('click', () => switchView('DomainComplexity'));

function switchView(view) {
  currentView = view;
  document.querySelectorAll('.view-toggle button').forEach(b => b.classList.remove('active'));
  document.getElementById('view' + view).classList.add('active');
  render();
}

// ============ RENDER ============
const tooltip = document.getElementById('tooltip');

function getVisibleProjects() {
  return projects.filter(p =>
    p.mlCategories.some(c => selected.mlCategory.has(c)) &&
    selected.domain.has(p.domain) &&
    selected.complexity.has(p.complexity) &&
    selected.tier.has(p.tier)
  );
}

function getAxes() {
  if (currentView === 'MLDomain') {
    return {
      xAxis: mlCategoryOrder.filter(c => allMLCategories.includes(c) && selected.mlCategory.has(c)),
      yAxis: [...selected.domain].sort(),
      xLabel: 'ML Category',
      yLabel: 'Domain',
      xKey: 'mlCategory',
      yKey: 'domain'
    };
  } else if (currentView === 'MLComplexity') {
    return {
      xAxis: mlCategoryOrder.filter(c => allMLCategories.includes(c) && selected.mlCategory.has(c)),
      yAxis: complexityOrder.filter(c => selected.complexity.has(c)),
      xLabel: 'ML Category',
      yLabel: 'Complexity',
      xKey: 'mlCategory',
      yKey: 'complexity'
    };
  } else { // DomainComplexity
    return {
      xAxis: [...selected.domain].sort(),
      yAxis: complexityOrder.filter(c => selected.complexity.has(c)),
      xLabel: 'Domain',
      yLabel: 'Complexity',
      xKey: 'domain',
      yKey: 'complexity'
    };
  }
}

function render() {
  const chart = document.getElementById('chart');
  const visible = getVisibleProjects();
  const axes = getAxes();

  // Calc dimensions
  const marginLeft = 180;
  const marginTop = 50;
  const marginRight = 20;
  const marginBottom = 30;
  const cellWidth = Math.max(140, (chart.offsetWidth - marginLeft - marginRight) / Math.max(axes.xAxis.length, 1));
  const cellHeight = 90;
  const innerWidth = cellWidth * axes.xAxis.length;
  const innerHeight = cellHeight * axes.yAxis.length;
  const svgWidth = marginLeft + innerWidth + marginRight;
  const svgHeight = marginTop + innerHeight + marginBottom;

  // Build bubbles: for each visible project, place in each of its categories (if applicable)
  const bubbles = [];
  visible.forEach(p => {
    if (axes.xKey === 'mlCategory') {
      // Project may appear in multiple X columns
      const matchingCats = p.mlCategories.filter(c => axes.xAxis.includes(c));
      matchingCats.forEach((cat, idx) => {
        const yVal = axes.yKey === 'mlCategory' ? cat : p[axes.yKey];
        if (!axes.yAxis.includes(yVal)) return;
        bubbles.push({
          project: p,
          xVal: cat,
          yVal: yVal,
          isPrimary: idx === 0 || cat === p.mlCategories[0],
          isMulti: p.mlCategories.length > 1
        });
      });
    } else if (axes.yKey === 'mlCategory') {
      const matchingCats = p.mlCategories.filter(c => axes.yAxis.includes(c));
      matchingCats.forEach((cat, idx) => {
        const xVal = p[axes.xKey];
        if (!axes.xAxis.includes(xVal)) return;
        bubbles.push({
          project: p,
          xVal: xVal,
          yVal: cat,
          isPrimary: idx === 0 || cat === p.mlCategories[0],
          isMulti: p.mlCategories.length > 1
        });
      });
    } else {
      // Neither axis is ML category — show once
      const xVal = p[axes.xKey];
      const yVal = p[axes.yKey];
      if (axes.xAxis.includes(xVal) && axes.yAxis.includes(yVal)) {
        bubbles.push({
          project: p,
          xVal: xVal,
          yVal: yVal,
          isPrimary: true,
          isMulti: p.mlCategories.length > 1
        });
      }
    }
  });

  // Group bubbles by cell for jitter positioning
  const cellGroups = {};
  bubbles.forEach(b => {
    const key = `${b.xVal}__${b.yVal}`;
    if (!cellGroups[key]) cellGroups[key] = [];
    cellGroups[key].push(b);
  });

  // Position within cells (packed circles)
  Object.values(cellGroups).forEach(group => {
    const n = group.length;
    if (n === 1) {
      group[0].cellX = 0.5;
      group[0].cellY = 0.5;
    } else {
      // Grid packing
      const cols = Math.ceil(Math.sqrt(n));
      const rows = Math.ceil(n / cols);
      group.forEach((b, i) => {
        const col = i % cols;
        const row = Math.floor(i / cols);
        b.cellX = (col + 0.5) / cols;
        b.cellY = (row + 0.5) / rows;
      });
    }
  });

  // Build SVG
  const svgNS = "http://www.w3.org/2000/svg";
  let svg = `<svg xmlns="${svgNS}" width="${svgWidth}" height="${svgHeight}" viewBox="0 0 ${svgWidth} ${svgHeight}">`;

  // Grid bands (alternate row backgrounds)
  axes.yAxis.forEach((y, i) => {
    if (i % 2 === 0) {
      svg += `<rect class="grid-band" x="${marginLeft}" y="${marginTop + i*cellHeight}" width="${innerWidth}" height="${cellHeight}"/>`;
    }
  });

  // Vertical grid lines
  for (let i = 0; i <= axes.xAxis.length; i++) {
    svg += `<line class="grid-line" x1="${marginLeft + i*cellWidth}" y1="${marginTop}" x2="${marginLeft + i*cellWidth}" y2="${marginTop + innerHeight}"/>`;
  }
  // Horizontal grid lines
  for (let i = 0; i <= axes.yAxis.length; i++) {
    svg += `<line class="grid-line" x1="${marginLeft}" y1="${marginTop + i*cellHeight}" x2="${marginLeft + innerWidth}" y2="${marginTop + i*cellHeight}"/>`;
  }

  // X-axis labels
  axes.xAxis.forEach((x, i) => {
    const cx = marginLeft + (i + 0.5) * cellWidth;
    svg += `<text class="axis-tick" x="${cx}" y="${marginTop - 10}" text-anchor="middle">${x}</text>`;
  });
  // Y-axis labels
  axes.yAxis.forEach((y, i) => {
    const cy = marginTop + (i + 0.5) * cellHeight;
    svg += `<text class="axis-tick" x="${marginLeft - 10}" y="${cy + 4}" text-anchor="end">${y}</text>`;
  });

  // X-axis title
  svg += `<text class="axis-label" x="${marginLeft + innerWidth/2}" y="${marginTop - 30}" text-anchor="middle">${axes.xLabel}</text>`;
  // Y-axis title
  svg += `<text class="axis-label" x="${marginLeft - 160}" y="${marginTop + innerHeight/2}" text-anchor="start" transform="rotate(-90 ${marginLeft - 160} ${marginTop + innerHeight/2})">${axes.yLabel}</text>`;

  // Bubbles (primary on top of secondary)
  const sortedBubbles = [...bubbles].sort((a, b) => (a.isPrimary ? 1 : 0) - (b.isPrimary ? 1 : 0));
  sortedBubbles.forEach((b, idx) => {
    const xIdx = axes.xAxis.indexOf(b.xVal);
    const yIdx = axes.yAxis.indexOf(b.yVal);
    if (xIdx < 0 || yIdx < 0) return;
    const cx = marginLeft + xIdx*cellWidth + b.cellX*cellWidth;
    const cy = marginTop + yIdx*cellHeight + b.cellY*cellHeight;
    const r = complexitySize[b.project.complexity];
    const fill = tierColors[b.project.tier];
    const stroke = b.isPrimary ? '#1a1a1a' : '#666';
    const strokeWidth = b.isPrimary ? 2 : 1.5;
    const dashArray = b.isPrimary ? '' : 'stroke-dasharray="3 2"';
    const opacity = b.isPrimary ? 0.92 : 0.5;
    const cls = b.isPrimary ? 'bubble' : 'bubble secondary';
    svg += `<circle class="${cls}" cx="${cx}" cy="${cy}" r="${r}" fill="${fill}" stroke="${stroke}" stroke-width="${strokeWidth}" ${dashArray} opacity="${opacity}" data-bubble-idx="${idx}"/>`;
  });

  svg += '</svg>';
  chart.innerHTML = svg;

  // Wire tooltips
  const circles = chart.querySelectorAll('circle.bubble');
  circles.forEach(circle => {
    const idx = parseInt(circle.getAttribute('data-bubble-idx'));
    const b = sortedBubbles[idx];
    circle.addEventListener('mousemove', e => showTooltip(b, e));
    circle.addEventListener('mouseleave', hideTooltip);
  });

  // Stats
  document.getElementById('statProjects').textContent = visible.length;
  document.getElementById('statMulti').textContent = visible.filter(p => p.mlCategories.length > 1).length;
  document.getElementById('statCategories').textContent = new Set(visible.flatMap(p => p.mlCategories)).size;
  document.getElementById('statDomains').textContent = new Set(visible.map(p => p.domain)).size;
}

function showTooltip(b, event) {
  const p = b.project;
  const multiBadge = b.isMulti ? `<span class="multi-badge">${p.mlCategories.length} categories</span>` : '';
  tooltip.innerHTML = `
    <div class="tooltip-title">${p.name}${multiBadge}</div>
    <div class="tooltip-row"><span class="tooltip-label">Categories:</span> ${p.mlCategories.join(", ")}</div>
    <div class="tooltip-row"><span class="tooltip-label">Techniques:</span> ${p.techniques.join(", ")}</div>
    <div class="tooltip-row"><span class="tooltip-label">Domain:</span> ${p.domain}</div>
    <div class="tooltip-row"><span class="tooltip-label">Complexity:</span> ${p.complexity}</div>
    <div class="tooltip-row"><span class="tooltip-label">Tier:</span> ${p.tier}</div>
    ${!b.isPrimary ? '<div class="tooltip-row" style="color:#FFC107;font-style:italic;margin-top:4px">↳ Shown here as secondary category</div>' : ''}
  `;
  tooltip.style.left = (event.pageX + 12) + "px";
  tooltip.style.top = (event.pageY - 10) + "px";
  tooltip.classList.add("visible");
}

function hideTooltip() {
  tooltip.classList.remove("visible");
}

// ============ LEGENDS ============
const tierLegendEl = document.getElementById('legendTier');
Object.entries(tierColors).forEach(([tier, color]) => {
  if (!allTiers.includes(tier)) return;
  const item = document.createElement('div');
  item.className = 'legend-item';
  item.innerHTML = `<div class="legend-color" style="background:${color}"></div><span>${tier}</span>`;
  tierLegendEl.appendChild(item);
});

// ============ INITIAL RENDER ============
render();
window.addEventListener('resize', render);
</script>
</body>
</html>
