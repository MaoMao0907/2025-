<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>比賽報名費用計算</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .race-category {
            background-color: white;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        .race-option {
            display: flex;
            align-items: center;
            margin: 10px 0;
            padding: 10px;
            background-color: #f8f8f8;
            border-radius: 4px;
        }
        .race-option:hover {
            background-color: #f0f0f0;
        }
        h2 {
            color: #2c3e50;
            margin-bottom: 15px;
        }
        .price {
            margin-left: auto;
            color: #e74c3c;
            font-weight: bold;
        }
        .distance {
            color: #7f8c8d;
            margin-left: 15px;
            min-width: 60px;
        }
        .total-section {
            background-color: #2c3e50;
            color: white;
            padding: 20px;
            border-radius: 8px;
            margin-top: 20px;
        }
        .selected-count {
            font-size: 1.2em;
            margin-bottom: 10px;
        }
        .original-price, .discount-price {
            display: flex;
            justify-content: space-between;
            margin: 5px 0;
        }
        .discount-price {
            font-size: 1.3em;
            font-weight: bold;
            border-top: 1px solid rgba(255,255,255,0.2);
            padding-top: 10px;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h1>比賽報名費用計算</h1>
    
    <div class="race-category">
        <h2>大肚山越野</h2>
        <div class="race-option">
            <input type="radio" name="dasy" id="dasy_1" value="1480">
            <label for="dasy_1">進階越野‧競速</label>
            <span class="distance">30K</span>
            <span class="price">1480元</span>
        </div>
        <div class="race-option">
            <input type="radio" name="dasy" id="dasy_2" value="980">
            <label for="dasy_2">初階越野</label>
            <span class="distance">18K</span>
            <span class="price">980元</span>
        </div>
        <div class="race-option">
            <input type="radio" name="dasy" id="dasy_3" value="980">
            <label for="dasy_3">健行‧進階親子‧初階越野</label>
            <span class="distance">12K</span>
            <span class="price">980元</span>
        </div>
        <div class="race-option">
            <input type="radio" name="dasy" id="dasy_4" value="800">
            <label for="dasy_4">健行‧親子</label>
            <span class="distance">4K</span>
            <span class="price">800元</span>
        </div>
    </div>

    <div class="race-category">
        <h2>越野‧發發廟衛</h2>
        <div class="race-option">
            <input type="radio" name="temple" id="temple_1" value="4500">
            <label for="temple_1">發發廟衛 70K</label>
            <span class="distance">70K</span>
            <span class="price">4500元</span>
        </div>
        <div class="race-option">
            <input type="radio" name="temple" id="temple_2" value="3600">
            <label for="temple_2">發廟衛 40K</label>
            <span class="distance">40K</span>
            <span class="price">3600元</span>
        </div>
        <div class="race-option">
            <input type="radio" name="temple" id="temple_3" value="1800">
            <label for="temple_3">波津加宮高賽</label>
            <span class="distance">4.3K</span>
            <span class="price">1800元</span>
        </div>
        <div class="race-option">
            <input type="radio" name="temple" id="temple_4" value="1800">
            <label for="temple_4">屋我尾急速越降組</label>
            <span class="distance">12K</span>
            <span class="price">1800元</span>
        </div>
        <div class="race-option">
            <input type="radio" name="temple" id="temple_5" value="800">
            <label for="temple_5">快活拗來組</label>
            <span class="distance">2.5K</span>
            <span class="price">800元</span>
        </div>
    </div>

    <div class="race-category">
        <h2>火炎山甜甜圈</h2>
        <div class="race-option">
            <input type="radio" name="fire" id="fire_1" value="1800">
            <label for="fire_1">無限循環賽</label>
            <span class="distance">∞K</span>
            <span class="price">1800元</span>
        </div>
        <div class="race-option">
            <input type="radio" name="fire" id="fire_2" value="1800">
            <label for="fire_2">急速越降賽</label>
            <span class="distance">13.4K</span>
            <span class="price">1800元</span>
        </div>
        <div class="race-option">
            <input type="radio" name="fire" id="fire_3" value="1800">
            <label for="fire_3">火炎山登高賽</label>
            <span class="distance">3.4K</span>
            <span class="price">1800元</span>
        </div>
    </div>

    <div class="total-section">
        <div class="selected-count">已選擇: <span id="selected-races">0</span> 場比賽</div>
        <div class="original-price">
            <span>原價總計:</span>
            <span id="original-total">0元</span>
        </div>
        <div class="original-price">
            <span>折扣:</span>
            <span id="discount-rate">0%</span>
        </div>
        <div class="discount-price">
            <span>折扣後總價:</span>
            <span id="final-price">0元</span>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const radioButtons = document.querySelectorAll('input[type="radio"]');
            
            function calculateTotal() {
                let total = 0;
                let selectedCount = 0;
                
                // 計算選擇的比賽數量和總金額
                const categories = ['dasy', 'temple', 'fire'];
                categories.forEach(category => {
                    const selected = document.querySelector(`input[name="${category}"]:checked`);
                    if (selected) {
                        total += parseInt(selected.value);
                        selectedCount++;
                    }
                });
                
                // 計算折扣
                let discountRate = 1;
                if (selectedCount === 2) {
                    discountRate = 0.95;
                } else if (selectedCount === 3) {
                    discountRate = 0.90;
                }
                
                // 更新顯示
                document.getElementById('selected-races').textContent = selectedCount;
                document.getElementById('original-total').textContent = total + '元';
                document.getElementById('discount-rate').textContent = 
                    ((1 - discountRate) * 100).toFixed(0) + '%';
                document.getElementById('final-price').textContent = 
                    Math.round(total * discountRate) + '元';
            }
            
            // 添加事件監聽器
            radioButtons.forEach(button => {
                button.addEventListener('change', calculateTotal);
            });
        });
    </script>
</body>
</html>
