<!DOCTYPE html>
<html lang="zh‑CN">
<head>
    <meta charset="UTF‑8">
    <meta name="viewport" content="width=device‑width, initial‑scale=1.0">
    <title>Bugku‑MISC｜这是一张单纯的图片 Writeup</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border‑box;
        }
        body {
            min‑height: 100vh;
            background:
                radial‑gradient(circle at 12% 8%, rgba(16,80,110,0.22), transparent 55%),
                radial‑gradient(circle at 88% 90%, rgba(12,90,70,0.18), transparent 55%),
                #070b10;
            color: #d1d9e6;
            font‑family: "JetBrains Mono", Consolas, monospace;
            padding: 40px 20px 60px;
            display: flex;
            justify‑content: center;
        }
        .glass‑shell {
            width: 100%;
            max‑width: 980px;
            border‑radius: 18px;
            border: 1px solid rgba(148,163,184,0.16);
            background: linear‑gradient(145deg, rgba(26,34,48,0.75), rgba(14,20,32,0.82));
            box‑shadow: 0 22px 70px rgba(0,0,0,0.55);
            backdrop‑filter: blur(14px);
            overflow: hidden;
        }
        .window‑bar {
            padding:14px 20px;
            border‑bottom:1px solid rgba(148,163,184,0.14);
            display:flex;
            align‑items:center;
            gap:8px;
        }
        .dot {
            width:12px;
            height:12px;
            border‑radius:50%;
        }
        .dot‑red{background:#ff5f57;}
        .dot‑yellow{background:#ffbd2e;}
        .dot‑green{background:#28c840;}
        .win‑title{
            font‑size:13px;
            color:#94a3b8;
            margin‑left:8px;
        }
        .content‑wrap{
            padding:34px;
        }
        h1{
            color:#7dd3fc;
            font‑size:22px;
            margin‑bottom:14px;
        }
        .meta‑info{
            color:#64748b;
            font‑size:14px;
            margin‑bottom:26px;
        }
        h2{
            color:#a5f3fc;
            font‑size:18px;
            margin:28px 0 12px;
        }
        h3{
            color:#bae6fd;
            font‑size:16px;
            margin:20px 0 10px;
        }
        p{
            line‑height:1.75;
            margin:10px 0;
            color:#cbd5e1;
        }
        ul{
            padding‑left:22px;
            margin:12px 0;
        }
        li{
            line‑height:1.7;
            margin:6px 0;
            color:#cbd5e1;
        }
        code{
            background:rgba(15,23,42,0.7);
            color:#fcd34d;
            padding:2px 7px;
            border‑radius:4px;
        }
        .tip‑note{
            border‑left:3px solid #38bdf8;
            background:rgba(56,189,248,0.08);
            padding:10px 14px;
            margin:14px 0;
            font‑size:14px;
        }
        .back‑btn{
            display:inline‑block;
            margin‑top:34px;
            padding:10px 20px;
            border‑radius:10px;
            border:1px solid rgba(125,211,252,0.24);
            background:rgba(30,41,59,0.6);
            color:#7dd3fc;
            text‑decoration:none;
            transition:0.22s ease;
        }
        .back‑btn:hover{
            background:rgba(56,189,248,0.16);
            box‑shadow:0 0 14px rgba(56,189,248,0.22);
        }
        footer{
            margin‑top:38px;
            padding‑top:16px;
            border‑top:1px dashed rgba(148,163,184,0.16);
            display:flex;
            justify‑content:space‑between;
            font‑size:13px;
            color:#64748b;
        }
    </style>
</head>
<body>
<div class="glass‑shell">
    <div class="window‑bar">
        <div class="dot dot‑red"></div>
        <div class="dot dot‑yellow"></div>
        <div class="dot dot‑green"></div>
        <div class="win‑title">bugku‑misc‑单纯的图片.html — Writeup</div>
    </div>
    <div class="content‑wrap">
        <h1>Bugku‑MISC｜这是一张单纯的图片</h1>
        <div class="meta‑info">平台：Bugku CTF｜题型：MISC</div>

        <h2>题目信息</h2>
        <ul>
            <li>平台：Bugku CTF</li>
            <li>题型：MISC</li>
            <li>题目描述：这是一张单纯的图片，找到flag。</li>
            <li>附件：一张 jpg 图片文件</li>
        </ul>

        <h2>解题思路</h2>
        <p>这道题属于文件追加考点。出题人没有修改图片本身内容，直接在 <code>jpg</code> 文件的最末尾，追加了一段 HTML 十进制实体编码字符串。</p>
        <p>编码格式为 <code>&#数字;</code>，浏览器渲染会自动解析解码，但是查看网页源代码看到的仍是原始编码字符，无法直接搜索 <code>key{</code>，需要使用解码工具还原出明文flag。</p>

        <h2>详细解题过程</h2>
        <h3>步骤1：下载附件</h3>
        <p>拿到题目提供的jpg图片。</p>
        <div class="tip‑note">
            Windows系统默认<strong>隐藏已知文件扩展名</strong>，这是高频坑点，需要先在文件资源管理器设置中取消该选项，否则修改后缀不会生效。
        </div>

        <h3>步骤2：修改文件后缀</h3>
        <p>把 <code>.jpg</code> 修改为 <code>.html</code>。</p>
        <p>双击使用浏览器打开该文件，图片会正常显示在页面上。</p>

        <h3>步骤3：查看网页源代码</h3>
        <p>浏览器页面快捷键 <code>Ctrl + U</code>，打开view‑source源代码窗口。</p>
        <p>页面绝大部分内容是jpg图片的二进制乱码。</p>
        <p>直接按键盘 <code>End</code> 键，直接跳转到源代码文档<strong>最底部</strong>，得到一长串HTML十进制实体编码。</p>

        <h3>步骤4：实体编码解码</h3>
        <p>复制底部那一大段 <code>&#xxx;</code> 实体编码，使用HTML实体解码器，解码即可得到最终flag。</p>

        <a href="./index.html" class="back‑btn">← 返回首页</a>

        <footer>
            <span>© 2026 陆楷中</span>
            <span>GitHub Pages</span>
        </footer>
    </div>
</div>
</body>
</html>
