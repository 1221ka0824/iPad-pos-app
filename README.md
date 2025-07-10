<!DOCTYPE html>

<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>商品タップ計算アプリ - iPad POS</title>
    <meta name="description" content="iPadに最適化された商品タップ計算アプリ。簡単操作で合計金額を計算できます。">
    <meta name="keywords" content="iPad,POS,計算,アプリ,商品,レジ">

```
<!-- PWA設定 -->
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="POS計算アプリ">
<meta name="theme-color" content="#397DF6">

<!-- アイコン -->
<link rel="apple-touch-icon" sizes="180x180" href="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTgwIiBoZWlnaHQ9IjE4MCIgdmlld0JveD0iMCAwIDE4MCAxODAiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PHJlY3Qgd2lkdGg9IjE4MCIgaGVpZ2h0PSIxODAiIHJ4PSI0MCIgZmlsbD0iIzM5N0RGNiIvPjx0ZXh0IHg9IjkwIiB5PSIxMDAiIGZvbnQtZmFtaWx5PSJzeXN0ZW0tdWkiIGZvbnQtc2l6ZT0iNzAiIGZvbnQtd2VpZ2h0PSJib2xkIiBmaWxsPSJ3aGl0ZSIgdGV4dC1hbmNob3I9Im1pZGRsZSI+PoS8PC90ZXh0Pjwvc3ZnPg==">
<link rel="icon" href="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzIiIGhlaWdodD0iMzIiIHZpZXdCb3g9IjAgMCAzMiAzMiIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cmVjdCB3aWR0aD0iMzIiIGhlaWdodD0iMzIiIHJ4PSI4IiBmaWxsPSIjMzk3REY2Ii8+PHRleHQgeD0iMTYiIHk9IjIwIiBmb250LWZhbWlseT0ic3lzdGVtLXVpIiBmb250LXNpemU9IjE0IiBmb250LXdlaWdodD0iYm9sZCIgZmlsbD0id2hpdGUiIHRleHQtYW5jaG9yPSJtaWRkbGUiPu+8mPC8jzwvdGV4dD48L3N2Zz4=">

<!-- 外部ライブラリ -->
<script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/lucide-react/0.263.1/lucide-react.min.js"></script>
<script src="https://cdn.tailwindcss.com"></script>

<style>
    * {
        box-sizing: border-box;
    }
    
    body {
        margin: 0;
        padding: 0;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell', sans-serif;
        overflow-x: hidden;
        background: linear-gradient(135deg, #EBF4FF 0%, #C3DAFE 100%);
    }
    
    /* iPad用のスタイル調整 */
    @media screen and (min-width: 768px) {
        .container {
            max-width: 100vw;
            padding: 20px;
        }
    }
    
    /* モバイル対応 */
    @media screen and (max-width: 767px) {
        .grid-cols-3 {
            grid-template-columns: 1fr;
        }
        
        .col-span-2 {
            grid-column: span 1;
        }
        
        .col-span-1 {
            grid-column: span 1;
        }
        
        .text-5xl {
            font-size: 2.5rem;
        }
        
        .text-2xl {
            font-size: 1.5rem;
        }
        
        .mobile-grid {
            grid-template-columns: repeat(2, 1fr);
        }
    }
    
    /* タッチ操作の改善 */
    button {
        -webkit-touch-callout: none;
        -webkit-user-select: none;
        -khtml-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        touch-action: manipulation;
    }
    
    /* スクロール改善 */
    .scroll-area {
        -webkit-overflow-scrolling: touch;
    }
    
    /* ローディング画面 */
    .loading {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(135deg, #EBF4FF 0%, #C3DAFE 100%);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 9999;
    }
    
    .loading-spinner {
        width: 50px;
        height: 50px;
        border: 4px solid #E5E7EB;
        border-top: 4px solid #3B82F6;
        border-radius: 50%;
        animation: spin 1s linear infinite;
    }
    
    @keyframes spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
    }
    
    /* アニメーション */
    .fade-in {
        animation: fadeIn 0.5s ease-in;
    }
    
    @keyframes fadeIn {
        from { opacity: 0; transform: translateY(20px); }
        to { opacity: 1; transform: translateY(0); }
    }
    
    /* パフォーマンス改善 */
    .transform {
        transform: translateZ(0);
    }
    
    /* 印刷用スタイル */
    @media print {
        body {
            background: white;
        }
        
        .no-print {
            display: none;
        }
    }
</style>
```

</head>
<body>
    <!-- ローディング画面 -->
    <div id="loading" class="loading">
        <div class="loading-spinner"></div>
    </div>

