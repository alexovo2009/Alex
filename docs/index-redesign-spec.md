# index.html 重新設計規格

## 頁面結構

### 1. HTML 骨架
```html
<!DOCTYPE html>
<html lang="zh-HK" data-theme="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Alex's Game Center - 探索精彩遊戲世界</title>
    <meta name="description" content="Alex's Game Center - 精選 HTML5 遊戲集合，包含貪食蛇、五子棋、跳跳鳥等經典遊戲">
    <link rel="stylesheet" href="css/styles.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <!-- 主題切換按鈕 -->
    <div class="theme-toggle">
        <button id="theme-toggle-btn" aria-label="切換主題">
            <span class="theme-icon dark-icon">🌙</span>
            <span class="theme-icon light-icon">☀️</span>
        </button>
    </div>

    <!-- 主容器 -->
    <div class="container">
        <!-- 頁首 -->
        <header class="header">
            <div class="logo">
                <h1><i class="fas fa-gamepad"></i> Alex's Game Center</h1>
                <p class="slogan">探索精彩遊戲世界</p>
            </div>
            <nav class="nav">
                <a href="#games" class="nav-link">遊戲列表</a>
                <a href="#about" class="nav-link">關於我們</a>
                <a href="#contact" class="nav-link">聯絡我們</a>
            </nav>
        </header>

        <!-- 主內容 -->
        <main class="main-content">
            <!-- 英雄區域 -->
            <section class="hero">
                <div class="hero-content">
                    <h2>歡迎來到遊戲中心</h2>
                    <p>精選 HTML5 遊戲集合，無需下載，直接在瀏覽器中遊玩！</p>
                    <a href="#games" class="btn-primary">開始遊戲</a>
                </div>
                <div class="hero-image">
                    <i class="fas fa-chess-queen"></i>
                    <i class="fas fa-snake"></i>
                    <i class="fas fa-dove"></i>
                </div>
            </section>

            <!-- 遊戲卡片區域 -->
            <section id="games" class="games-section">
                <h2><i class="fas fa-dice"></i> 精選遊戲</h2>
                <p class="section-description">點擊卡片開始遊玩您喜愛的遊戲</p>
                
                <div class="games-grid">
                    <!-- 遊戲卡片 1: 貪食蛇 -->
                    <div class="game-card">
                        <div class="game-icon">
                            <i class="fas fa-snake"></i>
                        </div>
                        <h3 class="game-title">貪食蛇遊戲</h3>
                        <p class="game-description">經典的貪食蛇遊戲，控制蛇吃食物並避免撞牆或自己。挑戰你的反應速度和策略！</p>
                        <div class="game-tags">
                            <span class="tag">經典</span>
                            <span class="tag">反應</span>
                            <span class="tag">策略</span>
                        </div>
                        <a href="game1.html" class="btn-play">
                            <i class="fas fa-play"></i> 開始遊戲
                        </a>
                    </div>

                    <!-- 遊戲卡片 2: 五子棋 -->
                    <div class="game-card">
                        <div class="game-icon">
                            <i class="fas fa-chess-board"></i>
                        </div>
                        <h3 class="game-title">五子棋對戰 AI</h3>
                        <p class="game-description">與人工智能對戰的五子棋遊戲，挑戰你的策略思維。誰能先連成五子？</p>
                        <div class="game-tags">
                            <span class="tag">棋類</span>
                            <span class="tag">策略</span>
                            <span class="tag">AI</span>
                        </div>
                        <a href="game2.html" class="btn-play">
                            <i class="fas fa-play"></i> 開始遊戲
                        </a>
                    </div>

                    <!-- 遊戲卡片 3: 跳跳鳥 -->
                    <div class="game-card">
                        <div class="game-icon">
                            <i class="fas fa-dove"></i>
                        </div>
                        <h3 class="game-title">跳跳鳥 Pro</h3>
                        <p class="game-description">類似 Flappy Bird 的跳躍遊戲，控制小鳥穿越障礙物。考驗你的節奏感和反應！</p>
                        <div class="game-tags">
                            <span class="tag">動作</span>
                            <span class="tag">反應</span>
                            <span class="tag">挑戰</span>
                        </div>
                        <a href="game3.html" class="btn-play">
                            <i class="fas fa-play"></i> 開始遊戲
                        </a>
                    </div>

                    <!-- 遊戲卡片 4: Demo Click -->
                    <div class="game-card">
                        <div class="game-icon">
                            <i class="fas fa-mouse-pointer"></i>
                        </div>
                        <h3 class="game-title">Demo Click</h3>
                        <p class="game-description">簡單的點擊反應遊戲，點擊移動的圓球獲得高分。適合放鬆和訓練反應速度！</p>
                        <div class="game-tags">
                            <span class="tag">簡單</span>
                            <span class="tag">反應</span>
                            <span class="tag">點擊</span>
                        </div>
                        <a href="games/demo_click/index.html" class="btn-play">
                            <i class="fas fa-play"></i> 開始遊戲
                        </a>
                    </div>
                </div>
            </section>

            <!-- 關於區域 -->
            <section id="about" class="about-section">
                <h2><i class="fas fa-info-circle"></i> 關於遊戲中心</h2>
                <div class="about-content">
                    <div class="about-text">
                        <h3>我們的使命</h3>
                        <p>Alex's Game Center 致力於提供高品質的 HTML5 遊戲體驗，所有遊戲均為純前端實現，無需下載或安裝任何插件。</p>
                        <h3>遊戲特色</h3>
                        <ul>
                            <li>所有遊戲完全免費</li>
                            <li>無需註冊或登入</li>
                            <li>響應式設計，支援各種裝置</li>
                            <li>深色/明亮模式切換</li>
                            <li>繁體中文介面</li>
                        </ul>
                    </div>
                    <div class="about-stats">
                        <div class="stat">
                            <i class="fas fa-gamepad"></i>
                            <span class="stat-number">4</span>
                            <span class="stat-label">款遊戲</span>
                        </div>
                        <div class="stat">
                            <i class="fas fa-code"></i>
                            <span class="stat-number">100%</span>
                            <span class="stat-label">純前端</span>
                        </div>
                        <div class="stat">
                            <i class="fas fa-language"></i>
                            <span class="stat-number">繁體中文</span>
                            <span class="stat-label">介面</span>
                        </div>
                    </div>
                </div>
            </section>
        </main>

        <!-- 頁尾 -->
        <footer class="footer">
            <div class="footer-content">
                <div class="footer-logo">
                    <h3><i class="fas fa-gamepad"></i> Alex's Game Center</h3>
                    <p>探索精彩遊戲世界</p>
                </div>
                <div class="footer-links">
                    <h4>快速連結</h4>
                    <a href="#games">遊戲列表</a>
                    <a href="#about">關於我們</a>
                    <a href="#contact">聯絡我們</a>
                </div>
                <div class="footer-contact" id="contact">
                    <h4>聯絡我們</h4>
                    <p><i class="fas fa-envelope"></i> alex@example.com</p>
                    <p><i class="fas fa-map-marker-alt"></i> 香港</p>
                </div>
            </div>
            <div class="footer-bottom">
                <p>&copy; 2026 Alex's Game Center. 保留所有權利。</p>
                <p class="footer-note">本網站所有遊戲均為 HTML5 實現，建議使用最新版瀏覽器遊玩。</p>
            </div>
        </footer>
    </div>

    <!-- JavaScript -->
    <script src="js/theme-manager.js"></script>
    <script src="js/main.js"></script>
</body>
</html>
```

