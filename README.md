<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>RanZZ AI - Code Architect Premium</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: radial-gradient(circle at 20% 30%, #0a0a0a, #030303);
            font-family: 'Inter', 'Segoe UI', 'Fira Code', monospace;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 1.5rem;
        }

        /* main container glassmorphism dark */
        .app-container {
            max-width: 1400px;
            width: 100%;
            background: rgba(18, 18, 24, 0.85);
            backdrop-filter: blur(12px);
            border-radius: 2.5rem;
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.8), 0 0 0 1px rgba(255,255,255,0.02) inset;
            overflow: hidden;
            transition: all 0.2s ease;
        }

        /* premium ribbon effect */
        .premium-badge {
            position: fixed;
            top: 1.2rem;
            right: 1.8rem;
            z-index: 100;
            background: rgba(0,0,0,0.6);
            backdrop-filter: blur(8px);
            padding: 0.4rem 1.2rem;
            border-radius: 60px;
            font-size: 0.8rem;
            font-weight: 600;
            letter-spacing: 0.5px;
            border-left: 3px solid #eab308;
            color: #f5f5f5;
            font-family: monospace;
            pointer-events: none;
        }

        .premium-badge span {
            color: #facc15;
            text-shadow: 0 0 2px gold;
        }

        /* header area */
        .ai-header {
            padding: 1.6rem 2rem;
            background: rgba(10, 10, 14, 0.7);
            border-bottom: 1px solid #2a2a2e;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            gap: 1rem;
        }

        .title-section h1 {
            font-size: 1.9rem;
            font-weight: 700;
            background: linear-gradient(135deg, #f0f0f0, #b9b9c3);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            letter-spacing: -0.5px;
        }

        .title-section h1 span {
            background: linear-gradient(135deg, #e0e0e0, #9ca3af);
            -webkit-background-clip: text;
            background-clip: text;
            font-weight: 800;
        }

        .sub {
            color: #9ca3af;
            font-size: 0.85rem;
            margin-top: 0.3rem;
            font-family: monospace;
        }

        .premium-ctrl {
            background: #1e1e24;
            padding: 0.5rem 1.2rem;
            border-radius: 2rem;
            border: 1px solid #3a3a44;
            display: flex;
            align-items: center;
            gap: 0.8rem;
        }

        .premium-status {
            font-weight: 500;
            font-size: 0.9rem;
        }

        .premium-status.free {
            color: #9ca3af;
        }

        .premium-status.premium {
            color: #facc15;
            text-shadow: 0 0 1px #ffd966;
        }

        .upgrade-btn {
            background: linear-gradient(95deg, #2c2c34, #1f1f26);
            border: none;
            padding: 0.4rem 1.2rem;
            border-radius: 2rem;
            font-weight: 600;
            font-size: 0.8rem;
            color: #ddd;
            cursor: pointer;
            transition: 0.2s;
            font-family: monospace;
            border: 0.5px solid #4b4b55;
        }

        .upgrade-btn:hover {
            background: #3a3a44;
            color: white;
            border-color: #facc15;
            box-shadow: 0 0 6px rgba(250,204,21,0.3);
        }

        /* main layout: 2 cols */
        .workspace {
            display: flex;
            flex-wrap: wrap;
            gap: 0;
        }

        .prompt-area {
            flex: 1.2;
            padding: 2rem 1.8rem;
            background: rgba(12, 12, 16, 0.5);
            border-right: 1px solid #25252c;
        }

        .output-area {
            flex: 1.8;
            padding: 2rem 1.8rem;
            background: #0c0c10;
        }

        .section-label {
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 1.5px;
            font-weight: 600;
            color: #8e8e9e;
            margin-bottom: 1rem;
        }

        textarea {
            width: 100%;
            background: #111116;
            border: 1px solid #2b2b33;
            border-radius: 1.2rem;
            padding: 1rem 1.2rem;
            color: #e3e3ec;
            font-family: 'Fira Code', monospace;
            font-size: 0.9rem;
            resize: vertical;
            outline: none;
            transition: 0.2s;
        }

        textarea:focus {
            border-color: #5f5f73;
            box-shadow: 0 0 0 2px rgba(100, 100, 140, 0.3);
        }

        .btn-generate {
            background: #1e1e28;
            border: 1px solid #3e3e4a;
            color: #f0f0f8;
            font-weight: 600;
            padding: 0.7rem 1.6rem;
            border-radius: 2rem;
            margin-top: 1.2rem;
            cursor: pointer;
            font-family: monospace;
            transition: 0.2s;
            width: 100%;
            font-size: 1rem;
        }

        .btn-generate:hover {
            background: #2c2c38;
            border-color: #a0a0b0;
            transform: scale(0.99);
        }

        .code-output {
            background: #09090c;
            border-radius: 1.2rem;
            border: 1px solid #25252e;
            overflow: auto;
            margin-top: 0.5rem;
        }

        pre {
            padding: 1rem;
            font-family: 'Fira Code', monospace;
            font-size: 0.8rem;
            color: #d4d4dc;
            white-space: pre-wrap;
            word-wrap: break-word;
            min-height: 280px;
            max-height: 480px;
            overflow-y: auto;
        }

        .copy-btn {
            background: transparent;
            border: none;
            color: #9ca3af;
            font-size: 0.7rem;
            cursor: pointer;
            margin-top: 0.5rem;
            text-align: right;
            display: inline-block;
            padding: 0.2rem 1rem;
            border-radius: 20px;
            background: #1a1a22;
        }

        .error-rate {
            background: #121218;
            padding: 0.5rem 1rem;
            border-radius: 2rem;
            font-size: 0.75rem;
            color: #bbb;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .footer-note {
            border-top: 1px solid #202026;
            padding: 1rem 2rem;
            text-align: center;
            font-size: 0.7rem;
            color: #5f5f6e;
        }

        @media (max-width: 780px) {
            .workspace {
                flex-direction: column;
            }
            .prompt-area {
                border-right: none;
                border-bottom: 1px solid #25252c;
            }
            .ai-header {
                flex-direction: column;
                align-items: flex-start;
            }
        }

        button:active {
            transform: scale(0.97);
        }
    </style>
</head>
<body>
<div class="app-container" id="ranzzApp">
    <div class="premium-badge" id="premiumRibbon">
        ⚡ RanZZ · <span id="ribbonStatus">FREE TIER</span>
    </div>
    <div class="ai-header">
        <div class="title-section">
            <h1>⚡ RanZZ <span>AI</span> — Code Architect</h1>
            <div class="sub">super inteligensi · error tolerance &lt; 10% · neural precision</div>
        </div>
        <div class="premium-ctrl">
            <div class="premium-status" id="premiumStatusLabel">🔓 Mode: Free</div>
            <button class="upgrade-btn" id="upgradeTrigger">✨ Upgrade Premium</button>
        </div>
    </div>

    <div class="workspace">
        <div class="prompt-area">
            <div class="section-label">📟 PROMPT ENGINE</div>
            <textarea id="promptInput" rows="5" placeholder="Contoh: &#10;Buatkan fungsi JavaScript untuk menghitung Fibonacci dengan memoization&#10;&#10;Atau: &#10;CSS grid responsive modern untuk galeri foto 3 kolom&#10;&#10;RanZZ akan menghasilkan kode berkualitas tinggi dengan error rate hanya 10% (premium bahkan lebih stabil)"></textarea>
            <div style="display: flex; justify-content: space-between; align-items: center; margin-top: 0.5rem;">
                <div class="error-rate">
                    <span>🧠 AI error margin : </span>
                    <strong id="errorRateDisplay">10%</strong>
                </div>
                <button class="btn-generate" id="generateBtn">⚙️ GENERATE CODE</button>
            </div>
            <div style="margin-top: 1rem; background:#0f0f14; border-radius: 1rem; padding: 0.5rem 1rem; font-size:0.7rem; color:#a1a1b0">
                💡 <strong>Premium Hint</strong> : Masukkan prompt <code>"upgrade to premium"</code> atau tekan tombol premium. Upgrade akan membuka fitur zero-noise dan code lebih kompleks.
            </div>
        </div>
        <div class="output-area">
            <div style="display: flex; justify-content: space-between; align-items: baseline; flex-wrap: wrap;">
                <div class="section-label">📜 GENERATED CODE (ranZZ output)</div>
                <button id="copyCodeBtn" class="copy-btn">📋 Salin Kode</button>
            </div>
            <div class="code-output">
                <pre id="codeResult">// RanZZ AI siap menerima prompt... 
// Berikan deskripsi kebutuhan kode, error rate terjaga <10%</pre>
            </div>
            <div style="margin-top: 1rem; font-size: 0.7rem; color:#7c7c8a; text-align:right">
                ✔️ akurasi & error rate dikontrol oleh sistem pintar
            </div>
        </div>
    </div>
    <div class="footer-note">
        RanZZ AI · Core engine dengan validasi syntax otomatis & error mitigation · Premium: akses zero-bug pipeline
    </div>
</div>

<script>
    // ******************************
    // RanZZ AI Super Pintar + Premium system
    // Error rate dasar ~10% (premium turun jadi 2-3% secara konsep)
    // Nama AI : RanZZ
    // ******************************

    (function(){
        // state
        let isPremium = false;
        const promptInput = document.getElementById('promptInput');
        const generateBtn = document.getElementById('generateBtn');
        const codeResultPre = document.getElementById('codeResult');
        const premiumStatusLabel = document.getElementById('premiumStatusLabel');
        const upgradeTrigger = document.getElementById('upgradeTrigger');
        const ribbonStatusSpan = document.getElementById('ribbonStatus');
        const errorRateSpan = document.getElementById('errorRateDisplay');
        const copyBtn = document.getElementById('copyCodeBtn');

        // helper: perbaharui UI premium
        function updatePremiumUI() {
            if(isPremium) {
                premiumStatusLabel.innerHTML = "👑 Mode: Premium ⚡";
                premiumStatusLabel.className = "premium-status premium";
                ribbonStatusSpan.innerHTML = "PREMIUM UNLOCKED";
                ribbonStatusSpan.style.color = "#facc15";
                errorRateSpan.innerHTML = "~2%";
                // visual premium effect di container
                document.getElementById('ranzzApp').style.boxShadow = "0 0 0 1px rgba(250,204,21,0.2), 0 25px 40px -12px black";
            } else {
                premiumStatusLabel.innerHTML = "🔓 Mode: Free";
                premiumStatusLabel.className = "premium-status free";
                ribbonStatusSpan.innerHTML = "FREE TIER";
                ribbonStatusSpan.style.color = "#bbbbdd";
                errorRateSpan.innerHTML = "10%";
                document.getElementById('ranzzApp').style.boxShadow = "";
            }
        }

        // fungsi untuk upgrade premium via prompt detection / tombol
        function performUpgrade() {
            if(!isPremium) {
                isPremium = true;
                updatePremiumUI();
                // tambah notifikasi ke output
                codeResultPre.innerText = "✨ PREMIUM ACTIVATED ✨\nRanZZ sekarang dalam mode premium penuh.\n- Error rate berkurang drastis\n- Code generation lebih kompleks & optimal\n- Sekarang coba prompt apapun untuk kode superior!";
                // optional: simpan ke localStorage
                localStorage.setItem('ranzz_premium', 'true');
            } else {
                codeResultPre.innerText = "// Anda sudah dalam mode premium. Nikmati kode tanpa batas!";
            }
        }

        // Cek localstorage apakah pernah premium
        function loadPremiumStatus() {
            const saved = localStorage.getItem('ranzz_premium');
            if(saved === 'true') {
                isPremium = true;
                updatePremiumUI();
            } else {
                isPremium = false;
                updatePremiumUI();
            }
        }

        // Sistem generate kode super pintar: error rate dijaga ~10% (Free) / premium ~2-3%
        // Menggunakan heuristic pintar + fallback untuk meminimalisir error sintaks.
        // Ai RanZZ akan membuat kode berdasarkan prompt dengan analisis cerdas.
        function generateCodeFromPrompt(promptText) {
            if(!promptText.trim()) {
                return "// [RanZZ] Tidak ada prompt. Masukkan deskripsi kode yang dibutuhkan.\n// Contoh: 'Buat fungsi sorting merge sort dalam JavaScript'";
            }
            
            // Deteksi jika prompt mengandung "upgrade to premium" tanpa case sensitive
            if(promptText.toLowerCase().includes("upgrade to premium")) {
                if(!isPremium) {
                    performUpgrade();
                    return "// ✅ PREMIUM AKTIF! ✅\n// RanZZ telah meningkatkan dirinya. Sekarang error rate hanya ~2%.\n// Silakan masukkan prompt teknis lainnya untuk merasakan kekuatan penuh AI.";
                } else {
                    return "// Anda sudah premium, masukkan prompt teknis untuk menghasilkan kode premium.";
                }
            }

            // === INTELLIGENT CODE GENERATION dengan style & error mitigation ===
            // Simulasi AI canggih dengan berbagai template dinamis + validasi.
            let generated = "";
            let lowerPrompt = promptText.toLowerCase();
            
            // kategori deteksi cerdas
            const isJS = /javascript|js|node|react|vue|frontend|function|array|map|filter|promise|async/i.test(lowerPrompt);
            const isPython = /python|django|flask|pandas|numpy|list comprehension|def /i.test(lowerPrompt);
            const isCSS = /css|style|flex|grid|responsive|animation|keyframes|hover/i.test(lowerPrompt);
            const isHTML = /html|tag|div|form|semantic|web component|dom/i.test(lowerPrompt);
            const isReact = /react|component|jsx|usestate|useeffect|props/i.test(lowerPrompt);
            
            // Premium menambah kompleksitas + optimalisasi error handling
            let complexityBoost = isPremium ? "with robust error boundaries, JSDoc, edge cases covered" : "basic implementation, error rate <10%";

            if(isReact && (isJS || isReact)) {
                generated = generateReactCode(promptText, isPremium);
            }
            else if(isJS) {
                generated = generateJavaScriptCode(promptText, isPremium);
            }
            else if(isPython) {
                generated = generatePythonCode(promptText, isPremium);
            }
            else if(isCSS) {
                generated = generateCSSCode(promptText);
            }
            else if(isHTML) {
                generated = generateHTMLCode(promptText);
            }
            else {
                // fallback generic : buat kode multi-purpose elegan dengan error handling
                generated = generateSmartGeneric(promptText, isPremium);
            }
            
            // Tambahan footer error rate info sebagai komentar
            let errorMsg = isPremium ? "// Error probability: ~2% (Premium mode aktif)" : "// Error rate dijaga ≤ 10% (Intelligent filtering)";
            return `${generated}\n\n/* ${errorMsg} */\n// RanZZ AI — generated with love & precision`;
        }
        
        // JAVASCRIPT (Node/Browser)
        function generateJavaScriptCode(prompt, premiumFlag) {
            let base = "";
            if(prompt.includes("fibonacci") || prompt.includes("fib")) {
                base = `function fibonacci(n, memo = {}) {\n  if (n <= 1) return n;\n  if (memo[n]) return memo[n];\n  memo[n] = fibonacci(n-1, memo) + fibonacci(n-2, memo);\n  return memo[n];\n}\n\n// Example:\nconsole.log(fibonacci(10)); // 55`;
                if(premiumFlag) base += `\n// Premium optimized: iterative O(n) dengan bigint support\nfunction fibIterative(n) {\n  let a=0,b=1;\n  for(let i=2;i<=n;i++) [a,b]=[b,a+b];\n  return b;\n}`;
            }
            else if(prompt.includes("sort") || prompt.includes("quick sort") || prompt.includes("merge")) {
                base = `function quickSort(arr) {\n  if (arr.length <= 1) return arr;\n  const pivot = arr[0];\n  const left = [], right = [];\n  for (let i = 1; i < arr.length; i++) {\n    arr[i] < pivot ? left.push(arr[i]) : right.push(arr[i]);\n  }\n  return [...quickSort(left), pivot, ...quickSort(right)];\n}\n// Test: quickSort([3,6,2,8,1]) → [1,2,3,6,8]`;
                if(premiumFlag) base += `\n// Premium: Merge Sort stabil dengan kompleksitas O(n log n)\nfunction mergeSort(arr) { if(arr.length<2) return arr; const mid=Math.floor(arr.length/2); return merge(mergeSort(arr.slice(0,mid)), mergeSort(arr.slice(mid))); }\nfunction merge(left,right){ let res=[]; while(left.length&&right.length) res.push(left[0]<right[0]?left.shift():right.shift()); return [...res,...left,...right]; }`;
            }
            else {
                base = `// RanZZ AI - custom JavaScript solution\n${premiumFlag ? "// Premium: async/await + error handling canggih\n" : "// Standalone safe code\n"}const executeTask = (input) => {\n  try {\n    // logika berdasarkan prompt: "${prompt.substring(0, 60)}"\n    const result = { status: "success", data: input?.toUpperCase?.() || "RanZZ output" };\n    return result;\n  } catch (err) {\n    return { error: err.message };\n  }\n};\n\n// export / contoh penggunaan\nconsole.log(executeTask("hello world"));`;
            }
            return base;
        }
        
        function generateReactCode(prompt, premiumFlag) {
            let component = `import React, { useState } from 'react';\n\nconst SmartComponent = () => {\n  const [data, setData] = useState(null);\n  const [loading, setLoading] = useState(false);\n  \n  const handleFetch = async () => {\n    setLoading(true);\n    try {\n      // simulasi fetch data\n      const res = await new Promise(resolve => setTimeout(() => resolve("RanZZ data"), 500));\n      setData(res);\n    } catch(e) { console.error(e); }\n    finally { setLoading(false); }\n  };\n  \n  return (\n    <div style={{ padding: '1rem' }}>\n      <h2>⚛️ RanZZ React Module</h2>\n      <button onClick={handleFetch}>Load Data</button>\n      {loading && <p>Loading...</p>}\n      {data && <pre>{data}</pre>}\n    </div>\n  );\n};\n\nexport default SmartComponent;`;
            if(premiumFlag) {
                component += `\n// Premium: useMemo + custom hook untuk performa tinggi\nimport { useMemo, useCallback } from 'react';\nexport const usePremiumHook = (dep) => useMemo(() => dep * 2, [dep]);`;
            }
            return component;
        }
        
        function generatePythonCode(prompt, premiumFlag) {
            let code = `# RanZZ AI Python code generator\n# Prompt: ${prompt}\n\ndef smart_solution(data):\n    """Intelligent processing with error rate ≤10%"""\n    try:\n        result = [x**2 for x in data] if isinstance(data, list) else str(data).upper()\n        return result\n    except Exception as e:\n        return f"Error handled: {e}"\n\nif __name__ == "__main__":\n    test = [1,2,3,4]\n    print(smart_solution(test))  # [1,4,9,16]`;
            if(premiumFlag) {
                code += `\n\n# Premium extra: type hints & async\nfrom typing import List\nasync def premium_process(items: List[int]) -> List[int]:\n    return [i*2 for i in items]`;
            }
            return code;
        }
        
        function generateCSSCode(prompt) {
            return `/* RanZZ CSS Genius */\n/* prompt: ${prompt} */\n.gallery-container {\n  display: grid;\n  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));\n  gap: 1.5rem;\n  padding: 2rem;\n  background: #111;\n}\n.card {\n  background: #1e1e2a;\n  border-radius: 1.5rem;\n  transition: transform 0.2s, box-shadow 0.2s;\n  overflow: hidden;\n}\n.card:hover {\n  transform: translateY(-6px);\n  box-shadow: 0 20px 30px -12px rgba(0,0,0,0.5);\n}\n@media (max-width: 640px) {\n  .gallery-container { gap: 1rem; padding: 1rem; }\n}`;
        }
        
        function generateHTMLCode(prompt) {
            return `<!DOCTYPE html>\n<html>\n<head><meta charset="UTF-8"><meta name="viewport" content="width=device-width"><title>RanZZ AI Page</title><style>body{background:#0b0b10;color:#eee;font-family:system-ui}</style></head>\n<body>\n<main style="max-width:800px;margin:3rem auto;padding:1rem;">\n<h1>⚡ RanZZ Smart HTML</h1>\n<p>Prompt: ${prompt.substring(0,80)}</p>\n<button id="magic">Klik Saya</button>\n<script>\ndocument.getElementById('magic')?.addEventListener('click',()=>alert('RanZZ AI sukses!'));\n<\/script>\n</main>\n</body>\n</html>`;
        }
        
        function generateSmartGeneric(prompt, premiumFlag) {
            let gen = `// RanZZ AI universal code snippet (error rate ≤10%)\n// Kebutuhan: ${prompt}\nclass RanZZAgent {\n  constructor(config) { this.config = config || { mode: "${premiumFlag ? 'premium' : 'free'}" }; }\n  \n  async execute(input) {\n    try {\n      // Simulasi proses cerdas\n      const output = \`RanZZ memproses: \${input} dengan presisi tinggi\`;\n      return { success: true, data: output };\n    } catch (err) {\n      return { success: false, error: err.message };\n    }\n  }\n}\n\nconst instance = new RanZZAgent();\ninstance.execute("sample").then(console.log);`;
            if(premiumFlag) gen += "\n// Premium advanced: built-in caching & stream processing\n// [Premium] active zero-friction pipeline";
            return gen;
        }
        
        // MAIN GENERATE EVENT
        function onGenerate() {
            let rawPrompt = promptInput.value;
            if(!rawPrompt.trim()) {
                codeResultPre.innerText = "// ⚠️ RanZZ butuh prompt...\n// Tulis deskripsi kode yang ingin dibuat. Contoh: buatkan fungsi validasi email JS";
                return;
            }
            // cek jika user menulis "upgrade to premium" pada prompt
            if(rawPrompt.toLowerCase().includes("upgrade to premium") && !isPremium) {
                performUpgrade();
                codeResultPre.innerText = "🌟 Premium unlocked via prompt! Sekarang RanZZ dalam mode superior.\nCoba prompt teknis lainnya untuk kode terbaik.";
                return;
            }
            const outputCode = generateCodeFromPrompt(rawPrompt);
            codeResultPre.innerText = outputCode;
        }
        
        // copy to clipboard
        function copyCode() {
            const codeText = codeResultPre.innerText;
            navigator.clipboard.writeText(codeText).then(() => {
                const originalText = copyBtn.innerText;
                copyBtn.innerText = "✅ Tersalin!";
                setTimeout(() => { copyBtn.innerText = originalText; }, 1500);
            }).catch(() => alert("Gagal menyalin, tapi kode bisa di-copy manual."));
        }
        
        // event listeners
        generateBtn.addEventListener('click', onGenerate);
        copyBtn.addEventListener('click', copyCode);
        upgradeTrigger.addEventListener('click', () => performUpgrade());
        
        // init premium status from localStorage
        loadPremiumStatus();
        // jika sudah premium perbarui tampilan error rate
        if(isPremium) errorRateSpan.innerHTML = "~2%";
        
        // tambahkan welcome message
        codeResultPre.innerText = "// RanZZ AI Code Architect siap ⚡\n// Error rate <10% (free) / premium <2%\n// Tulis prompt coding apapun, hasilkan kode tangguh.\n// Contoh: 'buatkan fungsi binary search di javascript'";
    })();
</script>
</body>
</html>
```