```
<!-- メインアプリ -->
<div id="root" style="display: none;"></div>

<script type="text/babel">
    const { useState, useEffect } = React;
    const { Plus, Minus, Trash2, Edit3, Save, X, ShoppingCart, Download, Share2 } = lucide;

    function iPadPOSCalculator() {
        const [products, setProducts] = useState([
            { id: 1, name: 'コーヒー', price: 400 },
            { id: 2, name: '紅茶', price: 350 },
            { id: 3, name: 'サンドイッチ', price: 580 },
            { id: 4, name: 'ケーキ', price: 450 },
            { id: 5, name: 'パスタ', price: 980 },
            { id: 6, name: 'サラダ', price: 680 },
            { id: 7, name: 'ハンバーガー', price: 850 },
            { id: 8, name: 'オムライス', price: 1200 },
            { id: 9, name: 'カレーライス', price: 950 },
            { id: 10, name: 'デザートプレート', price: 650 }
        ]);
        
        const [cart, setCart] = useState([]);
        const [showAddForm, setShowAddForm] = useState(false);
        const [editingProduct, setEditingProduct] = useState(null);
        const [newProduct, setNewProduct] = useState({ name: '', price: '' });
        const [isMobile, setIsMobile] = useState(false);

        // 画面サイズ検出
        useEffect(() => {
            const checkScreenSize = () => {
                setIsMobile(window.innerWidth < 768);
            };
            
            checkScreenSize();
            window.addEventListener('resize', checkScreenSize);
            
            return () => window.removeEventListener('resize', checkScreenSize);
        }, []);

        const addToCart = (product) => {
            const existingItem = cart.find(item => item.id === product.id);
            if (existingItem) {
                setCart(cart.map(item => 
                    item.id === product.id 
                        ? { ...item, quantity: item.quantity + 1 }
                        : item
                ));
            } else {
                setCart([...cart, { ...product, quantity: 1 }]);
            }
        };

        const removeFromCart = (productId) => {
            const existingItem = cart.find(item => item.id === productId);
            if (existingItem.quantity === 1) {
                setCart(cart.filter(item => item.id !== productId));
            } else {
                setCart(cart.map(item => 
                    item.id === productId 
                        ? { ...item, quantity: item.quantity - 1 }
                        : item
                ));
            }
        };

        const clearCart = () => {
            setCart([]);
        };

        const getTotalAmount = () => {
            return cart.reduce((total, item) => total + (item.price * item.quantity), 0);
        };

        const addProduct = () => {
            if (newProduct.name && newProduct.price) {
                const id = Math.max(...products.map(p => p.id), 0) + 1;
                setProducts([...products, {
                    id,
                    name: newProduct.name,
                    price: parseInt(newProduct.price)
                }]);
                setNewProduct({ name: '', price: '' });
                setShowAddForm(false);
            }
        };

        const deleteProduct = (productId) => {
            setProducts(products.filter(p => p.id !== productId));
            setCart(cart.filter(item => item.id !== productId));
        };

        const startEdit = (product) => {
            setEditingProduct({ ...product });
        };

        const saveEdit = () => {
            if (editingProduct.name && editingProduct.price) {
                setProducts(products.map(p => 
                    p.id === editingProduct.id ? editingProduct : p
                ));
                setCart(cart.map(item => 
                    item.id === editingProduct.id 
                        ? { ...item, name: editingProduct.name, price: editingProduct.price }
                        : item
                ));
                setEditingProduct(null);
            }
        };

        const cancelEdit = () => {
            setEditingProduct(null);
        };

        const exportReceipt = () => {
            const receiptData = {
                date: new Date().toLocaleString('ja-JP'),
                items: cart,
                total: getTotalAmount(),
                itemCount: cart.reduce((total, item) => total + item.quantity, 0)
            };
            
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(receiptData, null, 2));
            const downloadElement = document.createElement("a");
            downloadElement.setAttribute("href", dataStr);
            downloadElement.setAttribute("download", `receipt_${new Date().getTime()}.json`);
            document.body.appendChild(downloadElement);
            downloadElement.click();
            document.body.removeChild(downloadElement);
        };

        const shareReceipt = async () => {
            const receiptText = `
```

📱 商品タップ計算アプリ
📅 ${new Date().toLocaleString(‘ja-JP’)}

🛍️ 注文内容:
${cart.map(item => `• ${item.name} × ${item.quantity} = ¥${(item.price * item.quantity).toLocaleString()}`).join(’\n’)}

💰 合計金額: ¥${getTotalAmount().toLocaleString()}
📦 商品数: ${cart.reduce((total, item) => total + item.quantity, 0)}点
`.trim();

