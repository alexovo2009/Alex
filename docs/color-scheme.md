# Alex's Game Center 顏色方案

## 深色科技感主題 (預設)

### 主要顏色
- **主色調**: 深藍 #1e3a5f + 金色 #ffd700
- **背景漸層**: 
  - 頂部: #1e3a5f (深藍)
  - 底部: #0d1b2a (更深的藍)
- **文字顏色**:
  - 主要文字: #ffffff (白色)
  - 次要文字: #cccccc (淺灰)
  - 強調文字: #ffd700 (金色)
- **卡片設計**:
  - 背景: rgba(30, 58, 95, 0.8) (半透明深藍)
  - 邊框: #ffd700 (金色), 1px 實線
  - 陰影: rgba(255, 215, 0, 0.3) 0px 4px 12px
- **按鈕設計**:
  - 背景漸層: 從 #ffd700 到 #ffed4e (金色漸層)
  - 文字顏色: #1e3a5f (深藍)
  - 懸停背景: 從 #ffed4e 到 #fff8b3 (更亮的金色)
- **Header/Footer**:
  - 背景: rgba(13, 27, 42, 0.9) (深藍半透明)
  - 邊框: #ffd700 (金色), 底部 2px 實線

### 輔助顏色
- **成功**: #4CAF50 (綠色)
- **警告**: #FF9800 (橙色)
- **錯誤**: #F44336 (紅色)
- **資訊**: #2196F3 (藍色)

## 明亮模式主題

### 主要顏色
- **主色調**: 淺藍 #4a6fa5 + 深藍 #1e3a5f
- **背景漸層**:
  - 頂部: #f5f7fa (淺灰藍)
  - 底部: #e4e8f0 (淺灰)
- **文字顏色**:
  - 主要文字: #1e3a5f (深藍)
  - 次要文字: #666666 (中灰)
  - 強調文字: #4a6fa5 (淺藍)
- **卡片設計**:
  - 背景: #ffffff (白色)
  - 邊框: #4a6fa5 (淺藍), 1px 實線
  - 陰影: rgba(74, 111, 165, 0.1) 0px 4px 12px
- **按鈕設計**:
  - 背景漸層: 從 #4a6fa5 到 #5a7fb5 (淺藍漸層)
  - 文字顏色: #ffffff (白色)
  - 懸停背景: 從 #5a7fb5 到 #6a8fc5 (更亮的藍色)
- **Header/Footer**:
  - 背景: rgba(255, 255, 255, 0.9) (白色半透明)
  - 邊框: #4a6fa5 (淺藍), 底部 2px 實線

## CSS 變數定義

```css
:root {
  /* 深色主題 (預設) */
  --primary-dark: #1e3a5f;
  --primary-light: #4a6fa5;
  --accent: #ffd700;
  --accent-light: #ffed4e;
  
  --bg-gradient-top: #1e3a5f;
  --bg-gradient-bottom: #0d1b2a;
  --card-bg: rgba(30, 58, 95, 0.8);
  --card-border: #ffd700;
  --text-primary: #ffffff;
  --text-secondary: #cccccc;
  --text-accent: #ffd700;
  
  --button-bg-from: #ffd700;
  --button-bg-to: #ffed4e;
  --button-text: #1e3a5f;
  
  --header-bg: rgba(13, 27, 42, 0.9);
  --header-border: #ffd700;
}

[data-theme="light"] {
  /* 明亮主題 */
  --primary-dark: #1e3a5f;
  --primary-light: #4a6fa5;
  --accent: #4a6fa5;
  --accent-light: #5a7fb5;
  
  --bg-gradient-top: #f5f7fa;
  --bg-gradient-bottom: #e4e8f0;
  --card-bg: #ffffff;
  --card-border: #4a6fa5;
  --text-primary: #1e3a5f;
  --text-secondary: #666666;
  --text-accent: #4a6fa5;
  
  --button-bg-from: #4a6fa5;
  --button-bg-to: #5a7fb5;
  --button-text: #ffffff;
  
  --header-bg: rgba(255, 255, 255, 0.9);
  --header-border: #4a6fa5;
}
```

## 使用指南

1. **背景應用**:
   ```css
   body {
     background: linear-gradient(135deg, var(--bg-gradient-top), var(--bg-gradient-bottom));
   }
   ```

2. **卡片樣式**:
   ```css
   .game-card {
     background: var(--card-bg);
     border: 1px solid var(--card-border);
     color: var(--text-primary);
   }
   ```

3. **按鈕樣式**:
   ```css
   .btn-primary {
     background: linear-gradient(to bottom, var(--button-bg-from), var(--button-bg-to));
     color: var(--button-text);
   }
   ```

4. **文字樣式**:
   ```css
   h1, h2, h3 {
     color: var(--text-primary);
   }
   
   p, .description {
     color: var(--text-secondary);
   }
   
   .highlight {
     color: var(--text-accent);
   }
   ```

## 視覺層次

1. **主要焦點**: 金色 (#ffd700) 用於重要按鈕和強調元素
2. **次要元素**: 深藍 (#1e3a5f) 用於背景和卡片
3. **文字層次**: 白色用於主要文字，淺灰用於次要文字
4. **互動反饋**: 懸停時使用更亮的金色 (#ffed4e) 或藍色 (#5a7fb5)

## 無障礙設計考慮

- 對比度: 金色文字在深藍背景上達到 WCAG AA 標準
- 字體大小: 使用相對單位 (rem) 確保可縮放性
- 焦點狀態: 所有互動元素都有明顯的焦點樣式
- 顏色無關: 不使用僅靠顏色傳達的資訊