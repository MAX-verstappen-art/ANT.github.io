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
