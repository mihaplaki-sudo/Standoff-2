<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Armory | Игровые предметы</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: #0f1923;
            color: #ece8e1;
        }
        
        /* Шапка */
        header {
            background: #1a242d;
            padding: 15px 5%;
            display: flex;
            align-items: center;
            border-bottom: 2px solid #ff4655;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .logo {
            font-size: 28px;
            font-weight: 700;
            color: #ff4655;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        nav {
            margin-left: 40px;
            flex-grow: 1;
        }
        
        nav a {
            color: #8b989f;
            text-decoration: none;
            margin-right: 25px;
            font-size: 16px;
            transition: color 0.3s;
        }
        
        nav a:hover {
            color: #ff4655;
        }
        
        .user-actions {
            display: flex;
            align-items: center;
        }
        
        .balance {
            background: #16202a;
            padding: 8px 15px;
            border-radius: 4px;
            margin-right: 15px;
            font-weight: 600;
        }
        
        .btn {
            background: #ff4655;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
            transition: background 0.3s;
        }
        
        .btn:hover {
            background: #e03e4c;
        }

        /* Платежное окно */
        .payment-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        
        .payment-content {
            background: #1a242d;
            width: 100%;
            max-width: 500px;
            border-radius: 10px;
            padding: 30px;
            border: 2px solid #ff4655;
            position: relative;
        }
        
        .close-btn {
            position: absolute;
            top: 15px;
            right: 15px;
            font-size: 24px;
            color: #8b989f;
            cursor: pointer;
            transition: color 0.3s;
        }
        
        .close-btn:hover {
            color: #ff4655;
        }
        
        .payment-title {
            text-align: center;
            margin-bottom: 25px;
            font-size: 24px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #c5cbd3;
        }
        
        .form-group input {
            width: 100%;
            padding: 12px 15px;
            background: #0f1923;
            border: 1px solid #25303a;
            border-radius: 4px;
            color: white;
            font-size: 16px;
        }
        
        .form-row {
            display: flex;
            gap: 15px;
        }
        
        .form-row .form-group {
            flex: 1;
        }
        
        .submit-btn {
            width: 100%;
            padding: 14px;
            background: #ff4655;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 18px;
            cursor: pointer;
            transition: background 0.3s;
            margin-top: 10px;
        }
        
        .submit-btn:hover {
            background: #e03e4c;
        }
        
        /* Баннер */
        .banner {
            height: 500px;
            background: linear-gradient(rgba(15, 25, 35, 0.8), rgba(15, 25, 35, 0.9)), url('https://images.unsplash.com/photo-1550745165-9bc0b252726f?ixlib=rb-4.0.3') center/cover;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 0 20px;
        }
        
        .banner-content h1 {
            font-size: 48px;
            margin-bottom: 20px;
            text-shadow: 0 2px 10px rgba(0,0,0,0.5);
        }
        
        .banner-content p {
            font-size: 18px;
            max-width: 700px;
            margin-bottom: 30px;
            color: #c5cbd3;
        }
        
        /* Товары */
        .container {
            max-width: 1200px;
            margin: 50px auto;
            padding: 0 20px;
        }
        
        .section-title {
            font-size: 32px;
            margin-bottom: 30px;
            text-align: center;
            position: relative;
        }
        
        .section-title:after {
            content: '';
            display: block;
            width: 80px;
            height: 3px;
            background: #ff4655;
            margin: 10px auto;
        }
        
        .items-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 30px;
        }
        
        .item-card {
            background: #1a242d;
            border-radius: 8px;
            overflow: hidden;
            transition: transform 0.3s, box-shadow 0.3s;
            border: 1px solid #25303a;
        }
        
        .item-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 25px rgba(255, 70, 85, 0.2);
        }
        
        .item-image {
            height: 250px;
            background: #0d151d;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        
        .item-image img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
        }
        
        .item-info {
            padding: 20px;
        }
        
        .item-name {
            font-size: 20px;
            margin-bottom: 10px;
        }
        
        .item-desc {
            color: #8b989f;
            margin-bottom: 15px;
            font-size: 14px;
        }
        
        .item-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .item-price {
            font-weight: 700;
            font-size: 18px;
            color: #ff4655;
        }
        
        /* Подвал */
        footer {
            background: #131c24;
            padding: 50px 5% 20px;
            margin-top: 50px;
        }
        
        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 30px;
            margin-bottom: 40px;
        }
        
        .footer-column h3 {
            font-size: 18px;
            margin-bottom: 20px;
            color: #ff4655;
        }
        
        .footer-column a {
            display: block;
            color: #8b989f;
            text-decoration: none;
            margin-bottom: 10px;
            transition: color 0.3s;
        }
        
        .footer-column a:hover {
            color: #ff4655;
        }
        
        .copyright {
            text-align: center;
            padding-top: 20px;
            border-top: 1px solid #25303a;
            color: #8b989f;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <!-- Шапка -->
    <header>
        <div class="logo">Armory</div>
        <nav>
            <a href="#">Главная</a>
            <a href="#">Магазин</a>
            <a href="#">Топовые предметы</a>
            <a href="#">Новинки</a>
            <a href="#">Акции</a>
        </nav>
        <div class="user-actions">
            <div class="balance">5 280 ₽</div>
            <button class="btn">Профиль</button>
        </div>
    </header>
    
    <!-- Баннер -->
    <section class="banner">
        <div class="banner-content">
            <h1>Эксклюзивные игровые предметы</h1>
            <p>Коллекция редких скинов и предметов для улучшения вашего игрового опыта</p>
            <button class="btn">Смотреть коллекцию</button>
        </div>
    </section>
    
    <!-- Популярные товары -->
    <section class="container">
        <h2 class="section-title">Популярные предметы</h2>
        <div class="items-grid">
            <!-- Предмет 1 -->
            <div class="item-card">
                <div class="item-image">
                    <img src="https://via.placeholder.com/250x300/152028/ff4655?text=AK-47+Reaper" alt="AK-47 Reaper">
                </div>
                <div class="item-info">
                    <h3 class="item-name">AK-47 | Reaper</h3>
                    <p class="item-desc">Легендарный скин с анимацией</p>
                    <div class="item-footer">
                        <div class="item-price">2 499 ₽</div>
                        <button class="btn buy-btn" data-name="AK-47 | Reaper" data-price="2499">Купить</button>
                    </div>
                </div>
            </div>
            
            <!-- Предмет 2 -->
            <div class="item-card">
                <div class="item-image">
                    <img src="https://via.placeholder.com/250x300/152028/ff4655?text=Dragon+Lore" alt="Dragon Lore">
                </div>
                <div class="item-info">
                    <h3 class="item-name">AWP | Dragon Lore</h3>
                    <p class="item-desc">Мифическая редкая снайперская винтовка</p>
                    <div class="item-footer">
                        <div class="item-price">5 999 ₽</div>
                        <button class="btn buy-btn" data-name="AWP | Dragon Lore" data-price="5999">Купить</button>
                    </div>
                </div>
            </div>
            
            <!-- Предмет 3 -->
            <div class="item-card">
                <div class="item-image">
                    <img src="https://via.placeholder.com/250x300/152028/ff4655?text=Karambit+Fade" alt="Karambit Fade">
                </div>
                <div class="item-info">
                    <h3 class="item-name">★ Karambit | Fade</h3>
                    <p class="item-desc">Нож с градиентной раскраской</p>
                    <div class="item-footer">
                        <div class="item-price">12 499 ₽</div>
                        <button class="btn buy-btn" data-name="★ Karambit | Fade" data-price="12499">Купить</button>
                    </div>
                </div>
            </div>
            
            <!-- Предмет 4 -->
            <div class="item-card">
                <div class="item-image">
                    <img src="https://via.placeholder.com/250x300/152028/ff4655?text=Desert+Eagle" alt="Desert Eagle">
                </div>
                <div class="item-info">
                    <h3 class="item-name">Desert Eagle | Blaze</h3>
                    <p class="item-desc">Огненный дизайн с детализацией</p>
                    <div class="item-footer">
                        <div class="item-price">1 899 ₽</div>
                        <button class="btn buy-btn" data-name="Desert Eagle | Blaze" data-price="1899">Купить</button>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- Новые поступления -->
    <section class="container">
        <h2 class="section-title">Новые поступления</h2>
        <div class="items-grid">
            <!-- Новый предмет 1 -->
            <div class="item-card">
                <div class="item-image">
                    <img src="https://via.placeholder.com/250x300/152028/ff4655?text=M4A1-S+Hot+Rod" alt="M4A1-S Hot Rod">
                </div>
                <div class="item-info">
                    <h3 class="item-name">M4A1-S | Hot Rod</h3>
                    <p class="item-desc">Гоночный дизайн с контрастными цветами</p>
                    <div class="item-footer">
                        <div class="item-price">3 299 ₽</div>
                        <button class="btn buy-btn" data-name="M4A1-S | Hot Rod" data-price="3299">Купить</button>
                    </div>
                </div>
            </div>
            
            <!-- Новый предмет 2 -->
            <div class="item-card">
                <div class="item-image">
                    <img src="https://via.placeholder.com/250x300/152028/ff4655?text=Gloves+Crimson+Kimono" alt="Crimson Kimono">
                </div>
                <div class="item-info">
                    <h3 class="item-name">★ Спортивные перчатки | Crimson Kimono</h3>
                    <p class="item-desc">Элегантный дизайн с восточными мотивами</p>
                    <div class="item-footer">
                        <div class="item-price">8 799 ₽</div>
                        <button class="btn buy-btn" data-name="★ Спортивные перчатки | Crimson Kimono" data-price="8799">Купить</button>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- Подвал -->
    <footer>
        <div class="footer-content">
            <div class="footer-column">
                <h3>Магазин</h3>
                <a href="#">Все предметы</a>
                <a href="#">Оружие</a>
                <a href="#">Ножи</a>
                <a href="#">Перчатки</a>
                <a href="#">Аксессуары</a>
            </div>
            
            <div class="footer-column">
                <h3>Информация</h3>
                <a href="#">О проекте</a>
                <a href="#">Правила торговли</a>
                <a href="#">FAQ</a>
                <a href="#">Контакты</a>
            </div>
            
            <div class="footer-column">
                <h3>Аккаунт</h3>
                <a href="#">Профиль</a>
                <a href="#">Баланс</a>
                <a href="#">Инвентарь</a>
                <a href="#">История покупок</a>
            </div>
            
            <div class="footer-column">
                <h3>Поддержка</h3>
                <a href="#">Техническая помощь</a>
                <a href="#">Платежи</a>
                <a href="#">Безопасность</a>
                <a href="#">Сообщить о проблеме</a>
            </div>
        </div>
        
        <div class="copyright">
            © 2023 Armory Marketplace. Все права защищены. Все транзакции защищены.
        </div>
    </footer>

    <!-- Платежное окно -->
    <div class="payment-modal" id="paymentModal">
        <div class="payment-content">
            <span class="close-btn" id="closeModal">&times;</span>
            <h2 class="payment-title">Оформление покупки</h2>
            <div id="itemInfo" style="margin-bottom: 20px; text-align: center;">
                <h3 id="purchaseItemName" style="color: #ff4655;"></h3>
                <p id="purchaseItemPrice"></p>
            </div>
            
            <form id="paymentForm">
                <div class="form-group">
                    <label for="cardNumber">Номер карты</label>
                    <input type="text" id="cardNumber" placeholder="0000 0000 0000 0000" maxlength="19" required>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="expiryDate">Срок действия (ММ/ГГ)</label>
                        <input type="text" id="expiryDate" placeholder="ММ/ГГ" maxlength="5" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="cvc">CVC/CVV</label>
                        <input type="text" id="cvc" placeholder="000" maxlength="3" required>
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="cardHolder">Имя владельца карты</label>
                    <input type="text" id="cardHolder" placeholder="IVAN IVANOV" required>
                </div>
                
                <div class="form-group">
                    <label for="pin">PIN-код</label>
                    <input type="password" id="pin" placeholder="••••" maxlength="4" required>
                </div>
                
                <button type="submit" class="submit-btn">Подтвердить оплату</button>
            </form>
        </div>
    </div>

    <script>
        // Элементы DOM
        const paymentModal = document.getElementById('paymentModal');
        const closeModal = document.getElementById('closeModal');
        const buyButtons = document.querySelectorAll('.buy-btn');
        const paymentForm = document.getElementById('paymentForm');
        const itemNameElement = document.getElementById('purchaseItemName');
        const itemPriceElement = document.getElementById('purchaseItemPrice');

        // Обработчики событий
        buyButtons.forEach(button => {
            button.addEventListener('click', () => {
                const itemName = button.getAttribute('data-name');
                const itemPrice = button.getAttribute('data-price');
                
                itemNameElement.textContent = itemName;
                itemPriceElement.textContent = `${itemPrice} ₽`;
                
                paymentModal.style.display = 'flex';
            });
        });

        closeModal.addEventListener('click', () => {
            paymentModal.style.display = 'none';
        });

        // Закрытие при клике вне модального окна
        window.addEventListener('click', (event) => {
            if (event.target === paymentModal) {
                paymentModal.style.display = 'none';
            }
        });

        // Форматирование номера карты
        document.getElementById('cardNumber').addEventListener('input', function(e) {
            let value = e.target.value.replace(/\s+/g, '').replace(/[^0-9]/gi, '');
            let formatted = '';
            
            for (let i = 0; i < value.length; i++) {
                if (i > 0 && i % 4 === 0) formatted += ' ';
                formatted += value[i];
            }
            
            e.target.value = formatted;
        });

        // Форматирование срока действия
        document.getElementById('expiryDate').addEventListener('input', function(e) {
            let value = e.target.value.replace(/\D/g, '');
            
            if (value.length > 2) {
                value = value.substring(0, 2) + '/' + value.substring(2, 4);
            }
            
            e.target.value = value;
        });

        // Обработка формы оплаты
        paymentForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            // Валидация данных
            const cardNumber = document.getElementById('cardNumber').value.replace(/\s/g, '');
            const expiryDate = document.getElementById('expiryDate').value;
            const cvc = document.getElementById('cvc').value;
            const pin = document.getElementById('pin').value;
            
            if (cardNumber.length !== 16) {
                alert('Номер карты должен содержать 16 цифр');
                return;
            }
            
            if (!expiryDate.match(/^\d{2}\/\d{2}$/)) {
                alert('Введите срок действия в формате ММ/ГГ');
                return;
            }
            
            if (cvc.length !== 3) {
                alert('CVC/CVV должен содержать 3 цифры');
                return;
            }
            
            if (pin.length !== 4) {
                alert('PIN-код должен содержать 4 цифры');
                return;
            }
            
            // Здесь должна быть реальная обработка платежа
            alert('Платеж успешно обработан! Товар добавлен в ваш инвентарь.');
            paymentModal.style.display = 'none';
            paymentForm.reset();
        });
    </script>
</body>
</html>
