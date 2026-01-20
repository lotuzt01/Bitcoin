<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gemini Bitcoin Wallet Clone</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        body { background-color: #0f172a; color: white; font-family: 'Inter', sans-serif; }
        .gradient-card { background: linear-gradient(135deg, #2563eb 0%, #7c3aed 100%); }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen p-4">

    <div class="w-full max-w-md bg-slate-900 rounded-3xl shadow-2xl overflow-hidden border border-slate-800">
        <div class="p-6 text-center">
            <h1 class="text-xl font-bold tracking-tight">BTC WALLET CLONE</h1>
            <p class="text-xs text-slate-400 mt-1">Decentralized & Secure</p>
        </div>

        <div class="mx-6 p-6 rounded-2xl gradient-card shadow-lg mb-6">
            <div class="flex justify-between items-start mb-8">
                <div>
                    <p class="text-sm opacity-80">Total Saldo</p>
                    <h2 class="text-3xl font-extrabold mt-1">1.2450 BTC</h2>
                </div>
                <i class="fab fa-bitcoin text-3xl opacity-50"></i>
            </div>
            <div class="bg-black/20 p-3 rounded-lg flex items-center justify-between">
                <code class="text-[10px] break-all" id="walletAddr">bc1qm34lsc65zpw79lxes69zkqmk6ee3ewf0j77s3h</code>
                <button onclick="copyAddr()" class="ml-2 hover:text-yellow-400 transition">
                    <i class="far fa-copy text-sm"></i>
                </button>
            </div>
        </div>

        <div class="flex justify-around mb-8 px-6">
            <button class="flex flex-col items-center group">
                <div class="w-12 h-12 bg-slate-800 rounded-full flex items-center justify-center group-hover:bg-blue-600 transition">
                    <i class="fas fa-arrow-up"></i>
                </div>
                <span class="text-xs mt-2">Kirim</span>
            </button>
            <button class="flex flex-col items-center group">
                <div class="w-12 h-12 bg-slate-800 rounded-full flex items-center justify-center group-hover:bg-green-600 transition">
                    <i class="fas fa-arrow-down"></i>
                </div>
                <span class="text-xs mt-2">Terima</span>
            </button>
            <button class="flex flex-col items-center group">
                <div class="w-12 h-12 bg-slate-800 rounded-full flex items-center justify-center group-hover:bg-yellow-600 transition">
                    <i class="fas fa-history"></i>
                </div>
                <span class="text-xs mt-2">Riwayat</span>
            </button>
        </div>

        <div class="bg-slate-800/50 p-6 rounded-t-3xl border-t border-slate-700">
            <h3 class="text-sm font-semibold mb-4">Transaksi Terakhir</h3>
            <div class="space-y-4">
                <div class="flex items-center justify-between">
                    <div class="flex items-center">
                        <div class="w-8 h-8 bg-green-500/20 text-green-500 rounded-full flex items-center justify-center text-xs">
                            <i class="fas fa-plus"></i>
                        </div>
                        <div class="ml-3">
                            <p class="text-sm font-medium">Diterima</p>
                            <p class="text-[10px] text-slate-500">20 Jan 2026</p>
                        </div>
                    </div>
                    <p class="text-sm font-bold text-green-400">+0.05 BTC</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        function copyAddr() {
            const addr = document.getElementById('walletAddr').innerText;
            navigator.clipboard.writeText(addr);
            alert("Alamat berhasil disalin!");
        }
    </script>
</body>
</html>
