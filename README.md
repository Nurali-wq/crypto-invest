<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crypto Vision - Инвестиционная платформа</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', 'Roboto', sans-serif;
        }

        :root {
            --bg-primary: #121212;
            --bg-secondary: #1E1E1E;
            --bg-card: #252525;
            --accent-blue: #2962FF;
            --accent-green: #00C853;
            --accent-red: #FF5252;
            --text-primary: #E0E0E0;
            --text-secondary: #A0A0A0;
            --border: #424242;
        }

        body {
            background-color: var(--bg-primary);
            color: var(--text-primary);
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header */
        header {
            background-color: var(--bg-secondary);
            padding: 1rem 0;
            border-bottom: 1px solid var(--border);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logo h1 {
            font-size: 1.5rem;
            background: linear-gradient(90deg, var(--accent-blue), var(--accent-green));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .logo i {
            color: var(--accent-blue);
            font-size: 1.5rem;
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        nav a {
            color: var(--text-primary);
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
        }

        nav a:hover {
            color: var(--accent-blue);
        }

        .auth-buttons {
            display: flex;
            gap: 1rem;
        }

        .btn {
            padding: 0.5rem 1.5rem;
            border-radius: 4px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            border: none;
        }

        .btn-outline {
            background: transparent;
            border: 1px solid var(--accent-blue);
            color: var(--accent-blue);
        }

        .btn-primary {
            background: var(--accent-blue);
            color: white;
        }

        .btn-outline:hover {
            background: var(--accent-blue);
            color: white;
        }

        /* Hero Section */
        .hero {
            padding: 4rem 0;
            background: linear-gradient(135deg, var(--bg-secondary) 0%, var(--bg-primary) 100%);
            text-align: center;
        }

        .hero h2 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            line-height: 1.2;
        }

        .hero p {
            font-size: 1.2rem;
            color: var(--text-secondary);
            max-width: 700px;
            margin: 0 auto 2rem;
        }

        /* Market Overview */
        .market-overview {
            padding: 2rem 0;
        }

        .section-title {
            font-size: 1.8rem;
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .market-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .card {
            background-color: var(--bg-card);
            border-radius: 8px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border: 1px solid var(--border);
        }

        .card h3 {
            font-size: 1rem;
            color: var(--text-secondary);
            margin-bottom: 0.5rem;
        }

        .card .value {
            font-size: 1.5rem;
            font-weight: 600;
        }

        .positive {
            color: var(--accent-green);
        }

        .negative {
            color: var(--accent-red);
        }

        /* Crypto Table */
        .crypto-table {
            padding: 2rem 0;
        }

        .table-container {
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th, td {
            padding: 1rem;
            text-align: left;
            border-bottom: 1px solid var(--border);
        }

        th {
            color: var(--text-secondary);
            font-weight: 500;
        }

        .crypto-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .crypto-icon {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background-color: var(--bg-secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        /* Filters */
        .filters {
            padding: 1.5rem;
            background-color: var(--bg-card);
            border-radius: 8px;
            margin-bottom: 2rem;
        }

        .filter-row {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-bottom: 1rem;
        }

        .filter-group {
            flex: 1;
            min-width: 200px;
        }

        .filter-group label {
            display: block;
            margin-bottom: 0.5rem;
            color: var(--text-secondary);
        }

        .filter-group select, .filter-group input {
            width: 100%;
            padding: 0.7rem;
            background-color: var(--bg-secondary);
            border: 1px solid var(--border);
            border-radius: 4px;
            color: var(--text-primary);
        }

        /* Charts */
        .charts {
            padding: 2rem 0;
        }

        .chart-container {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 1.5rem;
        }

        .main-chart, .portfolio-chart {
            background-color: var(--bg-card);
            border-radius: 8px;
            padding: 1.5rem;
            border: 1px solid var(--border);
        }

        .chart-placeholder {
            height: 300px;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: var(--bg-secondary);
            border-radius: 4px;
            margin-top: 1rem;
        }

        /* Expert Recommendations */
        .recommendations {
            padding: 2rem 0;
        }

        .rec-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
        }

        .rec-card {
            background-color: var(--bg-card);
            border-radius: 8px;
            padding: 1.5rem;
            border: 1px solid var(--border);
        }

        .rec-header {
            display: flex;
            justify-content: between;
            align-items: center;
            margin-bottom: 1rem;
        }

        .rec-rating {
            background-color: var(--accent-green);
            color: white;
            padding: 0.3rem 0.7rem;
            border-radius: 4px;
            font-size: 0.9rem;
        }

        /* Footer */
        footer {
            background-color: var(--bg-secondary);
            padding: 3rem 0 1.5rem;
            margin-top: 3rem;
            border-top: 1px solid var(--border);
        }

        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .footer-column h3 {
            font-size: 1.2rem;
            margin-bottom: 1.5rem;
            color: var(--text-primary);
        }

        .footer-column ul {
            list-style: none;
        }

        .footer-column li {
            margin-bottom: 0.7rem;
        }

        .footer-column a {
            color: var(--text-secondary);
            text-decoration: none;
            transition: color 0.3s;
        }

        .footer-column a:hover {
            color: var(--accent-blue);
        }

        .copyright {
            text-align: center;
            padding-top: 1.5rem;
            border-top: 1px solid var(--border);
            color: var(--text-secondary);
            font-size: 0.9rem;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .chart-container {
                grid-template-columns: 1fr;
            }
            
            nav ul {
                display: none;
            }
            
            .hero h2 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">
                    <i class="fas fa-chart-line"></i>
                    <h1>Crypto Vision</h1>
                </div>
                <nav>
                    <ul>
                        <li><a href="#market">Рынок</a></li>
                        <li><a href="#crypto">Криптовалюты</a></li>
                        <li><a href="#companies">Компании</a></li>
                        <li><a href="#recommendations">Рекомендации</a></li>
                        <li><a href="#portfolio">Портфель</a></li>
                    </ul>
                </nav>
                <div class="auth-buttons">
                    <button class="btn btn-outline">Войти</button>
                    <button class="btn btn-primary">Регистрация</button>
                </div>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="container">
            <h2>Видеть крипторынок насквозь. Принимать выверенные решения.</h2>
            <p>Инвестиционная платформа с реальными данными по криптовалютам, компаниям и стартапам, фильтрацией по отраслям и честными экспертными рекомендациями.</p>
            <button class="btn btn-primary">Начать анализ</button>
        </div>
    </section>

    <!-- Market Overview -->
    <section class="market-overview" id="market">
        <div class="container">
            <h2 class="section-title"><i class="fas fa-globe"></i> Обзор рынка</h2>
            <div class="market-cards">
                <div class="card">
                    <h3>Общая капитализация</h3>
                    <div class="value">$2.34 трлн</div>
                    <div class="positive">+2.4%</div>
                </div>
                <div class="card">
                    <h3>Bitcoin (BTC)</h3>
                    <div class="value">$61,245.80</div>
                    <div class="positive">+1.8%</div>
                </div>
                <div class="card">
                    <h3>Ethereum (ETH)</h3>
                    <div class="value">$3,412.50</div>
                    <div class="positive">+3.2%</div>
                </div>
                <div class="card">
                    <h3>Индекс страха и жадности</h3>
                    <div class="value">76/100</div>
                    <div class="positive">Жадность</div>
                </div>
            </div>
        </div>
    </section>

    <!-- Crypto Table with Filters -->
    <section class="crypto-table" id="crypto">
        <div class="container">
            <h2 class="section-title"><i class="fas fa-list"></i> Криптовалюты</h2>
            
            <div class="filters">
                <div class="filter-row">
                    <div class="filter-group">
                        <label>Отрасль</label>
                        <select>
                            <option>Все отрасли</option>
                            <option>DeFi</option>
                            <option>NFT</option>
                            <option>Gaming</option>
                            <option>AI</option>
                            <option>Infrastructure</option>
                        </select>
                    </div>
                    <div class="filter-group">
                        <label>Капитализация</label>
                        <select>
                            <option>Любая</option>
                            <option>Менее $100M</option>
                            <option>$100M - $1B</option>
                            <option>Более $1B</option>
                        </select>
                    </div>
                    <div class="filter-group">
                        <label>Изменение цены</label>
                        <select>
                            <option>Любое</option>
                            <option>Растущие</option>
                            <option>Падающие</option>
                        </select>
                    </div>
                </div>
                <button class="btn btn-primary">Применить фильтры</button>
            </div>
            
            <div class="table-container">
                <table>
                    <thead>
                        <tr>
                            <th>Актив</th>
                            <th>Цена</th>
                            <th>Изменение (24ч)</th>
                            <th>Капитализация</th>
                            <th>Объем (24ч)</th>
                            <th>Отрасль</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>
                                <div class="crypto-info">
                                    <div class="crypto-icon">B</div>
                                    <div>Bitcoin (BTC)</div>
                                </div>
                            </td>
                            <td>$61,245.80</td>
                            <td class="positive">+1.8%</td>
                            <td>$1.21 трлн</td>
                            <td>$24.5 млрд</td>
                            <td>Store of Value</td>
                        </tr>
                        <tr>
                            <td>
                                <div class="crypto-info">
                                    <div class="crypto-icon">E</div>
                                    <div>Ethereum (ETH)</div>
                                </div>
                            </td>
                            <td>$3,412.50</td>
                            <td class="positive">+3.2%</td>
                            <td>$409.8 млрд</td>
                            <td>$14.2 млрд</td>
                            <td>Smart Contracts</td>
                        </tr>
                        <tr>
                            <td>
                                <div class="crypto-info">
                                    <div class="crypto-icon">U</div>
                                    <div>Uniswap (UNI)</div>
                                </div>
                            </td>
                            <td>$10.24</td>
                            <td class="positive">+5.7%</td>
                            <td>$6.1 млрд</td>
                            <td>$320 млн</td>
                            <td>DeFi</td>
                        </tr>
                        <tr>
                            <td>
                                <div class="crypto-info">
                                    <div class="crypto-icon">A</div>
                                    <div>Aave (AAVE)</div>
                                </div>
                            </td>
                            <td>$87.65</td>
                            <td class="negative">-2.1%</td>
                            <td>$1.3 млрд</td>
                            <td>$89 млн</td>
                            <td>DeFi</td>
                        </tr>
                        <tr>
                            <td>
                                <div class="crypto-info">
                                    <div class="crypto-icon">M</div>
                                    <div>Maker (MKR)</div>
                                </div>
                            </td>
                            <td>$2,541.30</td>
                            <td class="positive">+0.8%</td>
                            <td>$2.4 млрд</td>
                            <td>$45 млн</td>
                            <td>DeFi</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </section>

    <!-- Charts -->
    <section class="charts">
        <div class="container">
            <h2 class="section-title"><i class="fas fa-chart-bar"></i> Аналитика</h2>
            <div class="chart-container">
                <div class="main-chart">
                    <h3>BTC/USD График цены</h3>
                    <div class="chart-placeholder">
                        <canvas id="priceChart"></canvas>
                    </div>
                </div>
                <div class="portfolio-chart">
                    <h3>Распределение портфеля</h3>
                    <div class="chart-placeholder">
                        <canvas id="portfolioChart"></canvas>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Expert Recommendations -->
    <section class="recommendations" id="recommendations">
        <div class="container">
            <h2 class="section-title"><i class="fas fa-star"></i> Экспертные рекомендации</h2>
            <div class="rec-cards">
                <div class="rec-card">
                    <div class="rec-header">
                        <h3>Bitcoin (BTC)</h3>
                        <div class="rec-rating">Сильная покупка</div>
                    </div>
                    <p>Аналитики ожидают рост до $70,000 в ближайшие 3 месяца. Сильные on-chain метрики и институциональный интерес.</p>
                    <div style="margin-top: 1rem;">
                        <span class="positive">Цель: $70,000</span> | <span class="negative">Стоп-лосс: $58,000</span>
                    </div>
                </div>
                <div class="rec-card">
                    <div class="rec-header">
                        <h3>Ethereum (ETH)</h3>
                        <div class="rec-rating">Покупка</div>
                    </div>
                    <p>Обновление сети и рост DeFi способствуют фундаментальной стоимости. Рекомендуется накапливать на коррекциях.</p>
                    <div style="margin-top: 1rem;">
                        <span class="positive">Цель: $4,000</span> | <span class="negative">Стоп-лосс: $3,200</span>
                    </div>
                </div>
                <div class="rec-card">
                    <div class="rec-header">
                        <h3>Uniswap (UNI)</h3>
                        <div class="rec-rating">Умеренная покупка</div>
                    </div>
                    <p>Лидер в сегменте DEX с устойчивой моделью доходов. V4 обновление может стать катализатором роста.</p>
                    <div style="margin-top: 1rem;">
                        <span class="positive">Цель: $15.00</span> | <span class="negative">Стоп-лосс: $9.50</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-column">
                    <h3>Crypto Vision</h3>
                    <p>Инвестиционная платформа с реальными данными и честными экспертными рекомендациями.</p>
                </div>
                <div class="footer-column">
                    <h3>Навигация</h3>
                    <ul>
                        <li><a href="#market">Обзор рынка</a></li>
                        <li><a href="#crypto">Криптовалюты</a></li>
                        <li><a href="#companies">Компании</a></li>
                        <li><a href="#recommendations">Рекомендации</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Ресурсы</h3>
                    <ul>
                        <li><a href="#">Блог</a></li>
                        <li><a href="#">Обучение</a></li>
                        <li><a href="#">FAQ</a></li>
                        <li><a href="#">Поддержка</a></li>
                    </ul>
                </div>
                <div class="footer-column">
                    <h3>Подписка</h3>
                    <p>Получайте уведомления о новых рекомендациях и рыночных инсайтах.</p>
                    <div style="display: flex; margin-top: 1rem;">
                        <input type="email" placeholder="Ваш email" style="flex: 1; padding: 0.7rem; background: var(--bg-primary); border: 1px solid var(--border); color: var(--text-primary); border-radius: 4px 0 0 4px;">
                        <button class="btn btn-primary" style="border-radius: 0 4px 4px 0;">OK</button>
                    </div>
                </div>
            </div>
            <div class="copyright">
                <p>&copy; 2023 Crypto Vision. Все права защищены.</p>
            </div>
        </div>
    </footer>

    <script>
        // Price Chart
        const priceCtx = document.getElementById('priceChart').getContext('2d');
        const priceChart = new Chart(priceCtx, {
            type: 'line',
            data: {
                labels: ['Янв', 'Фев', 'Мар', 'Апр', 'Май', 'Июн', 'Июл', 'Авг', 'Сен', 'Окт'],
                datasets: [{
                    label: 'BTC/USD',
                    data: [38000, 42000, 45000, 48000, 52000, 58000, 62000, 59000, 61000, 61245],
                    borderColor: '#2962FF',
                    backgroundColor: 'rgba(41, 98, 255, 0.1)',
                    tension: 0.4,
                    fill: true
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        display: false
                    }
                },
                scales: {
                    y: {
                        grid: {
                            color: 'rgba(255, 255, 255, 0.1)'
                        },
                        ticks: {
                            color: '#E0E0E0'
                        }
                    },
                    x: {
                        grid: {
                            color: 'rgba(255, 255, 255, 0.1)'
                        },
                        ticks: {
                            color: '#E0E0E0'
                        }
                    }
                }
            }
        });

        // Portfolio Chart
        const portfolioCtx = document.getElementById('portfolioChart').getContext('2d');
        const portfolioChart = new Chart(portfolioCtx, {
            type: 'doughnut',
            data: {
                labels: ['Bitcoin', 'Ethereum', 'DeFi', 'NFT', 'Другое'],
                datasets: [{
                    data: [40, 25, 15, 10, 10],
                    backgroundColor: [
                        '#2962FF',
                        '#00C853',
                        '#FF5252',
                        '#FFC107',
                        '#9C27B0'
                    ]
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'bottom',
                        labels: {
                            color: '#E0E0E0',
                            padding: 15
                        }
                    }
                }
            }
        });
    </script>
</body>
</html>
