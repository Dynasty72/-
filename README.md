<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>羽球活動報名</title>
    <link rel="stylesheet" href="style.css">
    <script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.0.0/firebase-database.js"></script>
</head>
<body>
    <header>
        <h1>羽球活動報名</h1>
    </header>

    <section id="registration-data">
        <h2>報名資料</h2>
        <table id="registrations-table">
            <thead>
                <tr>
                    <th>姓名</th>
                    <th>電子郵件</th>
                    <th>技能水平</th>
                    <th>聯絡電話</th>
                </tr>
            </thead>
            <tbody>
                <!-- 資料會在這裡動態顯示 -->
            </tbody>
        </table>
    </section>
    table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
      }

    table, th, td {
    border: 1px solid #ccc;
    }

    th, td {
    padding: 8px;
    text-align: left;
    }

    th {
    background-color: #f2f2f2;
    }


    <script>
        // Firebase 配置
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
            databaseURL: "https://YOUR_PROJECT_ID.firebaseio.com",
            projectId: "YOUR_PROJECT_ID",
            storageBucket: "YOUR_PROJECT_ID.appspot.com",
            messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
            appId: "YOUR_APP_ID"
        };

        // 初始化 Firebase
        const app = firebase.initializeApp(firebaseConfig);
        const database = firebase.database(app);

        // 讀取資料並顯示
        const registrationsRef = database.ref('registrations');
        registrationsRef.on('value', function(snapshot) {
            const registrations = snapshot.val();
            const tableBody = document.getElementById("registrations-table").getElementsByTagName('tbody')[0];

            // 清空表格
            tableBody.innerHTML = '';

            // 檢查是否有資料
            if (registrations) {
                // 逐筆遍歷資料並顯示
                for (const key in registrations) {
                    if (registrations.hasOwnProperty(key)) {
                        const reg = registrations[key];
                        const row = tableBody.insertRow();

                        // 新增資料列
                        const cell1 = row.insertCell(0);
                        const cell2 = row.insertCell(1);
                        const cell3 = row.insertCell(2);
                        const cell4 = row.insertCell(3);

                        // 填充資料
                        cell1.textContent = reg.name;
                        cell2.textContent = reg.email;
                        cell3.textContent = reg.skillLevel;
                        cell4.textContent = reg.phone;
                    }
                }
            } else {
                // 如果沒有資料，顯示一條提示信息
                const row = tableBody.insertRow();
                const cell = row.insertCell(0);
                cell.colSpan = 4;
                cell.textContent = "目前沒有報名資料";
            }
        });
    </script>

</body>
</html>