```
            if (navigator.share) {
                try {
                    await navigator.share({
                        title: '注文内容',
                        text: receiptText,
                    });
                } catch (err) {
                    console.log('シェアがキャンセルされました');
                }
            } else {
                // フォールバック：クリップボードにコピー
                try {
                    await navigator.clipboard.writeText(receiptText);
                    alert('注文内容をクリップボードにコピーしました！');
                } catch (err) {
                    console.log('クリップボードへのコピーに失敗しました');
                }
            }
        };

        const gridCols = isMobile ? 'mobile-grid' : 'grid-cols-3';
        const containerCols = isMobile ? 'grid-cols-1' : 'grid-cols-3';
        const span2 = isMobile ? 'col-span-1' : 'col-span-2';
        const span1 = isMobile ? 'col-span-1' : 'col-span-1';

        return (
            <div className="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 p-4 md:p-6 fade-in">
                <div className="max-w-7xl mx-auto">
                    <div className="mb-6 md:mb-8 text-center">
                        <h1 className="text-3xl md:text-5xl font-bold text-gray-800 mb-2">
                            商品タップ計算アプリ
                        </h1>
                        <p className="text-lg md:text-xl text-gray-600">
                            {isMobile ? 'モバイル対応版' : 'iPad最適化版'}
                        </p>
                    </div>
                    
                    <div className={`grid ${containerCols} gap-4 md:gap-8 min-h-[calc(100vh-200px)]`}>
                        <div className={`${span2} bg-white rounded-2xl shadow-lg p-4 md:p-6 overflow-hidden`}>
                            <div className="flex flex-col md:flex-row justify-between items-center mb-4 md:mb-6 gap-4">
                                <h2 className="text-xl md:text-2xl font-semibold text-gray-800">商品一覧</h2>
                                <button
                                    onClick={() => setShowAddForm(!showAddForm)}
                                    className="bg-blue-500 text-white px-4 md:px-6 py-2 md:py-3 rounded-xl hover:bg-blue-600 transition-colors flex items-center gap-2 md:gap-3 text-base md:text-lg font-medium shadow-md"
                                >
                                    <Plus size={20} />
                                    商品追加
                                </button>
                            </div>

                            {showAddForm && (
                                <div className="mb-4 md:mb-6 p-4 md:p-6 bg-gray-50 rounded-xl border-2 border-gray-200">
                                    <div className="flex flex-col md:flex-row gap-4 mb-4">
                                        <input
                                            type="text"
                                            placeholder="商品名を入力"
                                            value={newProduct.name}
                                            onChange={(e) => setNewProduct({ ...newProduct, name: e.target.value })}
                                            className="flex-1 px-3 md:px-4 py-2 md:py-3 border-2 border-gray-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 text-base md:text-lg"
                                        />
                                        <input
                                            type="number"
                                            placeholder="価格"
                                            value={newProduct.price}
                                            onChange={(e) => setNewProduct({ ...newProduct, price: e.target.value })}
                                            className="w-full md:w-32 px-3 md:px-4 py-2 md:py-3 border-2 border-gray-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 text-base md:text-lg"
                                        />
                                    </div>
                                    <div className="flex gap-3">
                                        <button
                                            onClick={addProduct}
                                            className="bg-green-500 text-white px-4 md:px-6 py-2 md:py-3 rounded-xl hover:bg-green-600 transition-colors flex items-center gap-2 text-base md:text-lg font-medium"
                                        >
                                            <Save size={18} />
                                            追加
                                        </button>
                                        <button
                                            onClick={() => setShowAddForm(false)}
                                            className="bg-gray-500 text-white px-4 md:px-6 py-2 md:py-3 rounded-xl hover:bg-gray-600 transition-colors flex items-center gap-2 text-base md:text-lg font-medium"
                                        >
                                            <X size={18} />
                                            キャンセル
                                        </button>
                                    </div>
                                </div>
                            )}

                            <div className={`grid ${gridCols} gap-3 md:gap-4 overflow-y-auto h-[calc(100%-120px)] scroll-area`}>
                                {products.map((product) => (
                                    <div key={product.id} className="bg-gray-50 border-2 border-gray-200 rounded-xl p-3 md:p-4 hover:shadow-lg transition-all hover:border-blue-300 transform">
                                        {editingProduct && editingProduct.id === product.id ? (
                                            <div className="space-y-3">
                                                <input
                                                    type="text"
                                                    value={editingProduct.name}
                                                    onChange={(e) => setEditingProduct({ ...editingProduct, name: e.target.value })}
                                                    className="w-full px-3 py-2 border-2 border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-base md:text-lg"
                                                />
                                                <input
                                                    type="number"
                                                    value={editingProduct.price}
                                                    onChange={(e) => setEditingProduct({ ...editingProduct, price: parseInt(e.target.value) || 0 })}
                                                    className="w-full px-3 py-2 border-2 border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-base md:text-lg"
                                                />
                                                <div className="flex gap-2">
                                                    <button
                                                        onClick={saveEdit}
                                                        className="bg-green-500 text-white px-3 md:px-4 py-2 rounded-lg hover:bg-green-600 transition-colors flex items-center gap-2 text-sm md:text-base"
                                                    >
                                                        <Save size={16} />
                                                        保存
                                                    </button>
                                                    <button
                                                        onClick={cancelEdit}
                                                        className="bg-gray-500 text-white px-3 md:px-4 py-2 rounded-lg hover:bg-gray-600 transition-colors flex items-center gap-2 text-sm md:text-base"
                                                    >
                                                        <X size={16} />
                                                        キャンセル
                                                    </button>
                                                </div>
                                            </div>
                                        ) : (
                                            <>
                                                <div className="flex justify-between items-start mb-2 md:mb-3">
                                                    <h3 className="font-bold text-gray-800 text-base md:text-lg leading-tight">{product.name}</h3>
                                                    <div className="flex gap-1 md:gap-2 no-print">
                                                        <button
                                                            onClick={() => startEdit(product)}
                                                            className="text-blue-500 hover:text-blue-700 transition-colors p-1"
                                                        >
                                                            <Edit3 size={isMobile ? 16 : 20} />
                                                        </button>
                                                        <button
                                                            onClick={() => deleteProduct(product.id)}
                                                            className="text-red-500 hover:text-red-700 transition-colors p-1"
                                                        >
                                                            <Trash2 size={isMobile ? 16 : 20} />
                                                        </button>
                                                    </div>
                                                </div>
                                                <p className="text-xl md:text-2xl font-bold text-blue-600 mb-2 md:mb-4">¥{product.price.toLocaleString()}</p>
                                                <button
                                                    onClick={() => addToCart(product)}
                                                    className="w-full bg-gradient-to-r from-blue-500 to-blue-600 text-white py-2 md:py-3 rounded-xl hover:from-blue-600 hover:to-blue-700 transition-all font-bold text-base md:text-lg shadow-md transform hover:scale-105 active:scale-95"
                                                >
                                                    カートに追加
                                                </button>
                                            </>
                                        )}
                                    </div>
                                ))}
                            </div>
                        </div>

                        <div className={`${span1} bg-white rounded-2xl shadow-lg p-4 md:p-6 overflow-hidden`}>
                            <div className="flex flex-col md:flex-row justify-between items-center mb-4 md:mb-6 gap-4">
                                <h2 className="text-xl md:text-2xl font-semibold text-gray-800 flex items-center gap-2 md:gap-3">
                                    <ShoppingCart size={isMobile ? 24 : 28} />
                                    注文内容
                                </h2>
                                <div className="flex gap-2 no-print">
                                    <button
                                        onClick={clearCart}
                                        className="bg-red-500 text-white px-3 md:px-4 py-2 rounded-xl hover:bg-red-600 transition-colors flex items-center gap-2 text-sm md:text-lg font-medium"
                                    >
                                        <Trash2 size={16} />
                                        クリア
                                    </button>
                                </div>
                            </div>

                            <div className="space-y-3 mb-4 md:mb-6 overflow-y-auto h-[calc(100%-350px)] md:h-[calc(100%-300px)] scroll-area">
                                {cart.length === 0 ? (
                                    <div className="text-center py-8 md:py-12">
                                        <ShoppingCart size={isMobile ? 32 : 48} className="mx-auto text-gray-300 mb-4" />
                                        <p className="text-gray-500 text-base md:text-lg">商品を選択してください</p>
                                    </div>
                                ) : (
                                    cart.map((item) => (
                                        <div key={item.id} className="bg-gray-50 rounded-xl p-3 md:p-4 border-2 border-gray-200">
                                            <div className="flex justify-between items-start mb-2 md:mb-3">
                                                <div className="flex-1">
                                                    <h4 className="font-bold text-gray-800 text-base md:text-lg">{item.name}</h4>
                                                    <p className="text-gray-600 text-sm md:text-base">¥{item.price.toLocaleString()} × {item.quantity}</p>
                                                </div>
                                                <div className="font-bold text-gray-800 text-base md:text-lg">
                                                    ¥{(item.price * item.quantity).toLocaleString()}
                                                </div>
                                            </div>
                                            <div className="flex items-center justify-center gap-3 md:gap-4 no-print">
                                                <button
                                                    onClick={() => removeFromCart(item.id)}
                                                    className="bg-red-500 text-white w-8 h-8 md:w-10 md:h-10 rounded-full flex items-center justify-center hover:bg-red-600 transition-colors shadow-md"
                                                >
                                                    <Minus size={16} />
                                                </button>
                                                <span className="w-8 md:w-12 text-center font-bold text-lg md:text-xl">{item.quantity}</span>
                                                <button
                                                    onClick={() => addToCart(item)}
                                                    className="bg-green-500 text-white w-8 h-8 md:w-10 md:h-10 rounded-full flex items-center justify-center hover:bg-green-600 transition-colors shadow-md"
```