<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="theme-color" content="#004D98">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>Barça Organizer Ultimate</title>
    
    <!-- Manifiesto PWA Dinámico (Base64) -->
    <link rel="manifest" id="my-manifest">

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <style>
        @media print { body { -webkit-print-color-adjust: exact; } }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        .prevent-select { -webkit-user-select: none; user-select: none; -webkit-tap-highlight-color: transparent; }
        @keyframes slideUp { from { transform: translateY(100%); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        .toast-animate { animation: slideUp 0.3s cubic-bezier(0.18, 0.89, 0.32, 1.28) forwards; }
        .h-dvh { height: 100vh; height: 100dvh; }
    </style>

    <!-- Script PWA Installer & Manifest Generator -->
    <script>
        // 1. Generar Icono Barça SVG Base64
        const iconSvg = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><rect width="512" height="512" fill="#004D98"/><path d="M0 0h512v150H0z" fill="#004D98"/><path d="M0 150h512v362H0z" fill="#A50044"/><path d="M256 200l-50 150h100z" fill="#EDBB00"/><text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle" font-family="Arial" font-size="250" font-weight="bold" fill="#EDBB00">B</text></svg>`;
        const iconBlob = new Blob([iconSvg], {type: 'image/svg+xml'});
        const iconUrl = 'data:image/svg+xml;base64,' + btoa(iconSvg);

        // 2. Generar Manifest JSON
        const manifest = {
            "name": "Barça Organizer",
            "short_name": "BarçaOrg",
            "start_url": ".",
            "display": "standalone",
            "background_color": "#121212",
            "theme_color": "#004D98",
            "orientation": "portrait",
            "icons": [
                { "src": iconUrl, "sizes": "512x512", "type": "image/svg+xml" }
            ]
        };
        const stringManifest = JSON.stringify(manifest);
        const blobManifest = new Blob([stringManifest], {type: 'application/json'});
        document.getElementById('my-manifest').href = URL.createObjectURL(blobManifest);

        // 3. Registrar Service Worker (Blob) para permitir instalación
        if ('serviceWorker' in navigator) {
            const swCode = `
                self.addEventListener('install', (e) => self.skipWaiting());
                self.addEventListener('activate', (e) => self.clients.claim());
                self.addEventListener('fetch', (e) => e.respondWith(fetch(e.request).catch(() => new Response("Offline"))));
            `;
            const swBlob = new Blob([swCode], {type: 'application/javascript'});
            navigator.serviceWorker.register(URL.createObjectURL(swBlob))
                .then(() => console.log('SW Registrado para PWA'))
                .catch(err => console.log('Error SW', err));
        }
    </script>
</head>
<body class="bg-gray-900 text-gray-100 overflow-hidden select-none touch-manipulation">
    
    <div id="root"></div>

    <script type="importmap">
    {
        "imports": {
            "react": "https://esm.sh/react@18.2.0",
            "react-dom/client": "https://esm.sh/react-dom@18.2.0/client",
            "lucide-react": "https://esm.sh/lucide-react@0.292.0"
        }
    }
    </script>

    <script type="module">
        import React, { useState, useEffect, useRef } from 'react';
        import { createRoot } from 'react-dom/client';
        import { 
            Truck, ShoppingCart, CheckSquare, Package, 
            Plus, Trash2, Download, Upload, 
            ArrowUp, ArrowDown, Archive, RotateCcw, 
            AlertCircle, X, Store, User, ArrowRight, Home,
            ArrowRightLeft, CircleSlash, Pencil,
            Settings, Save, History, Calendar, TrendingDown,
            Clock, ChevronRight, FileText, Printer, GripVertical, AlertTriangle, DollarSign, ListFilter, Check, Repeat, Bell, BellRing
        } from 'lucide-react';

        // Iconos SVG auxiliares
        const ChevronDownIcon = () => React.createElement('svg', { xmlns: "http://www.w3.org/2000/svg", width: "16", height: "16", viewBox: "0 0 24 24", fill: "none", stroke: "currentColor", strokeWidth: "2", strokeLinecap: "round", strokeLinejoin: "round" }, React.createElement('path', { d: "m6 9 6 6 6-6" }));
        const ChevronUpIcon = () => React.createElement('svg', { xmlns: "http://www.w3.org/2000/svg", width: "16", height: "16", viewBox: "0 0 24 24", fill: "none", stroke: "currentColor", strokeWidth: "2", strokeLinecap: "round", strokeLinejoin: "round" }, React.createElement('path', { d: "m18 15-6-6-6 6" }));

        function App() {
            // --- Estados Principales ---
            const [activeTab, setActiveTab] = useState(3); 
            const [items, setItems] = useState([]);
            const [templates, setTemplates] = useState([]); 
            const [isModalOpen, setIsModalOpen] = useState(false);
            const [showBodega, setShowBodega] = useState(false);
            const [showSettings, setShowSettings] = useState(false);
            const [showTemplatesDrawer, setShowTemplatesDrawer] = useState(false);
            const [editingItem, setEditingItem] = useState(null); 
            const [reorderModeId, setReorderModeId] = useState(null);
            
            // Estado de Ordenamiento
            const [sortBy, setSortBy] = useState('manual'); 
            const [sortDir, setSortDir] = useState('asc'); 
            const [showSortMenu, setShowSortMenu] = useState(false);

            // UI Feedback
            const [itemToDelete, setItemToDelete] = useState(null);
            const [toastMessage, setToastMessage] = useState(null);

            // Modales Extra
            const [isConsumeModalOpen, setIsConsumeModalOpen] = useState(false);
            const [consumeItem, setConsumeItem] = useState(null);
            const [consumeQty, setConsumeQty] = useState('');
            const [consumeLocation, setConsumeLocation] = useState('Sara');

            const [isHistoryModalOpen, setIsHistoryModalOpen] = useState(false);
            const [historyItem, setHistoryItem] = useState(null);

            const [isReportModalOpen, setIsReportModalOpen] = useState(false);
            const [reportStartDate, setReportStartDate] = useState('');
            const [reportEndDate, setReportEndDate] = useState('');

            // --- Estados Formulario ---
            const [newItemText, setNewItemText] = useState('');
            const [newItemPriority, setNewItemPriority] = useState('none');
            const [newItemQuantity, setNewItemQuantity] = useState(''); 
            const [newItemFrom, setNewItemFrom] = useState('Sara'); 
            const [newItemTo, setNewItemTo] = useState('Negocio');
            const [newItemContext, setNewItemContext] = useState('-'); 
            const [addToInventory, setAddToInventory] = useState(false);
            
            const [newItemPrice, setNewItemPrice] = useState('');
            const [newItemDate, setNewItemDate] = useState('');
            
            // Estado Recurrencia
            const [newItemRecurrence, setNewItemRecurrence] = useState([]);

            // Estados Inventario
            const [invHasSara, setInvHasSara] = useState(false);
            const [invHasNegocio, setInvHasNegocio] = useState(false);
            const [invQtySara, setInvQtySara] = useState('');
            const [invQtyNegocio, setInvQtyNegocio] = useState('');

            // Autocompletado
            const [suggestions, setSuggestions] = useState([]);
            const [showSuggestions, setShowSuggestions] = useState(false);

            const fileInputRef = useRef(null);
            const longPressTimer = useRef(null);

            // --- NOTIFICACIONES Y ALARMAS ---
            useEffect(() => {
                // Solicitar permisos al cargar
                if ('Notification' in window && Notification.permission !== 'granted') {
                    Notification.requestPermission();
                }

                // Intervalo de revisión cada 60 segundos
                const interval = setInterval(() => {
                    checkAlarms();
                }, 60000);

                // Chequear inmediatamente al cargar
                checkAlarms();

                return () => clearInterval(interval);
            }, [items]);

            const checkAlarms = () => {
                const now = new Date();
                // Ajustar a fecha local YYYY-MM-DD
                const todayStr = new Date(now.getTime() - (now.getTimezoneOffset() * 60000)).toISOString().split('T')[0];

                items.forEach(item => {
                    // Solo Tab HACER (id 2) y No completados
                    if (item.tabId === 2 && !item.completed) {
                        // Si tiene fecha deseada Y esa fecha es HOY
                        if (item.desiredDate === todayStr) {
                            const notificationKey = `notified_${item.id}_${todayStr}`;
                            const alreadyNotified = localStorage.getItem(notificationKey);

                            if (!alreadyNotified) {
                                sendNotification(`¡A hacer hoy!`, `Tarea pendiente: ${item.text}`);
                                localStorage.setItem(notificationKey, 'true'); // Marcar como notificado hoy
                            }
                        }
                    }
                });
            };

            const sendNotification = (title, body) => {
                if (!('Notification' in window)) return;
                
                if (Notification.permission === 'granted') {
                    // Vibración (si es compatible, aunque la notificación nativa suele vibrar)
                    if (navigator.vibrate) navigator.vibrate([200, 100, 200]);
                    
                    try {
                        new Notification(title, {
                            body: body,
                            icon: 'https://upload.wikimedia.org/wikipedia/en/4/47/FC_Barcelona_%28crest%29.svg', // Icono web generico
                            badge: 'https://upload.wikimedia.org/wikipedia/en/4/47/FC_Barcelona_%28crest%29.svg',
                            vibrate: [200, 100, 200]
                        });
                    } catch (e) {
                        console.error("Error lanzando notificación", e);
                    }
                }
            };

            const triggerTestNotification = () => {
                if (Notification.permission !== 'granted') {
                    Notification.requestPermission().then(permission => {
                        if (permission === 'granted') {
                            sendNotification("Barça Organizer", "¡Prueba exitosa! Recibirás alertas de tus tareas.");
                        } else {
                            alert("Permisos denegados. No podrás recibir alarmas.");
                        }
                    });
                } else {
                    sendNotification("Barça Organizer", "¡El sistema de alertas funciona correctamente!");
                }
            };

            // Toast Timer
            useEffect(() => {
                if (toastMessage) {
                    const timer = setTimeout(() => setToastMessage(null), 3000);
                    return () => clearTimeout(timer);
                }
            }, [toastMessage]);

            const TABS = [
                { id: 3, title: 'Inventario', icon: React.createElement(Package, { size: 18 }), color: 'yellow' },
                { id: 0, title: 'Movilizar', icon: React.createElement(Truck, { size: 18 }), color: 'blue' },
                { id: 2, title: 'Hacer', icon: React.createElement(CheckSquare, { size: 18 }), color: 'blue-red' },
                { id: 1, title: 'Comprar', icon: React.createElement(ShoppingCart, { size: 18 }), color: 'red' }
            ];

            const DAYS_OF_WEEK = [
                { id: 0, label: 'D' }, { id: 1, label: 'L' }, { id: 2, label: 'M' },
                { id: 3, label: 'M' }, { id: 4, label: 'J' }, { id: 5, label: 'V' }, { id: 6, label: 'S' },
            ];

            const PRIORITIES = {
                none:  { value: 0, color: 'bg-gray-700', label: '---', icon: React.createElement(CircleSlash, { size: 12 }) }, 
                baja:  { value: 1, color: 'bg-red-600', label: 'Baja' },
                media: { value: 2, color: 'bg-yellow-500', label: 'Media' }, 
                alta:  { value: 3, color: 'bg-green-600', label: 'Alta' }   
            };

            // --- Persistencia ---
            useEffect(() => {
                const savedItems = localStorage.getItem('barcaData_Ultimate_PWA');
                const savedTemplates = localStorage.getItem('barcaTemplates_PWA');
                if (savedItems) try { setItems(JSON.parse(savedItems)); } catch (e) { console.error(e); }
                if (savedTemplates) try { setTemplates(JSON.parse(savedTemplates)); } catch (e) { console.error(e); }
                
                const now = new Date();
                const today = now.toLocaleDateString('en-CA'); 
                setReportEndDate(today);
                const lastMonth = new Date(now);
                lastMonth.setMonth(now.getMonth() - 1);
                setReportStartDate(lastMonth.toLocaleDateString('en-CA'));
            }, []);

            useEffect(() => {
                localStorage.setItem('barcaData_Ultimate_PWA', JSON.stringify(items));
            }, [items]);

            useEffect(() => {
                localStorage.setItem('barcaTemplates_PWA', JSON.stringify(templates));
            }, [templates]);

            // --- Helpers Fechas ---
            const getLocalISOString = () => {
                const date = new Date();
                const offset = date.getTimezoneOffset() * 60000;
                return new Date(date.getTime() - offset).toISOString().slice(0, -1);
            };

            const getTodayDateStr = () => {
                const now = new Date();
                return new Date(now.getTime() - (now.getTimezoneOffset() * 60000)).toISOString().split('T')[0];
            };

            const formatDate = (isoString) => {
                if(!isoString) return '';
                const date = new Date(isoString);
                return date.toLocaleDateString('es-ES', { day: '2-digit', month: '2-digit', hour: '2-digit', minute:'2-digit' });
            };

            const formatDesiredDate = (dateStr) => {
                if(!dateStr) return '';
                const date = new Date(dateStr);
                const userTimezoneOffset = date.getTimezoneOffset() * 60000;
                const adjustedDate = new Date(date.getTime() + userTimezoneOffset);
                return adjustedDate.toLocaleDateString('es-ES', { day: '2-digit', month: '2-digit' });
            };

            const vibrate = (ms = 50) => {
                if (navigator.vibrate) navigator.vibrate(ms);
            };

            // --- Swipe Navigation Logic ---
            const onTouchStart = (e) => {
                setTouchEnd(null); 
                setTouchStart(e.targetTouches[0].clientX);
            };

            const onTouchMove = (e) => {
                setTouchEnd(e.targetTouches[0].clientX);
            };

            const onTouchEnd = () => {
                if (!touchStart || !touchEnd) return;
                const distance = touchStart - touchEnd;
                const isLeftSwipe = distance > 50;
                const isRightSwipe = distance < -50;
                
                const currentIndex = TABS.findIndex(t => t.id === activeTab);
                
                if (isLeftSwipe) {
                    if (currentIndex < TABS.length - 1) {
                        setActiveTab(TABS[currentIndex + 1].id);
                        vibrate(30);
                    }
                } else if (isRightSwipe) {
                    if (currentIndex > 0) {
                        setActiveTab(TABS[currentIndex - 1].id);
                        vibrate(30);
                    }
                }
            };

            // --- Long Press Logic ---
            const handleItemLongPressStart = (id) => {
                if (activeTab !== 3 || sortBy !== 'manual') return; 
                longPressTimer.current = setTimeout(() => {
                    setReorderModeId(id);
                    vibrate([50, 50, 50]); 
                }, 600);
            };

            const handleItemLongPressEnd = () => {
                if (longPressTimer.current) clearTimeout(longPressTimer.current);
            };

            const handleClickItem = (item) => {
                if (reorderModeId === item.id) {
                    setReorderModeId(null);
                    return;
                }
                if (item.tabId === 3) {
                    setHistoryItem(item);
                    openEditModal(item);
                } else if (!showBodega) {
                    openEditModal(item);
                }
            };

            // --- Ordenamiento ---
            const handleSortChange = (newSortBy) => {
                if (sortBy === newSortBy) {
                    setSortDir(sortDir === 'asc' ? 'desc' : 'asc');
                } else {
                    setSortBy(newSortBy);
                    setSortDir('asc');
                }
                setShowSortMenu(false);
            };

            // --- Autocompletado ---
            const handleTextChange = (text) => {
                setNewItemText(text);
                if ((activeTab === 0 || activeTab === 3)) {
                    const inventoryItems = items.filter(i => i.tabId === 3); 
                    if (text.trim().length === 0) {
                        setSuggestions(inventoryItems.filter(i => !i.completed));
                        setShowSuggestions(true);
                    } else {
                        const matches = inventoryItems.filter(i => 
                            i.text.toLowerCase().includes(text.toLowerCase()) && 
                            i.text.toLowerCase() !== text.toLowerCase() 
                        );
                        setSuggestions(matches);
                        setShowSuggestions(matches.length > 0);
                    }
                } else {
                    setShowSuggestions(false);
                }
            };

            const selectSuggestion = (itemOrText) => {
                const itemText = typeof itemOrText === 'string' ? itemOrText : itemOrText.text;
                const selectedItem = typeof itemOrText === 'object' ? itemOrText : items.find(i => i.text === itemOrText && i.tabId === 3);
                setNewItemText(itemText);
                setShowSuggestions(false);
                if (activeTab === 0 && selectedItem) {
                    const qtyS = parseInt(selectedItem.qtySara) || 0;
                    const qtyN = parseInt(selectedItem.qtyNegocio) || 0;
                    if (qtyS > 0 && qtyN === 0) { setNewItemFrom('Sara'); setNewItemTo('Negocio'); }
                    else if (qtyN > 0 && qtyS === 0) { setNewItemFrom('Negocio'); setNewItemTo('Sara'); }
                }
            };

            const initiateMoveFromInventory = (item) => {
                setActiveTab(0); 
                resetForm();     
                setNewItemText(item.text); 
                const qtyS = parseInt(item.qtySara) || 0;
                const qtyN = parseInt(item.qtyNegocio) || 0;
                if (qtyN > 0 && qtyS === 0) { setNewItemFrom('Negocio'); setNewItemTo('Sara'); }
                else { setNewItemFrom('Sara'); setNewItemTo('Negocio'); }
                setIsModalOpen(true); 
            };

            const existsInInventory = items.some(i => 
                i.tabId === 3 && i.text.toLowerCase().trim() === newItemText.toLowerCase().trim()
            );

            const swapLocations = () => {
                setNewItemFrom(prev => { 
                    const oldTo = newItemTo; 
                    setNewItemTo(prev); 
                    return oldTo; 
                });
            };

            const processLogisticsMove = (item) => {
                if (item.tabId !== 0) return items;
                const moveQty = parseInt(item.quantity);
                if (isNaN(moveQty)) return items; 
                const inventoryIndex = items.findIndex(i => i.tabId === 3 && i.text.toLowerCase().trim() === item.text.toLowerCase().trim());
                if (inventoryIndex === -1) return items;
                const newItems = [...items];
                const product = { ...newItems[inventoryIndex] };
                
                let newSara = parseInt(product.qtySara) || 0;
                let newNegocio = parseInt(product.qtyNegocio) || 0;
                if (item.from === 'Sara') newSara = Math.max(0, newSara - moveQty);
                if (item.from === 'Negocio') newNegocio = Math.max(0, newNegocio - moveQty);
                if (item.to === 'Sara') newSara += moveQty;
                if (item.to === 'Negocio') newNegocio += moveQty;

                product.qtySara = newSara;
                product.qtyNegocio = newNegocio;
                product.hasSara = newSara > 0;
                product.hasNegocio = newNegocio > 0;

                const historyEntry = {
                    date: getLocalISOString(),
                    type: 'move',
                    detail: `Movido ${moveQty} de ${item.from} a ${item.to}`,
                    saraAfter: newSara,
                    negocioAfter: newNegocio
                };
                product.history = product.history ? [historyEntry, ...product.history] : [historyEntry];
                product.updatedAt = getLocalISOString();
                newItems[inventoryIndex] = product;
                return newItems;
            };

            const openConsumeModal = (item) => {
                setConsumeItem(item);
                setConsumeQty('');
                const s = parseInt(item.qtySara) || 0;
                const n = parseInt(item.qtyNegocio) || 0;
                if (s > 0) setConsumeLocation('Sara');
                else if (n > 0) setConsumeLocation('Negocio');
                else setConsumeLocation(''); 
                setIsConsumeModalOpen(true);
            };

            const handleConsume = () => {
                if (!consumeItem || !consumeQty) return;
                const qtyToConsume = parseInt(consumeQty);
                if (isNaN(qtyToConsume) || qtyToConsume <= 0) return;
                const newItems = [...items];
                const index = newItems.findIndex(i => i.id === consumeItem.id);
                if (index === -1) return;
                const product = { ...newItems[index] };
                let currentStock = consumeLocation === 'Sara' ? (parseInt(product.qtySara) || 0) : (parseInt(product.qtyNegocio) || 0);
                
                if (qtyToConsume > currentStock) {
                    alert(`No hay suficiente stock en ${consumeLocation}.`);
                    return;
                }

                if (consumeLocation === 'Sara') product.qtySara = (parseInt(product.qtySara) || 0) - qtyToConsume;
                else product.qtyNegocio = (parseInt(product.qtyNegocio) || 0) - qtyToConsume;

                product.hasSara = (product.qtySara > 0);
                product.hasNegocio = (product.qtyNegocio > 0);

                const historyEntry = {
                    date: getLocalISOString(),
                    type: 'consume',
                    qty: qtyToConsume,
                    location: consumeLocation,
                    saraAfter: product.qtySara,
                    negocioAfter: product.qtyNegocio
                };
                
                const totalRemaining = (parseInt(product.qtySara)||0) + (parseInt(product.qtyNegocio)||0);
                let extraEntry = null;
                
                if (totalRemaining === 0) {
                    extraEntry = { date: getLocalISOString(), type: 'exhausted', detail: '⚠️ STOCK AGOTADO' };
                    product.completed = true; 
                    vibrate(100); 
                }

                let newHistory = product.history ? [historyEntry, ...product.history] : [historyEntry];
                if (extraEntry) newHistory = [extraEntry, ...newHistory];
                product.history = newHistory;
                product.updatedAt = getLocalISOString();
                
                newItems[index] = product;
                setItems(newItems);
                setIsConsumeModalOpen(false);
                setConsumeItem(null);
            };

            // --- CRUD ---
            const saveItem = () => {
                if (!newItemText.trim()) return;
                
                if (activeTab === 3 && !editingItem) {
                    const s = parseInt(invQtySara) || 0;
                    const n = parseInt(invQtyNegocio) || 0;
                    if (s + n <= 0) {
                        alert("El inventario debe tener al menos 1 unidad en Sara o Negocio.");
                        return;
                    }
                }

                if (activeTab === 0 && currentInventoryItem) {
                    if (currentInventoryItem.completed) {
                        alert("Este producto está AGOTADO en el archivo. Debes reabastecerlo en Inventario antes de moverlo.");
                        return;
                    }
                    if (!isMoveQuantityValid) {
                        alert(`Solo cuentas en ${newItemFrom} con ${availableStock} unidades.`);
                        return;
                    }
                }

                let newItemsList = [...items];
                const timestamp = getLocalISOString();

                if (activeTab === 3 && !editingItem && existsInInventory) {
                    const existingIndex = newItemsList.findIndex(i => i.tabId === 3 && i.text.toLowerCase().trim() === newItemText.toLowerCase().trim());
                    if (existingIndex !== -1) {
                        const product = { ...newItemsList[existingIndex] };
                        const addSara = invHasSara ? (parseInt(invQtySara) || 0) : 0;
                        const addNegocio = invHasNegocio ? (parseInt(invQtyNegocio) || 0) : 0;
                        
                        if (addSara + addNegocio <= 0) { alert("Debes agregar al menos 1 unidad."); return; }

                        product.qtySara = (parseInt(product.qtySara) || 0) + addSara;
                        product.qtyNegocio = (parseInt(product.qtyNegocio) || 0) + addNegocio;
                        
                        if (product.completed && (product.qtySara > 0 || product.qtyNegocio > 0)) product.completed = false;
                        if(product.qtySara > 0) product.hasSara = true;
                        if(product.qtyNegocio > 0) product.hasNegocio = true;

                        const historyEntry = {
                            date: timestamp,
                            addedSara: addSara,
                            addedNegocio: addNegocio,
                            type: 'add',
                            saraAfter: product.qtySara,
                            negocioAfter: product.qtyNegocio
                        };
                        product.history = product.history ? [historyEntry, ...product.history] : [historyEntry];
                        product.updatedAt = timestamp;
                        newItemsList[existingIndex] = product;
                        setItems(newItemsList);
                        closeModal();
                        vibrate(30);
                        return;
                    }
                }

                const itemData = {
                    text: newItemText,
                    priority: newItemPriority,
                    updatedAt: timestamp, 
                };

                if (activeTab === 0) { 
                    itemData.from = newItemFrom;
                    itemData.to = newItemTo;
                    itemData.quantity = newItemQuantity;
                    itemData.completed = editingItem ? editingItem.completed : false;
                } else if (activeTab === 3) { 
                    itemData.qtySara = invHasSara ? (parseInt(invQtySara) || 0) : 0;
                    itemData.qtyNegocio = invHasNegocio ? (parseInt(invQtyNegocio) || 0) : 0;
                    itemData.hasSara = (itemData.qtySara > 0);
                    itemData.hasNegocio = (itemData.qtyNegocio > 0);
                    
                    if (editingItem && (itemData.qtySara > 0 || itemData.qtyNegocio > 0)) itemData.completed = false;
                    else itemData.completed = editingItem ? editingItem.completed : false;

                    if (!editingItem) {
                        itemData.history = [{
                            date: timestamp,
                            addedSara: itemData.qtySara,
                            addedNegocio: itemData.qtyNegocio,
                            type: 'create',
                            saraAfter: itemData.qtySara,
                            negocioAfter: itemData.qtyNegocio
                        }];
                        itemData.createdAt = timestamp;
                    } else {
                        itemData.history = editingItem.history;
                        itemData.createdAt = editingItem.createdAt;
                    }
                } else {
                    // HACER / COMPRAR
                    itemData.context = newItemContext || '-'; 
                    itemData.quantity = newItemQuantity;
                    itemData.price = newItemPrice;
                    itemData.desiredDate = newItemDate;
                    itemData.recurrence = activeTab === 2 ? newItemRecurrence : null; 
                    itemData.completed = editingItem ? editingItem.completed : false;
                }

                if (editingItem) {
                    newItemsList = newItemsList.map(i => i.id === editingItem.id ? { ...i, ...itemData } : i);
                } else {
                    const newItem = { ...itemData, id: Date.now(), tabId: activeTab, createdAt: timestamp };
                    newItemsList = [newItem, ...newItemsList];
                    
                    if (activeTab === 0 && addToInventory && !existsInInventory) {
                        const moveQty = parseInt(newItemQuantity) || 0;
                        let initialSara = 0; let initialNegocio = 0;
                        if (newItemTo === 'Negocio') initialNegocio = moveQty; 
                        if (newItemTo === 'Sara') initialSara = moveQty;
                        
                        const invItem = {
                            id: Date.now() + 1,
                            tabId: 3,
                            text: newItemText,
                            qtySara: initialSara,
                            qtyNegocio: initialNegocio,
                            hasSara: initialSara > 0,
                            hasNegocio: initialNegocio > 0,
                            priority: 'none',
                            completed: false,
                            createdAt: timestamp,
                            updatedAt: timestamp,
                            history: [{ date: timestamp, addedSara: initialSara, addedNegocio: initialNegocio, type: 'auto-create', saraAfter: initialSara, negocioAfter: initialNegocio }]
                        };
                        newItemsList = [invItem, ...newItemsList];
                    }
                }
                setItems(newItemsList);
                closeModal();
                vibrate(30);
            };

            const openEditModal = (item) => {
                setEditingItem(item);
                setNewItemText(item.text);
                setNewItemPriority(item.priority || 'none');
                
                if (item.tabId === 0) {
                    setNewItemQuantity(item.quantity || '');
                    setNewItemFrom(item.from || 'Sara');
                    setNewItemTo(item.to || 'Negocio');
                } else if (item.tabId === 3) {
                    setInvHasSara(item.hasSara || item.qtySara > 0);
                    setInvHasNegocio(item.hasNegocio || item.qtyNegocio > 0);
                    setInvQtySara(item.qtySara);
                    setInvQtyNegocio(item.qtyNegocio);
                } else {
                    setNewItemQuantity(item.quantity || '');
                    setNewItemContext(item.context || '-');
                    setNewItemPrice(item.price || '');
                    setNewItemDate(item.desiredDate || '');
                    setNewItemRecurrence(item.recurrence || []); 
                }
                setActiveTab(item.tabId);
                setIsModalOpen(true);
            };

            const closeModal = () => { setIsModalOpen(false); setEditingItem(null); resetForm(); };

            const resetForm = () => {
                setNewItemText(''); setSuggestions([]); setShowSuggestions(false);
                setNewItemQuantity(''); setNewItemPriority('none');
                setNewItemFrom('Sara'); setNewItemTo('Negocio'); setAddToInventory(false);
                setInvHasSara(false); setInvHasNegocio(false); setInvQtySara(''); setInvQtyNegocio('');
                setNewItemPrice(''); setNewItemDate('');
                setNewItemRecurrence([]); 
                setNewItemContext('-'); 
            };

            const handleKeyDown = (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault(); 
                    saveItem();
                }
            };

            const toggleStatus = (id) => {
                vibrate(20);
                const todayStr = getTodayDateStr();
                
                let updatedItems = [...items];
                const targetItem = updatedItems.find(i => i.id === id);
                if (!targetItem) return;

                if (targetItem.tabId === 0 && !targetItem.completed && !showBodega) {
                    updatedItems = processLogisticsMove(targetItem);
                    const processedItem = updatedItems.find(i => i.id === id);
                    processedItem.completed = true;
                }
                else if (targetItem.recurrence && targetItem.recurrence.length > 0) {
                     if (targetItem.lastCompletedDate === todayStr) {
                         targetItem.lastCompletedDate = null;
                     } else {
                         targetItem.lastCompletedDate = todayStr;
                     }
                } 
                else {
                    targetItem.completed = !targetItem.completed;
                }
                
                setItems([...updatedItems]);
            };

            const requestDelete = (id, e) => {
                if(e) { e.stopPropagation(); e.preventDefault(); }
                setTimeout(() => {
                    if(window.confirm("¿Eliminar definitivamente?")) {
                        setItems(prevItems => prevItems.filter(item => item.id !== id));
                        if (isModalOpen) closeModal();
                        setToastMessage("Eliminado correctamente");
                    }
                }, 10);
            };

            const moveItem = (id, direction) => {
                const currentList = visibleItems;
                const indexInVisible = currentList.findIndex(i => i.id === id);
                if (indexInVisible === -1) return;
                const swapIndexInVisible = indexInVisible + direction;
                if (swapIndexInVisible < 0 || swapIndexInVisible >= currentList.length) return;
                const itemA = currentList[indexInVisible];
                const itemB = currentList[swapIndexInVisible];
                const indexRealA = items.findIndex(i => i.id === itemA.id);
                const indexRealB = items.findIndex(i => i.id === itemB.id);
                const newItems = [...items];
                const temp = newItems[indexRealA];
                newItems[indexRealA] = newItems[indexRealB];
                newItems[indexRealB] = temp;
                setItems(newItems);
                vibrate(20);
            };

            const generatePDFReport = () => {
                const allMovements = [];
                const startParts = reportStartDate.split('-');
                const start = new Date(startParts[0], startParts[1]-1, startParts[2], 0, 0, 0);
                const endParts = reportEndDate.split('-');
                const end = new Date(endParts[0], endParts[1]-1, endParts[2], 23, 59, 59);

                items.forEach(item => {
                    if (item.tabId === 3 && item.history && Array.isArray(item.history)) {
                        item.history.forEach(h => {
                            const hDate = new Date(h.date);
                            const hDateLocal = new Date(hDate.getTime() - (hDate.getTimezoneOffset() * 60000));
                            if (hDateLocal >= start && hDateLocal <= end) {
                                allMovements.push({ ...h, productName: item.text, productId: item.id });
                            }
                        });
                    }
                });
                
                allMovements.sort((a, b) => new Date(a.date) - new Date(b.date));

                const printWindow = window.open('', '_blank');
                if (!printWindow) { alert("Permite las ventanas emergentes"); return; }

                const htmlContent = `
                    <html><head><title>Reporte Inventario</title><style>
                    body { font-family: 'Arial', sans-serif; padding: 20px; font-size: 14px; }
                    h1 { color: #004D98; border-bottom: 3px solid #A50044; padding-bottom: 10px; }
                    table { width: 100%; border-collapse: collapse; margin-top: 20px; }
                    th, td { border: 1px solid #ccc; padding: 10px; text-align: left; }
                    th { background: #f2f2f2; color: #004D98; font-weight: bold; }
                    </style></head><body>
                        <h1>Reporte de Movimientos</h1><p>${reportStartDate} a ${reportEndDate}</p>
                        <table><thead><tr><th>Fecha</th><th>Producto</th><th>Acción</th><th>Detalle</th></tr></thead><tbody>
                            ${allMovements.length === 0 ? '<tr><td colspan="4">Sin movimientos.</td></tr>' : allMovements.map(m => `
                            <tr><td>${new Date(m.date).toLocaleString('es-ES')}</td><td>${m.productName}</td>
                            <td>${m.type.toUpperCase()}</td>
                            <td>${m.type === 'consume' ? `Restado ${m.qty} de ${m.location}` : m.type === 'exhausted' ? 'STOCK 0' : m.type === 'move' ? m.detail : `+${m.addedSara||0}S +${m.addedNegocio||0}N`}</td></tr>`).join('')}
                        </tbody></table><script>window.onload=function(){window.print()}<\/script></body></html>`;
                printWindow.document.write(htmlContent);
                printWindow.document.close();
            };

            const exportData = () => {
                const dataStr = JSON.stringify(items, null, 2);
                const blob = new Blob([dataStr], { type: "application/json" });
                const link = document.createElement("a");
                link.href = URL.createObjectURL(blob);
                const now = new Date();
                const pad = (n) => n.toString().padStart(2,'0');
                link.download = `barca_backup_${now.getFullYear()}-${pad(now.getMonth()+1)}-${pad(now.getDate())}_${pad(now.getHours())}-${pad(now.getMinutes())}.json`;
                link.click();
            };

            const importData = (e) => {
                const file = e.target.files[0];
                if (!file) return;
                const reader = new FileReader();
                reader.onload = (ev) => {
                    try { setItems(JSON.parse(ev.target.result)); } catch (er) { alert('Error JSON'); }
                };
                reader.readAsText(file);
                e.target.value = null;
            };

            // Filtrado
            const getVisibleItems = () => {
                const todayStr = getTodayDateStr();
                const todayIndex = new Date().getDay();

                let filtered = items.filter(item => {
                    if (showBodega) {
                        return item.tabId === activeTab && item.completed && (!item.recurrence || item.recurrence.length === 0);
                    }
                    if (activeTab === 2 && item.recurrence && item.recurrence.length > 0) {
                         if (!item.recurrence.includes(todayIndex)) return false;
                         return true;
                    }
                    if (activeTab === 1 || activeTab === 2) {
                        return item.tabId === activeTab;
                    }
                    return item.tabId === activeTab && !item.completed;
                });

                if (sortBy === 'priority') {
                    filtered.sort((a, b) => {
                        const valA = PRIORITIES[a.priority]?.value || 0;
                        const valB = PRIORITIES[b.priority]?.value || 0;
                        return sortDir === 'asc' ? valB - valA : valA - valB;
                    });
                } else if (sortBy === 'zone') {
                    filtered.sort((a, b) => {
                        const valA = a.context || a.from || '';
                        const valB = b.context || b.from || '';
                        return sortDir === 'asc' ? valA.localeCompare(valB) : valB.localeCompare(valA);
                    });
                } else if (sortBy === 'date') {
                    filtered.sort((a, b) => {
                        const dateA = a.desiredDate || a.createdAt;
                        const dateB = b.desiredDate || b.createdAt;
                        return sortDir === 'asc' ? new Date(dateA) - new Date(dateB) : new Date(dateB) - new Date(dateA);
                    });
                }
                
                if ((activeTab === 1 || activeTab === 2) && !showBodega && sortBy === 'manual') {
                    filtered.sort((a, b) => {
                        const aDone = a.recurrence ? a.lastCompletedDate === todayStr : a.completed;
                        const bDone = b.recurrence ? b.lastCompletedDate === todayStr : b.completed;
                        return (aDone === bDone ? 0 : aDone ? 1 : -1);
                    });
                }
                return filtered;
            };

            const visibleItems = getVisibleItems();

            // Helpers UI
            const currentInventoryItem = activeTab === 0 ? items.find(i => i.tabId === 3 && i.text.toLowerCase().trim() === newItemText.toLowerCase().trim()) : null;
            const availableStock = currentInventoryItem ? (newItemFrom === 'Sara' ? (parseInt(currentInventoryItem.qtySara)||0) : (parseInt(currentInventoryItem.qtyNegocio)||0)) : null;
            const isMoveQuantityValid = currentInventoryItem 
                ? (newItemQuantity && parseInt(newItemQuantity) <= availableStock && parseInt(newItemQuantity) > 0)
                : true;
            const canSwap = currentInventoryItem 
                ? (newItemFrom === 'Sara' ? (parseInt(currentInventoryItem.qtyNegocio)||0) > 0 : (parseInt(currentInventoryItem.qtySara)||0) > 0)
                : true;
            const stockSara = consumeItem ? (parseInt(consumeItem.qtySara) || 0) : 0;
            const stockNegocio = consumeItem ? (parseInt(consumeItem.qtyNegocio) || 0) : 0;
            const qtyNum = parseInt(consumeQty) || 0;
            const isValidConsume = qtyNum > 0 && ((consumeLocation === 'Sara' && qtyNum <= stockSara) || (consumeLocation === 'Negocio' && qtyNum <= stockNegocio));
            
            const toggleDay = (dayId) => {
                if (newItemRecurrence.includes(dayId)) setNewItemRecurrence(newItemRecurrence.filter(d => d !== dayId));
                else setNewItemRecurrence([...newItemRecurrence, dayId].sort());
            };
            const isRecurringCompletedToday = (item) => item.recurrence && item.lastCompletedDate === getTodayDateStr();

            return React.createElement("div", { className: "flex flex-col h-dvh bg-[#121212] font-sans max-w-full mx-auto shadow-2xl overflow-hidden relative border-x-0 sm:border-x-4 border-[#004D98] text-gray-100", 
                onTouchStart: onTouchStart, onTouchMove: onTouchMove, onTouchEnd: onTouchEnd 
            },
                
                // HEADER
                React.createElement("header", { className: "bg-gradient-to-r from-[#004D98] via-[#081f38] to-[#A50044] text-white pt-4 pb-0 shadow-lg z-10 sticky top-0" },
                    React.createElement("div", { className: "flex justify-between items-center px-4 mb-2" },
                        React.createElement("h1", { className: "text-xl font-bold text-[#EDBB00] tracking-tight italic drop-shadow-md" }, showBodega ? 'Archivo' : 'Força Stock'),
                        React.createElement("div", { className: "flex gap-2" },
                            React.createElement("button", { 
                                onClick: () => setShowSortMenu(!showSortMenu), 
                                className: `p-3 rounded-full transition active:scale-95 ${showSortMenu ? 'bg-[#EDBB00] text-[#004D98]' : 'bg-white/10 text-white'}`,
                                title: "Ordenar"
                            }, React.createElement(ListFilter, { size: 20 })),
                            React.createElement("button", { onClick: () => setShowBodega(!showBodega), className: `p-3 rounded-full transition active:scale-95 ${showBodega ? 'bg-[#EDBB00] text-[#004D98]' : 'bg-white/10 text-white'}`, title: "Bodega" }, React.createElement(Archive, { size: 20 })),
                            React.createElement("button", { onClick: () => setShowSettings(!showSettings), className: `p-3 rounded-full transition active:scale-95 ${showSettings ? 'bg-[#EDBB00] text-[#004D98]' : 'bg-white/10 text-white'}`, title: "Config" }, React.createElement(Settings, { size: 20 }))
                        )
                    ),
                    
                    // MENU ORDENAR
                    showSortMenu && React.createElement("div", { className: "px-4 pb-3 flex gap-2 overflow-x-auto no-scrollbar" },
                        ['manual', 'priority', 'zone', 'date'].map(s => 
                            React.createElement("button", { 
                                key: s, 
                                onClick: () => handleSortChange(s),
                                className: `px-4 py-2 rounded-full text-xs font-bold whitespace-nowrap border flex items-center gap-1 active:scale-95 transition ${sortBy === s ? 'bg-[#EDBB00] text-[#004D98] border-[#EDBB00]' : 'bg-white/10 text-gray-300 border-white/20'}`
                            }, 
                                s === 'manual' ? 'Manual' : s === 'priority' ? 'Importancia' : s === 'zone' ? 'Zona' : 'Fecha',
                                sortBy === s && React.createElement("span", null, sortDir === 'asc' ? '⬆️' : '⬇️')
                            )
                        )
                    ),

                    // Settings Menu
                    showSettings && React.createElement("div", { className: "absolute top-16 right-4 bg-[#1e1e1e] border border-gray-700 rounded-xl shadow-2xl p-4 z-50 w-64 animate-in fade-in zoom-in-95" },
                        React.createElement("div", { className: "flex flex-col gap-3" },
                            React.createElement("button", { onClick: triggerTestNotification, className: "flex items-center gap-3 p-3 text-sm hover:bg-gray-800 rounded-lg text-[#EDBB00] font-bold active:bg-gray-700" }, React.createElement(BellRing, { size: 18 }), "Probar Notificación"),
                            React.createElement("button", { onClick: () => { setIsReportModalOpen(true); setShowSettings(false); }, className: "flex items-center gap-3 p-3 text-sm hover:bg-gray-800 rounded-lg text-[#EDBB00] font-bold active:bg-gray-700" }, React.createElement(FileText, { size: 18 }), "Generar Reporte PDF"),
                            React.createElement("div", { className: "h-px bg-gray-700 my-1" }),
                            React.createElement("button", { onClick: () => fileInputRef.current.click(), className: "flex items-center gap-3 p-3 text-sm hover:bg-gray-800 rounded-lg text-gray-300 active:bg-gray-700" }, React.createElement(Upload, { size: 18 }), "Importar Backup"),
                            React.createElement("button", { onClick: exportData, className: "flex items-center gap-3 p-3 text-sm hover:bg-gray-800 rounded-lg text-gray-300 active:bg-gray-700" }, React.createElement(Download, { size: 18 }), "Exportar Backup")
                        )
                    ),
                    // Tabs
                    React.createElement("div", { className: "flex justify-between items-end mt-2 overflow-x-auto no-scrollbar" },
                        TABS.map((tab, index) => 
                            React.createElement("button", { key: tab.id, onClick: () => { setActiveTab(tab.id); setShowBodega(false); vibrate(20); }, className: `flex-1 min-w-[80px] flex flex-col items-center pb-3 px-1 transition-all ${activeTab === tab.id ? 'text-[#EDBB00] border-b-4 border-[#EDBB00] bg-white/5' : 'text-gray-400 border-b-4 border-transparent'}` },
                                React.createElement("div", { className: "mb-1" }, tab.icon),
                                React.createElement("span", { className: "text-[10px] uppercase font-bold tracking-wider" }, tab.title)
                            )
                        )
                    )
                ),

                // MAIN LIST
                React.createElement("main", { className: "flex-1 overflow-y-auto bg-[#0a0a0a] p-3 pb-32" },
                    showBodega && React.createElement("div", { className: "bg-[#EDBB00]/10 border-l-4 border-[#EDBB00] text-[#EDBB00] p-3 text-sm mb-4 flex items-center gap-3 rounded-r font-medium" }, React.createElement(AlertCircle, { size: 18 }), React.createElement("span", null, activeTab === 3 ? "Inventario Agotado" : "Items completados")),
                    
                    React.createElement("div", { className: "space-y-3" },
                        visibleItems.length === 0 && React.createElement("div", { className: "flex flex-col items-center justify-center py-20 text-gray-600 opacity-50" }, 
                            React.createElement("div", { className: "mb-2 scale-150" }, TABS.find(t=>t.id===activeTab)?.icon),
                            React.createElement("p", { className: "text-sm" }, "Lista vacía")
                        ),
                        visibleItems.map((item, idx) => {
                            const isRecurCompleted = isRecurringCompletedToday(item);
                            const isItemCompleted = (item.recurrence && item.recurrence.length > 0) ? isRecurCompleted : item.completed;
                            
                            return React.createElement("div", { 
                                key: item.id, 
                                className: `flex items-stretch bg-[#1e1e1e] rounded-xl shadow-md border overflow-hidden min-h-[60px] transition relative prevent-select active:scale-[0.99] touch-pan-y ${reorderModeId === item.id ? 'border-[#EDBB00] ring-2 ring-[#EDBB00] z-20 scale-105' : 'border-gray-800'} ${isItemCompleted && (item.tabId===1 || item.tabId===2) ? 'opacity-50' : ''}`,
                                onContextMenu: (e) => e.preventDefault(),
                                onMouseDown: () => handleItemLongPressStart(item.id),
                                onTouchStart: () => handleItemLongPressStart(item.id),
                                onMouseUp: handleItemLongPressEnd,
                                onTouchEnd: handleItemLongPressEnd,
                                onMouseLeave: handleItemLongPressEnd
                            },
                                React.createElement("div", { className: `w-2 ${PRIORITIES[item.priority]?.color || 'bg-gray-800'}` }),
                                
                                // Checkbox
                                item.tabId !== 3 && React.createElement("button", { onClick: () => toggleStatus(item.id), className: "w-12 flex items-center justify-center bg-[#252525] border-r border-gray-800 active:bg-black touch-manipulation" },
                                    isItemCompleted ? React.createElement(CheckSquare, { size: 20, className: "text-[#004D98]" }) : React.createElement("div", { className: "w-6 h-6 rounded-md border-2 border-gray-500 hover:border-[#A50044]" })
                                ),

                                // Contenido Central
                                React.createElement("div", { 
                                    className: "flex-1 py-3 px-4 flex flex-col justify-center min-w-0 cursor-pointer active:bg-[#252525]",
                                    onClick: () => handleClickItem(item)
                                },
                                    React.createElement("div", { className: "flex justify-between items-start mb-2" },
                                        React.createElement("span", { className: `text-base font-semibold leading-tight line-clamp-2 mr-2 select-none ${showBodega && item.tabId === 3 ? 'text-red-400' : 'text-gray-100'} ${isItemCompleted && (item.tabId===1||item.tabId===2) ? 'line-through text-gray-500' : ''}` }, 
                                            item.text,
                                            showBodega && item.tabId === 3 && React.createElement("span", { className: "ml-2 text-[10px] bg-red-900/50 text-red-300 px-1 rounded uppercase font-bold" }, "AGOTADO"),
                                            item.recurrence && item.recurrence.length > 0 && React.createElement("span", { className: "ml-2 inline-flex items-center text-[#EDBB00]" }, React.createElement(Repeat, {size:12}))
                                        ),
                                        // Gastar Button
                                        item.tabId === 3 && !showBodega && React.createElement("button", { 
                                            onClick: (e) => { e.stopPropagation(); openConsumeModal(item); vibrate(20); },
                                            className: "p-2 bg-red-900/20 text-red-500 border border-red-900/40 rounded-lg active:bg-red-900/40 transition shrink-0",
                                            title: "Gastar"
                                        }, React.createElement(TrendingDown, { size: 18 }))
                                    ),
                                    // Info Inferior
                                    React.createElement("div", { className: "flex flex-wrap items-center gap-2 select-none" },
                                        item.tabId === 3 && React.createElement(React.Fragment, null,
                                            !showBodega ? (
                                                React.createElement(React.Fragment, null,
                                                    (item.hasSara || item.qtySara > 0) && React.createElement("div", { className: "flex items-center gap-1 px-2 py-0.5 bg-purple-900/40 text-purple-300 rounded border border-purple-800" }, React.createElement("span", { className: "text-[10px] font-bold" }, "S:"), React.createElement("span", { className: "text-xs font-bold" }, item.qtySara)),
                                                    (item.hasNegocio || item.qtyNegocio > 0) && React.createElement("div", { className: "flex items-center gap-1 px-2 py-0.5 bg-blue-900/40 text-blue-300 rounded border border-blue-800" }, React.createElement(Store, { size: 10 }), React.createElement("span", { className: "text-xs font-bold" }, item.qtyNegocio)),
                                                    React.createElement("div", { className: "flex items-center gap-1 px-2 py-0.5 bg-gray-800 text-gray-200 rounded border border-gray-600" }, React.createElement("span", { className: "text-[10px] font-bold" }, "T:"), React.createElement("span", { className: "text-xs font-bold text-[#EDBB00]" }, (parseInt(item.qtySara)||0) + (parseInt(item.qtyNegocio)||0)))
                                                )
                                            ) : (
                                                React.createElement("div", { className: "text-xs text-gray-500 italic" }, "Toca para reabastecer")
                                            )
                                        ),
                                        
                                        (item.tabId === 1 || item.tabId === 2) && item.context && item.context !== '-' && React.createElement("div", { className: "flex items-center gap-1 px-2 py-0.5 bg-gray-800 rounded border border-gray-700 text-xs text-gray-400" },
                                            item.context === 'Casa' ? React.createElement(Home, { size: 10 }) : item.context === 'Negocio' ? React.createElement(Store, { size: 10 }) : React.createElement(User, { size: 10 }),
                                            item.context
                                        ),
                                        
                                        (item.tabId === 1 || item.tabId === 2) && item.price && React.createElement("span", { className: "text-xs text-green-400 font-mono" }, "$", item.price),
                                        (item.tabId === 1 || item.tabId === 2) && item.desiredDate && React.createElement("span", { className: "text-xs text-blue-300 flex items-center gap-1" }, React.createElement(Calendar, { size: 10 }), formatDesiredDate(item.desiredDate)),

                                        item.tabId !== 3 && item.quantity && React.createElement("span", { className: "px-2 py-0.5 bg-[#EDBB00]/20 text-[#EDBB00] text-[10px] font-bold rounded uppercase border border-[#EDBB00]/30" }, item.quantity),
                                        
                                        item.tabId === 0 && React.createElement("div", { className: "flex items-center gap-1 text-[10px] bg-black/30 px-2 py-1 rounded border border-gray-800 text-gray-400 font-medium" },
                                            item.from === 'Sara' ? React.createElement(User, {size: 10, className: "text-purple-400"}) : React.createElement(Store, {size: 10, className: "text-blue-400"}),
                                            React.createElement("span", null, item.from),
                                            React.createElement(ArrowRight, { size: 10, className: "text-[#EDBB00]" }),
                                            item.to === 'Sara' ? React.createElement(User, {size: 10, className: "text-purple-400"}) : React.createElement(Store, {size: 10, className: "text-blue-400"}),
                                            React.createElement("span", null, item.to)
                                        ),
                                        React.createElement("span", { className: "text-[9px] text-gray-600 flex items-center gap-1 ml-auto" }, React.createElement(Calendar, { size: 10 }), formatDate(item.createdAt || item.updatedAt))
                                    )
                                ),

                                // Botones Laterales
                                React.createElement("div", { className: "flex flex-col items-center justify-between py-2 px-1 border-l border-gray-800 bg-[#252525] w-12" },
                                    reorderModeId === item.id ? (
                                        React.createElement("div", { className: "flex flex-col h-full justify-between items-center w-full" },
                                            React.createElement("button", { onClick: (e) => { e.stopPropagation(); moveItem(item.id, -1); }, disabled: idx === 0, className: "p-2 text-[#EDBB00] active:bg-gray-700 disabled:opacity-30 rounded-full" }, React.createElement(ArrowUp, { size: 20 })),
                                            React.createElement(GripVertical, { size: 16, className: "text-gray-500" }),
                                            React.createElement("button", { onClick: (e) => { e.stopPropagation(); moveItem(item.id, 1); }, disabled: idx === visibleItems.length - 1, className: "p-2 text-[#EDBB00] active:bg-gray-700 disabled:opacity-30 rounded-full" }, React.createElement(ArrowDown, { size: 20 }))
                                        )
                                    ) : (
                                        React.createElement(React.Fragment, null,
                                            item.tabId === 3 && !showBodega && React.createElement("button", { onClick: (e) => { e.stopPropagation(); initiateMoveFromInventory(item); vibrate(20); }, className: "p-2 text-blue-400 active:text-white transition rounded-full" }, React.createElement(Truck, { size: 18 })),
                                            
                                            // LOGICA ELIMINAR/EDITAR
                                            (item.tabId === 1 || item.tabId === 2) ? (
                                                React.createElement(React.Fragment, null,
                                                    React.createElement("button", { onClick: (e) => { e.stopPropagation(); openEditModal(item); vibrate(20); }, className: "p-2 text-gray-500 active:text-[#EDBB00] transition rounded-full" }, React.createElement(Pencil, { size: 18 })),
                                                    React.createElement("button", { onClick: (e) => requestDelete(item.id, e), className: "p-2 text-red-500/70 active:text-red-500 transition rounded-full" }, React.createElement(Trash2, { size: 18 }))
                                                )
                                            ) : 
                                            !showBodega ? 
                                                React.createElement("button", { onClick: (e) => { e.stopPropagation(); item.tabId===3 ? (setHistoryItem(item), setIsHistoryModalOpen(true)) : openEditModal(item); vibrate(20); }, className: "p-2 text-gray-500 active:text-[#EDBB00] transition rounded-full" }, item.tabId === 3 ? React.createElement(History, { size: 18 }) : React.createElement(Pencil, { size: 18 }))
                                            : 
                                                React.createElement("button", { onClick: (e) => requestDelete(item.id, e), className: "p-2 text-gray-500 hover:text-red-500 transition rounded-full" }, React.createElement(Trash2, { size: 18 }))
                                        )
                                    )
                                )
                            )
                        })
                    )
                ),

                // FAB (Fixed at bottom right)
                !showBodega && React.createElement("button", { 
                    onClick: () => { resetForm(); setIsModalOpen(true); vibrate(30); }, 
                    className: "fixed bottom-8 right-6 w-16 h-16 bg-[#EDBB00] rounded-full shadow-[0_4px_20px_rgba(237,187,0,0.4)] flex items-center justify-center text-[#004D98] active:scale-90 transition-transform z-40 border-2 border-[#004D98]" 
                }, React.createElement(Plus, { size: 36, strokeWidth: 3 })),

                // TOAST
                toastMessage && React.createElement("div", { className: "fixed bottom-28 left-1/2 -translate-x-1/2 bg-[#1e1e1e] text-white px-6 py-3 rounded-full text-sm font-bold shadow-2xl border border-[#004D98] z-50 flex items-center gap-3 toast-animate" },
                    React.createElement(Check, { size: 20, className: "text-green-400" }),
                    toastMessage
                ),

                // Hidden File Input
                React.createElement("input", { type: "file", ref: fileInputRef, onChange: importData, className: "hidden", accept: ".json" }),

                // --- MODALES ---
                
                // Modal Confirmar Eliminación
                itemToDelete && React.createElement("div", { className: "fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 animate-in fade-in" },
                    React.createElement("div", { className: "bg-[#1e1e1e] w-full max-w-xs rounded-2xl p-6 border border-gray-700 text-center" },
                        React.createElement("div", { className: "w-12 h-12 bg-red-900/30 rounded-full flex items-center justify-center mx-auto mb-4" }, React.createElement(Trash2, { className: "text-red-500", size: 24 })),
                        React.createElement("h3", { className: "text-lg font-bold text-white mb-2" }, "¿Borrar definitivamente?"),
                        React.createElement("p", { className: "text-gray-400 text-sm mb-6" }, "Esta acción no se puede deshacer."),
                        React.createElement("div", { className: "flex gap-3" },
                            React.createElement("button", { onClick: () => setItemToDelete(null), className: "flex-1 py-3 bg-gray-700 rounded-xl text-white font-bold" }, "Cancelar"),
                            React.createElement("button", { onClick: confirmDelete, className: "flex-1 py-3 bg-red-600 rounded-xl text-white font-bold active:bg-red-700" }, "Borrar")
                        )
                    )
                ),

                // Modal Crear/Editar
                isModalOpen && React.createElement("div", { className: "fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-end sm:items-center justify-center p-4" },
                    React.createElement("div", { className: "bg-[#1e1e1e] w-full max-w-sm rounded-t-2xl sm:rounded-2xl shadow-2xl p-6 flex flex-col max-h-[85dvh] overflow-y-auto border border-gray-800" },
                        React.createElement("div", { className: "flex justify-between items-center mb-6 border-b border-gray-700 pb-4" },
                            React.createElement("h2", { className: "text-xl font-bold text-[#EDBB00] flex items-center gap-2" }, editingItem ? React.createElement(Pencil, { size: 20 }) : React.createElement(Plus, { size: 20 }), editingItem ? (editingItem.completed && editingItem.tabId === 3 ? 'Reabastecer' : 'Editar') : 'Nuevo', ": ", TABS.find(t => t.id === activeTab)?.title),
                            React.createElement("button", { onClick: closeModal, className: "text-gray-500 hover:text-white p-2" }, React.createElement(X, { size: 24 }))
                        ),
                        React.createElement("div", { className: "space-y-5 relative" },
                            React.createElement("div", { className: "relative" },
                                React.createElement("label", { className: "text-xs font-bold text-gray-500 uppercase mb-1 block" }, "Nombre"),
                                React.createElement("input", { 
                                    type: "text", 
                                    className: "w-full p-4 bg-[#121212] border border-gray-700 rounded-xl outline-none text-base text-white focus:border-[#EDBB00] transition", 
                                    value: newItemText, 
                                    onChange: (e) => handleTextChange(e.target.value), 
                                    onKeyDown: handleKeyDown,
                                    autoFocus: true 
                                }),
                                showSuggestions && (activeTab === 0 || activeTab === 3) && React.createElement("div", { className: "absolute top-full left-0 right-0 bg-[#252525] border border-gray-700 rounded-xl shadow-xl mt-1 z-50 max-h-48 overflow-y-auto" },
                                    suggestions.map(s => React.createElement("button", { key: s.id, onClick: () => selectSuggestion(s), className: "w-full text-left px-4 py-3 text-sm text-gray-300 hover:bg-[#EDBB00] hover:text-[#004D98] block border-b border-gray-800 last:border-0" }, s.text))
                                )
                            ),
                            // Lógica inputs
                            activeTab === 3 ? React.createElement("div", { className: "bg-[#252525] p-4 rounded-xl border border-gray-700" },
                                React.createElement("div", { className: "flex justify-between items-center mb-3" },
                                    React.createElement("label", { className: "text-xs font-bold text-[#EDBB00] uppercase" }, "Stock Actual"),
                                    editingItem && editingItem.completed && React.createElement("span", { className: "text-xs text-green-400 font-bold" }, "REACTIVAR")
                                ),
                                React.createElement("div", { className: "flex gap-3 mb-3" },
                                    React.createElement("button", { onClick: () => setInvHasSara(!invHasSara), className: `flex-1 py-2 rounded-lg border text-sm font-bold transition ${invHasSara?'bg-purple-900/40 border-purple-500 text-white':'bg-[#121212] border-gray-700 text-gray-500'}` }, "Sara"),
                                    React.createElement("button", { onClick: () => setInvHasNegocio(!invHasNegocio), className: `flex-1 py-2 rounded-lg border text-sm font-bold transition ${invHasNegocio?'bg-blue-900/40 border-blue-500 text-white':'bg-[#121212] border-gray-700 text-gray-500'}` }, "Negocio")
                                ),
                                React.createElement("div", { className: "flex gap-3" },
                                    invHasSara && React.createElement("input", { type: "number", placeholder: "Cant.", value: invQtySara, onChange: e=>setInvQtySara(e.target.value), onKeyDown: handleKeyDown, className: "flex-1 p-3 bg-[#121212] border border-purple-900 rounded-lg text-center text-white font-bold text-lg" }),
                                    invHasNegocio && React.createElement("input", { type: "number", placeholder: "Cant.", value: invQtyNegocio, onChange: e=>setInvQtyNegocio(e.target.value), onKeyDown: handleKeyDown, className: "flex-1 p-3 bg-[#121212] border border-blue-900 rounded-lg text-center text-white font-bold text-lg" })
                                )
                            ) : React.createElement("div", { className: "relative" },
                                React.createElement("label", { className: "text-xs font-bold text-gray-500 uppercase mb-1 block" }, "Cantidad"),
                                React.createElement("input", { 
                                    type: "number", 
                                    className: `w-full p-4 bg-[#121212] border rounded-xl outline-none text-base text-white transition ${!isMoveQuantityValid && activeTab === 0 ? 'border-red-500 focus:border-red-500' : 'border-gray-700 focus:border-[#EDBB00]'}`, 
                                    value: newItemQuantity, 
                                    onChange: (e) => setNewItemQuantity(e.target.value),
                                    onKeyDown: handleKeyDown
                                }),
                                activeTab === 0 && currentInventoryItem && React.createElement("div", { className: "mt-2 flex justify-between text-xs" },
                                    React.createElement("span", { className: "text-gray-400" }, `Disponible en ${newItemFrom}:`),
                                    React.createElement("span", { className: `${!isMoveQuantityValid ? 'text-red-500 font-bold' : 'text-green-400 font-bold'}` }, availableStock)
                                )
                            ),
                            
                            // Campos Extra Compras
                            (activeTab === 1 || activeTab === 2) && React.createElement("div", { className: "flex gap-3" },
                                React.createElement("div", { className: "relative flex-1" },
                                    React.createElement("label", { className: "text-xs font-bold text-gray-500 uppercase mb-1 block" }, "Precio"),
                                    React.createElement("input", { type: "number", className: "w-full p-3 pl-8 bg-[#121212] border border-gray-700 rounded-lg text-white text-sm", value: newItemPrice, onChange: e=>setNewItemPrice(e.target.value), onKeyDown: handleKeyDown }),
                                    React.createElement(DollarSign, { size: 14, className: "absolute left-3 top-9 text-gray-500" })
                                ),
                                React.createElement("div", { className: "relative flex-1" },
                                    React.createElement("label", { className: "text-xs font-bold text-gray-500 uppercase mb-1 block" }, "Fecha"),
                                    React.createElement("input", { type: "date", className: "w-full p-3 pl-8 bg-[#121212] border border-gray-700 rounded-lg text-white text-sm", value: newItemDate, onChange: e=>setNewItemDate(e.target.value), onKeyDown: handleKeyDown }),
                                    React.createElement(Calendar, { size: 14, className: "absolute left-3 top-9 text-gray-500" })
                                )
                            ),

                            // Recurrencia (Solo Hacer)
                            activeTab === 2 && React.createElement("div", { className: "bg-[#252525] p-4 rounded-xl border border-gray-700" },
                                React.createElement("label", { className: "text-xs font-bold text-[#EDBB00] uppercase mb-2 block flex items-center gap-2" }, React.createElement(Repeat, {size:14}), " Repetir los días"),
                                React.createElement("div", { className: "flex justify-between gap-1" },
                                    DAYS_OF_WEEK.map(day => 
                                        React.createElement("button", {
                                            key: day.id,
                                            onClick: () => toggleDay(day.id),
                                            className: `w-9 h-9 rounded-full text-xs font-bold flex items-center justify-center transition-all ${newItemRecurrence.includes(day.id) ? 'bg-[#004D98] text-white ring-2 ring-[#EDBB00]' : 'bg-[#121212] text-gray-500 border border-gray-600'}`
                                        }, day.label)
                                    )
                                )
                            ),

                            // Contexto Compras
                            (activeTab === 1 || activeTab === 2) && React.createElement("div", { className: "flex gap-2" },
                                ['-', 'Negocio', 'Casa', 'Personal'].map(ctx => 
                                    React.createElement("button", { 
                                        key: ctx,
                                        onClick: () => setNewItemContext(ctx),
                                        className: `flex-1 py-2 rounded-lg border text-xs flex items-center justify-center gap-1 transition ${newItemContext === ctx ? 'bg-gray-700 border-gray-500 text-white font-bold' : 'bg-[#121212] border-gray-700 text-gray-500'}`
                                    },
                                    ctx === '-' ? React.createElement(CircleSlash, {size:12}) : ctx === 'Negocio' ? React.createElement(Store, {size:12}) : ctx === 'Casa' ? React.createElement(Home, {size:12}) : React.createElement(User, {size:12}),
                                    ctx === '-' ? 'Sin Cat.' : ctx)
                                )
                            ),

                            // Prioridad
                            React.createElement("div", null,
                                React.createElement("label", { className: "text-xs font-bold text-gray-500 uppercase mb-1 block" }, "Prioridad"),
                                React.createElement("div", { className: "flex gap-2" }, Object.entries(PRIORITIES).map(([k, s]) => React.createElement("button", { key: k, onClick: () => setNewItemPriority(k), className: `flex-1 py-2 text-xs font-bold rounded-lg border transition ${newItemPriority===k? s.color+' text-white border-transparent shadow-lg':'bg-[#121212] text-gray-500 border-gray-700'}` }, s.label)))
                            ),
                            
                            // LOGISTICA UI SIMPLIFICADA (SWAP BUTTON)
                            activeTab === 0 && React.createElement("div", { className: "bg-[#004D98]/10 p-4 rounded-xl border border-[#004D98]/30 mt-4 flex items-center justify-between gap-2" },
                                React.createElement("div", { className: "flex flex-col items-center flex-1" },
                                    React.createElement("span", { className: "text-xs text-gray-400 mb-1 font-bold uppercase" }, "Desde"),
                                    React.createElement("div", { className: `px-3 py-3 rounded-lg font-bold w-full text-center text-sm ${newItemFrom === 'Sara' ? 'text-purple-400 border border-purple-900/50 bg-purple-900/20' : 'text-blue-400 border border-blue-900/50 bg-blue-900/20'}` }, newItemFrom)
                                ),
                                
                                React.createElement("button", { 
                                    onClick: swapLocations, 
                                    disabled: currentInventoryItem && !canSwap,
                                    className: `p-3 bg-[#1e1e1e] rounded-full border border-gray-600 hover:scale-110 transition-transform shadow-lg z-10 ${currentInventoryItem && !canSwap ? 'opacity-50 cursor-not-allowed text-gray-500' : 'text-[#EDBB00] hover:bg-gray-700'}`
                                }, React.createElement(ArrowRightLeft, { size: 20 })),

                                React.createElement("div", { className: "flex flex-col items-center flex-1" },
                                    React.createElement("span", { className: "text-xs text-gray-400 mb-1 font-bold uppercase" }, "Hasta"),
                                    React.createElement("div", { className: `px-3 py-3 rounded-lg font-bold w-full text-center text-sm ${newItemTo === 'Sara' ? 'text-purple-400 border border-purple-900/50 bg-purple-900/20' : 'text-blue-400 border border-blue-900/50 bg-blue-900/20'}` }, newItemTo)
                                )
                            ),

                            // Botón Guardar
                            React.createElement("button", { 
                                onClick: saveItem, 
                                disabled: activeTab === 0 && currentInventoryItem && !isMoveQuantityValid,
                                className: `w-full py-4 mt-2 font-bold rounded-xl shadow-lg text-lg active:scale-95 transition ${activeTab === 0 && currentInventoryItem && !isMoveQuantityValid ? 'bg-gray-700 text-gray-500 cursor-not-allowed' : 'bg-[#004D98] text-[#EDBB00]'}` 
                            }, editingItem ? (editingItem.completed && editingItem.tabId === 3 ? 'Reabastecer' : 'Guardar') : 'Agregar')
                        )
                    )
                ),

                // Modal Gastar
                isConsumeModalOpen && consumeItem && React.createElement("div", { className: "fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 animate-in fade-in" },
                    React.createElement("div", { className: "bg-[#1e1e1e] w-full max-w-sm rounded-2xl p-6 border border-red-900/50" },
                        React.createElement("h3", { className: "text-xl font-bold text-red-500 mb-4 flex items-center gap-2" }, React.createElement(TrendingDown), " Registrar Gasto"),
                        React.createElement("p", { className: "text-gray-400 text-sm mb-4" }, "Restar de: ", React.createElement("strong", { className: "text-white" }, consumeItem.text)),
                        
                        React.createElement("div", { className: "flex gap-3 mb-6" },
                            React.createElement("button", { 
                                onClick: () => setConsumeLocation('Sara'), 
                                disabled: stockSara <= 0,
                                className: `flex-1 p-3 rounded-xl border transition-all ${
                                    consumeLocation === 'Sara' ? 'bg-purple-900/60 border-purple-500 text-white ring-2 ring-purple-500/30' : 
                                    stockSara <= 0 ? 'bg-gray-800/50 border-gray-800 text-gray-600 cursor-not-allowed' :
                                    'bg-[#121212] border-gray-700 text-gray-400 hover:bg-gray-800'
                                }` 
                            }, 
                                React.createElement("div", { className: "text-xs font-bold uppercase mb-1" }, "Sara"),
                                React.createElement("div", { className: "text-2xl font-bold" }, stockSara)
                            ),
                            React.createElement("button", { 
                                onClick: () => setConsumeLocation('Negocio'), 
                                disabled: stockNegocio <= 0,
                                className: `flex-1 p-3 rounded-xl border transition-all ${
                                    consumeLocation === 'Negocio' ? 'bg-blue-900/60 border-blue-500 text-white ring-2 ring-blue-500/30' : 
                                    stockNegocio <= 0 ? 'bg-gray-800/50 border-gray-800 text-gray-600 cursor-not-allowed' :
                                    'bg-[#121212] border-gray-700 text-gray-400 hover:bg-gray-800'
                                }` 
                            }, 
                                React.createElement("div", { className: "text-xs font-bold uppercase mb-1" }, "Negocio"),
                                React.createElement("div", { className: "text-2xl font-bold" }, stockNegocio)
                            )
                        ),

                        React.createElement("div", { className: "relative mb-6" },
                            React.createElement("input", { 
                                type: "number", 
                                value: consumeQty, 
                                onChange: e => setConsumeQty(e.target.value), 
                                className: `w-full p-4 bg-[#121212] border rounded-xl text-white text-xl font-bold outline-none focus:ring-2 ${
                                    consumeQty && !isValidConsume ? 'border-red-500 focus:ring-red-500/30' : 'border-gray-700 focus:ring-red-500/30'
                                }`, 
                                placeholder: "Cantidad a gastar", 
                                autoFocus: true 
                            }),
                            consumeQty && !isValidConsume && parseInt(consumeQty) > 0 && React.createElement("div", { className: "absolute top-full left-0 text-red-500 text-xs mt-1 flex items-center gap-1 font-bold" }, 
                                React.createElement(AlertTriangle, { size: 12 }), "Excede el stock disponible"
                            )
                        ),

                        React.createElement("div", { className: "flex gap-3" },
                            React.createElement("button", { onClick: () => setIsConsumeModalOpen(false), className: "flex-1 py-3 bg-gray-800 rounded-xl text-gray-300 font-bold" }, "Cancelar"),
                            React.createElement("button", { 
                                onClick: handleConsume, 
                                disabled: !isValidConsume,
                                className: `flex-1 py-3 rounded-xl text-white font-bold transition-all ${
                                    isValidConsume ? 'bg-red-700 hover:bg-red-600 shadow-lg shadow-red-900/20' : 'bg-gray-700 text-gray-500 cursor-not-allowed'
                                }` 
                            }, "Confirmar")
                        )
                    )
                ),

                // Modal Historial
                isHistoryModalOpen && historyItem && React.createElement("div", { className: "fixed inset-0 bg-black/80 z-50 flex items-center justify-center p-4 animate-in fade-in" },
                    React.createElement("div", { className: "bg-[#1e1e1e] w-full max-w-sm rounded-2xl p-6 border border-gray-700 h-[60vh] overflow-y-auto flex flex-col" },
                        React.createElement("div", { className: "flex justify-between mb-4 border-b border-gray-700 pb-2" },
                            React.createElement("h3", { className: "text-[#EDBB00] font-bold text-lg" }, "Historial de Movimientos"),
                            React.createElement("button", { onClick: () => setIsHistoryModalOpen(false) }, React.createElement(X))
                        ),
                        React.createElement("div", { className: "space-y-3" },
                            historyItem.history?.map((h,i) => React.createElement("div", { key: i, className: "bg-[#121212] p-3 rounded-lg border border-gray-800 text-sm text-gray-300" },
                                React.createElement("div", { className: "flex justify-between mb-1 text-xs text-gray-500" },
                                    React.createElement("span", null, new Date(h.date).toLocaleString()),
                                    React.createElement("strong", { className: "uppercase text-[#004D98]" }, h.type)
                                ),
                                React.createElement("div", { className: "font-medium" }, h.type === 'consume' ? `-${h.qty} (${h.location})` : h.type === 'exhausted' ? '⚠️ STOCK AGOTADO' : h.type === 'move' ? h.detail : `+${h.addedSara||0}S +${h.addedNegocio||0}N`)
                            ))
                        )
                    )
                ),

                // Modal Reporte PDF
                isReportModalOpen && React.createElement("div", { className: "fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 animate-in fade-in" },
                    React.createElement("div", { className: "bg-[#1e1e1e] w-full max-w-sm rounded-2xl shadow-2xl p-6 border border-gray-700" },
                        React.createElement("h3", { className: "text-lg font-bold text-[#EDBB00] mb-6 flex items-center gap-2" }, React.createElement(FileText, { size: 20 }), " Generar Reporte PDF"),
                        React.createElement("div", { className: "space-y-4" },
                            React.createElement("div", null, React.createElement("label", { className: "text-xs text-gray-400 uppercase font-bold block mb-1" }, "Desde"), React.createElement("input", { type: "date", value: reportStartDate, onChange: e=>setReportStartDate(e.target.value), className: "w-full p-3 bg-[#121212] border border-gray-700 rounded-xl text-white" })),
                            React.createElement("div", null, React.createElement("label", { className: "text-xs text-gray-400 uppercase font-bold block mb-1" }, "Hasta"), React.createElement("input", { type: "date", value: reportEndDate, onChange: e=>setReportEndDate(e.target.value), className: "w-full p-3 bg-[#121212] border border-gray-700 rounded-xl text-white" })),
                            React.createElement("div", { className: "flex gap-3 mt-6" },
                                React.createElement("button", { onClick: () => setIsReportModalOpen(false), className: "flex-1 py-3 bg-gray-800 rounded-xl font-bold text-gray-400" }, "Cancelar"),
                                React.createElement("button", { onClick: generatePDFReport, className: "flex-1 py-3 bg-[#004D98] rounded-xl font-bold text-white flex justify-center gap-2 items-center" }, React.createElement(Printer, { size: 18 }), " Imprimir")
                            )
                        )
                    )
                )
            );
        }

        const root = createRoot(document.getElementById('root'));
        root.render(React.createElement(App));
    </script>
</body>
</html>
