/* ========================    管理者用：お知らせ枠書き換えエリア
========================================= */
const UPDATE_CONFIG = {
    notice: "長期間に及ぶ不具合により、ご不便ご迷惑おかけいたしましたこと、深くお詫び申し上げます。4/15 19:13より復旧いたしました。",
    tag: "お知らせ" 
};
/* ========================================= */

const STORAGE_KEY = 'portal_v7_2_data';
const themes = ["#2196F3", "#00BFA5", "#E91E63", "#673AB7", "#37474F"];
const fontColors = ["#FFFFFF", "#FFEB3B", "#000000", "#A7FFEB", "#F8BBD0"];
const fontStyles = [
    { name: 'Standard', family: 'sans-serif' },
    { name: 'Digital', family: 'DotGothic16' },
    { name: 'Modern', family: 'Oswald' },
    { name: 'Mono', family: 'Roboto Mono' },
    { name: 'Classic', family: 'Courier Prime' }
];

let userConfig = { memo: "", bookmarks: [{ title: "Google", url: "https://www.google.com" }], theme: themes[0], fontColor: fontColors[0], fontFamily: fontStyles[0].family };

function loadData() {
    const saved = localStorage.getItem(STORAGE_KEY);
    if(saved) userConfig = {...userConfig, ...JSON.parse(saved)};
    document.getElementById('memo-area').value = userConfig.memo || "";
    
    // 管理者設定の反映
    document.getElementById('notice-text').innerText = UPDATE_CONFIG.notice;
    document.querySelector('.notice-tag').innerText = UPDATE_CONFIG.tag;

    applyStyles();
    renderBookmarks();
    initPickers();
}

function applyStyles() {
    document.documentElement.style.setProperty('--p', userConfig.theme);
    document.documentElement.style.setProperty('--clock-c', userConfig.fontColor);
    document.documentElement.style.setProperty('--clock-f', userConfig.fontFamily);
}

function initPickers() {
    document.getElementById('theme-colors').innerHTML = themes.map(c => `<div class="color-dot" style="background:${c}" onclick="setTheme('${c}')"></div>`).join('');
    document.getElementById('font-colors').innerHTML = fontColors.map(c => `<div class="color-dot" style="background:${c}" onclick="setFontColor('${c}')"></div>`).join('');
    document.getElementById('font-styles').innerHTML = fontStyles.map(f => `<button class="font-btn" style="font-family:${f.family}" onclick="setFontFamily('${f.family}')">${f.name}</button>`).join('');
}

function setTheme(c) { userConfig.theme = c; applyStyles(); save(); }
function setFontColor(c) { userConfig.fontColor = c; applyStyles(); save(); }
function setFontFamily(f) { userConfig.fontFamily = f; applyStyles(); save(); }
function toggleModal() { const m = document.getElementById('modal-overlay'); m.style.display = (m.style.display === 'block') ? 'none' : 'block'; }
function save() { localStorage.setItem(STORAGE_KEY, JSON.stringify(userConfig)); }

function updateClock() {
    const now = new Date();
    document.getElementById('clock').innerText = now.getHours().toString().padStart(2,'0') + ":" + now.getMinutes().toString().padStart(2,'0');
    document.getElementById('greeting').innerText = "ブラウトップへようこそ。";
}

function renderBookmarks() {
    const grid = document.getElementById('bookmark-grid');
    grid.innerHTML = userConfig.bookmarks.map(b => `<a href="${b.url}" class="bookmark-item" target="_blank"><div class="icon-placeholder">${b.title[0]}</div><span>${b.title}</span></a>`).join('');
}

function addBookmark() {
    const t = prompt("タイトル:"); const u = prompt("URL:", "https://");
    if(t && u) { userConfig.bookmarks.push({title:t, url:u}); save(); renderBookmarks(); }
}

async function fetchNews() {
    const list = document.getElementById('news-list');
    try {
        const res = await fetch(`https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent("https://news.google.com/rss?hl=ja&gl=JP&ceid=JP:ja")}`);
        const data = await res.json();
        list.innerHTML = data.items.slice(0, 10).map(item => `<li><a href="${item.link}" target="_blank">${item.title.split(' - ')[0]}</a></li>`).join('');
    } catch (e) { list.innerHTML = "<li>問題が発生しました。</li>"; }
}

document.getElementById('memo-area').addEventListener('input', () => { userConfig.memo = document.getElementById('memo-area').value; save(); });
window.onload = () => { loadData(); updateClock(); setInterval(updateClock, 1000); fetchNews(); };
