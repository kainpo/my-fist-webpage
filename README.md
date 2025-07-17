<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>✨ My Diary - あなたの特別な日記帳</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', -apple-system, BlinkMacSystemFont, 'Roboto', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }

        .floating-shapes {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .shape {
            position: absolute;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            animation: float 6s ease-in-out infinite;
        }

        .shape:nth-child(1) {
            width: 80px;
            height: 80px;
            top: 20%;
            left: 10%;
            animation-delay: 0s;
        }

        .shape:nth-child(2) {
            width: 120px;
            height: 120px;
            top: 60%;
            right: 15%;
            animation-delay: 2s;
        }

        .shape:nth-child(3) {
            width: 60px;
            height: 60px;
            bottom: 30%;
            left: 20%;
            animation-delay: 4s;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
        }

        .container {
            position: relative;
            z-index: 2;
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
            min-height: 100vh;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
            animation: fadeInDown 0.8s ease-out;
        }

        .header h1 {
            font-size: 3rem;
            color: white;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            font-weight: 700;
        }

        .header p {
            color: rgba(255, 255, 255, 0.9);
            font-size: 1.1rem;
            font-weight: 300;
        }

        .card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            animation: fadeInUp 0.8s ease-out;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.15);
        }

        .card h2 {
            color: #4a5568;
            font-size: 1.8rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .emoji {
            font-size: 1.5rem;
        }

        .input-group {
            margin-bottom: 20px;
        }

        .input-field {
            width: 100%;
            padding: 15px 20px;
            border: 2px solid #e2e8f0;
            border-radius: 12px;
            font-size: 1rem;
            transition: all 0.3s ease;
            background: white;
            font-family: inherit;
        }

        .input-field:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
            transform: translateY(-2px);
        }

        .input-field::placeholder {
            color: #a0aec0;
        }

        textarea.input-field {
            resize: vertical;
            min-height: 120px;
            line-height: 1.6;
        }

        .btn {
            padding: 15px 30px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            position: relative;
            overflow: hidden;
        }

        .btn:before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            transition: left 0.5s;
        }

        .btn:hover:before {
            left: 100%;
        }

        .btn.primary {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
        }

        .btn.primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.6);
        }

        .btn.secondary {
            background: linear-gradient(135deg, #6c757d, #495057);
            color: white;
            box-shadow: 0 4px 15px rgba(108, 117, 125, 0.4);
        }

        .btn.secondary:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(108, 117, 125, 0.6);
        }

        .btn.danger {
            background: linear-gradient(135deg, #e53e3e, #c53030);
            color: white;
            box-shadow: 0 4px 15px rgba(229, 62, 62, 0.4);
        }

        .btn.danger:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(229, 62, 62, 0.6);
        }

        .btn.small {
            padding: 8px 16px;
            font-size: 0.9rem;
        }

        .search-container {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
        }

        .search-container .input-field {
            flex: 1;
        }

        .diary-item {
            background: white;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 20px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
            border-left: 4px solid #667eea;
            transition: all 0.3s ease;
            animation: slideInLeft 0.6s ease-out;
        }

        .diary-item:hover {
            transform: translateX(5px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.12);
        }

        .diary-item .date {
            font-size: 0.9rem;
            color: #667eea;
            font-weight: 600;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .diary-item h3 {
            color: #2d3748;
            font-size: 1.4rem;
            margin-bottom: 15px;
            font-weight: 700;
        }

        .diary-item p {
            color: #4a5568;
            line-height: 1.7;
            margin-bottom: 20px;
        }

        .diary-item .actions {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }

        .stats {
            display: flex;
            justify-content: space-around;
            margin-bottom: 30px;
        }

        .stat-item {
            text-align: center;
            color: white;
            animation: fadeInUp 0.8s ease-out;
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            display: block;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        .stat-label {
            font-size: 0.9rem;
            opacity: 0.9;
            margin-top: 5px;
        }

        .empty-state {
            text-align: center;
            padding: 60px 20px;
            color: #a0aec0;
        }

        .empty-state .emoji {
            font-size: 4rem;
            margin-bottom: 20px;
            display: block;
        }

        .empty-state h3 {
            font-size: 1.5rem;
            margin-bottom: 10px;
            color: #4a5568;
        }

        .empty-state p {
            font-size: 1rem;
            line-height: 1.6;
        }

        .mood-selector {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            justify-content: center;
        }

        .mood-btn {
            background: white;
            border: 2px solid #e2e8f0;
            border-radius: 50px;
            padding: 10px 20px;
            cursor: pointer;
            font-size: 1.2rem;
            transition: all 0.3s ease;
        }

        .mood-btn:hover, .mood-btn.active {
            border-color: #667eea;
            background: #667eea;
            color: white;
            transform: scale(1.1);
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes slideInLeft {
            from {
                opacity: 0;
                transform: translateX(-30px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }
            
            .header h1 {
                font-size: 2.5rem;
            }
            
            .card {
                padding: 20px;
            }
            
            .search-container {
                flex-direction: column;
            }
            
            .stats {
                flex-direction: column;
                gap: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="floating-shapes">
        <div class="shape"></div>
        <div class="shape"></div>
        <div class="shape"></div>
    </div>

    <div class="container">
        <div class="header">
            <h1>✨ My Diary</h1>
            <p>あなたの特別な瞬間を美しく記録しましょう</p>
        </div>

        <div class="stats">
            <div class="stat-item">
                <span class="stat-number" id="totalEntries">0</span>
                <div class="stat-label">総記録数</div>
            </div>
            <div class="stat-item">
                <span class="stat-number" id="thisMonth">0</span>
                <div class="stat-label">今月の記録</div>
            </div>
            <div class="stat-item">
                <span class="stat-number" id="currentStreak">0</span>
                <div class="stat-label">連続記録日数</div>
            </div>
        </div>

        <div class="card">
            <h2><span class="emoji">✍️</span> 新しい日記を書く</h2>
            
            <div class="input-group">
                <input type="date" id="diaryDate" class="input-field">
            </div>
            
            <div class="input-group">
                <input type="text" id="diaryTitle" placeholder="今日はどんな日でしたか？" class="input-field">
            </div>
            
            <div class="input-group">
                <div class="mood-selector">
                    <div class="mood-btn" data-mood="😊">😊</div>
                    <div class="mood-btn" data-mood="😢">😢</div>
                    <div class="mood-btn" data-mood="😴">😴</div>
                    <div class="mood-btn" data-mood="😍">😍</div>
                    <div class="mood-btn" data-mood="😤">😤</div>
                    <div class="mood-btn" data-mood="🤔">🤔</div>
                </div>
            </div>
            
            <div class="input-group">
                <textarea id="diaryContent" placeholder="今日の出来事、感じたこと、学んだことを自由に書いてください..." class="input-field"></textarea>
            </div>
            
            <button id="saveDiary" class="btn primary">
                <span class="emoji">💾</span> 日記を保存
            </button>
        </div>

        <div class="card">
            <h2><span class="emoji">📖</span> 過去の日記</h2>
            
            <div class="search-container">
                <input type="text" id="searchKeyword" placeholder="キーワードや気分で検索..." class="input-field">
                <button id="searchDiary" class="btn secondary">🔍 検索</button>
            </div>
            
            <div id="diariesContainer">
                <div class="empty-state">
                    <span class="emoji">📝</span>
                    <h3>まだ日記がありません</h3>
                    <p>上のフォームから最初の日記を書いてみましょう！<br>あなたの素敵な思い出を記録していきましょう。</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const diaryDateInput = document.getElementById('diaryDate');
            const diaryTitleInput = document.getElementById('diaryTitle');
            const diaryContentInput = document.getElementById('diaryContent');
            const saveDiaryButton = document.getElementById('saveDiary');
            const diariesContainer = document.getElementById('diariesContainer');
            const searchKeywordInput = document.getElementById('searchKeyword');
            const searchDiaryButton = document.getElementById('searchDiary');
            const moodButtons = document.querySelectorAll('.mood-btn');
            const totalEntriesEl = document.getElementById('totalEntries');
            const thisMonthEl = document.getElementById('thisMonth');
            const currentStreakEl = document.getElementById('currentStreak');

            // 今日の日付をデフォルトで設定
            const today = new Date();
            diaryDateInput.value = today.toISOString().split('T')[0];

            let diaries = [];
            let selectedMood = '';

            // ローカルストレージから日記データを読み込む
            function loadDiaries() {
                const storedDiaries = localStorage.getItem('myDiaries');
                if (storedDiaries) {
                    try {
                        diaries = JSON.parse(storedDiaries);
                    } catch (e) {
                        console.error('日記データの読み込みに失敗しました:', e);
                        diaries = [];
                    }
                }
            }

            // 日記データをローカルストレージに保存する
            function saveDiaries() {
                try {
                    localStorage.setItem('myDiaries', JSON.stringify(diaries));
                } catch (e) {
                    console.error('日記データの保存に失敗しました:', e);
                    alert('日記の保存に失敗しました。ブラウザのストレージ容量を確認してください。');
                }
            }

            // 気分選択の処理
            moodButtons.forEach(btn => {
                btn.addEventListener('click', () => {
                    moodButtons.forEach(b => b.classList.remove('active'));
                    btn.classList.add('active');
                    selectedMood = btn.dataset.mood;
                });
            });

            // 統計を更新する関数
            function updateStats() {
                const currentDate = new Date();
                const currentMonth = currentDate.getMonth();
                const currentYear = currentDate.getFullYear();
                
                totalEntriesEl.textContent = diaries.length;
                
                const thisMonthEntries = diaries.filter(diary => {
                    const diaryDate = new Date(diary.date);
                    return diaryDate.getMonth() === currentMonth && diaryDate.getFullYear() === currentYear;
                });
                thisMonthEl.textContent = thisMonthEntries.length;
                
                // 連続記録日数の計算
                const sortedDiaries = [...diaries].sort((a, b) => new Date(b.date) - new Date(a.date));
                let streak = 0;
                let lastDate = null;
                
                for (const diary of sortedDiaries) {
                    const diaryDate = new Date(diary.date);
                    if (lastDate === null) {
                        lastDate = diaryDate;
                        streak = 1;
                    } else {
                        const diffTime = lastDate - diaryDate;
                        const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                        if (diffDays === 1) {
                            streak++;
                            lastDate = diaryDate;
                        } else {
                            break;
                        }
                    }
                }
                
                currentStreakEl.textContent = streak;
            }

            // 日記をレンダリングする関数
            function renderDiaries(filterKeyword = '') {
                const filteredDiaries = diaries.filter(diary => {
                    const lowerCaseKeyword = filterKeyword.toLowerCase();
                    return diary.title.toLowerCase().includes(lowerCaseKeyword) ||
                           diary.content.toLowerCase().includes(lowerCaseKeyword) ||
                           (diary.mood && diary.mood.includes(lowerCaseKeyword));
                });

                filteredDiaries.sort((a, b) => new Date(b.date) - new Date(a.date));

                if (filteredDiaries.length === 0) {
                    diariesContainer.innerHTML = `
                        <div class="empty-state">
                            <span class="emoji">${filterKeyword ? '🔍' : '📝'}</span>
                            <h3>${filterKeyword ? '検索結果がありません' : 'まだ日記がありません'}</h3>
                            <p>${filterKeyword ? '別のキーワードで検索してみてください' : '上のフォームから最初の日記を書いてみましょう！<br>あなたの素敵な思い出を記録していきましょう。'}</p>
                        </div>
                    `;
                    return;
                }

                diariesContainer.innerHTML = filteredDiaries.map(diary => `
                    <div class="diary-item">
                        <div class="date">
                            📅 ${new Date(diary.date).toLocaleDateString('ja-JP')}
                            ${diary.mood ? `<span style="margin-left: 10px;">${diary.mood}</span>` : ''}
                        </div>
                        <h3>${diary.title}</h3>
                        <p>${diary.content.replace(/\n/g, '<br>')}</p>
                        <div class="actions">
                            <button class="btn danger small delete-btn" data-id="${diary.id}">
                                🗑️ 削除
                            </button>
                        </div>
                    </div>
                `).join('');

                // 削除ボタンにイベントリスナーを設定
                document.querySelectorAll('.delete-btn').forEach(button => {
                    button.addEventListener('click', (event) => {
                        if (confirm('本当にこの日記を削除しますか？')) {
                            const diaryIdToDelete = event.target.dataset.id;
                            deleteDiary(diaryIdToDelete);
                        }
                    });
                });
            }

            // 日記を保存する関数
            saveDiaryButton.addEventListener('click', () => {
                const date = diaryDateInput.value;
                const title = diaryTitleInput.value.trim();
                const content = diaryContentInput.value.trim();

                if (!date || !title || !content) {
                    alert('日付、タイトル、内容をすべて入力してください。');
                    return;
                }

                const newDiary = {
                    id: Date.now().toString(),
                    date: date,
                    title: title,
                    content: content,
                    mood: selectedMood
                };

                diaries.push(newDiary);
                saveDiaries(); // ローカルストレージに保存

                // フォームをリセット
                diaryTitleInput.value = '';
                diaryContentInput.value = '';
                selectedMood = '';
                moodButtons.forEach(btn => btn.classList.remove('active'));

                // 成功メッセージ
                const originalText = saveDiaryButton.innerHTML;
                saveDiaryButton.innerHTML = '✅ 保存完了！';
                saveDiaryButton.disabled = true;
                
                setTimeout(() => {
                    saveDiaryButton.innerHTML = originalText;
                    saveDiaryButton.disabled = false;
                }, 2000);

                renderDiaries();
                updateStats();
            });

            // 日記を削除する関数
            function deleteDiary(idToDelete) {
                diaries = diaries.filter(diary => diary.id !== idToDelete);
                saveDiaries(); // ローカルストレージに保存
                renderDiaries();
                updateStats();
            }

            // 検索機能
            searchDiaryButton.addEventListener('click', () => {
                const keyword = searchKeywordInput.value.trim();
                renderDiaries(keyword);
            });

            searchKeywordInput.addEventListener('input', () => {
                if (searchKeywordInput.value.trim() === '') {
                    renderDiaries();
                }
            });

            // Enterキーでの検索
            searchKeywordInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    const keyword = searchKeywordInput.value.trim();
                    renderDiaries(keyword);
                }
            });

            // 初期化：ローカルストレージからデータを読み込んで表示
            loadDiaries();
            renderDiaries();
            updateStats();
        });
    </script>
</body>
</html>