## CSS 樣式規劃

### 1. 檔案結構
```
css/
├── styles.css        # 主要樣式
├── variables.css     # CSS 變數定義
├── components.css    # 組件樣式
└── responsive.css    # 響應式設計
```

### 2. 主要樣式特性

#### 容器與佈局
```css
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* 響應式網格 */
.games-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 30px;
    margin-top: 40px;
}
```

#### 遊戲卡片設計
```css
.game-card {
    background: var(--card-bg);
    border: 1px solid var(--card-border);
    border-radius: 12px;
    padding: 25px;
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
    height: 100%;
}

.game-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
}

.game-icon {
    font-size: 3rem;
    color: var(--text-accent);
    margin-bottom: 15px;
    text-align: center;
}

.game-title {
    font-size: 1.5rem;
    margin-bottom: 10px;
    color: var(--text-primary);
}

.game-description {
    color: var(--text-secondary);
    line-height: 1.6;
    margin-bottom: 15px;
    flex-grow: 1;
}

.btn-play {
    display: inline-block;
    background: linear-gradient(to bottom, var(--button-bg-from), var(--button-bg-to));
    color: var(--button-text);
    padding: 12px 24px;
    border-radius: 8px;
    text-decoration: none;
    font-weight: bold;
    text-align: center;
    transition: all 0.3s ease;
    margin-top: 15px;
}

.btn-play:hover {
    transform: scale(1.05);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}
```

