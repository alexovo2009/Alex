# 深色/明亮模式切換功能規格

## 功能概述
提供用戶在 Alex's Game Center 中切換深色科技感主題和明亮模式主題的功能。

## 技術實現

### 1. HTML 結構
```html
<!-- 主題切換開關 -->
<div class="theme-toggle">
  <button id="theme-toggle-btn" aria-label="切換主題">
    <span class="theme-icon dark-icon">🌙</span>
    <span class="theme-icon light-icon">☀️</span>
  </button>
</div>
```

### 2. CSS 變數系統
使用 CSS 自定義屬性（變數）來管理主題顏色，如 `docs/color-scheme.md` 中定義。

### 3. JavaScript 功能
```javascript
// 主題管理模組
const ThemeManager = {
  // 主題常量
  THEMES: {
    DARK: 'dark',
    LIGHT: 'light'
  },
  
  // 初始化
  init() {
    this.loadSavedTheme();
    this.setupEventListeners();
    this.updateUI();
  },
  
  // 加載保存的主題
  loadSavedTheme() {
    const savedTheme = localStorage.getItem('gameCenterTheme');
    const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
    
    if (savedTheme) {
      this.setTheme(savedTheme);
    } else if (prefersDark) {
      this.setTheme(this.THEMES.DARK);
    } else {
      this.setTheme(this.THEMES.LIGHT);
    }
  },
  
  // 設置主題
  setTheme(theme) {
    document.documentElement.setAttribute('data-theme', theme);
    localStorage.setItem('gameCenterTheme', theme);
    this.currentTheme = theme;
    this.updateUI();
  },
  
  // 切換主題
  toggleTheme() {
    const newTheme = this.currentTheme === this.THEMES.DARK 
      ? this.THEMES.LIGHT 
      : this.THEMES.DARK;
    this.setTheme(newTheme);
  },
  
  // 設置事件監聽器
  setupEventListeners() {
    const toggleBtn = document.getElementById('theme-toggle-btn');
    if (toggleBtn) {
      toggleBtn.addEventListener('click', () => this.toggleTheme());
    }
    
    // 監聽系統主題變化
    window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (e) => {
      if (!localStorage.getItem('gameCenterTheme')) {
        this.setTheme(e.matches ? this.THEMES.DARK : this.THEMES.LIGHT);
      }
    });
  },
  
  // 更新 UI 元素
  updateUI() {
    const toggleBtn = document.getElementById('theme-toggle-btn');
    if (!toggleBtn) return;
    
    const isDark = this.currentTheme === this.THEMES.DARK;
    const darkIcon = toggleBtn.querySelector('.dark-icon');
    const lightIcon = toggleBtn.querySelector('.light-icon');
    
    // 更新按鈕文字
    toggleBtn.setAttribute('aria-label', isDark ? '切換到明亮模式' : '切換到深色模式');
    
    // 顯示/隱藏圖標
    if (darkIcon) darkIcon.style.display = isDark ? 'none' : 'inline';
    if (lightIcon) lightIcon.style.display = isDark ? 'inline' : 'none';
    
    // 更新按鈕樣式
    toggleBtn.classList.toggle('dark-mode', isDark);
    toggleBtn.classList.toggle('light-mode', !isDark);
  }
};

// 初始化主題管理器
document.addEventListener('DOMContentLoaded', () => {
  ThemeManager.init();
});
```

### 4. CSS 樣式
```css
/* 主題切換按鈕樣式 */
.theme-toggle {
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 1000;
}

#theme-toggle-btn {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  transition: all 0.3s ease;
  background: var(--button-bg-from);
  color: var(--button-text);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

#theme-toggle-btn:hover {
  transform: scale(1.1);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
}

#theme-toggle-btn:active {
  transform: scale(0.95);
}

.theme-icon {
  transition: opacity 0.3s ease;
}

/* 深色模式下的按鈕 */
[data-theme="dark"] #theme-toggle-btn {
  background: linear-gradient(135deg, #ffd700, #ffed4e);
  color: #1e3a5f;
}

/* 明亮模式下的按鈕 */
[data-theme="light"] #theme-toggle-btn {
  background: linear-gradient(135deg, #4a6fa5, #5a7fb5);
  color: white;
}

/* 平滑過渡效果 */
* {
  transition: background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease;
}
```

## 功能特性

### 1. 主題持久化
- 使用 `localStorage` 保存用戶選擇的主題
- 頁面刷新後保持相同主題
- 清除瀏覽器數據後恢復默認主題

### 2. 系統主題檢測
- 自動檢測操作系統的主題偏好
- 首次訪問時使用系統主題作為默認值
- 提供選項覆蓋系統設置

### 3. 無障礙功能
- 按鈕具有 `aria-label` 屬性
- 鍵盤導航支持 (Tab, Enter/Space)
- 高對比度主題切換

### 4. 視覺反饋
- 平滑的顏色過渡動畫
- 按鈕懸停和點擊效果
- 圖標切換動畫

## 整合到現有頁面

### 修改 index.html
1. 在 `<head>` 中添加 CSS 變數定義
2. 在 `<body>` 開頭添加主題切換按鈕
3. 在 `<script>` 標籤中添加主題管理 JavaScript

### 修改現有 CSS
1. 將硬編碼的顏色值替換為 CSS 變數
2. 確保所有元素使用主題相關的顏色變數
3. 添加過渡效果以實現平滑主題切換

## 測試計劃

### 功能測試
1. 點擊主題切換按鈕應切換主題
2. 刷新頁面後應保持相同主題
3. 清除 localStorage 後應恢復默認主題
4. 系統主題變化應影響默認主題（當未手動設置時）

### 視覺測試
1. 深色模式下所有元素應使用深色主題顏色
2. 明亮模式下所有元素應使用明亮主題顏色
3. 過渡動畫應平滑無閃爍
4. 響應式設計在不同屏幕尺寸下正常工作

### 無障礙測試
1. 鍵盤應能聚焦並激活主題切換按鈕
2. 屏幕閱讀器應正確朗讀按鈕標籤
3. 對比度應符合 WCAG 標準

## 錯誤處理

1. **localStorage 不可用**: 降級為會話級存儲或僅使用默認主題
2. **無效主題值**: 重置為默認主題並清除錯誤值
3. **JavaScript 禁用**: 顯示默認主題（深色模式）並隱藏切換按鈕

## 性能考慮

1. **CSS 變數**: 使用 CSS 變數而非 JavaScript 直接修改樣式以提高性能
2. **最小化重繪**: 批量樣式更新減少瀏覽器重繪
3. **延遲加載**: 主題切換代碼在 DOM 加載後執行
4. **緩存**: 主題設置緩存在 localStorage 中減少讀取時間