<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>트라페지움 - 천문 관측 커뮤니티</title>
    <style>
        html {
            scroll-behavior: smooth;
        }
        body {
            background-color: #0b132b;
            color: #ffffff;
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
        }
        header {
            background-color: #1c2541;
            padding: 20px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 1000;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
        }
        h1 { margin: 0; font-size: 24px; }
        nav a {
            color: #6fffe9;
            text-decoration: none;
            margin-left: 25px;
            font-weight: bold;
        }
        nav a:hover { color: #5bc0be; }
        
        .container {
            padding: 140px 40px 40px 40px;
            max-width: 1100px;
            margin: 0 auto;
        }
        .content-box {
            background-color: #1c2541;
            padding: 30px;
            border-radius: 10px;
            margin-bottom: 40px;
            scroll-margin-top: 120px; 
        }
        h2 { color: #5bc0be; margin-top: 0; }
        
        .edit-info-box {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px dashed #2a3454;
        }
        .edit-info-box input {
            padding: 6px;
            margin-right: 5px;
            background-color: #0b132b;
            color: white;
            border: 1px solid #5bc0be;
            border-radius: 4px;
        }

        .auth-container {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        .auth-box {
            flex: 1;
            background-color: #0b132b;
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #2a3454;
            min-width: 280px;
        }
        .auth-box h3 { margin-top: 0; color: #6fffe9; font-size: 16px; }
        .auth-form { display: flex; flex-direction: column; gap: 8px; }
        .auth-form input {
            padding: 8px;
            background-color: #1c2541;
            color: white;
            border: 1px solid #5bc0be;
            border-radius: 4px;
        }

        .community-ctrl {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            gap: 15px;
        }
        .search-box {
            flex: 1;
            padding: 10px;
            background-color: #0b132b;
            color: white;
            border: 1px solid #5bc0be;
            border-radius: 5px;
        }

        .community-main {
            display: none;
            border-top: 1px solid #2a3454;
            padding-top: 20px;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0,0,0,0.7);
            z-index: 2000;
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background-color: #1c2541;
            padding: 30px;
            border-radius: 10px;
            width: 90%;
            max-width: 500px;
            border: 1px solid #5bc0be;
        }
        .modal-content input[type="text"], .modal-content textarea {
            width: 100%;
            padding: 10px;
            margin-bottom: 12px;
            background-color: #0b132b;
            color: white;
            border: 1px solid #5bc0be;
            border-radius: 5px;
            box-sizing: border-box;
        }
        .modal-buttons {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }

        button {
            background-color: #5bc0be;
            color: #0b132b;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
        }
        button:hover { background-color: #6fffe9; }
        
        .post-list { margin-top: 20px; }
        .post-item {
            background-color: #0b132b;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 15px;
            border: 1px solid #2a3454;
        }
        .post-header {
            display: flex;
            justify-content: space-between;
            color: #6fffe9;
            font-size: 14px;
            margin-bottom: 8px;
        }
        .post-title {
            font-size: 18px;
            font-weight: bold;
            color: #5bc0be;
            margin-bottom: 10px;
        }
        .post-body {
            line-height: 1.6;
            white-space: pre-wrap;
        }
        .post-img {
            max-width: 100%;
            max-height: 300px;
            margin-top: 15px;
            border-radius: 5px;
            display: block;
        }

        /* 💬 댓글 구역 디자인 스타일 */
        .comment-section {
            margin-top: 20px;
            padding-top: 15px;
            border-top: 1px solid #2a3454;
        }
        .comment-list {
            margin-bottom: 10px;
        }
        .comment-item {
            font-size: 14px;
            padding: 6px 0;
            border-bottom: 1px dashed #1c2541;
        }
        .comment-input-box {
            display: flex;
            gap: 8px;
            margin-top: 10px;
        }
        .comment-input-box input {
            flex: 1;
            padding: 8px;
            background-color: #1c2541;
            color: white;
            border: 1px solid #5bc0be;
            border-radius: 4px;
        }
        .comment-input-box button {
            padding: 8px 15px;
            font-size: 13px;
        }

        .photo-preview { margin-top: 20px; }
        .preview-img { max-width: 300px; margin-top: 15px; border-radius: 5px; display: block; }
    </style>
</head>
<body>

    <header>
        <h1>✨ 트라페지움 (Trapezium)</h1>
        <nav>
            <a href="#info">천문 관측 정보</a>
            <a href="#community">커뮤니티</a>
            <a href="#mypage">내 페이지</a>
        </nav>
    </header>

    <div class="container">
        <div id="info" class="content-box">
            <h2>🔭 오늘의 천문 관측 정보</h2>
            <p>오늘 밤 관측 지수: <b id="displayIndex">[매우 좋음]</b></p>
            <p>추천 관측 대상: <span id="displayTarget">토성, 여름철 대삼각형</span></p>
            
            <div class="edit-info-box">
                <input type="text" id="inputIndex" placeholder="관측 지수 변경">
                <input type="text" id="inputTarget" placeholder="추천 대상 변경">
                <button onclick="updateInfo()">정보 수정하기</button>
            </div>
        </div>

        <div id="community" class="content-box">
            <h2>💬 커뮤니티</h2>
            
            <div class="auth-container" id="authSection">
                <div class="auth-box">
                    <h3>1. 회원가입</h3>
                    <div class="auth-form">
                        <input type="text" id="regId" placeholder="아이디">
                        <input type="password" id="regPw" placeholder="비밀번호">
                        <input type="text" id="regName" placeholder="닉네임">
                        <button onclick="registerUser()">가입하기</button>
                    </div>
                </div>
                <div class="auth-box">
                    <h3>2. 로그인</h3>
                    <div class="auth-form">
                        <input type="text" id="loginId" placeholder="아이디">
                        <input type="password" id="loginPw" placeholder="비밀번호">
                        <button onclick="loginUser()">로그인</button>
                    </div>
                </div>
            </div>

            <div id="welcomeMessage" style="display: none; margin-bottom: 20px; color: #6fffe9; font-weight: bold;"></div>

            <div class="community-main" id="communityMain">
                <div class="community-ctrl">
                    <input type="text" id="searchBar" class="search-box" placeholder="글 제목으로 검색해보세요..." onkeyup="searchPosts()">
                    <button onclick="openModal()">글쓰기</button>
                </div>
                
                <div class="post-list" id="postList">
                    </div>
            </div>
        </div>

        <div class="modal" id="postModal">
            <div class="modal-content">
                <h3 style="color: #5bc0be; margin-top:0;">새 글 작성하기</h3>
                <input type="text" id="postTitleInput" placeholder="제목을 입력하세요">
                <textarea id="postContentInput" rows="5" placeholder="내용을 입력하세요..."></textarea>
                <label style="display:block; margin-bottom:12px; color:#6fffe9; font-size:14px;">
                    📷 사진 첨부: <input type="file" id="postImageInput" accept="image/*">
                </label>
                <div class="modal-buttons">
                    <button style="background-color:#2a3454; color:white;" onclick="closeModal()">취소</button>
                    <button onclick="addPost()">등록하기</button>
                </div>
            </div>
        </div>

        <div id="mypage" class="content-box">
            <h2>⭐ 나의 관측 일지 (내 페이지)</h2>
            <p>반가워요, 트라페지움 회원님! 나만의 사진을 보관해 보세요.</p>
            <input type="file" id="imageInput" accept="image/*" onchange="previewImage()">
            <div class="photo-preview" id="photoPreview"></div>
        </div>
    </div>

    <script>
        let userList = JSON.parse(localStorage.getItem('trapeziumUserList')) || [];
        // 기본 예시 게시글 목록 (comments 배열 추가)
        let postListArray = JSON.parse(localStorage.getItem('trapeziumPostList')) || [
            { id: 1, nickname: "스타게이저", title: "오늘 은하수 촬영 성공했습니다!", content: "강원도 영월에 가서 찍었는데 정말 별이 쏟아질 것 같았어요.", img: "", comments: [{ nickname: "은하수행", text: "와 정말 멋지네요!" }] },
            { id: 2, nickname: "은하수행", title: "초보자용 망원경 고르는 팁 공유해요.", content: "처음에는 구경이 큰 반사망원경보다는 다루기 쉬운 굴절망원경을 추천합니다.", img: "", comments: [] }
        ];
        let loggedInNickname = ""; 

        window.onload = function() {
            const savedIndex = localStorage.getItem('infoIndex');
            const savedTarget = localStorage.getItem('infoTarget');
            if (savedIndex) document.getElementById('displayIndex').innerText = savedIndex;
            if (savedTarget) document.getElementById('displayTarget').innerText = savedTarget;
            renderPosts(postListArray);
        }

        function updateInfo() {
            const newIndex = document.getElementById('inputIndex').value;
            const newTarget = document.getElementById('inputTarget').value;
            if (newIndex) { document.getElementById('displayIndex').innerText = newIndex; localStorage.setItem('infoIndex', newIndex); }
            if (newTarget) { document.getElementById('displayTarget').innerText = newTarget; localStorage.setItem('infoTarget', newTarget); }
            document.getElementById('inputIndex').value = '';
            document.getElementById('inputTarget').value = '';
            alert('관측 정보가 업데이트 되었습니다!');
        }

        function registerUser() {
            const id = document.getElementById('regId').value.trim();
            const pw = document.getElementById('regPw').value.trim();
            const name = document.getElementById('regName').value.trim();

            if (!id || !pw || !name) { alert('회원가입 정보를 모두 입력해 주세요!'); return; }

            const isNameDuplicate = userList.some(user => user.name === name);
            const isIdDuplicate = userList.some(user => user.id === id);

            if (isIdDuplicate) { alert('이미 가입된 아이디입니다!'); return; }
            if (isNameDuplicate) { alert('이미 존재하는 닉네임입니다! 다른 닉네임을 입력해 주세요.'); return; }

            userList.push({ id: id, pw: pw, name: name });
            localStorage.setItem('trapeziumUserList', JSON.stringify(userList));
            alert('회원가입이 완료되었습니다! 이제 로그인을 해주세요.');
            
            document.getElementById('regId').value = ''; document.getElementById('regPw').value = ''; document.getElementById('regName').value = '';
        }

        function loginUser() {
            const id = document.getElementById('loginId').value.trim();
            const pw = document.getElementById('loginPw').value.trim();
            const foundUser = userList.find(user => user.id === id && user.pw === pw);

            if (foundUser) {
                loggedInNickname = foundUser.name;
                document.getElementById('authSection').style.display = 'none';
                document.getElementById('welcomeMessage').style.display = 'block';
                document.getElementById('welcomeMessage').innerText = `✨ ${loggedInNickname}님, 환영합니다!`;
                document.getElementById('communityMain').style.display = 'block';
            } else {
                alert('아이디 또는 비밀번호가 틀렸습니다!');
            }
        }

        function openModal() { document.getElementById('postModal').style.display = 'flex'; }
        function closeModal() {
            document.getElementById('postModal').style.display = 'none';
            document.getElementById('postTitleInput').value = '';
            document.getElementById('postContentInput').value = '';
            document.getElementById('postImageInput').value = '';
        }

        // 게시글 및 댓글 함께 출력하기
        function renderPosts(posts) {
            const postListDiv = document.getElementById('postList');
            postListDiv.innerHTML = '';
            
            // 최신 글이 위로 오도록 정렬
            [...posts].reverse().forEach(post => {
                const item = document.createElement('div');
                item.className = 'post-item';
                
                let imgHtml = post.img ? `<img src="${post.img}" class="post-img">` : '';
                
                // 댓글 목록 구성
                let commentHtml = '';
                if (post.comments && post.comments.length > 0) {
                    post.comments.forEach(c => {
                        commentHtml += `<div class="comment-item"><b>${c.nickname}:</b> ${c.text}</div>`;
                    });
                } else {
                    commentHtml = `<div class="comment-item" style="color:#aaa; border:none;">아직 댓글이 없습니다.</div>`;
                }

                item.innerHTML = `
                    <div class="post-header"><span>✍️ 작성자: ${post.nickname}</span></div>
                    <div class="post-title">${post.title}</div>
                    <div class="post-body">${post.content}</div>
                    ${imgHtml}
                    
                    <div class="comment-section">
                        <div class="comment-list">${commentHtml}</div>
                        <div class="comment-input-box">
                            <input type="text" id="cmtInput-${post.id}" placeholder="댓글을 입력하세요...">
                            <button onclick="addComment(${post.id})">댓글 등록</button>
                        </div>
                    </div>
                `;
                postListDiv.appendChild(item);
            });
        }

        function addPost() {
            const title = document.getElementById('postTitleInput').value.trim();
            const content = document.getElementById('postContentInput').value.trim();
            const imageFile = document.getElementById('postImageInput').files[0];

            if (!title || !content) { alert('제목과 내용을 모두 적어주세요!'); return; }

            if (imageFile) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    saveAndRenderPost(title, content, e.target.result);
                };
                reader.readAsDataURL(imageFile);
            } else {
                saveAndRenderPost(title, content, "");
            }
        }

        function saveAndRenderPost(title, content, imgData) {
            const newPost = {
                id: Date.now(), // 고유한 글 ID값 생성
                nickname: loggedInNickname,
                title: title,
                content: content,
                img: imgData,
                comments: [] // 댓글을 담을 빈 배열 생성
            };
            postListArray.push(newPost);
            localStorage.setItem('trapeziumPostList', JSON.stringify(postListArray));
            
            renderPosts(postListArray);
            closeModal();
        }

        // 💬 댓글 등록 함수
        function addComment(postId) {
            const commentInput = document.getElementById(`cmtInput-${postId}`);
            const commentText = commentInput.value.trim();

            if (!commentText) { alert('댓글 내용을 입력해주세요!'); return; }

            // 해당 ID를 가진 게시글을 찾아서 댓글 리스트에 추가
            const post = postListArray.find(p => p.id === postId);
            if (post) {
                if (!post.comments) post.comments = [];
                post.comments.push({
                    nickname: loggedInNickname,
                    text: commentText
                });

                // 업데이트된 전체 글 배열을 로컬 스토리지에 다시 저장
                localStorage.setItem('trapeziumPostList', JSON.stringify(postListArray));
                
                // 검색바의 상태를 유지하기 위해 전체 또는 필터링된 화면 다시 출력
                searchPosts(); 
            }
        }

        function searchPosts() {
            const keyword = document.getElementById('searchBar').value.toLowerCase();
            const filteredPosts = postListArray.filter(post => 
                post.title.toLowerCase().includes(keyword)
            );
            renderPosts(filteredPosts);
        }

        function previewImage() {
            const file = document.getElementById('imageInput').files[0];
            const previewContainer = document.getElementById('photoPreview');
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                previewContainer.innerHTML = '';
                const img = document.createElement('img');
                img.src = e.target.result;
                img.className = 'preview-img';
                previewContainer.appendChild(img);
            };
            reader.readAsDataURL(file);
        }
    </script>
</body>
</html>
