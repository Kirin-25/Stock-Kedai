<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Urus Niaga Patchers</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap');
        body { font-family: 'Inter', sans-serif; }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen p-4 md:p-8">

    <div class="max-w-6xl mx-auto">
        <div class="flex flex-col md:flex-row justify-between items-center mb-8 gap-4">
            <div>
                <h1 class="text-3xl font-bold text-green-400">PATCHERS SYSTEM</h1>
                <p class="text-slate-400">Pengurusan Stok & Pengiraan Jualan Automatik</p>
            </div>
            <div class="flex gap-2">
                <select id="filterSupplier" onchange="renderItems()" class="bg-slate-800 border border-slate-700 rounded px-4 py-2">
                    <option value="Semua">Semua Supplier</option>
                    <option value="Barang Tuan">Barang Tuan</option>
                    <option value="Barang Acid">Barang Acid</option>
                    <option value="Abang Din">Abang Din</option>
                    <option value="Sjn Sudiman">Sjn Sudiman</option>
                    <option value="LZ Ent">LZ Ent</option>
                </select>
            </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-10">
            <div class="bg-slate-800 p-6 rounded-xl border-l-4 border-blue-500 shadow-lg">
                <h2 class="text-sm text-slate-400 uppercase font-semibold">Total Bayaran Supplier</h2>
                <p id="totalSupplier" class="text-3xl font-bold mt-2 text-blue-400">RM 0.00</p>
            </div>
            <div class="bg-slate-800 p-6 rounded-xl border-l-4 border-green-500 shadow-lg">
                <h2 class="text-sm text-slate-400 uppercase font-semibold">Total Untung Bersih</h2>
                <p id="totalProfit" class="text-3xl font-bold mt-2 text-green-400">RM 0.00</p>
            </div>
            <div class="bg-slate-800 p-6 rounded-xl border-l-4 border-yellow-500 shadow-lg">
                <h2 class="text-sm text-slate-400 uppercase font-semibold">Baki Stok Keseluruhan</h2>
                <p id="totalStock" class="text-3xl font-bold mt-2 text-yellow-400">0 Unit</p>
            </div>
        </div>

        <div class="bg-slate-800 p-6 rounded-xl mb-10 border border-slate-700">
            <h2 class="text-xl font-semibold mb-4 text-white">Input Data Jualan Baru</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4">
                <input type="text" id="itemName" placeholder="Nama Produk" class="bg-slate-700 p-2 rounded border border-slate-600 focus:outline-none focus:border-green-500">
                <select id="supplier" class="bg-slate-700 p-2 rounded border border-slate-600">
                    <option value="Barang Tuan">Barang Tuan</option>
                    <option value="Barang Acid">Barang Acid</option>
                    <option value="Abang Din">Abang Din</option>
                    <option value="Sjn Sudiman">Sjn Sudiman</option>
                    <option value="LZ Ent">LZ Ent</option>
                </select>
                <input type="file" id="itemImage" accept="image/*" class="text-sm text-slate-400 file:mr-4 file:py-2 file:px-4 file:rounded file:border-0 file:text-sm file:font-semibold file:bg-green-600 file:text-white hover:file:bg-green-700">
                <input type="number" id="qtyRec" placeholder="Bil. Diterima" class="bg-slate-700 p-2 rounded border border-slate-600">
                <input type="number" id="qtySold" placeholder="Bil. Dijual" class="bg-slate-700 p-2 rounded border border-slate-600">
                <input type="number" id="costPrice" placeholder="Kos Asal (RM)" class="bg-slate-700 p-2 rounded border border-slate-600">
                <input type="number" id="salePrice" placeholder="Harga Jual (RM)" class="bg-slate-700 p-2 rounded border border-slate-600">
                <button onclick="saveItem()" class="bg-green-600 text-white font-bold p-2 rounded hover:bg-green-500 transition-colors">SIMPAN DATA</button>
            </div>
        </div>

        <div class="bg-slate-800 rounded-xl overflow-hidden border border-slate-700 shadow-xl">
            <div class="overflow-x-auto">
                <table class="w-full text-left border-collapse">
                    <thead class="bg-slate-700 text-slate-300 uppercase text-xs font-bold">
                        <tr>
                            <th class="p-4">Produk</th>
                            <th class="p-4">Supplier</th>
                            <th class="p-4 text-center">Diterima</th>
                            <th class="p-4 text-center">Dijual</th>
                            <th class="p-4 text-center">Stok Baki</th>
                            <th class="p-4 text-right">Bayaran Supplier</th>
                            <th class="p-4 text-right">Untung Bersih</th>
                            <th class="p-4 text-center">Tindakan</th>
                        </tr>
                    </thead>
                    <tbody id="itemList" class="divide-y divide-slate-700">
                        </tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        let items = JSON.parse(localStorage.getItem('patchersData')) || [];
        let editIndex = null;

        function saveItem() {
            const name = document.getElementById('itemName').value;
            const supplier = document.getElementById('supplier').value;
            const qtyR = parseFloat(document.getElementById('qtyRec').value) || 0;
            const qtyS = parseFloat(document.getElementById('qtySold').value) || 0;
            const cost = parseFloat
