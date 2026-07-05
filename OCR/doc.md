# 基于通义千问VL 公式OCR识别系统 \- 需求文档\+技术方案\+完整代码

# 1\. 项目概述

## 1\.1 项目背景

市面现有公式OCR工具存在广告多、收费贵、数据隐私泄露、功能固化、无法自定义等问题。为解决印刷公式、手写数学公式快速识别转LaTeX的刚需，基于**通义千问VL多模态大模型**自研轻量化公式OCR工具，自主开发前端界面，实现本地运行、私密安全、零部署成本、高精度识别的公式数字化工具，适配学生、教师、科研人员日常使用场景。

## 1\.2 项目目标

搭建一套**纯前端、无后端依赖、开箱即用**的数学公式OCR识别系统，实现图片公式一键识别、标准LaTeX输出、实时公式渲染预览、一键复制，替代第三方付费工具，兼顾实用性、低成本、高隐私性与可扩展性。

# 2\. 需求分析

## 2\.1 功能需求

|功能模块|具体需求|
|---|---|
|图片输入模块|1\. 支持本地图片上传；2\. 支持剪贴板截图粘贴（Ctrl\+V快速导入）；3\. 实时预览导入图片|
|公式识别模块|1\. 调用通义千问VL模型；2\. 支持印刷公式、手写公式、复杂嵌套公式识别；3\. 输出标准无冗余LaTeX代码|
|结果展示模块|1\. 展示原始LaTeX代码；2\. 基于KaTeX实时渲染公式可视化预览；3\. 区分代码区和预览区|
|快捷操作模块|1\. 一键复制LaTeX代码；2\. 一键清空所有内容重置页面；3\. 识别中加载状态提示|
|异常处理模块|1\. 空图片、空Key报错提示；2\. 网络异常、API调用失败提示；3\. 公式渲染容错处理|
|配置模块|支持前端自主配置阿里云千问API Key，无需修改代码|

## 2\.2 非功能需求

- **易用性**：单HTML文件，无需安装、无需部署、无需环境配置，浏览器直接打开即用

- **隐私性**：本地处理图片，仅向阿里云API传输识别数据，无第三方数据留存，无隐私泄露风险

- **低成本**：仅消耗阿里云千问API计费，单次识别成本极低，个人使用几乎免费

- **兼容性**：适配Chrome、Edge等主流现代浏览器，支持Windows、Mac系统

- **可扩展性**：代码结构清晰，可快速拓展批量识别、历史记录、文件导出等功能

## 2\.3 应用场景

- 教育场景：师生试卷、课件、错题公式快速提取转LaTeX

- 科研场景：论文、期刊复杂公式数字化录入

- 办公场景：文档、PPT公式标准化排版

- 学习场景：手写公式快速识别、校对整理

# 3\. 整体技术方案

## 3\.1 系统架构

采用**纯前端轻量化架构**，无后端服务器依赖，架构极简、落地零成本

核心流程：图片导入 → 前端Base64编码 → 调用千问VL多模态API → 后端AI识别解析 → 前端接收LaTeX结果 → 代码展示\+公式渲染 → 快捷操作

## 3\.2 技术选型

|模块|技术选型|作用说明|
|---|---|---|
|前端界面|原生HTML\+CSS\+JavaScript|轻量化页面，无框架依赖，极致兼容|
|公式渲染引擎|KaTeX|轻量高速渲染LaTeX公式，容错性高|
|AI识别模型|通义千问VL（qwen\-vl\-plus）|多模态视觉大模型，专攻图文理解、公式结构识别|
|数据传输格式|Base64|前端本地编码图片，无需文件上传，传输便捷|

## 3\.3 核心优势（对比传统工具）

- **无广告无限制**：自研界面，无弹窗、无会员限制、无次数封顶

- **识别精度更高**：千问VL针对数学符号、嵌套结构、手写变形优化，优于传统OCR引擎

- **极致便捷**：截图粘贴秒识别，无需保存图片，操作链路最短

- **完全可控**：自主掌控代码和数据，可自定义提示词、界面、功能

- **成本极低**：官方API低价计费，个人月度使用成本可忽略

# 4\. 核心优化策略

## 4\.1 模型Prompt优化

固定专属公式识别提示词，过滤冗余输出，保证结果标准化：

> 识别图片中的数学公式，只输出标准的LaTeX代码，不要任何多余文字、解释、标点符号
> 
> 

## 4\.2 前端体验优化

- 支持剪贴板快速粘贴，省去文件上传繁琐操作

- 增加加载、报错状态提示，交互反馈清晰

- KaTeX容错渲染，识别轻微误差不导致页面崩溃

- 一键复制、一键重置，提升操作效率

## 4\.3 识别效果优化建议

- 输入图片尽量裁剪，仅保留公式区域，减少干扰元素

- 保证图片清晰度，避免模糊、反光、倾斜

- 复杂矩阵、微积分公式优先使用高清截图

# 5\. 部署与使用教程

