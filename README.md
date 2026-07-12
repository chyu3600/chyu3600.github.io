# chyu3600.githun.io
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>金属重量计算器</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Microsoft JhengHei', Arial, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            line-height: 1.6;
            padding: 20px;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            padding: 30px;
        }
        
        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 20px;
            border-bottom: 2px solid #3498db;
            padding-bottom: 10px;
        }
        
        .description {
            text-align: center;
            margin-bottom: 30px;
            color: #7f8c8d;
        }
        
        .calculator {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        
        @media (max-width: 768px) {
            .calculator {
                grid-template-columns: 1fr;
            }
        }
        
        .input-section, .result-section {
            padding: 20px;
            border-radius: 8px;
            background: #f9f9f9;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        select, input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
        }
        
        .dimension-inputs {
            display: none;
        }
        
        .dimension-group {
            margin-bottom: 10px;
        }
        
        .dimension-group label {
            font-weight: normal;
        }
        
        button {
            width: 100%;
            padding: 12px;
            background: #3498db;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            cursor: pointer;
            transition: background 0.3s;
        }
        
        button:hover {
            background: #2980b9;
        }
        
        .result-section {
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        
        .result {
            text-align: center;
            padding: 20px;
            background: white;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.05);
        }
        
        .result-value {
            font-size: 32px;
            font-weight: bold;
            color: #e74c3c;
            margin: 10px 0;
        }
        
        .result-unit {
            font-size: 18px;
            color: #7f8c8d;
        }
        
        .metal-info {
            margin-top: 20px;
            font-size: 14px;
            color: #7f8c8d;
        }
        
        .shape-diagram {
            text-align: center;
            margin: 15px 0;
            font-size: 60px;
        }
        
        .footer {
            text-align: center;
            margin-top: 30px;
            color: #7f8c8d;
            font-size: 14px;
        }
        
        .unit-toggle {
            display: flex;
            justify-content: center;
            margin-top: 10px;
        }
        
        .unit-toggle button {
            width: auto;
            margin: 0 5px;
            padding: 5px 10px;
            font-size: 14px;
            background: #95a5a6;
        }
        
        .unit-toggle button.active {
            background: #3498db;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>金属重量计算器</h1>
        <p class="description">选择金属类型、形状和尺寸，计算金属重量</p>
        
        <div class="calculator">
            <div class="input-section">
                <div class="form-group">
                    <label for="metal-type">金属种类</label>
                    <select id="metal-type">
                        <option value="7.93">不锈钢 (密度: 7.93 g/cm³)</option>
                        <option value="4.51">钛合金 (密度: 4.51 g/cm³)</option>
                        <option value="2.70">铝 (密度: 2.70 g/cm³)</option>
                        <option value="7.85">一般碳钢 (密度: 7.85 g/cm³)</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="shape">形状</label>
                    <select id="shape">
                        <option value="circle">圆形</option>
                        <option value="disk">圆盘形</option>
                        <option value="rectangle">四角形</option>
                        <option value="hexagon">六角形</option>
                    </select>
                </div>
                
                <div id="dimension-inputs">
                    <!-- 圆形尺寸输入 -->
                    <div id="circle-dimensions" class="dimension-inputs">
                        <div class="dimension-group">
                            <label for="diameter">直径 (mm)</label>
                            <input type="number" id="diameter" min="1" step="0.1" placeholder="输入直径">
                        </div>
                        <div class="dimension-group">
                            <label for="length-circle">长度 (mm)</label>
                            <input type="number" id="length-circle" min="1" step="0.1" placeholder="输入长度">
                        </div>
                    </div>
                    
                    <!-- 圆盘形尺寸输入 -->
                    <div id="disk-dimensions" class="dimension-inputs">
                        <div class="dimension-group">
                            <label for="large-diameter">大头直径 (mm)</label>
                            <input type="number" id="large-diameter" min="1" step="0.1" placeholder="输入大头直径">
                        </div>
                        <div class="dimension-group">
                            <label for="small-diameter">小头直径 (mm)</label>
                            <input type="number" id="small-diameter" min="1" step="0.1" placeholder="输入小头直径">
                        </div>
                        <div class="dimension-group">
                            <label for="height-disk">高度 (mm)</label>
                            <input type="number" id="height-disk" min="1" step="0.1" placeholder="输入高度">
                        </div>
                    </div>
                    
                    <!-- 四角形尺寸输入 -->
                    <div id="rectangle-dimensions" class="dimension-inputs">
                        <div class="dimension-group">
                            <label for="width">宽度 (mm)</label>
                            <input type="number" id="width" min="1" step="0.1" placeholder="输入宽度">
                        </div>
                        <div class="dimension-group">
                            <label for="height-rect">高度 (mm)</label>
                            <input type="number" id="height-rect" min="1" step="0.1" placeholder="输入高度">
                        </div>
                        <div class="dimension-group">
                            <label for="length-rect">长度 (mm)</label>
                            <input type="number" id="length-rect" min="1" step="0.1" placeholder="输入长度">
                        </div>
                    </div>
                    
                    <!-- 六角形尺寸输入 -->
                    <div id="hexagon-dimensions" class="dimension-inputs">
                        <div class="dimension-group">
                            <label for="side-length">对边距离 (mm)</label>
                            <input type="number" id="side-length" min="1" step="0.1" placeholder="输入对边距离">
                        </div>
                        <div class="dimension-group">
                            <label for="length-hex">长度 (mm)</label>
                            <input type="number" id="length-hex" min="1" step="0.1" placeholder="输入长度">
                        </div>
                    </div>
                </div>
                
                <button id="calculate-btn">计算重量</button>
            </div>
            
            <div class="result-section">
                <div class="shape-diagram" id="shape-diagram">●</div>
                <div class="result">
                    <div>计算结果</div>
                    <div class="result-value" id="result-value">0.00</div>
                    <div class="result-unit">公克 (g)</div>
                </div>
                <div class="unit-toggle">
                    <button id="unit-g" class="active">公克 (g)</button>
                    <button id="unit-kg">公斤 (kg)</button>
                </div>
                <div class="metal-info" id="metal-info">
                    当前选择: 不锈钢 | 密度: 7.93 g/cm³
                </div>
            </div>
        </div>
        
        <div class="footer">
            金属重量计算器 &copy; 2023 | 输入尺寸单位为毫米(mm)
        </div>
    </div>

    <script>
        // 金属密度数据
        const metalDensities = {
            '7.93': { name: '不锈钢', density: 7.93 },
            '4.51': { name: '钛合金', density: 4.51 },
            '2.70': { name: '铝', density: 2.70 },
            '7.85': { name: '一般碳钢', density: 7.85 }
        };
        
        // 形状图标
        const shapeIcons = {
            'circle': '●',
            'disk': '◍',
            'rectangle': '■',
            'hexagon': '⬢'
        };
        
        // 获取DOM元素
        const metalTypeSelect = document.getElementById('metal-type');
        const shapeSelect = document.getElementById('shape');
        const dimensionInputs = document.getElementById('dimension-inputs');
        const calculateBtn = document.getElementById('calculate-btn');
        const resultValue = document.getElementById('result-value');
        const metalInfo = document.getElementById('metal-info');
        const shapeDiagram = document.getElementById('shape-diagram');
        const unitG = document.getElementById('unit-g');
        const unitKg = document.getElementById('unit-kg');
        const resultUnit = document.querySelector('.result-unit');
        
        // 当前单位状态
        let currentUnit = 'g';
        
        // 显示对应形状的尺寸输入
        function showDimensionInputs(shape) {
            // 隐藏所有尺寸输入
            const allDimensionInputs = document.querySelectorAll('.dimension-inputs');
            allDimensionInputs.forEach(input => {
                input.style.display = 'none';
            });
            
            // 显示当前形状的尺寸输入
            const currentDimensions = document.getElementById(`${shape}-dimensions`);
            if (currentDimensions) {
                currentDimensions.style.display = 'block';
            }
            
            // 更新形状图标
            shapeDiagram.textContent = shapeIcons[shape] || '●';
        }
        
        // 更新金属信息
        function updateMetalInfo() {
            const selectedMetal = metalDensities[metalTypeSelect.value];
            metalInfo.textContent = `当前选择: ${selectedMetal.name} | 密度: ${selectedMetal.density} g/cm³`;
        }
        
        // 计算体积函数
        function calculateVolume(shape) {
            // 将毫米转换为厘米
            const toCm = (mm) => mm / 10;
            
            switch(shape) {
                case 'circle':
                    const diameter = parseFloat(document.getElementById('diameter').value) || 0;
                    const lengthCircle = parseFloat(document.getElementById('length-circle').value) || 0;
                    const radius = toCm(diameter) / 2;
                    const heightCircle = toCm(lengthCircle);
                    return Math.PI * Math.pow(radius, 2) * heightCircle;
                    
                case 'disk':
                    const largeDiameter = parseFloat(document.getElementById('large-diameter').value) || 0;
                    const smallDiameter = parseFloat(document.getElementById('small-diameter').value) || 0;
                    const heightDisk = parseFloat(document.getElementById('height-disk').value) || 0;
                    
                    // 圆盘体积计算：使用圆台体积公式
                    const largeRadius = toCm(largeDiameter) / 2;
                    const smallRadius = toCm(smallDiameter) / 2;
                    const diskHeight = toCm(heightDisk);
                    
                    // 圆台体积公式：V = (1/3) * π * h * (R² + R*r + r²)
                    return (1/3) * Math.PI * diskHeight * 
                           (Math.pow(largeRadius, 2) + largeRadius * smallRadius + Math.pow(smallRadius, 2));
                    
                case 'rectangle':
                    const width = parseFloat(document.getElementById('width').value) || 0;
                    const heightRect = parseFloat(document.getElementById('height-rect').value) || 0;
                    const lengthRect = parseFloat(document.getElementById('length-rect').value) || 0;
                    return toCm(width) * toCm(heightRect) * toCm(lengthRect);
                    
                case 'hexagon':
                    const sideLength = parseFloat(document.getElementById('side-length').value) || 0;
                    const lengthHex = parseFloat(document.getElementById('length-hex').value) || 0;
                    const side = toCm(sideLength);
                    const hexHeight = toCm(lengthHex);
                    // 正六边形面积公式: (3√3/2) * a²，其中a为边长
                    // 对边距离 = 2a，所以a = 对边距离/2
                    const a = side / 2;
                    const area = (3 * Math.sqrt(3) / 2) * Math.pow(a, 2);
                    return area * hexHeight;
                    
                default:
                    return 0;
            }
        }
        
        // 计算重量
        function calculateWeight() {
            const shape = shapeSelect.value;
            const density = parseFloat(metalTypeSelect.value);
            const volume = calculateVolume(shape);
            
            // 重量 = 密度 * 体积 (单位: 克)
            let weight = density * volume;
            
            // 如果当前单位是公斤，则转换为公斤
            if (currentUnit === 'kg') {
                weight = weight / 1000;
            }
            
            // 显示结果
            resultValue.textContent = weight.toFixed(2);
        }
        
        // 切换单位
        function toggleUnit(unit) {
            currentUnit = unit;
            
            // 更新按钮状态
            if (unit === 'g') {
                unitG.classList.add('active');
                unitKg.classList.remove('active');
                resultUnit.textContent = '公克 (g)';
            } else {
                unitG.classList.remove('active');
                unitKg.classList.add('active');
                resultUnit.textContent = '公斤 (kg)';
            }
            
            // 重新计算重量
            calculateWeight();
        }
        
        // 事件监听
        shapeSelect.addEventListener('change', function() {
            showDimensionInputs(this.value);
        });
        
        metalTypeSelect.addEventListener('change', updateMetalInfo);
        
        calculateBtn.addEventListener('click', calculateWeight);
        
        unitG.addEventListener('click', function() {
            toggleUnit('g');
        });
        
        unitKg.addEventListener('click', function() {
            toggleUnit('kg');
        });
        
        // 初始化
        showDimensionInputs(shapeSelect.value);
        updateMetalInfo();
    </script>
</body>
</html>


