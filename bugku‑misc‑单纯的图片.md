<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Bugku - 这不是md5 Writeup</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            background:
                radial-gradient(circle at 12% 8%, rgba(56, 189, 248, 0.12), transparent 46%),
                radial-gradient(circle at 88% 82%, rgba(16, 185, 129, 0.08), transparent 46%),
                #07090d;
            color: #d6deeb;
            font-family: "JetBrains Mono", "Fira Code", Consolas, "Microsoft YaHei", monospace;
            padding: 40px 20px 60px;
            display: flex;
            justify-content: center;
        }

        .glass-shell {
            width: 100%;
            max-width: 980px;
            border-radius: 18px;
            border: 1px solid rgba(148, 163, 184, 0.18);
            background: linear-gradient(
                145deg,
                rgba(22, 30, 44, 0.78),
                rgba(12, 18, 30, 0.9)
            );
            box-shadow:
                0 25px 70px rgba(0, 0, 0, 0.65),
                0 0 1px rgba(125, 211, 252, 0.15),
                inset 0 1px 0 rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            overflow: hidden;
        }

        .window-bar {
            padding: 14px 20px;
            border-bottom: 1px solid rgba(148, 163, 184, 0.15);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
        }

        .dot-red {
            background: linear-gradient(145deg, #ff6058, #d9443c);
        }

        .dot-yellow {
            background: linear-gradient(145deg, #ffd166, #e0b143);
        }

        .dot-green {
            background: linear-gradient(145deg, #69db7c, #3fa358);
        }

        .window-title {
            margin-left: 8px;
            font-size: 13px;
            color: #94a3b8;
        }

        .content-box {
            padding: 34px;
        }

        h1 {
            color: #7dd3fc;
            font-size: 22px;
            margin-bottom: 14px;
        }

        .meta-info {
            color: #64748b;
            font-size: 14px;
            margin-bottom: 24px;
        }

        h2 {
            color: #a5f3fc;
            font-size: 18px;
            margin: 28px 0 12px;
        }

        p {
            line-height: 1.75;
            margin: 10px 0;
            color: #cbd5e1;
        }

        ul {
            padding-left: 22px;
            margin: 12px 0;
        }

        li {
            line-height: 1.7;
            margin: 6px 0;
            color: #cbd5e1;
        }

        code {
            color: #fcd34d;
            background: rgba(252, 211, 77, 0.1);
            padding: 2px 6px;
            border-radius: 4px;
        }

        pre {
            background: rgba(15, 23, 42, 0.75);
            border: 1px solid rgba(125, 211, 252, 0.16);
            border-radius: 10px;
            padding: 18px;
            overflow-x: auto;
            margin: 16px 0;
            color: #94e2d5;
        }

        .flag-box {
            border: 1px solid rgba(125, 211, 252, 0.35);
            background: rgba(56, 189, 248, 0.12);
            padding: 14px 16px;
            border-radius: 10px;
            color: #67e8f9;
            margin: 16px 0;
        }

        .back-btn {
            display: inline-block;
            margin-top: 32px;
            padding: 10px 18px;
            border-radius: 10px;
            border: 1px solid rgba(125, 211, 252, 0.25);
            background: rgba(30, 41, 59, 0.55);
            color: #7dd3fc;
            text-decoration: none;
            transition: 0.22s ease;
        }

        .back-btn:hover {
            border-color: #38bdf8;
            background: rgba(56, 189, 248, 0.18);
            box-shadow: 0 0 14px rgba(56, 189, 248, 0.22);
        }

        footer {
            margin-top: 36px;
            padding-top: 18px;
            border-top: 1px dashed rgba(148, 163, 184, 0.18);
            font-size: 13px;
            color: #64748b;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 10px;
        }
    </style>
</head>
<body>
    <div class="glass-shell">
        <div class="window-bar">
            <div class="dot dot-red"></div>
            <div class="dot dot-yellow"></div>
            <div class="dot dot-green"></div>
            <div class="window-title">bugku-crypto-not-md5.html - Writeup</div>
        </div>

        <div class="content-box">
            <h1>Bugku - 这不是md5 Writeup</h1>
            <div class="meta-info">
                题目：这不是md5 | 题型：Crypto 密码学 | 考点：Hex 十六进制转 ASCII
            </div>

            <h2>题目描述</h2>
            <ul>
                <li>题目名称：这不是md5</li>
                <li>提示：十六进制，每两个一组解密</li>
                <li>密文：<code>666c61677b616537333538376261353662616566357d</code></li>
            </ul>

            <h2>解题思路</h2>
            <p>题目名为“这不是md5”，实际是干扰信息。字符串由 0-9、a-f 组成，符合十六进制特征，且长度为偶数，因此可以按每两个字符一组转换为 ASCII 字符串。</p>

            <h2>Python 解密代码</h2>
<pre><code>hex_str = "666c61677b616537333538376261353662616566357d"
result = bytes.fromhex(hex_str).decode("utf-8")
print(result)</code></pre>

            <h2>运行结果</h2>
            <div class="flag-box">
                flag{ae73587ba56baef5}
            </div>

            <h2>总结</h2>
            <p>本题考察 Hex 编码识别与十六进制转 ASCII。不要被题目名称误导，直接按 Hex 解码即可得到 flag。</p>

            <a href="./index.html" class="back-btn">← 返回首页</a>

            <footer>
                <span>© 2026 陆楷中</span>
                <span>GitHub Pages</span>
            </footer>
        </div>
    </div>
</body>
</html>
