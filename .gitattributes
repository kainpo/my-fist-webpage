<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>日記アプリ ユースケース図</title>
    <script type="module">
        import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.js';
        mermaid.initialize({ startOnLoad: true });
    </script>
    <style>
        body {
            font-family: sans-serif;
            margin: 20px;
            background-color: #f4f4f4;
            color: #333;
        }
        h1 {
            color: #0056b3;
        }
        .mermaid {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            overflow-x: auto; /* 図がはみ出す場合にスクロールを可能にする */
        }
    </style>
</head>
<body>
    <h1>日記アプリ ユースケース図</h1>

    <div class="mermaid">
        graph TD
            A[ユーザー] --> B(日記を記録する)
            A --> C(過去の日記を閲覧する)
            A --> D(健康情報を記録する)
            A --> E(運動記録を記録する)
            A --> F(消費カロリーを確認する)
            A --> G(水分補給のアラートを受け取る)

            B --> H{日付を選択する}
            B --> I{出来事を入力する}
            C --> J{日付やキーワードで検索する}

            D --> K{食事内容を記録する}
            D --> L{水分摂取量を記録する}
            D --> M{睡眠時間を記録する}

            E --> N{運動の種類を選択する}
            E --> O{運動時間を記録する}
            E --> P{運動強度を入力する}
    </div>

    <p>上記は日記アプリのユーザーが利用できる機能を表すユースケース図です。</p>
</body>
</html>