## 5\.1 前置准备

1. 注册/登录[阿里云百炼平台](https://dashscope.aliyun.com/)

2. 进入API\-KEY管理页面，创建并复制Key（格式：sk\-xxxxxx）

3. 确保账号拥有API调用额度（新用户免费额度充足）

## 5\.2 部署方式

无需部署、无需编译、无需环境依赖：将下方代码保存为`index\.html`，双击用浏览器打开即可使用。

## 5\.3 使用步骤

1. 打开页面后，填入阿里云千问API Key

2. 上传公式图片 或 截图后直接 Ctrl\+V 粘贴

3. 点击「开始识别公式」，1\-2秒生成结果

4. 查看LaTeX代码与可视化预览，一键复制使用

# 6\. 完整可运行代码

保存为 `index\.html` 直接运行

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>公式OCR识别工具 - 基于千问VL</title>
    <!-- 引入KaTeX公式渲染 -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.css">
    <script src="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft YaHei", sans-serif;
        }

        body {
            max-width: 1000px;
            margin: 20px auto;
            padding: 0 20px;
            background: #f5f7fa;
        }

        .title {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 30px;
            font-size: 24px;
        }

        .container {
            background: white;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .config-box {
            margin-bottom: 20px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 8px;
        }

        .config-box input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 6px;
            margin-top: 8px;
            font-size: 14px;
        }

        .upload-area {
            border: 2px dashed #3498db;
            border-radius: 8px;
            padding: 40px 20px;
            text-align: center;
            cursor: pointer;
            margin-bottom: 20px;
            background: #fafdff;
        }

        .upload-area:hover {
            background: #f1f8ff;
        }

        #imageInput {
            display: none;
        }

        .preview-img {
            max-width: 100%;
            max-height: 300px;
            margin: 15px 0;
            border-radius: 8px;
            display: none;
        }

        .btn-group {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 15px;
            transition: 0.2s;
        }

        .btn-primary {
            background: #3498db;
            color: white;
        }

        .btn-primary:hover {
            background: #2980b9;
        }

        .btn-default {
            background: #95a5a6;
            color: white;
        }

        .btn-default:hover {
            background: #7f8c8d;
        }

        .result-box {
            margin-top: 20px;
        }

        .result-title {
            font-weight: bold;
            margin-bottom: 10px;
            color: #2c3e50;
        }

        .latex-code {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 6px;
            border: 1px solid #eee;
            min-height: 80px;
            white-space: pre-wrap;
            font-family: monospace;
            margin-bottom: 15px;
        }

        .formula-preview {
            padding: 20px;
            background: #fdfefe;
            border: 1px solid #eee;
            border-radius: 6px;
            min-height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .loading {
            color: #3498db;
            text-align: center;
            padding: 10px;
            display: none;
        }

        .error {
            color: #e74c3c;
            padding: 10px;
            display: none;
        }
    </style>
</head>
<body>
    <h1 class="title">数学公式OCR识别工具（基于通义千问VL）</h1>
    <div class="container">
        <!-- API Key 配置 -->
        <div class="config-box">
            <label>请输入阿里云通义千问 API Key：</label>
            <input type="text" id="apiKey" placeholder="格式：sk-xxxxxxxxxxxxxxxxxxxxxxxx">
        </div>

        <!-- 图片上传区域 -->
        <div class="upload-area" onclick="document.getElementById('imageInput').click()">
            <p>📷 点击上传图片 / 粘贴截图（Ctrl+V）</p>
            <p>支持：公式截图、试卷公式、手写公式</p>
            <input type="file" id="imageInput" accept="image/*">
            <img id="previewImg" class="preview-img">
        </div>

        <!-- 按钮组 -->
        <div class="btn-group">
            <button class="btn btn-primary" onclick="recognizeFormula()">开始识别公式</button>
            <button class="btn btn-default" onclick="clearAll()">清空重置</button>
            <button class="btn btn-default" onclick="copyLatex()">复制LaTeX代码</button>
        </div>

        <!-- 状态提示 -->
        <div class="loading" id="loading">⏳ 正在识别中，请稍候...</div>
        <div class="error" id="error"></div>

        <!-- 识别结果 -->
        <div class="result-box" id="resultBox" style="display: none;">
            <div class="result-title">识别结果 (LaTeX代码)：</div>
            <div class="latex-code" id="latexResult"></div>

            <div class="result-title">公式预览：</div>
            <div class="formula-preview" id="formulaPreview"></div>
        </div>
    </div>

    <script>
        let currentImageBase64 = "";
        const apiUrl = "https://dashscope.aliyuncs.com/api/v1/services/aigc/multimodal-generation/generation";

        // 页面加载完成初始化
        window.onload = function () {
            initPaste(); // 初始化粘贴功能
        };

        // 初始化粘贴图片
        function initPaste() {
            document.addEventListener('paste', function (e) {
                const items = e.clipboardData.items;
                for (let i = 0; i < items.length; i++) {
                    if (items[i].type.indexOf('image') !== -1) {
                        const file = items[i].getAsFile();
                        handleImageFile(file);
                        break;
                    }
                }
            });
        }

        // 图片上传监听
        document.getElementById('imageInput').addEventListener('change', function (e) {
            if (e.target.files[0]) {
                handleImageFile(e.target.files[0]);
            }
        });

        // 处理图片文件，转Base64
        function handleImageFile(file) {
            const reader = new FileReader();
            reader.onload = function (e) {
                currentImageBase64 = e.target.result;
                document.getElementById('previewImg').src = currentImageBase64;
                document.getElementById('previewImg').style.display = "block";
                hideError();
            };
            reader.readAsDataURL(file);
        }

        // 调用千问VL API识别公式
        async function recognizeFormula() {
            const apiKey = document.getElementById('apiKey').value.trim();
            if (!apiKey) {
                showError("请先输入阿里云API Key！");
                return;
            }
            if (!currentImageBase64) {
                showError("请上传或粘贴公式图片！");
                return;
            }

            // 显示加载
            showLoading();
            hideError();
            document.getElementById('resultBox').style.display = "none";

            try {
                // 去除Base64前缀
                const base64Data = currentImageBase64.split(',')[1];

                // 请求参数
                const requestData = {
                    "model": "qwen-vl-plus",
                    "input": {
                        "messages": [
                            {
                                "role": "user",
                                "content": [
                                    {
                                        "type": "image",
                                        "image": base64Data
                                    },
                                    {
                                        "type": "text",
                                        "text": "识别图片中的数学公式，只输出标准的LaTeX代码，不要任何多余文字、解释、标点符号"
                                    }
                                ]
                            }
                        ]
                    },
                    "parameters": {}
                };

                // 发送请求
                const response = await fetch(apiUrl, {
                    method: "POST",
                    headers: {
                        "Authorization": `Bearer ${apiKey}`,
                        "Content-Type": "application/json"
                    },
                    body: JSON.stringify(requestData)
                });

                const result = await response.json();

                if (response.ok) {
                    const latex = result.output.choices[0].message.content[0].text.trim();
                    showResult(latex);
                } else {
                    showError(`API调用失败：${result.code || response.status} - ${result.message || '未知错误'}`);
                }
            } catch (err) {
                showError(`网络错误：${err.message}`);
            } finally {
                hideLoading();
            }
        }

        // 显示识别结果
        function showResult(latex) {
            document.getElementById('latexResult').innerText = latex;
            document.getElementById('resultBox').style.display = "block";

            // 渲染公式
            const previewDom = document.getElementById('formulaPreview');
            previewDom.innerHTML = "";
            katex.render(latex, previewDom, {
                throwOnError: false,
                displayMode: true
            });
        }

        // 复制LaTeX代码
        function copyLatex() {
            const latex = document.getElementById('latexResult').innerText;
            if (!latex) {
                showError("暂无内容可复制");
                return;
            }
            navigator.clipboard.writeText(latex).then(() => {
                alert("复制成功！");
            });
        }

        // 清空所有内容
        function clearAll() {
            currentImageBase64 = "";
            document.getElementById('imageInput').value = "";
            document.getElementById('previewImg').style.display = "none";
            document.getElementById('resultBox').style.display = "none";
            document.getElementById('latexResult').innerText = "";
            document.getElementById('error').style.display = "none";
        }

        // 工具函数
        function showLoading() { document.getElementById('loading').style.display = "block"; }
        function hideLoading() { document.getElementById('loading').style.display = "none"; }
        function showError(msg) {
            const dom = document.getElementById('error');
            dom.innerText = msg;
            dom.style.display = "block";
        }
        function hideError() { document.getElementById('error').style.display = "none"; }
    </script>
</body>
</html>
```

# 7\. 成本与常见问题

## 7\.1 计费成本

通义千问VL\-plus 官方定价：**0\.008元/次调用**，1元可识别约125次，个人日常使用月成本低于1元，新用户赠送免费额度。

## 7\.2 常见问题排查

- **API调用失败**：检查Key是否正确、账号是否欠费、网络是否正常

- **识别效果差**：裁剪图片仅保留公式、提升图片清晰度、避免反光倾斜

- **公式渲染异常**：模型输出轻微语法误差，可手动微调LaTeX代码

# 8\. 后续扩展方向

- 新增识别历史记录本地存储功能

- 支持批量图片公式识别

- 新增LaTeX代码格式化、纠错功能

- 支持公式导出为图片、Word、Markdown格式

- 适配移动端响应式布局

# 9\. 项目总结

本项目基于通义千问VL多模态大模型，自研纯前端公式OCR系统，摒弃传统第三方工具的弊端，具备**零成本、高隐私、高精度、易拓展、开箱即用**的特点。整体架构极简、开发落地成本极低，完全满足个人及小型团队的公式识别刚需，是替代付费公式OCR工具的最优轻量化方案。

> （注：文档部分内容可能由 AI 生成）
