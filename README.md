<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Портал "Буквоежка"</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f5f5f5;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        h1 {
            text-align: center;
            color: #333;
        }
        
        .form-group {
            margin: 15px 0;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        
        input {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        
        button {
            background: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin: 5px;
        }
        
        button:hover {
            background: #45a049;
        }
        
        .tab-buttons {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .tab-buttons button {
            background: #ddd;
            color: black;
        }
        
        .tab-buttons button.active {
            background: #4CAF50;
            color: white;
        }
        
        .hidden {
            display: none;
        }
        
        .book-item {
            border: 1px solid #ddd;
            padding: 10px;
            margin: 10px 0;
            background: #f9f9f9;
            border-radius: 5px;
        }
        
        .admin-section {
            background: #ffe6e6;
            border: 1px solid #ff9999;
            padding: 15px;
            margin: 20px 0;
            border-radius: 5px;
        }
        
        .user-info {
            background: #e6f3ff;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
        }
        
        .section {
            margin: 30px 0;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Портал "Буквоежка"</h1>
        
        <!-- Раздел авторизации -->
        <div id="authSection">
            <div class="tab-buttons">
                <button id="loginTab" class="active" onclick="showTab('login')">Вход</button>
                <button id="registerTab" onclick="showTab('register')">Регистрация</button>
            </div>
            
            <!-- Форма входа -->
            <div id="loginForm">
                <h2>Вход в систему</h2>
                <div class="form-group">
                    <label>Логин или Email:</label>
                    <input type="text" id="loginEmail" placeholder="Введите логин или email">
                </div>
                <div class="form-group">
                    <label>Пароль:</label>
                    <input type="password" id="loginPassword" placeholder="Введите пароль">
                </div>
                <button onclick="login()">Войти</button>
            </div>
            
            <!-- Форма регистрации -->
            <div id="registerForm" class="hidden">
                <h2>Регистрация</h2>
                <div class="form-group">
                    <label>ФИО:</label>
                    <input type="text" id="regName" placeholder="Введите ФИО">
                </div>
                <div class="form-group">
                    <label>Телефон:</label>
                    <input type="text" id="regPhone" placeholder="Введите телефон">
                </div>
                <div class="form-group">
                    <label>Email:</label>
                    <input type="email" id="regEmail" placeholder="Введите email">
                </div>
                <div class="form-group">
                    <label>Логин:</label>
                    <input type="text" id="regLogin" placeholder="Введите логин">
                </div>
                <div class="form-group">
                    <label>Пароль:</label>
                    <input type="password" id="regPassword" placeholder="Введите пароль">
                </div>
                <button onclick="register()">Зарегистрироваться</button>
            </div>
        </div>
        
        <!-- Основной контент -->
        <div id="mainContent" class="hidden">
            <div class="user-info">
                <p><strong>Пользователь:</strong> <span id="userName"></span></p>
                <button onclick="logout()">Выйти</button>
            </div>
            
            <!-- Мои книги -->
            <div class="section">
                <h2>Мои книги</h2>
                <div class="form-group">
                    <label>Автор:</label>
                    <input type="text" id="bookAuthor" placeholder="Автор книги">
                </div>
                <div class="form-group">
                    <label>Название:</label>
                    <input type="text" id="bookTitle" placeholder="Название книги">
                </div>
                <button onclick="addBook()">Добавить книгу</button>
                <div id="myBooks"></div>
            </div>
            
            <!-- Поиск книг -->
            <div class="section">
                <h2>Поиск книг</h2>
                <div class="form-group">
                    <input type="text" id="searchInput" placeholder="Введите название или автора">
                    <button onclick="searchBooks()">Найти</button>
                </div>
                <div id="searchResults"></div>
            </div>
            
            <!-- Список желаний -->
            <div class="section">
                <h2>Мой список желаний</h2>
                <div class="form-group">
                    <label>Автор:</label>
                    <input type="text" id="wishAuthor" placeholder="Автор желаемой книги">
                </div>
                <div class="form-group">
                    <label>Название:</label>
                    <input type="text" id="wishTitle" placeholder="Название желаемой книги">
                </div>
                <button onclick="addWish()">Добавить в желания</button>
                <div id="myWishes"></div>
            </div>
            
            <!-- Мои заявки -->
            <div class="section">
                <h2>Мои заявки</h2>
                <div id="myRequests"></div>
            </div>
            
            <!-- Панель администратора -->
            <div id="adminPanel" class="admin-section hidden">
                <h2>Панель администратора</h2>
                <button onclick="showAllUsers()">Показать всех пользователей</button>
                <button onclick="showAllBooks()">Показать все книги</button>
                <div id="adminContent"></div>
            </div>
        </div>
    </div>

    <script>
        // Данные в памяти
        let users = [
            {id: 1, name: "Администратор", phone: "123456789", email: "admin@test.ru", login: "admin", password: "123", isAdmin: true}
        ];
        let books = [];
        let wishes = [];
        let requests = [];
        let currentUser = null;

        // Переключение вкладок
        function showTab(tab) {
            if (tab === 'login') {
                document.getElementById('loginForm').classList.remove('hidden');
                document.getElementById('registerForm').classList.add('hidden');
                document.getElementById('loginTab').classList.add('active');
                document.getElementById('registerTab').classList.remove('active');
            } else {
                document.getElementById('loginForm').classList.add('hidden');
                document.getElementById('registerForm').classList.remove('hidden');
                document.getElementById('loginTab').classList.remove('active');
                document.getElementById('registerTab').classList.add('active');
            }
        }

        // Вход
        function login() {
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;
            
            if (!email || !password) {
                alert('Заполните все поля');
                return;
            }
            
            const user = users.find(u => (u.email === email || u.login === email) && u.password === password);
            
            if (user) {
                currentUser = user;
                document.getElementById('authSection').classList.add('hidden');
                document.getElementById('mainContent').classList.remove('hidden');
                document.getElementById('userName').textContent = user.name;
                
                if (user.isAdmin) {
                    document.getElementById('adminPanel').classList.remove('hidden');
                }
                
                loadData();
            } else {
                alert('Неверные данные');
            }
        }

        // Регистрация
        function register() {
            const name = document.getElementById('regName').value;
            const phone = document.getElementById('regPhone').value;
            const email = document.getElementById('regEmail').value;
            const login = document.getElementById('regLogin').value;
            const password = document.getElementById('regPassword').value;
            
            if (!name || !phone || !email || !login || !password) {
                alert('Заполните все поля');
                return;
            }
            
            if (users.find(u => u.email === email || u.login === login)) {
                alert('Пользователь уже существует');
                return;
            }
            
            users.push({
                id: users.length + 1,
                name: name,
                phone: phone,
                email: email,
                login: login,
                password: password,
                isAdmin: false
            });
            
            alert('Регистрация успешна');
            showTab('login');
        }

        // Выход
        function logout() {
            currentUser = null;
            document.getElementById('authSection').classList.remove('hidden');
            document.getElementById('mainContent').classList.add('hidden');
            document.getElementById('adminPanel').classList.add('hidden');
        }

        // Добавить книгу
        function addBook() {
            const author = document.getElementById('bookAuthor').value;
            const title = document.getElementById('bookTitle').value;
            
            if (!author || !title) {
                alert('Заполните все поля');
                return;
            }
            
            books.push({
                id: books.length + 1,
                author: author,
                title: title,
                ownerId: currentUser.id,
                ownerName: currentUser.name,
                available: true
            });
            
            document.getElementById('bookAuthor').value = '';
            document.getElementById('bookTitle').value = '';
            loadMyBooks();
        }

        // Загрузить мои книги
        function loadMyBooks() {
            const myBooks = books.filter(b => b.ownerId === currentUser.id);
            const html = myBooks.map(book => 
                `<div class="book-item">
                    <strong>${book.title}</strong> - ${book.author}
                    <button onclick="deleteBook(${book.id})">Удалить</button>
                </div>`
            ).join('');
            document.getElementById('myBooks').innerHTML = html || '<p>У вас нет книг</p>';
        }

        // Удалить книгу
        function deleteBook(id) {
            books = books.filter(b => b.id !== id);
            loadMyBooks();
        }

        // Поиск книг
        function searchBooks() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            if (!query) {
                alert('Введите запрос для поиска');
                return;
            }
            
            const results = books.filter(b => 
                b.ownerId !== currentUser.id && 
                b.available &&
                (b.title.toLowerCase().includes(query) || b.author.toLowerCase().includes(query))
            );
            
            const html = results.map(book => 
                `<div class="book-item">
                    <strong>${book.title}</strong> - ${book.author}<br>
                    Владелец: ${book.ownerName}
                    <button onclick="requestBook(${book.id})">Запросить</button>
                </div>`
            ).join('');
            document.getElementById('searchResults').innerHTML = html || '<p>Книги не найдены</p>';
        }

        // Запросить книгу
        function requestBook(bookId) {
            const book = books.find(b => b.id === bookId);
            requests.push({
                id: requests.length + 1,
                bookId: book.id,
                bookTitle: book.title,
                requesterId: currentUser.id,
                requesterName: currentUser.name,
                ownerId: book.ownerId,
                ownerName: book.ownerName,
                status: 'pending'
            });
            alert('Запрос отправлен');
            loadRequests();
        }

        // Добавить желание
        function addWish() {
            const author = document.getElementById('wishAuthor').value;
            const title = document.getElementById('wishTitle').value;
            
            if (!author || !title) {
                alert('Заполните все поля');
                return;
            }
            
            wishes.push({
                id: wishes.length + 1,
                author: author,
                title: title,
                userId: currentUser.id
            });
            
            document.getElementById('wishAuthor').value = '';
            document.getElementById('wishTitle').value = '';
            loadWishes();
        }

        // Загрузить желания
        function loadWishes() {
            const myWishes = wishes.filter(w => w.userId === currentUser.id);
            const html = myWishes.map(wish => 
                `<div class="book-item">
                    <strong>${wish.title}</strong> - ${wish.author}
                    <button onclick="deleteWish(${wish.id})">Удалить</button>
                </div>`
            ).join('');
            document.getElementById('myWishes').innerHTML = html || '<p>Список желаний пуст</p>';
        }

        // Удалить желание
        function deleteWish(id) {
            wishes = wishes.filter(w => w.id !== id);
            loadWishes();
        }

        // Загрузить заявки
        function loadRequests() {
            const myRequests = requests.filter(r => r.requesterId === currentUser.id || r.ownerId === currentUser.id);
            const html = myRequests.map(req => {
                const isOwner = req.ownerId === currentUser.id;
                return `<div class="book-item">
                    <strong>${req.bookTitle}</strong><br>
                    ${isOwner ? `Запросил: ${req.requesterName}` : `Владелец: ${req.ownerName}`}<br>
                    Статус: ${req.status === 'pending' ? 'Ожидает' : req.status === 'approved' ? 'Одобрено' : 'Отклонено'}
                    ${isOwner && req.status === 'pending' ? 
                        `<br><button onclick="approveRequest(${req.id})">Одобрить</button>
                         <button onclick="rejectRequest(${req.id})">Отклонить</button>` : ''}
                </div>`;
            }).join('');
            document.getElementById('myRequests').innerHTML = html || '<p>Заявок нет</p>';
        }

        // Одобрить заявку
        function approveRequest(id) {
            const req = requests.find(r => r.id === id);
            req.status = 'approved';
            const book = books.find(b => b.id === req.bookId);
            book.available = false;
            loadRequests();
        }

        // Отклонить заявку
        function rejectRequest(id) {
            const req = requests.find(r => r.id === id);
            req.status = 'rejected';
            loadRequests();
        }

        // Показать всех пользователей (админ)
        function showAllUsers() {
            if (!currentUser.isAdmin) return;
            const html = users.map(user => 
                `<div class="book-item">
                    <strong>${user.name}</strong><br>
                    Email: ${user.email}, Телефон: ${user.phone}
                    ${!user.isAdmin ? `<button onclick="deleteUser(${user.id})">Удалить</button>` : ''}
                </div>`
            ).join('');
            document.getElementById('adminContent').innerHTML = '<h3>Все пользователи:</h3>' + html;
        }

        // Показать все книги (админ)
        function showAllBooks() {
            if (!currentUser.isAdmin) return;
            const html = books.map(book => 
                `<div class="book-item">
                    <strong>${book.title}</strong> - ${book.author}<br>
                    Владелец: ${book.ownerName}
                    <button onclick="adminDeleteBook(${book.id})">Удалить</button>
                </div>`
            ).join('');
            document.getElementById('adminContent').innerHTML = '<h3>Все книги:</h3>' + html;
        }

        // Удалить пользователя (админ)
        function deleteUser(id) {
            users = users.filter(u => u.id !== id);
            showAllUsers();
        }

        // Удалить книгу (админ)
        function adminDeleteBook(id) {
            books = books.filter(b => b.id !== id);
            showAllBooks();
        }

        // Загрузить все данные
        function loadData() {
            loadMyBooks();
            loadWishes();
            loadRequests();
        }
    </script>
</body>
</html>
