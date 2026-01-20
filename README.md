<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bitcoin Key Generator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://bundle.run/bitcoinjs-lib@6.1.0"></script>
    <script src="https://bundle.run/bip39@3.1.0"></script>
    <script src="https://bundle.run/buffer@6.0.3"></script>
    <style>
        body { background-color: #0b0e11; color: #eaecef; font-family: 'Inter', sans-serif; }
        .key-box { background: #1e2329; border: 1px solid #474d57; }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen p-4">

    <div class="w-full max-w-lg bg-[#1e2329] p-8 rounded-2xl shadow-2xl border border-gray-700">
        <h1 class="text-2xl font-bold text-yellow-500 mb-2">Private Wallet Creator</h1>
        <p class="text-gray-400 text-sm mb-6">Hasilkan kunci pribadi dan alamat Bitcoin Anda sendiri.</p>

        <button onclick="generateNewWallet()" class="w-full bg-yellow-500 hover:bg-yellow-600 text-black font-bold py-3 rounded-xl transition mb-8">
            BUAT WALLET BARU
        </button>

        <div id="walletResult" class="hidden space-y-4">
            <div>
                <label class="text-xs text-gray-500 uppercase font-bold">12 Kata Rahasia (Mnemonic)</label>
                <div id="displayMnemonic" class="key-box p-4 rounded-lg mt-1 text-yellow-200 break-words text-sm italic"></div>
            </div>

            <div>
                <label class="text-xs text-gray-400 uppercase font-bold">Alamat Bitcoin (Public)</label>
                <div id="displayAddress" class="key-box p-3 rounded-lg mt-1 text-green-400 font-mono text-sm break-all"></div>
            </div>

            <div class="p-4 bg-red-900/20 border border-red-500/50 rounded-lg">
                <label class="text-xs text-red-400 uppercase font-bold">Private Key (WIF) - RAHASIA!</label>
                <div id="displayPrivateKey" class="mt-1 font-mono text-xs break-all text-red-300"></div>
                <p class="text-[10px] text-red-500 mt-2 font-bold italic text-center underline">JANGAN PERNAH BERIKAN PRIVATE KEY INI KEPADA SIAPAPUN!</p>
            </div>
        </div>
    </div>

    <script>
        function generateNewWallet() {
            try {
                // 1. Generate Mnemonic
                const mnemonic = bip39.generateMnemonic();
                
                // 2. Generate Seed dari Mnemonic
                const seed = bip39.mnemonicToSeedSync(mnemonic);
                
                // 3. Buat Master Node (Bitcoin Mainnet)
                const bitcoinLib = bitcoinjs;
                const root = bitcoinLib.bip32.fromSeed(seed);
                
                // 4. Derivasi path untuk SegWit (m/84'/0'/0'/0/0)
                const path = "m/84'/0'/0'/0/0";
                const child = root.derivePath(path);
                
                // 5. Generate Alamat Bech32 (bc1q...)
                const { address } = bitcoinLib.payments.p2wpkh({ 
                    pubkey: child.publicKey 
                });

                // Tampilkan di UI
                document.getElementById('displayMnemonic').innerText = mnemonic;
                document.getElementById('displayAddress').innerText = address;
                document.getElementById('displayPrivateKey').innerText = child.toWIF();
                document.getElementById('walletResult').classList.remove('hidden');
            } catch (e) {
                alert("Gagal membuat wallet: " + e.message);
            }
        }
    </script>
</body>
</html>