#### 響應式設計斷點
```css
/* 手機 */
@media (max-width: 768px) {
    .games-grid {
        grid-template-columns: 1fr;
    }
    
    .header {
        flex-direction: column;
        text-align: center;
    }
    
    .nav {
        margin-top: 20px;
    }
}

/* 平板 */
@media (min-width: 769px) and (max-width: 1024px) {
    .games-grid {
        grid-template-columns: repeat(2, 1fr);
    }
}

/* 桌面 */
@media (min-width: 1025px) {
    .games-grid {
        grid-template-columns: repeat(4, 1fr);
    }
}
```

## 功能需求

### 1. 主題切換
- 使用 `docs/theme-toggle-spec.md` 中定義的實現
- 平滑的顏色過渡動畫
- localStorage 持久化

### 2. 遊戲卡片互動
- 懸停效果：卡片上浮和陰影
- 點擊遊戲卡片進入對應遊戲頁面
- 遊戲標籤顯示

### 3. 響應式設計
- 適應手機、平板、桌面各種屏幕尺寸
- 觸控友好的按鈕和連結
- 可讀的字體大小和間距

### 4. 無障礙功能
- 語義化 HTML 標籤
- 適當的 ARIA 屬性
- 鍵盤導航支持
- 高對比度主題

## 整合步驟

### 步驟 1: 創建 CSS 檔案結構
1. 創建 `css/` 目錄
2. 創建 `css/variables.css` - 定義 CSS 變數
3. 創建 `css/components.css` - 組件樣式
4. 創建 `css/responsive.css` - 響應式設計
5. 創建 `css/styles.css` - 主樣式文件（導入其他文件）

### 步驟 2: 創建 JavaScript 檔案
1. 創建 `js/theme-manager.js` - 主題管理
2. 創建 `js/main.js` - 其他交互功能

### 步驟 3: 更新 index.html
1. 替換現有 index.html 內容為新設計
2. 添加 CSS 和 JavaScript 引用
3. 確保所有遊戲連結正確

### 步驟 4: 測試
1. 測試主題切換功能
2. 測試所有遊戲連結
3. 測試響應式設計
4. 測試無障礙功能

## 視覺設計指南

### 顏色使用
- 主要文字：`var(--text-primary)`
- 次要文字：`var(--text-secondary)`
- 強調顏色：`var(--text-accent)`
- 背景：`linear-gradient(135deg, var(--bg-gradient-top), var(--bg-gradient-bottom))`

### 字體
- 主要字體：系統字體堆疊 (Arial, sans-serif)
- 代碼字體：等寬字體堆疊
- 字體大小：使用 rem 單位確保可訪問性

### 間距
- 主要間距：1rem (16px)
- 卡片內邊距：1.5rem (24px)
- 區段間距：3rem (48px)

### 動畫
- 過渡時間：0.3s
- 懸停效果：transform 和 box-shadow
- 主題切換：平滑的顏色過渡