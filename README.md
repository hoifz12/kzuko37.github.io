<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Win95 Blog</title>

<style>
/* 🎨 기본 스타일 */
*{margin:0;padding:0;box-sizing:border-box}
body{
    font-family:'AbhayaLibre-Medium',AbhayaLibre-Medium;
    /* JS에서 배경을 설정하므로, 기본 CSS는 최소화 */
    background-size: cover;
    color:#fff;
    min-height:1500px;
    position: relative;
}
a{text-decoration:none;}

/* --- Windows95 창 버튼 스타일 --- */
.window-buttons { display:flex; gap: 2px; }
.window-button {
    width:20px; height:20px; text-align:center; line-height:16px;
    border:2px solid #fff; border-right-color:#808080; border-bottom-color:#808080;
    background:#c0c0c0; font-weight:bold; color:#000; cursor:pointer; user-select:none;
}
.window-button:hover { background:#dcdcdc; }

.win-btn {
    display:inline-block; background:#c0c0c0; padding:2px 6px;
    border-top:2px solid #fff; border-left:2px solid #fff;
    border-right:2px solid #808080; border-bottom:2px solid #808080;
    color:#000; font-size:0.8rem; margin:1px; cursor:pointer; text-decoration:none;
}
.win-btn:hover { background:#dcdcdc; color:#000; }

.top-menu a { color:#0000ff; text-decoration:underline; font-size:0.8rem; padding:2px 6px; display:inline-block;}
.top-menu a:hover { color:#ff0000; }

.window {
    background:#c0c0c0; border-top:2px solid #fff; border-left:2px solid #fff;
    border-right:2px solid #808080; border-bottom:2px solid #808080;
    position:absolute; z-index:1;
}
.window-titlebar {
    display:flex; justify-content:space-between; align-items:center;
    background:linear-gradient(to right,#000080,#1084d0);
    color:#fff; padding:2px 6px; font-weight:bold; font-size:0.9rem;
    cursor:move; user-select:none;
}
/* About 창 제목과 내용이 붙도록 조정 */
.window-titlebar #about-title {
    margin-left: 5px; 
}
.window-content { padding:10px; }

.inset-panel {
    background:#fff; border-top:2px solid #808080; border-left:2px solid #808080;
    border-right:2px solid #fff; border-bottom:2px solid #fff; padding:10px; color:#000;
    text-align:center;
}

/* --- 창 위치 수정 (요청 반영) --- */
/* 왼쪽 열 - 간격 일정하게 조정 */
#win-profile { top:160px; left:calc(50% - 390px); width:250px; }
/* ⬇️ Categories 창을 Profile 창 아래로 이동 (400px) */
#win-categories { top:400px; left:calc(50% - 390px); width:250px; } 
/* ⬇️ Search 창을 Categories 창 아래로 이동 (650px) */
#win-search { top:650px; left:calc(50% - 390px); width:250px; } 

/* 오른쪽 열 */
#win-about { top:160px; left:calc(50% - 110px); width:500px; } 
/* ⚙️ 설정 창 위치 (About 창 오른쪽 옆) */
#win-settings { top:160px; left:calc(50% + 140px); width:350px; display: none; }

/* 오른쪽 열 - Blog / Album */
#win-blog { top:160px; left:calc(50% - 110px); width:500px; display: none; }
#win-album { top:160px; left:calc(50% - 110px); width:500px; display: none; }

/* 🌟 새 글 작성/보기 창 위치 (기본 숨김) */
#win-new-post { top: 150px; left: calc(50% + 50px); width: 450px; display: none; }
#win-view-post { top: 100px; left: calc(50% + 50px); width: 450px; height: 500px; display: none; }
#win-new-album-post { top: 150px; left: calc(50% + 50px); width: 450px; display: none; }
#win-view-album-post { top: 100px; left: calc(50% + 50px); width: 450px; height: 500px; display: none; }

/* [푸터] */
footer {
    position: absolute;
    top:1200px; 
    width: 100%;
    text-align: center;
    padding-bottom: 50px;
}

/* 나머지 스타일 */
.top-menu{display:flex; justify-content:center; gap:5px; flex-wrap:wrap; margin:40px 0 20px 0;}
.site-header{text-align:center; color:#fff; margin-top:40px; margin-bottom:20px;}
.site-header h1{font-size:2rem; font-weight:bold; text-shadow:2px 2px 0 #000;}
.box-profile p.tit-g { font-weight:bold; margin-bottom:5px; color:#000; }
.box-profile p.text-profile { font-size:0.85rem; color:#333; margin-bottom:10px; }
.category-list ul { list-style:none; padding-left:0; text-align:left; } 
.category-list li { margin-bottom:5px; }
.category-list li a { text-decoration:none; color:#0000ff; font-size:0.85rem; }
.category-list li a:hover { color:#ff0000; }
.search-box input[type="text"] { width:70%; padding:5px; border:2px solid #808080; }
.search-box button { padding:2px 6px; border-top:2px solid #fff; border-left:2px solid #fff; border-right:2px solid #808080; border-bottom:2px solid #808080; background:#c0c0c0; cursor:pointer; }
.search-box button:hover{background:#dcdcdc;}

/* 블로그 목록 스타일 */
.post-list { text-align: left; margin-top: 10px; }
.post-list ul { list-style: none; padding-left: 0; margin-top: 10px; }
.post-list li { padding: 5px 0; border-bottom: 1px dashed #c0c0c0; display: flex; justify-content: space-between; align-items: center; }
.post-list li:last-child { border-bottom: none; }
.post-list a { color: #000080; text-decoration: none; font-weight: bold; }
.post-list a:hover { color: #ff0000; }
.post-info { display: flex; align-items: center; }
.post-category { font-size: 0.75rem; color: #800080; margin-right: 8px; border: 1px solid #dcdcdc; padding: 1px 3px; }
.post-date { font-size: 0.75rem; color: #808080; margin-left: 10px; }
.post-private { color: #ff0000; font-weight: bold; margin-left: 5px; font-size: 0.9rem; }
.new-post-btn-area { margin-bottom: 10px; text-align: right; }

/* 새 글 작성 창 스타일 */
.new-post-form input[type="text"], .new-post-form select { width: 100%; padding: 5px; margin-bottom: 10px; border: 2px solid #808080; }
.editor-toolbar { background: #dcdcdc; border: 2px solid #fff; border-right-color: #808080; border-bottom-color: #808080; padding: 3px; margin-bottom: 5px; display: flex; flex-wrap: wrap; gap: 3px;}
.editor-toolbar button, .editor-toolbar select { 
    background:#c0c0c0; border-top:2px solid #fff; border-left:2px solid #fff; 
    border-right:2px solid #808080; border-bottom:2px solid #808080; 
    padding: 1px 4px; cursor: pointer; font-size: 0.8rem; height: 25px;
}
.editor-toolbar button:hover { background:#dcdcdc; }

.new-post-form #post-content { 
    width: 100%; height: 250px; padding: 5px; margin-bottom: 10px; resize: vertical; 
    border: 2px solid #808080; background: #fff; color: #000;
    text-align: left;
    overflow-y: auto;
}
.new-post-form #post-content ul, .new-post-form #post-content ol {
    list-style-position: inside;
    margin-left: 15px;
}

.new-post-form .form-buttons { text-align: right; }

/* 글 보기 창 스타일 */
.view-post-area { text-align: left; }
.view-post-area h2 { 
    font-size: 1.5rem; 
    margin-bottom: 10px; 
    padding-bottom: 5px;
    border-bottom: 2px solid #c0c0c0;
    color: #000080;
}
.view-post-area .post-metadata { font-size: 0.8rem; color: #808080; margin-bottom: 10px; }
.view-post-area .post-body { 
    min-height: 200px; 
    font-size: 0.9rem;
    overflow-y: auto;
    padding: 5px 0;
    text-align: left;
}
.view-buttons { 
    text-align: right; 
    margin-top: 10px;
}

/* 할 일 목록 스타일 */
#post-content ul[data-role="tasklist"] {
    list-style: none;
    padding-left: 0;
}
#post-content ul[data-role="tasklist"] li {
    margin: 5px 0;
    text-indent: -1.4em;
    padding-left: 1.4em;
}
#post-content ul[data-role="tasklist"] li::before {
    content: "☐";
    margin-right: 5px;
    cursor: pointer;
}
#post-content ul[data-role="tasklist"] li[aria-checked="true"]::before {
    content: "☑";
}

/* 설정 창 스타일 */
.setting-section { 
    margin-bottom: 15px; 
    padding-bottom: 10px; 
    border-bottom: 1px dashed #c0c0c0;
    text-align: left;
}
.setting-section:last-child { border-bottom: none; }
.setting-section h3 { font-size: 1.1rem; color: #000080; margin-bottom: 8px; }
.setting-section input[type="text"], .setting-section textarea, .setting-section input[type="file"], .setting-section input[type="password"] {
    width: 100%; padding: 5px; margin-bottom: 8px; border: 2px solid #808080;
}
.setting-section button { margin-top: 5px; }

/* 카테고리 관리 스타일 */
#category-editor { margin-top: 10px; }
#category-list-container { max-height: 150px; overflow-y: auto; background: #f0f0f0; padding: 5px; border: 1px solid #c0c0c0; }
#category-list-container li { 
    display: flex; justify-content: space-between; align-items: center; 
    padding: 2px 0; border-bottom: 1px dotted #c0c0c0;
}
#category-list-container li:last-child { border-bottom: none; }
.cat-item-main { font-weight: bold; color: #000; }
.cat-item-sub { font-size: 0.85rem; color: #555; margin-left: 10px; }
.cat-btn-group button { margin-left: 3px; padding: 0 4px; font-size: 0.75rem; }

/* 앨범 목록 스타일 */
.album-list {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: flex-start;
    text-align: left;
}
.album-item {
    width: 100px;
    cursor: pointer;
    text-align: center;
    border: 1px solid #c0c0c0;
    padding: 5px;
    background: #f0f0f0;
}
.album-cover {
    width: 100%;
    height: 70px;
    background: #808080;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    margin-bottom: 5px;
}
.album-cover img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}
.album-title {
    font-size: 0.85rem;
    font-weight: bold;
    color: #000080;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}
.album-privacy {
    color: #ff0000;
    margin-left: 3px;
    font-size: 0.9rem;
}
.album-new-btn-area { margin-bottom: 10px; text-align: right; }

/* 앨범 보기/새 앨범 포스트 스타일 */
.album-post-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
    max-height: 300px;
    overflow-y: auto;
    background: #f0f0f0;
    padding: 5px;
    border: 1px solid #c0c0c0;
}
.album-media-item {
    width: 80px;
    height: 80px;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid #808080;
}
.album-media-item img, .album-media-item video {
    width: 100%;
    height: 100%;
    object-fit: cover;
}
.album-media-item span {
    color: #000;
    font-size: 0.7rem;
    text-align: center;
}
.album-new-post-form input[type="file"] { border: none; }
</style>
</head>

<body onload="initApp()">

<header class="site-header"><h1 id="site-title">Win95 Blog</h1></header>

<div class="top-menu">
    <a href="javascript:void(0)" onclick="showMainContent('about')" class="win-btn">Home</a>
    <a href="javascript:void(0)" onclick="showMainContent('blog')" class="win-btn">Blog</a>
    <a href="javascript:void(0)" onclick="showMainContent('album')" class="win-btn">Album</a>
    <a href="javascript:void(0)" onclick="openSettingsPrompt()" class="win-btn">Settings</a>
</div>

<div class="window" id="win-profile">
    <div class="window-titlebar">
        👤 Profile
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-profile')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel"> 
            <div class="box-profile">
                <img id="profile-image" src="https://via.placeholder.com/100" style="width:100px;height:100px;border:2px solid #808080;margin-bottom:10px;">
                <p class="tit-g" id="profile-title">Emergence</p>
                <p class="text-profile" id="profile-desc">kzuko37의 개인 블로그입니다.</p>
                <div id="profile-links" style="text-align: left;">
                </div>
            </div>
        </div>
    </div>
</div>

<div class="window" id="win-categories">
    <div class="window-titlebar">
        📂 Categories
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-categories')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel category-list">
            <ul id="category-list-target">
                <li><a href="javascript:void(0)" onclick="filterPosts('All')">전체 글 보기 (All)</a></li>
            </ul>
        </div>
    </div>
</div>

<div class="window" id="win-search">
    <div class="window-titlebar">
        🔍 Search
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-search')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel">
            <form class="search-box" action="http://kzuko37.tistory.com/search/" method="get">
                <input type="text" name="q" placeholder="검색어를 입력하지 마시오">
                <button type="submit">검색</button>
            </form>
        </div>
    </div>
</div>

<div class="window" id="win-about">
    <div class="window-titlebar">
        <span>ℹ️ About <span id="about-title">Win95 Blog</span></span> 
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-about')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel" id="about-content">
            <p>블로그 설정에서 내용을 입력해주세요.</p>
        </div>
    </div>
</div>

<div class="window" id="win-blog">
    <div class="window-titlebar">
        📄 Blog Posts
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-blog')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel" id="blog-content">
        </div>
    </div>
</div>

<div class="window" id="win-album">
    <div class="window-titlebar">
        🖼️ Photo Album
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-album')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel" id="album-content">
        </div>
    </div>
</div>

<div class="window" id="win-new-post">
    <div class="window-titlebar">
        ✏️ Post Editor
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-new-post')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel">
            <form class="new-post-form" onsubmit="savePost(event)">
                <input type="hidden" id="post-index">
                <div style="display: flex; gap: 10px; margin-bottom: 10px; text-align: left;">
                    <select id="post-main-category" required style="width: 100px;"></select>
                    <select id="post-sub-category" required style="flex-grow: 1;"></select>
                    <select id="post-is-private" required style="width: 120px;">
                        <option value="false">공개 (Public)</option>
                        <option value="true">비공개 (Private)</option>
                    </select>
                </div>

                <div style="margin-bottom: 10px; text-align: left; display: flex; align-items: center; gap: 5px;">
                    <label for="post-date-input" style="font-size: 0.85rem; color: #000;">Date:</label>
                    <input type="text" id="post-date-input" placeholder="YYYY.MM.DD (선택 사항)" title="날짜 형식: YYYY.MM.DD" style="width: 120px; flex-grow: 0; margin-bottom: 0;">
                    <span style="font-size: 0.75rem; color: #808080;">(YYYY.MM.DD)</span>
                </div>
                
                <input type="text" id="post-title" placeholder="제목을 입력하세요" required>
                
                <div class="editor-toolbar">
                    <button type="button" onclick="execCmd('bold')">B</button>
                    <button type="button" onclick="execCmd('italic')">I</button>
                    <button type="button" onclick="execCmd('underline')">U</button>
                    <button type="button" onclick="execCmd('strikeThrough')">S</button>
                    
                    <select onchange="execCmd('foreColor', this.value); this.value=''" title="글씨 색">
                        <option value="" selected hidden>색</option>
                        <option value="red">빨강</option>
                        <option value="blue">파랑</option>
                        <option value="yellow">노랑</option>
                        <option value="white">흰색</option>
                        <option value="gray">회색</option>
                        <option value="black">검정</option>
                    </select>
                    <select onchange="execCmd('backColor', this.value); this.value=''" title="글자 배경색">
                        <option value="" selected hidden>배경</option>
                        <option value="red">빨강</option>
                        <option value="blue">파랑</option>
                        <option value="yellow">노랑</option>
                        <option value="gray">회색</option>
                        <option value="black">검정</option>
                    </select>
                    <select onchange="execCmd('fontSize', this.value); this.value=''" title="글씨 크기">
                        <option value="" selected hidden>크기</option>
                        <option value="1">매우 작게</option>
                        <option value="2">작게</option>
                        <option value="3">보통</option>
                        <option value="5">크게</option>
                        <option value="7">매우 크게</option>
                    </select>
                    
                    <button type="button" onclick="execCmd('insertUnorderedList')">• 목록</button>
                    <button type="button" onclick="execCmd('insertOrderedList')">1. 목록</button>
                    <button type="button" onclick="insertTaskList()">☑ 할일</button>
                    <button type="button" onclick="execCmd('insertHorizontalRule')">구분선</button>
                </div>
                
                <div id="post-content" contenteditable="true" required></div>

                <div class="form-buttons">
                    <button type="submit" class="win-btn">Save</button>
                    <button type="button" class="win-btn" onclick="closeWindow('win-new-post')">Cancel</button>
                </div>
            </form>
        </div>
    </div>
</div>

<div class="window" id="win-view-post">
    <div class="window-titlebar" id="view-post-titlebar">
        📰 Post Viewer
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-view-post')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel view-post-area">
            <div class="post-metadata">
                <span id="view-category" class="post-category">카테고리</span>
                <span id="view-date">2025.01.01</span>
                <span id="view-privacy" style="font-weight: bold; margin-left: 10px;"></span>
            </div>
            
            <h2 id="view-title">Post Title</h2>
            
            <div class="post-body" id="view-content"></div>

            <div class="view-buttons">
                <button type="button" class="win-btn" id="edit-button">수정</button>
                <button type="button" class="win-btn" id="delete-button" style="background:#ff9999;">삭제</button>
            </div>
        </div>
    </div>
</div>

<div class="window" id="win-new-album-post">
    <div class="window-titlebar">
        📸 Album Post Editor
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-new-album-post')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel">
            <form class="album-new-post-form" onsubmit="saveAlbumPost(event)">
                <input type="hidden" id="album-post-index">
                <div style="display: flex; gap: 10px; margin-bottom: 10px; text-align: left;">
                    <select id="album-post-is-private" required style="width: 120px;">
                        <option value="false">공개 (Public)</option>
                        <option value="true">비공개 (Private)</option>
                    </select>
                </div>
                
                <div style="text-align: left; margin-bottom: 10px; display: flex; align-items: center; gap: 5px;">
                    <label for="album-post-date-input" style="font-size: 0.85rem; color: #000;">Date:</label>
                    <input type="text" id="album-post-date-input" placeholder="YYYY.MM.DD (선택 사항)" style="width: 120px; flex-grow: 0; margin-bottom: 0;">
                    <span style="font-size: 0.75rem; color: #808080;">(YYYY.MM.DD)</span>
                </div>
                
                <input type="text" id="album-post-title" placeholder="앨범 제목을 입력하세요" required>
                
                <div style="text-align: left; margin-bottom: 10px;">
                    <label for="album-post-cover-file" style="font-size: 0.85rem; color: #000; display: block; margin-bottom: 5px;">대표 표지 이미지 (선택):</label>
                    <input type="text" id="album-post-cover-url-text" placeholder="URL" style="width: 100%;">
                    <input type="file" id="album-post-cover-file" accept="image/*" onchange="previewImage(this, 'album-cover-preview'); handleFileToUrl(this, 'album-post-cover-url-text')" style="width: 100%;">
                    <div id="album-cover-preview" style="width: 100px; height: 70px; margin-top: 5px; background: #c0c0c0; border: 1px solid #808080; display: flex; align-items: center; justify-content: center;">
                        <span style="color: #000; font-size: 0.8rem;">Preview</span>
                    </div>
                    <input type="hidden" id="album-post-cover-url">
                </div>

                <div style="text-align: left; margin-bottom: 10px;">
                    <label for="album-post-media-files" style="font-size: 0.85rem; color: #000; display: block; margin-bottom: 5px;">사진/영상 추가 (URL or File):</label>
                    <input type="file" id="album-post-media-files" accept="image/*,video/*" multiple onchange="handleMediaFiles(this)">
                    <div class="album-post-grid" id="album-media-preview-grid">
                    </div>
                    <input type="hidden" id="album-post-media-urls">
                </div>
                
                <div class="form-buttons">
                    <button type="submit" class="win-btn">Save Album</button>
                    <button type="button" class="win-btn" onclick="closeWindow('win-new-album-post')">Cancel</button>
                </div>
            </form>
        </div>
    </div>
</div>

<div class="window" id="win-view-album-post">
    <div class="window-titlebar" id="view-album-post-titlebar">
        🖼️ Album Viewer
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-view-album-post')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel view-post-area">
            <div class="post-metadata">
                <span id="view-album-date">2025.01.01</span>
                <span id="view-album-privacy" style="font-weight: bold; margin-left: 10px;"></span>
            </div>
            
            <h2 id="view-album-title">Album Title</h2>
            
            <div class="post-body" id="view-album-content" style="min-height: 300px;">
            </div> 

            <div class="view-buttons">
                <button type="button" class="win-btn" id="edit-album-button">수정</button>
                <button type="button" class="win-btn" id="delete-album-button" style="background:#ff9999;">삭제</button>
            </div>
        </div>
    </div>
</div>

<div class="window" id="win-settings">
    <div class="window-titlebar">
        ⚙️ Settings
        <div class="window-buttons">
            <span class="window-button">-</span>
            <span class="window-button">□</span>
            <span class="window-button" onclick="closeWindow('win-settings')">×</span>
        </div>
    </div>
    <div class="window-content">
        <div class="inset-panel" style="text-align: left;">
            <form onsubmit="saveSettings(event)">
            
                <div class="setting-section">
                    <h3>🔒 관리자 비밀번호</h3>
                    <label for="setting-admin-password">새 비밀번호 입력:</label>
                    <input type="password" id="setting-admin-password" placeholder="변경할 비밀번호">
                    <span style="font-size: 0.75rem; color: #808080; display: block; margin-top: -5px;">*변경하려면 새 비밀번호를 입력하고 저장하세요. 비워두면 변경되지 않습니다.</span>
                </div>

                <div class="setting-section">
                    <h3>🖼️ 사이트 배경화면</h3>
                    <label for="setting-background-image">배경 이미지 URL (또는 파일 선택):</label>
                    <input type="text" id="setting-background-image-url" placeholder="URL">
                    <input type="file" id="setting-background-image-file" accept="image/*" onchange="handleFileToUrl(this, 'setting-background-image-url')"> 
                    <span style="font-size: 0.75rem; color: #808080; display: block; margin-top: -5px;">*URL 또는 파일을 선택하고 저장을 누르세요.</span>
                </div>

                <div class="setting-section">
                    <h3>👤 프로필 / 블로그 정보</h3>
                    <label for="setting-profile-image">프사 이미지 URL (또는 파일 선택):</label>
                    <input type="text" id="setting-profile-image-url" placeholder="URL">
                    <input type="file" id="setting-profile-image-file" accept="image/*" onchange="handleFileToUrl(this, 'setting-profile-image-url')">
                    
                    <label for="setting-title">블로그 이름:</label>
                    <input type="text" id="setting-title" required>

                    <label for="setting-desc">블로그 설명:</label>
                    <input type="text" id="setting-desc" required>

                    <label for="setting-home-content">About (블로그 정보) 내용:</label>
                    <textarea id="setting-home-content" rows="4" required></textarea>
                </div>

                <div class="setting-section">
                    <h3>🔗 링크 관리 (프로필)</h3>
                    <div id="link-list">
                    </div>
                    <input type="text" id="new-link-title" placeholder="링크 제목">
                    <input type="text" id="new-link-url" placeholder="URL">
                    <button type="button" class="win-btn" onclick="addLink()">링크 추가</button>
                </div>

                <div class="setting-section">
                    <h3>📂 카테고리 관리</h3>
                    <div id="category-editor">
                        <input type="text" id="new-main-category" placeholder="주 카테고리명">
                        <input type="text" id="new-sub-category" placeholder="하위 카테고리명 (선택)">
                        <button type="button" class="win-btn" onclick="addCategory()">카테고리 추가</button>
                        <div id="category-list-container">
                        </div>
                    </div>
                </div>
                
                <div class="setting-section">
                    <h3>📤 데이터 관리 (이동/백업)</h3>
                    <p style="font-size: 0.85rem; color: #555; margin-bottom: 8px;">*설정 및 모든 글/앨범 데이터를 파일로 내보내거나 가져옵니다.</p>
                    <button type="button" class="win-btn" onclick="exportData()">데이터 내보내기 (.json)</button>
                    
                    <label for="data-import-file" style="font-size: 0.85rem; color: #000; display: block; margin-top: 10px; margin-bottom: 5px;">데이터 가져오기 (.json 파일 선택):</label>
                    <input type="file" id="data-import-file" accept=".json">
                    <button type="button" class="win-btn" onclick="importData()">데이터 가져오기 및 적용</button>
                </div>
                <div class="form-buttons" style="text-align: right;">
                    <button type="submit" class="win-btn">설정 저장</button>
                    <button type="button" class="win-btn" onclick="closeWindow('win-settings')">취소</button>
                </div>
            </form>
        </div>
    </div>
</div>

<footer>
    <img src="https://pixelrino.neocities.org/hypnogifarchive/skeleton-wave.gif">
</footer>

<script>
const POSTS_STORAGE_KEY = 'win95BlogPosts';
const ALBUMS_STORAGE_KEY = 'win95BlogAlbums';
const SETTINGS_STORAGE_KEY = 'win95BlogSettings';

// ⚙️ 기본 설정
const DEFAULT_SETTINGS = {
    title: "Win95 Blog",
    desc: "Windows 95 스타일의 개인 블로그입니다.",
    profileImage: "https://via.placeholder.com/100",
    homeContent: "Windows 95 스타일의 개인 블로그입니다.",
    adminPassword: "heilner", // 초기 비밀번호 설정
    // 요청: 기본 배경 이미지 URL
    siteBackground: "https://img.notionusercontent.com/s3/prod-files-secure%2Fa475c2df-d7a8-435e-b12e-6c634aad507a%2F735b72db-c8ef-4d5f-b544-7d7978573e56%2FIMG_7262.jpeg/size/w=1800?exp=1764675874&sig=lx9dc2-a4wboFiY4lNXLEYpS8N7bBONSSoPfV4&wasReauthorized=true",
    links: [
        { title: "Github", url: "https://github.com/example" }
    ],
    categories: [
        { main: "미분류", sub: null },
        { main: "그리움", sub: null },
        { main: "대화", sub: null },
    ]
};

// 💾 설정 로드
function loadSettings() {
    const storedSettings = localStorage.getItem(SETTINGS_STORAGE_KEY);
    let settings = storedSettings ? JSON.parse(storedSettings) : DEFAULT_SETTINGS;
    // 이전 버전 호환성: adminPassword나 siteBackground가 없으면 기본값으로 설정
    if (!settings.adminPassword) {
        settings.adminPassword = DEFAULT_SETTINGS.adminPassword;
    }
    if (!settings.siteBackground) {
        settings.siteBackground = DEFAULT_SETTINGS.siteBackground;
    }
    return settings;
}

// ⚙️ 설정 저장
function saveSettingsToStorage(settings) {
    localStorage.setItem(SETTINGS_STORAGE_KEY, JSON.stringify(settings));
}

// 📂 현재 필터 상태
let currentFilter = { main: 'All', sub: null };

// 🖼️ 창 관리
let highestZ = 1;

function showWindow(id) {
    const win = document.getElementById(id);
    // 모든 창의 z-index를 비교하여 가장 높은 값 + 1로 설정
    highestZ++;
    win.style.zIndex = highestZ;
    win.style.display = 'block';
}

function closeWindow(id) {
    document.getElementById(id).style.display = 'none';
}

function showMainContent(type) {
    // About, Blog, Album 창만 전환
    const mainWindows = ['win-about', 'win-blog', 'win-album'];
    mainWindows.forEach(id => {
        closeWindow(id);
    });
    
    // Settings 창이 열려있다면 닫기
    closeWindow('win-settings');

    if (type === 'blog') {
        showWindow('win-blog');
        currentFilter = { main: 'All', sub: null }; // Blog 탭 클릭 시 필터 초기화
        showPosts();
    } else if (type === 'album') {
        showWindow('win-album');
        showAlbums();
    } else { // about
        showWindow('win-about');
    }
}

// 헬퍼 함수: 파일(File) 객체를 Data URL 문자열로 변환
function fileToDataUrl(file) {
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => resolve(reader.result);
        reader.onerror = error => reject(error);
        reader.readAsDataURL(file);
    });
}

// 헬퍼 함수: 파일 선택 시 URL 입력 필드에 Data URL을 채우는 함수
async function handleFileToUrl(fileInput, urlInputId) {
    const urlInput = document.getElementById(urlInputId);
    if (fileInput.files.length > 0) {
        try {
            urlInput.value = await fileToDataUrl(fileInput.files[0]);
             // 배경화면의 경우, 파일 선택 즉시 미리보기를 위해 body 스타일을 업데이트
            if (urlInputId === 'setting-background-image-url') {
                document.body.style.background = `url('${urlInput.value}') no-repeat center center fixed`;
                document.body.style.backgroundSize = 'cover';
            }
        } catch (error) {
            alert("파일 로드 오류!");
            console.error(error);
        }
    }
}

// 헬퍼 함수: 오늘 날짜 YYYY.MM.DD 형식 반환
function getTodayDate() {
    const now = new Date();
    const year = now.getFullYear();
    const month = String(now.getMonth() + 1).padStart(2, '0');
    const day = String(now.getDate()).padStart(2, '0');
    return `${year}.${month}.${day}`;
}

// ----------------------------------------------------
// START: 데이터 내보내기/가져오기 함수
// ----------------------------------------------------

// 📤 데이터 내보내기
function exportData() {
    const data = {
        settings: loadSettings(),
        posts: loadPosts(),
        albums: loadAlbums()
    };
    
    const dataStr = JSON.stringify(data, null, 2);
    const blob = new Blob([dataStr], { type: "application/json" });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `win95_blog_backup_${getTodayDate()}.json`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);

    alert("블로그 데이터가 성공적으로 내보내졌습니다!");
}

// 📥 데이터 가져오기
function importData() {
    const fileInput = document.getElementById('data-import-file');
    if (fileInput.files.length === 0) {
        alert("가져올 .json 파일을 선택해주세요.");
        return;
    }

    if (!confirm("현재 브라우저의 모든 블로그 데이터(설정, 글, 앨범)가 덮어쓰여집니다. 계속하시겠습니까?")) {
        return;
    }

    const file = fileInput.files[0];
    const reader = new FileReader();

    reader.onload = async (e) => {
        try {
            const importedData = JSON.parse(e.target.result);
            
            // 모든 데이터 덮어쓰기
            if (importedData.settings) {
                saveSettingsToStorage(importedData.settings);
            }
            if (importedData.posts) {
                savePostsToStorage(importedData.posts);
            }
            if (importedData.albums) {
                saveAlbumsToStorage(importedData.albums);
            }
            
            alert("데이터 가져오기 및 적용 완료! 새로고침합니다.");
            location.reload(); // 변경사항 적용을 위해 새로고침
        } catch (error) {
            alert("파일 분석 오류: 올바른 JSON 파일이 아닙니다.");
            console.error("Import Error:", error);
        }
    };

    reader.readAsText(file);
}

// ----------------------------------------------------
// END: 데이터 내보내기/가져오기 함수
// ----------------------------------------------------

// 🌐 설정 기반 UI 업데이트
function updateUIFromSettings() {
    const settings = loadSettings();
    // 요청: 배경화면 업데이트 로직 추가
    if (settings.siteBackground) {
        document.body.style.background = `url('${settings.siteBackground}') no-repeat center center fixed`;
        document.body.style.backgroundSize = 'cover';
    }
    document.getElementById('site-title').textContent = settings.title;
    document.getElementById('about-title').textContent = settings.title;
    document.getElementById('about-content').innerHTML = `<p>${settings.homeContent}</p>`;
    document.getElementById('profile-title').textContent = settings.title;
    document.getElementById('profile-desc').textContent = settings.desc;
    document.getElementById('profile-image').src = settings.profileImage || "https://via.placeholder.com/100";

    const linkContainer = document.getElementById('profile-links');
    // 요청: 'Links:' 제목 제거 반영
    linkContainer.innerHTML = '<ul style="list-style: none; padding-left: 0;">' + settings.links.map(link => 
        `<li><a href="${link.url}" target="_blank" style="font-size: 0.85rem;">🔗 ${link.title}</a></li>`
    ).join('') + '</ul>';

    // 카테고리 메뉴 업데이트
    updateCategoryMenu();
}

// 🖼️ 창 드래그 가능하게 설정
document.querySelectorAll('.window').forEach(win => {
    const titlebar = win.querySelector('.window-titlebar');
    const minBtn = win.querySelector('.window-button:nth-child(1)');
    const maxBtn = win.querySelector('.window-button:nth-child(2)');
    let isMax = false;
    let prev = {};
    let isMin = false;
    
    if (titlebar) titlebar.addEventListener('mousedown', (e) => {
        if (e.target.classList.contains('window-button')) return; // 버튼 클릭 무시
        if (isMax) return; // 최대화 상태에서는 이동 불가

        highestZ++;
        win.style.zIndex = highestZ;

        const rect = win.getBoundingClientRect();
        const offsetX = e.clientX - rect.left;
        const offsetY = e.clientY - rect.top;

        function moveHandler(ev) {
            win.style.left = (ev.clientX - offsetX) + 'px';
            win.style.top = (ev.clientY - offsetY) + 'px';
        }

        function upHandler() {
            document.removeEventListener('mousemove', moveHandler);
            document.removeEventListener('mouseup', upHandler);
        }

        document.addEventListener('mousemove', moveHandler);
        document.addEventListener('mouseup', upHandler);
    });

    if (minBtn) minBtn.addEventListener('click', () => {
        const content = win.querySelector('.window-content');
        if (content) {
            content.style.display = isMin ? '' : 'none';
            isMin = !isMin;
        }
    });

    if (maxBtn) maxBtn.addEventListener('click', () => {
        if (!isMax) {
            prev = {
                left: win.style.left,
                top: win.style.top,
                width: win.style.width,
                height: win.style.height
            };
            win.style.left = '0';
            win.style.top = '0';
            win.style.width = '100%';
            win.style.height = '100%';
            win.style.position = 'fixed';
            isMax = true;
        } else {
            win.style.left = prev.left;
            win.style.top = prev.top;
            win.style.width = prev.width;
            win.style.height = prev.height;
            win.style.position = 'absolute';
            isMax = false;
        }
        highestZ++;
        win.style.zIndex = highestZ;
    });
});

// 💾 블로그 포스트 관리
function loadPosts() {
    const storedPosts = localStorage.getItem(POSTS_STORAGE_KEY);
    let posts = storedPosts ? JSON.parse(storedPosts) : [
        { title: "환영합니다!", content: "이 글은 <span style=\"color:blue;\">공개</span> 상태입니다. 새로운 글을 작성해보세요.", date: getTodayDate(), mainCategory: "미분류", subCategory: null, isPrivate: false },
        { title: "비공개 테스트 글", content: "이 글은 비공개 상태입니다. 목록에서 클릭하면 비밀번호를 물어봅니다.", date: getTodayDate(), mainCategory: "개발", subCategory: "Web", isPrivate: true }
    ];
    // 요청: 날짜순(최신순)으로 정렬
    posts.sort((a, b) => {
        // 날짜가 없는 경우 ('null' 또는 빈 문자열)는 가장 오래된 것으로 간주
        const dateA = a.date || '0000.00.00';
        const dateB = b.date || '0000.00.00';
        return dateB.localeCompare(dateA); // 내림차순 (최신순) 정렬
    });
    return posts;
}

function savePostsToStorage(posts) {
    localStorage.setItem(POSTS_STORAGE_KEY, JSON.stringify(posts));
}

function showPosts() {
    const blogContent = document.getElementById('blog-content');
    const posts = loadPosts();
    const { main, sub } = currentFilter;
    let filteredPosts = posts;
    
    if (main !== 'All') {
        filteredPosts = posts.filter(post => 
            post.mainCategory === main && (sub === null || post.subCategory === sub)
        );
    }
    
    let html = `
        <div class="new-post-btn-area">
            <span class="win-btn" onclick="newPostPrompt()">New Post...</span>
        </div>
        <div class="post-list">
            <ul>
    `;

    filteredPosts.forEach((post, index) => {
        const categoryDisplay = post.subCategory ? `${post.mainCategory} > ${post.subCategory}` : post.mainCategory;
        const privacyIcon = post.isPrivate ? '🔒' : '';
        const titleLink = post.isPrivate ? 
            `<a href="javascript:void(0)" onclick="handlePostClick(${index}, true)">${post.title}</a>` : 
            `<a href="javascript:void(0)" onclick="viewPost(${index})">${post.title}</a>`;

        html += `
            <li>
                <div class="post-info">
                    <span class="post-category">${categoryDisplay}</span>
                    ${titleLink}
                    <span class="post-private">${privacyIcon}</span>
                </div>
                <span class="post-date">${post.date || ''}</span>
            </li>
        `;
    });

    html += `
            </ul>
        </div>
    `;
    blogContent.innerHTML = html;
}

function handlePostClick(index, isPrivate) {
    if (isPrivate) {
        const password = prompt("이 글은 비공개입니다. 비밀번호를 입력하세요.");
        if (password === loadSettings().adminPassword) {
            viewPost(index);
        } else if (password !== null) {
            alert("비밀번호가 틀렸습니다!");
        }
    } else {
        viewPost(index);
    }
}

// 📂 카테고리 관리
function updateCategoryMenu() {
    const categoryTarget = document.getElementById('category-list-target');
    const settings = loadSettings();
    let html = `<li><a href="javascript:void(0)" onclick="filterPosts('All')">전체 글 보기 (All)</a></li>`;

    // 주 카테고리 목록 생성
    const mainCategories = settings.categories.filter(c => !c.sub).map(c => c.main);

    mainCategories.forEach(mainCat => {
        html += `<li><a href="javascript:void(0)" onclick="filterPosts('${mainCat}')">${mainCat}</a>`;
        
        // 해당 주 카테고리의 하위 카테고리 목록 생성
        html += `<ul style="list-style: none; padding-left: 15px;">`;
        settings.categories
            .filter(c => c.main === mainCat && c.sub)
            .sort((a, b) => a.sub.localeCompare(b.sub))
            .forEach(cat => {
                html += `<li><a href="javascript:void(0)" onclick="filterPosts('${mainCat}', '${cat.sub}')">- ${cat.sub}</a></li>`;
            });
        html += `</ul></li>`;
    });

    categoryTarget.innerHTML = html;
}

function filterPosts(mainCategory, subCategory = null) {
    currentFilter = { main: mainCategory, sub: subCategory };
    showPosts();
}

// ✏️ 블로그 에디터 기능
function openPostEditorWindow(index) {
    const settings = loadSettings();
    const categorySelect = document.getElementById('post-main-category');
    const subCategorySelect = document.getElementById('post-sub-category');
    
    // 주 카테고리 드롭다운 채우기
    categorySelect.innerHTML = settings.categories
        .filter(c => !c.sub)
        .map(cat => `<option value="${cat.main}">${cat.main}</option>`)
        .join('');

    const updateSubCategories = (selectedMain) => {
        const subCategories = settings.categories.filter(c => c.main === selectedMain && c.sub);
        subCategorySelect.innerHTML = subCategories.length > 0 ? 
            subCategories.map(cat => `<option value="${cat.sub}">${cat.sub}</option>`).join('') : 
            '<option value="">(하위 카테고리 없음)</option>';
        subCategorySelect.disabled = subCategories.length === 0;
    };

    categorySelect.onchange = (e) => updateSubCategories(e.target.value);

    if (index === -1) {
        document.getElementById('post-index').value = '';
        document.getElementById('post-title').value = '';
        document.getElementById('post-content').innerHTML = '';
        document.getElementById('post-date-input').value = getTodayDate(); // 새 글은 오늘 날짜 자동 입력
        document.getElementById('post-is-private').value = 'false';
        
        // 기본 카테고리 선택
        const defaultMainCat = settings.categories.find(c => !c.sub)?.main || "";
        categorySelect.value = defaultMainCat;
        updateSubCategories(defaultMainCat);

    } else {
        const posts = loadPosts();
        const post = posts[index];
        document.getElementById('post-index').value = index;
        document.getElementById('post-title').value = post.title;
        document.getElementById('post-content').innerHTML = post.content;
        document.getElementById('post-date-input').value = post.date || ''; // 날짜가 null일 경우 빈 문자열
        document.getElementById('post-is-private').value = post.isPrivate ? 'true' : 'false';
        
        categorySelect.value = post.mainCategory;
        updateSubCategories(post.mainCategory);
        subCategorySelect.value = post.subCategory || "";
    }
    
    showWindow('win-new-post');
    document.getElementById('post-title').focus();
}

function savePost(event) {
    event.preventDefault();
    const index = parseInt(document.getElementById('post-index').value);
    const title = document.getElementById('post-title').value.trim();
    const content = document.getElementById('post-content').innerHTML;
    const mainCategory = document.getElementById('post-main-category').value;
    const subCategory = document.getElementById('post-sub-category').value || null;
    const isPrivate = document.getElementById('post-is-private').value === 'true';
    const date = document.getElementById('post-date-input').value.trim();
    
    // 날짜 유효성 검사 (YYYY.MM.DD 형식 또는 빈 문자열 허용)
    const datePattern = /^(\d{4}\.\d{2}\.\d{2})?$/;
    if (date && !datePattern.test(date)) {
        alert("날짜 형식이 올바르지 않습니다. (YYYY.MM.DD 또는 빈칸)");
        return;
    }

    const newPost = {
        title,
        content,
        mainCategory,
        subCategory,
        isPrivate,
        date: date || getTodayDate() // 날짜 미입력 시 오늘 날짜 사용
    };

    const posts = loadPosts();
    if (index >= 0) {
        // 수정
        posts[index] = newPost;
    } else {
        // 새 글 (최신 글이 배열의 맨 앞에 오도록 함)
        posts.unshift(newPost);
    }

    savePostsToStorage(posts);
    closeWindow('win-new-post');
    // 필터링 상태 유지하고 목록 업데이트
    showPosts();
}

function execCmd(command, value = null) {
    document.execCommand(command, false, value);
    document.getElementById('post-content').focus();
}

function insertTaskList() {
    execCmd('insertUnorderedList');

    const contentDiv = document.getElementById('post-content');
    const selection = window.getSelection();
    let listNode = selection.focusNode;

    // 현재 포커스된 위치에서 UL 노드를 찾습니다.
    while (listNode && listNode !== contentDiv) {
        if (listNode.nodeName === 'UL') break;
        listNode = listNode.parentNode;
    }

    // UL 노드를 찾았다면 tasklist 속성을 설정합니다.
    if (listNode && listNode.nodeName === 'UL') {
        listNode.setAttribute('data-role', 'tasklist');
        
        // 기존/새 LI 항목에 클릭 이벤트 바인딩
        listNode.querySelectorAll('li').forEach(li => {
            if (!li.hasAttribute('aria-checked')) {
                li.setAttribute('aria-checked', 'false');
                li.onclick = function() {
                    const isChecked = this.getAttribute('aria-checked') === 'true';
                    this.setAttribute('aria-checked', isChecked ? 'false' : 'true');
                };
            }
        });
    }
    document.getElementById('post-content').focus();
}

function viewPost(index) {
    const posts = loadPosts();
    const post = posts[index];
    const win = document.getElementById('win-view-post');
    const titlebar = win.querySelector('.window-titlebar');

    // 요청: 날짜가 있을 때만 표시
    document.getElementById('view-date').textContent = post.date || '날짜 없음';
    
    const categoryDisplay = post.subCategory ? `${post.mainCategory} > ${post.subCategory}` : post.mainCategory;
    document.getElementById('view-category').textContent = `[${categoryDisplay}]`;
    document.getElementById('view-privacy').textContent = post.isPrivate ? '🔒 Private' : '🌐 Public';
    document.getElementById('view-title').textContent = post.title;
    document.getElementById('view-content').innerHTML = post.content;
    titlebar.firstChild.textContent = `📰 ${post.title}`;

    document.getElementById('edit-button').onclick = () => { editPostPrompt(index); };
    document.getElementById('delete-button').onclick = () => deletePost(index);

    showWindow('win-view-post');
}

// 🗑️ 글 삭제
function deletePost(index) {
    if (confirm("정말로 이 글을 삭제하시겠습니까?")) {
        const posts = loadPosts();
        posts.splice(index, 1);
        savePostsToStorage(posts);
        closeWindow('win-view-post');
        showPosts();
    }
}

// 💾 앨범 관리
function loadAlbums() {
    const storedAlbums = localStorage.getItem(ALBUMS_STORAGE_KEY);
    return storedAlbums ? JSON.parse(storedAlbums) : [
        { title: "첫 앨범", coverUrl: "https://via.placeholder.com/100x70?text=Cover+1", media: [{ url: "https://via.placeholder.com/80?text=Photo+1", type: "image" }], date: getTodayDate(), isPrivate: false },
        { title: "비공개 추억", coverUrl: "https://via.placeholder.com/100x70?text=Cover+2", media: [{ url: "https://via.placeholder.com/80?text=Photo+2", type: "image" }], date: getTodayDate(), isPrivate: true }
    ];
}

function saveAlbumsToStorage(albums) {
    localStorage.setItem(ALBUMS_STORAGE_KEY, JSON.stringify(albums));
}

function showAlbums() {
    const albumContent = document.getElementById('album-content');
    const albums = loadAlbums();
    let html = `
        <div class="album-new-btn-area">
            <span class="win-btn" onclick="newAlbumPostPrompt()">New Album...</span>
        </div>
        <div class="album-list">
    `;

    albums.forEach((album, index) => {
        const privacyIcon = album.isPrivate ? '🔒' : '';
        const coverHtml = album.coverUrl ? `<img src="${album.coverUrl}" alt="${album.title} Cover">` : `<span>No Cover</span>`;
        html += `
            <div class="album-item" onclick="handleAlbumPostClick(${index}, ${album.isPrivate})">
                <div class="album-cover">${coverHtml}</div>
                <div class="album-title">${album.title} ${privacyIcon}</div>
            </div>
        `;
    });

    html += `</div>`;
    albumContent.innerHTML = html;
}

function handleAlbumPostClick(index, isPrivate) {
    if (isPrivate) {
        const password = prompt("이 앨범은 비공개입니다. 비밀번호를 입력하세요.");
        if (password === loadSettings().adminPassword) {
            viewAlbumPost(index);
        } else if (password !== null) {
            alert("비밀번호가 틀렸습니다!");
        }
    } else {
        viewAlbumPost(index);
    }
}

// 📸 앨범 에디터 기능
let currentMediaUrls = [];

async function handleMediaFiles(input) {
    const grid = document.getElementById('album-media-preview-grid');
    const urlsInput = document.getElementById('album-post-media-urls');
    
    // 기존 URL (Data URL 포함) 유지
    let mediaUrls = JSON.parse(urlsInput.value || '[]');
    
    // 새로 선택된 파일들을 Data URL로 변환하여 추가
    if (input.files.length > 0) {
        for (let i = 0; i < input.files.length; i++) {
            const file = input.files[i];
            const dataUrl = await fileToDataUrl(file);
            mediaUrls.push({
                url: dataUrl,
                type: file.type.startsWith('image/') ? 'image' : 'video'
            });
        }
    }
    
    urlsInput.value = JSON.stringify(mediaUrls);
    grid.innerHTML = '';
    
    // Grid 업데이트
    mediaUrls.forEach((media, index) => {
        const item = document.createElement('div');
        item.className = 'album-media-item';
        item.style.position = 'relative';

        const removeBtn = document.createElement('button');
        removeBtn.textContent = 'x';
        removeBtn.className = 'win-btn';
        removeBtn.style.position = 'absolute';
        removeBtn.style.top = '0';
        removeBtn.style.right = '0';
        removeBtn.style.padding = '0 3px';
        removeBtn.style.fontSize = '0.6rem';
        removeBtn.onclick = (e) => {
            e.stopPropagation();
            removeMediaFromAlbum(index);
        };
        
        let content;
        if (media.type === 'image') {
            content = document.createElement('img');
            content.src = media.url;
            content.alt = 'Image';
        } else if (media.type === 'video') {
            content = document.createElement('span');
            content.textContent = 'VIDEO';
            content.style.color = '#ff0000';
            content.style.fontSize = '0.9rem';
            content.style.fontWeight = 'bold';
        } else {
            content = document.createElement('span');
            content.textContent = 'URL';
        }
        
        item.appendChild(content);
        item.appendChild(removeBtn);
        grid.appendChild(item);
    });
    
    // 파일 인풋 초기화 (새로운 파일만 추가되도록)
    input.value = ''; 
}

function removeMediaFromAlbum(indexToRemove) {
    const urlsInput = document.getElementById('album-post-media-urls');
    let mediaUrls = JSON.parse(urlsInput.value || '[]');
    mediaUrls.splice(indexToRemove, 1);
    urlsInput.value = JSON.stringify(mediaUrls);
    
    // 가상의 파일 인풋을 만들어 handleMediaFiles를 호출하여 UI 업데이트
    const dummyInput = document.createElement('input');
    dummyInput.files = new DataTransfer().files; 
    handleMediaFiles(dummyInput);
}

async function previewImage(input, previewId) {
    const previewDiv = document.getElementById(previewId);
    const urlInput = document.getElementById('album-post-cover-url-text');
    previewDiv.innerHTML = '<span>Preview</span>';

    if (input.files && input.files[0]) {
        try {
            const dataUrl = await fileToDataUrl(input.files[0]);
            const img = document.createElement('img');
            img.src = dataUrl;
            previewDiv.innerHTML = '';
            previewDiv.appendChild(img);
            document.getElementById('album-post-cover-url').value = dataUrl; // Hidden input에 data URL 저장
        } catch (error) {
            alert("이미지 로드 오류!");
            console.error(error);
        }
    }
}

async function openAlbumPostEditorWindow(index) {
    const win = document.getElementById('win-new-album-post');
    const titleInput = document.getElementById('album-post-title');
    const isPrivateSelect = document.getElementById('album-post-is-private');
    const indexInput = document.getElementById('album-post-index');
    const coverUrlInput = document.getElementById('album-post-cover-url');
    const coverUrlTextInput = document.getElementById('album-post-cover-url-text');
    const mediaUrlsInput = document.getElementById('album-post-media-urls');
    const coverPreview = document.getElementById('album-cover-preview');
    const mediaGrid = document.getElementById('album-media-preview-grid');
    const titlebar = win.querySelector('.window-titlebar');
    const dateInput = document.getElementById('album-post-date-input'); // 날짜 필드

    indexInput.value = index;
    coverPreview.innerHTML = '<span>Preview</span>';
    mediaGrid.innerHTML = '';

    if (index === -1) {
        titleInput.value = '';
        isPrivateSelect.value = 'false';
        coverUrlInput.value = '';
        coverUrlTextInput.value = '';
        mediaUrlsInput.value = '[]';
        titlebar.firstChild.textContent = '📸 New Album';
        dateInput.value = getTodayDate(); // 새 앨범은 오늘 날짜 자동 입력
    } else {
        const albums = loadAlbums();
        const album = albums[index];
        titleInput.value = album.title;
        isPrivateSelect.value = album.isPrivate ? 'true' : 'false';
        coverUrlInput.value = album.coverUrl || '';
        coverUrlTextInput.value = album.coverUrl || '';
        mediaUrlsInput.value = JSON.stringify(album.media);
        titlebar.firstChild.textContent = `🖼️ Edit Album: ${album.title}`;
        dateInput.value = album.date || ''; // 날짜가 null일 경우 빈 문자열
        
        if (album.coverUrl) {
            coverPreview.innerHTML = `<img src="${album.coverUrl}" alt="Cover">`;
        }
    }
    
    // 미디어 미리보기 업데이트 (기존 미디어가 있다면)
    const dummyInput = document.createElement('input');
    dummyInput.files = new DataTransfer().files; 
    await handleMediaFiles(dummyInput); // mediaUrlsInput의 내용을 바탕으로 Grid 업데이트

    showWindow('win-new-album-post');
    titleInput.focus();
}

function saveAlbumPost(event) {
    event.preventDefault();
    const index = parseInt(document.getElementById('album-post-index').value);
    const title = document.getElementById('album-post-title').value.trim();
    const isPrivate = document.getElementById('album-post-is-private').value === 'true';
    const coverUrl = document.getElementById('album-post-cover-url').value.trim() || document.getElementById('album-post-cover-url-text').value.trim() || null;
    const media = JSON.parse(document.getElementById('album-post-media-urls').value || '[]');
    const date = document.getElementById('album-post-date-input').value.trim();

    // 날짜 유효성 검사 (YYYY.MM.DD 형식 또는 빈 문자열 허용)
    const datePattern = /^(\d{4}\.\d{2}\.\d{2})?$/;
    if (date && !datePattern.test(date)) {
        alert("날짜 형식이 올바르지 않습니다. (YYYY.MM.DD 또는 빈칸)");
        return;
    }
    
    if (media.length === 0) {
        alert("최소한 하나의 이미지 또는 영상을 추가해야 합니다.");
        return;
    }
    
    const newAlbumPost = {
        title,
        coverUrl,
        media,
        isPrivate,
        date: date || getTodayDate() // 날짜 미입력 시 오늘 날짜 사용
    };

    const albums = loadAlbums();
    if (index >= 0) {
        // 수정
        albums[index] = newAlbumPost;
    } else {
        // 새 앨범 (최신 앨범이 배열의 맨 앞에 오도록 함)
        albums.unshift(newAlbumPost);
    }

    saveAlbumsToStorage(albums);
    closeWindow('win-new-album-post');
    showAlbums();
}

function viewAlbumPost(index) {
    const albums = loadAlbums();
    const album = albums[index];
    const win = document.getElementById('win-view-album-post');
    const titlebar = win.querySelector('.window-titlebar');
    const contentDiv = document.getElementById('view-album-content');

    document.getElementById('view-album-title').textContent = album.title;
    // 요청: 날짜가 있을 때만 표시
    document.getElementById('view-album-date').textContent = album.date || '날짜 없음';
    document.getElementById('view-album-privacy').textContent = album.isPrivate ? '🔒 Private' : '🌐 Public';
    titlebar.firstChild.textContent = `🖼️ ${album.title}`;
    
    let mediaHtml = '<div style="display: flex; flex-direction: column; gap: 10px;">';
    album.media.forEach(media => {
        if (media.type === 'image') {
            mediaHtml += `<img src="${media.url}" alt="image" style="max-width: 100%; height: auto; border: 2px solid #c0c0c0;">`;
        } else if (media.type === 'video') {
            mediaHtml += `<video src="${media.url}" controls style="max-width: 100%; height: auto; border: 2px solid #c0c0c0;"></video>`;
        }
    });
    mediaHtml += '</div>';

    contentDiv.innerHTML = mediaHtml;

    document.getElementById('edit-album-button').onclick = () => { editAlbumPostPrompt(index); };
    document.getElementById('delete-album-button').onclick = () => deleteAlbumPost(index);

    showWindow('win-view-album-post');
}

function deleteAlbumPost(index) {
    if (confirm("정말로 이 앨범을 삭제하시겠습니까?")) {
        const albums = loadAlbums();
        albums.splice(index, 1);
        saveAlbumsToStorage(albums);
        closeWindow('win-view-album-post');
        showAlbums();
    }
}

// 🔒 권한 및 클릭 핸들러
function newPostPrompt() {
    const password = prompt("새 글 작성을 위해 비밀번호를 입력하세요.");
    if (password === loadSettings().adminPassword) {
        openPostEditorWindow(-1);
    } else if (password !== null) {
        alert("비밀번호가 틀렸습니다!");
    }
}

function newAlbumPostPrompt() {
    const password = prompt("새 앨범 작성을 위해 비밀번호를 입력하세요.");
    if (password === loadSettings().adminPassword) {
        openAlbumPostEditorWindow(-1);
    } else if (password !== null) {
        alert("비밀번호가 틀렸습니다!");
    }
}

function editPostPrompt(index) {
    const password = prompt("글 수정을 위해 비밀번호를 입력하세요.");
    if (password === loadSettings().adminPassword) {
        closeWindow('win-view-post');
        openPostEditorWindow(index);
    } else if (password !== null) {
        alert("비밀번호가 틀렸습니다!");
    }
}

function editAlbumPostPrompt(index) {
    const password = prompt("앨범 수정을 위해 비밀번호를 입력하세요.");
    if (password === loadSettings().adminPassword) {
        closeWindow('win-view-album-post');
        openAlbumPostEditorWindow(index);
    } else if (password !== null) {
        alert("비밀번호가 틀렸습니다!");
    }
}

function openSettingsPrompt() {
    const password = prompt("설정 변경을 위해 관리자 비밀번호를 입력하세요.");
    if (password === loadSettings().adminPassword) {
        openSettingsWindow();
    } else if (password !== null) {
        alert("비밀번호가 틀렸습니다!");
    }
}

// ⚙️ 설정 창 로직
function openSettingsWindow() {
    const settings = loadSettings();
    document.getElementById('setting-title').value = settings.title;
    document.getElementById('setting-desc').value = settings.desc;
    document.getElementById('setting-profile-image-url').value = settings.profileImage;
    document.getElementById('setting-home-content').value = settings.homeContent;
    // 요청: 배경화면 URL 필드 로드
    document.getElementById('setting-background-image-url').value = settings.siteBackground;
    
    // 비밀번호 입력 필드는 항상 비워둡니다.
    document.getElementById('setting-admin-password').value = '';

    renderLinkList();
    renderCategoryList();
    showWindow('win-settings');
}

function renderLinkList() {
    const linkListDiv = document.getElementById('link-list');
    const settings = loadSettings();
    linkListDiv.innerHTML = '';

    settings.links.forEach((link, index) => {
        const div = document.createElement('div');
        div.style.marginBottom = '5px';
        div.innerHTML = `
            <input type="text" value="${link.title}" id="link-title-${index}" placeholder="링크 제목" style="width: 45%; display: inline-block; margin-bottom: 0;">
            <input type="text" value="${link.url}" id="link-url-${index}" placeholder="URL" style="width: 45%; display: inline-block; margin-bottom: 0; margin-left: 5px;">
            <button type="button" class="win-btn" style="background:#ff9999; margin-left: 5px;" onclick="removeLink(${index})">삭제</button>
        `;
        linkListDiv.appendChild(div);
    });
}

function addLink() {
    const title = document.getElementById('new-link-title').value.trim();
    const url = document.getElementById('new-link-url').value.trim();

    if (title && url) {
        const settings = loadSettings();
        // 배열의 값을 변경하는 것이 아니라 기존 배열의 복사본을 수정하도록 합니다.
        // 하지만 여기서는 편의를 위해 직접 수정합니다.
        settings.links.push({ title, url });
        saveSettingsToStorage(settings);
        document.getElementById('new-link-title').value = '';
        document.getElementById('new-link-url').value = '';
        renderLinkList();
    } else {
        alert("링크 제목과 URL을 모두 입력하세요.");
    }
}

function removeLink(index) {
    const settings = loadSettings();
    settings.links.splice(index, 1);
    saveSettingsToStorage(settings);
    renderLinkList();
}

function renderCategoryList() {
    const container = document.getElementById('category-list-container');
    const settings = loadSettings();
    
    container.innerHTML = '<ul>' + settings.categories.map((cat, index) => {
        const subDisplay = cat.sub ? `<span class="cat-item-sub">(${cat.sub})</span>` : '';
        return `
            <li>
                <div><span class="cat-item-main">${cat.main}</span>${subDisplay}</div>
                <div class="cat-btn-group">
                    <button type="button" class="win-btn" style="background:#ff9999; padding: 1px 4px;" onclick="removeCategory(${index})">삭제</button>
                </div>
            </li>
        `;
    }).join('') + '</ul>';
}

function addCategory() {
    const main = document.getElementById('new-main-category').value.trim();
    const sub = document.getElementById('new-sub-category').value.trim() || null;

    if (main) {
        const settings = loadSettings();
        // 중복 체크 (주 카테고리/하위 카테고리 조합이 동일한 경우)
        const isDuplicate = settings.categories.some(c => c.main === main && c.sub === sub);
        
        if (isDuplicate) {
            alert("이미 존재하는 카테고리 조합입니다.");
            return;
        }

        settings.categories.push({ main, sub });
        saveSettingsToStorage(settings);
        document.getElementById('new-main-category').value = '';
        document.getElementById('new-sub-category').value = '';
        renderCategoryList();
        updateCategoryMenu();
    } else {
        alert("주 카테고리명을 입력하세요.");
    }
}

function removeCategory(index) {
    const settings = loadSettings();
    const categoryToRemove = settings.categories[index];

    if (confirm(`정말로 카테고리 [${categoryToRemove.main}${categoryToRemove.sub ? ' > ' + categoryToRemove.sub : ''}] 를 삭제하시겠습니까?`)) {
        settings.categories.splice(index, 1);
        saveSettingsToStorage(settings);
        renderCategoryList();
        updateCategoryMenu();

        // 현재 필터가 삭제된 카테고리인 경우 'All'로 초기화
        if (currentFilter.main === categoryToRemove.main && (currentFilter.sub === categoryToRemove.sub || (!currentFilter.sub && !categoryToRemove.sub))) {
            currentFilter = { main: 'All', sub: null };
            // Blog 탭이 활성화되어 있다면 목록도 새로고침
            if (document.getElementById('win-blog').style.display === 'block') {
                showPosts();
            }
        }
    }
}

function saveSettings(event) {
    event.preventDefault();

    const currentSettings = loadSettings();
    currentSettings.title = document.getElementById('setting-title').value.trim();
    currentSettings.desc = document.getElementById('setting-desc').value.trim();
    currentSettings.profileImage = document.getElementById('setting-profile-image-url').value.trim();
    currentSettings.homeContent = document.getElementById('setting-home-content').value.trim();
    // 요청: 배경화면 URL 저장
    currentSettings.siteBackground = document.getElementById('setting-background-image-url').value.trim();

    // 비밀번호 변경 처리
    const newPassword = document.getElementById('setting-admin-password').value.trim();
    if (newPassword) {
        currentSettings.adminPassword = newPassword;
    }

    // 링크 목록 업데이트 (인라인 수정된 내용을 반영)
    const linkListDiv = document.getElementById('link-list');
    currentSettings.links = Array.from(linkListDiv.children).map((div, index) => {
        return {
            title: document.getElementById(`link-title-${index}`).value.trim(),
            url: document.getElementById(`link-url-${index}`).value.trim()
        };
    }).filter(link => link.title && link.url); // 제목과 URL이 모두 있는 링크만 저장

    saveSettingsToStorage(currentSettings);
    updateUIFromSettings();
    closeWindow('win-settings');
    alert("설정이 저장되었습니다!");
}

// 🚀 앱 초기화 
function initApp() {
    updateUIFromSettings();
    
    // 기존 showMainContent('welcome') 대신 'about'으로 시작하도록 수정
    showMainContent('about'); 
    
    document.getElementById('win-profile').style.display = 'block';
    document.getElementById('win-categories').style.display = 'block';
    document.getElementById('win-search').style.display = 'block';
    
    // Z-index 설정
    highestZ = 5; 
    document.getElementById('win-about').style.zIndex = 5; // about 창이 가장 위에
    document.getElementById('win-profile').style.zIndex = 4;
    document.getElementById('win-categories').style.zIndex = 3;
    document.getElementById('win-search').style.zIndex = 2;
}

</script>

</body>
</html>
