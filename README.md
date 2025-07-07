<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>シンプル日記アプリ (単一ファイル版)</title>
    <style>
        /* ここからstyle.cssの内容 */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f2f5;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
        }

        .container {
            background-color: #ffffff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            width: 90%;
            max-width: 800px;
            margin: 30px 0;
        }

        h1 {
            text-align: center;
            color: #4a90e2;
            margin-bottom: 30px;
        }

        h2 {
            color: #333;
            border-bottom: 1px solid #eee;
            padding-bottom: 10px;
            margin-top: 30px;
        }

        .input-field {
            width: calc(100% - 20px);
            padding: 12px 10px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            box-sizing: border-box; /* パディングを含めて幅を計算 */
        }

        textarea.input-field {
            resize: vertical;
            min-height: 100px;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s ease;
            margin-right: 10px;
        }

        .btn.primary {
            background-color: #4a90e2;
            color: white;
        }

        .btn.primary:hover {
            background-color: #357ABD;
        }

        .btn.secondary {
            background-color: #6c757d;
            color: white;
        }

        .btn.secondary:hover {
            background-color: #5a6268;
        }

        .diary-item {
            background-color: #f9f9f9;
            border: 1px solid #eee;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
        }

        .diary-item h3 {
            margin-top: 0;
            color: #0056b3;
        }

        .diary-item p {
            line-height: 1.6;
            color: #555;
        }

        .diary-item .date {
            font-size: 0.9em;
            color: #888;
            margin-bottom: 5px;
            display: block;
        }

        .diary-item .actions {
            margin-top: 10px;
            text-align: right;
        }

        .diary-item .actions .btn {
            padding: 8px 15px;
            font-size: 0.85rem;
        }

        .diary-item .actions .btn.danger {
            background-color: #dc3545;
            color: white;
        }

        .diary-item .actions .btn.danger:hover {
            background-color: #c82333;
        }
        /* ここまでstyle.cssの内容 */
    </style>
</head>
<body>
    <div class="container">
        <h1>日記アプリ</h1>

        <div class="diary-input">
            <h2>新しい日記を書く</h2>
            <input type="date" id="diaryDate" class="input-field">
            <input type="text" id="diaryTitle" placeholder="タイトル" class="input-field">
            <textarea id="diaryContent" placeholder="今日の出来事を記録しよう..." class="input-field"></textarea>
            <button id="saveDiary" class="btn primary">日記を保存</button>
        </div>

        <div class="diary-list">
            <h2>過去の日記</h2>
            <input type="text" id="searchKeyword" placeholder="キーワードで検索" class="input-field">
            <button id="searchDiary" class="btn secondary">検索</button>
            <ul id="diariesContainer">
                </ul>
        </div>
    </div>

    <script>
        /* ここからscript.jsの内容 */
        document.addEventListener('DOMContentLoaded', () => {
            const diaryDateInput = document.getElementById('diaryDate');
            const diaryTitleInput = document.getElementById('diaryTitle');
            const diaryContentInput = document.getElementById('diaryContent');
            const saveDiaryButton = document.getElementById('saveDiary');
            const diariesContainer = document.getElementById('diariesContainer');
            const searchKeywordInput = document.getElementById('searchKeyword');
            const searchDiaryButton = document.getElementById('searchDiary');

            // 今日の日付をデフォルトで設定
            const today = new Date();
            const year = today.getFullYear();
            const month = String(today.getMonth() + 1).padStart(2, '0');
            const day = String(today.getDate()).padStart(2, '0');
            diaryDateInput.value = `${year}-${month}-${day}`;

            let diaries = JSON.parse(localStorage.getItem('diaries')) || [];

            // 日記をレンダリングする関数
            function renderDiaries(filterKeyword = '') {
                diariesContainer.innerHTML = ''; // 一度クリア

                const filteredDiaries = diaries.filter(diary => {
                    const lowerCaseKeyword = filterKeyword.toLowerCase();
                    return diary.title.toLowerCase().includes(lowerCaseKeyword) ||
                           diary.content.toLowerCase().includes(lowerCaseKeyword);
                });

                // 日付が新しい順にソート
                filteredDiaries.sort((a, b) => new Date(b.date) - new Date(a.date));

                if (filteredDiaries.length === 0) {
                    const noEntry = document.createElement('p');
                    noEntry.textContent = filterKeyword ? '検索条件に一致する日記はありません。' : 'まだ日記がありません。';
                    diariesContainer.appendChild(noEntry);
                    return;
                }

                filteredDiaries.forEach((diary, index) => {
                    const li = document.createElement('li');
                    li.className = 'diary-item';
                    li.dataset.index = index; // 削除用に元のインデックスを保持

                    li.innerHTML = `
                        <span class="date">${diary.date}</span>
                        <h3>${diary.title}</h3>
                        <p>${diary.content.replace(/\n/g, '<br>')}</p>
                        <div class="actions">
                            <button class="btn danger delete-btn" data-id="${diary.id}">削除</button>
                        </div>
                    `;
                    diariesContainer.appendChild(li);
                });

                // 削除ボタンにイベントリスナーを設定
                document.querySelectorAll('.delete-btn').forEach(button => {
                    button.addEventListener('click', (event) => {
                        const diaryIdToDelete = event.target.dataset.id;
                        deleteDiary(diaryIdToDelete);
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
                    id: Date.now().toString(), // ユニークなID
                    date: date,
                    title: title,
                    content: content
                };

                diaries.push(newDiary);
                localStorage.setItem('diaries', JSON.stringify(diaries));

                diaryTitleInput.value = '';
                diaryContentInput.value = '';
                alert('日記が保存されました！');
                renderDiaries(); // リストを更新
            });

            // 日記を削除する関数
            function deleteDiary(idToDelete) {
                diaries = diaries.filter(diary => diary.id !== idToDelete);
                localStorage.setItem('diaries', JSON.stringify(diaries));
                renderDiaries(); // リストを更新
            }

            // 検索機能
            searchDiaryButton.addEventListener('click', () => {
                const keyword = searchKeywordInput.value.trim();
                renderDiaries(keyword);
            });

            searchKeywordInput.addEventListener('input', () => {
                if (searchKeywordInput.value.trim() === '') {
                    renderDiaries(); // 検索ボックスが空になったら全表示
                }
            });

            // 初期表示
            renderDiaries();
        });
        /* ここまでscript.jsの内容 */
    </script>
</body>
</html>